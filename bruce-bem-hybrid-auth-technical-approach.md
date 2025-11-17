# Bruce BEM Dynamic Authentication - Hybrid Approach

**Date:** 2025-11-17
**Purpose:** Technical specification for OAuth + custom userToken authentication

---

## 1. Overview

### Current State
- Single hardcoded username/password in environment variables
- All users share the same Bruce BEM identity
- MCP server uses static credentials

### Desired State
- Dynamic per-user authentication
- No login prompts (automatic authentication)
- Multi-user concurrent access with token isolation

### Hybrid Solution
**Okta OAuth** handles LibreChat authentication (standard SSO pattern)
**Custom code** handles Bruce BEM userToken (API-specific authentication)

### Separation of Concerns
- **LibreChat Authentication:** Okta OAuth (user can access chat interface)
- **Bruce BEM API Authentication:** userToken (MCP makes API calls as specific user)
- **Two separate token systems:** OAuth tokens ≠ userToken

---

## 2. Key Assumptions

### Authentication Infrastructure
- Bruce BEM uses Okta for user authentication
- Users authenticate to Bruce BEM before opening chat interface
- Okta session exists in browser when chat is accessed

### Token Systems
- userToken comes from Bruce BEM `/users/getusertoken` endpoint
- userToken is short-lived (5-15 minutes)
- Okta manages its own OAuth tokens separately
- Both token types required for complete functionality

### Configuration Access
- Ryan can configure LibreChat as Okta OAuth client
- Ryan has access to Okta admin console
- LibreChat deployment accessible at defined URL

### Browser Environment
- Standard browser cookie behavior (Okta session cookies accessible)
- HTTPS enabled for production deployment
- Same-origin or CORS properly configured

---

## 3. Technical Flow

**Step 1: User Logs into Bruce BEM**
- User authenticates to Bruce BEM application
- Bruce BEM redirects to Okta for authentication
- Okta creates SSO session (stored as browser cookie)
- User redirected back to Bruce BEM

**Step 2: User Opens Chat Interface**
- Ryan generates userToken from Bruce BEM
- Opens iframe: `https://chat.example.com/?userToken=abc123xyz`

**Step 3: LibreChat Auto-Redirects to Okta**
- LibreChat detects no authentication
- OPENID_AUTO_REDIRECT triggers immediate redirect to Okta
- No login form shown to user

**Step 4: Okta Recognizes Existing Session**
- Browser automatically sends Okta session cookies
- Okta validates existing session
- Okta grants OAuth tokens immediately (~500ms)
- No user interaction required

**Step 5: OAuth Callback Completes**
- Okta redirects back to LibreChat with tokens
- LibreChat validates OAuth tokens
- User authenticated to LibreChat

**Step 6: userToken Extracted Separately**
- LibreChat client extracts userToken from URL query parameter
- Stores in session state (independent of OAuth)
- Includes in backend requests

**Step 7: Token Routing to MCP**
- Backend adds userToken to request body
- Placeholder system resolves to header: `X-User-Token`
- MCP server receives both OAuth context and userToken

**Step 8: Bruce BEM API Calls**
- MCP extracts userToken from request headers
- Stores in request-scoped Context
- Uses userToken + bearer token for Bruce BEM API calls

---

## 4. What We Need From Ryan

### Required Outcome
Deliver userToken to chat interface via iframe URL query parameter when user opens chat.

### Format
```
https://chat.example.com/?userToken=<generated_token>
```

### Token Source
- Same token Bruce BEM uses internally for API calls
- Obtained from `/users/getusertoken` endpoint
- Generated with: username + password + clientId

### Timing
- Token generated when user clicks to open chat
- Passed immediately in iframe URL
- Token already valid when iframe loads

### Lifecycle
- Token expires after 5-15 minutes (Bruce BEM controlled)
- No automatic refresh mechanism
- User may need to re-open chat after expiration

---

## 5. Okta OAuth Configuration

### LibreChat as Okta Client

**Required Okta Configuration:**
- Create new OAuth2/OIDC application in Okta
- Application type: Web Application
- Grant types: Authorization Code
- Redirect URI: `https://chat.example.com/oauth/openid/callback`

**LibreChat Environment Variables:**
```bash
# OAuth Provider
OPENID_CLIENT_ID=<okta_client_id>
OPENID_CLIENT_SECRET=<okta_client_secret>
OPENID_ISSUER=https://<okta_domain>/oauth2/default
OPENID_CALLBACK_URL=/oauth/openid/callback

# Auto-Login (Bypasses LibreChat Login Screen)
OPENID_AUTO_REDIRECT=true

# Token Management
OPENID_REUSE_TOKENS=true

# Scope
OPENID_SCOPE="openid profile email"
```

### Authentication Behavior

**With OPENID_AUTO_REDIRECT:**
- User visits LibreChat → Instant redirect to Okta
- No LibreChat login form shown
- If Okta session exists: OAuth completes in ~500ms
- If no Okta session: User sees Okta login page

**With OPENID_REUSE_TOKENS:**
- LibreChat uses Okta tokens for API authentication
- Session lifecycle tied to Okta token expiration
- Automatic token refresh via Okta refresh tokens

### Session Dependency

**Critical Requirement:**
User MUST log into Bruce BEM first (which creates Okta session) before opening chat. If user opens chat without Bruce BEM login, they'll be redirected to Okta login page.

**Flow Dependency:**
```
Bruce BEM Login (creates Okta session)
    ↓
Chat Opens (reuses Okta session)
    ↓
Auto-authentication succeeds
```

---

## 6. Our Custom userToken Implementation

### LibreChat Client Modifications

**Token Extraction:**
- Extract userToken from URL query parameter
- Store in Recoil state for session persistence
- Maintain throughout user session

**Request Integration:**
- Include userToken in every backend request payload
- Sent with each chat message and tool call

**Files Modified:**
- `useQueryParams.ts` - Extract token from URL
- `useSSE.ts` - Add token to request payload
- `store/userToken.ts` - Recoil atom (new file)

### LibreChat Backend Configuration

**Payload Whitelist:**
- Add `userToken` to `ALLOWED_BODY_FIELDS` array
- Enables placeholder system processing

**MCP Header Configuration:**
```yaml
# librechat.yaml
mcpServers:
  bruce-bem:
    url: "https://archibus-mcp.wilsch-deployment.com/mcp"
    type: "streamable-http"
    headers:
      X-User-Token: "{{LIBRECHAT_BODY_USERTOKEN}}"
```

**Placeholder Resolution:**
- Backend resolves `{{LIBRECHAT_BODY_USERTOKEN}}` from request body
- Injects as header to MCP server
- Automatic with ALLOWED_BODY_FIELDS configuration

### MCP Server Architecture

**Token Extraction:**
- Middleware extracts `X-User-Token` from HTTP headers
- Stores in request-scoped FastMCP Context

**Authentication Isolation:**
- Remove singleton BruceBEMClient instance
- Implement per-request token handling
- Each user request gets independent Context

**API Integration:**
- Extract userToken from Context per request
- Use bearer token from environment (system-level, static)
- Both tokens included in Bruce BEM API calls

---

## 7. Security Considerations

### Request-Scoped Authentication

**Problem:** Multiple concurrent users must not share authentication state

**Solution:**
- FastMCP Context is request-scoped (automatic isolation)
- No singleton instances (prevents token leakage)
- Each user request operates independently

**Result:** User A's userToken cannot leak to User B's request

### Token Lifecycle Management

**Okta OAuth Tokens:**
- Access token: Short-lived (typically 1 hour)
- Refresh token: Long-lived (refreshes access token)
- Managed automatically by LibreChat + Okta

**Bruce BEM userToken:**
- Short-lived: 5-15 minutes
- Not refreshable by Okta (separate system)
- Expires independent of OAuth session

**Implication:**
- User may remain authenticated to LibreChat (Okta session valid)
- But userToken expires (Bruce BEM API calls fail)
- User must re-open chat to get fresh userToken

### Multi-User Isolation

**Okta OAuth:**
- Each user has independent Okta session
- OAuth tokens stored per-user in LibreChat
- Session cookies prevent cross-user authentication

**userToken:**
- Passed per-request to MCP server
- Stored in request-scoped Context
- No shared state between concurrent users

---

## Summary

**Key Points:**

1. **Hybrid Approach:** Okta OAuth (LibreChat auth) + userToken (Bruce BEM API auth)
2. **No Login Prompts:** OPENID_AUTO_REDIRECT leverages existing Okta session
3. **Separate Token Systems:** OAuth and userToken are independent
4. **Browser Handles Okta:** Session cookies automatically sent to Okta
5. **Manual userToken Passing:** Via query parameter, custom code handling
6. **Request-Scoped Safety:** No token leakage between concurrent users

**Dependencies:**

- User logs into Bruce BEM first (creates Okta session)
- Ryan provides userToken via iframe URL
- LibreChat configured as Okta OAuth client
- Custom code extracts and routes userToken

**Benefits:**

- Standard OAuth pattern (reliable, well-understood)
- No custom auth bypass code (uses OPENID_AUTO_REDIRECT)
- Clean separation of concerns (OAuth ≠ userToken)
- Multi-user safe (request-scoped authentication)
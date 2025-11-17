# Bruce BEM Dynamic Authentication - Technical Approach

**Date:** 2025-11-17
**Purpose:** Technical specification for implementing dynamic per-user authentication

---

## 1. Overview

### Current State
- Single hardcoded username/password in environment variables
- All users share the same Bruce BEM identity
- MCP server uses static credentials from `.env`

### Desired State
- Dynamic authentication based on logged-in user
- Each user's Bruce BEM credentials used for their requests
- Multi-user concurrent access without credential conflicts

### Proposed Solution
Query parameter or postMessage-based token passing from Bruce BEM to chat interface, with request-scoped authentication in MCP server.

### Token Architecture
- **userToken** (user identity) - Dynamic, per-user, passed from Bruce BEM
- **Bearer token** (system identity) - Static, system-level, stays in `.env`
- **Both required** for Bruce BEM API authorization

---

## 2. Technical Flow

```
┌─────────────────────────────────────────────────────────────┐
│ 1. User logs into Bruce BEM                                 │
│    └─ Existing Bruce BEM authentication                     │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ 2. User opens AI chat interface                             │
│    └─ Bruce BEM generates userToken for logged-in user      │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ 3. Token passed to chat interface                           │
│    └─ Option A: ?userToken=xyz (URL query parameter)        │
│    └─ Option B: postMessage API (iframe communication)      │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ 4. LibreChat extracts and forwards token                    │
│    └─ Client: Extract from URL or postMessage               │
│    └─ Store in session state                                │
│    └─ Include in backend requests                           │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ 5. LibreChat backend processes request                      │
│    └─ ALLOWED_BODY_FIELDS: userToken permitted              │
│    └─ Placeholder resolution: {{LIBRECHAT_BODY_USERTOKEN}}  │
│    └─ Header injection: X-User-Token                        │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ 6. MCP server receives request                              │
│    └─ Middleware extracts X-User-Token from headers         │
│    └─ Stores in request-scoped Context                      │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│ 7. Bruce BEM API call                                       │
│    └─ Header: x-user-token (from Context - dynamic)         │
│    └─ Header: Authorization: Bearer (from .env - static)    │
└─────────────────────────────────────────────────────────────┘
```

### Request Lifecycle

**Per-Request Flow:**
1. Each user request carries their unique userToken
2. MCP middleware extracts token into request-scoped Context
3. BruceBEMClient reads token from Context (not from instance variable)
4. API call made with user's token + system bearer token
5. Context destroyed after request completes

**Multi-User Safety:**
- FastMCP Context is request-scoped (not shared between requests)
- No singleton BruceBEMClient instance (prevents token leakage)
- Concurrent users operate with complete isolation

---

## 3. What We Need From Ryan

### Required Outcome
**Deliver userToken to chat interface when user opens AI chat.**

The userToken should be the same token Bruce BEM uses internally for API calls - obtained from the `/users/getusertoken` endpoint with username + password + clientId.

### Two Implementation Options

#### Option A: Query Parameter (Recommended for MVP)

**What Ryan Does:**
```javascript
// When opening chat iframe
const chatUrl = `https://chat.example.com/?userToken=${generatedToken}`;
iframe.src = chatUrl;
```

**Trade-offs:**
- ✅ **Simple:** Single line of code, no iframe messaging
- ✅ **Fast:** Immediate implementation, easy to test
- ✅ **Compatible:** Works with all browsers, no CORS issues
- ⚠️ **Token in URL:** Visible in browser address bar/history
- ⚠️ **Mitigation:** Short-lived tokens (5-15 minutes) + HTTPS only

#### Option B: PostMessage API (Recommended for Production)

**What Ryan Does:**
```javascript
// After iframe loads
const iframe = document.getElementById('chat-iframe');
iframe.addEventListener('load', () => {
  iframe.contentWindow.postMessage({
    type: 'AUTH_TOKEN',
    userToken: generatedToken,
    expiresAt: Date.now() + 900000  // 15 minutes
  }, 'https://chat.example.com');  // Explicit target origin
});
```

**Trade-offs:**
- ✅ **Secure:** Token never visible in URL
- ✅ **Best Practice:** Standard pattern for iframe communication
- ✅ **Production-Ready:** Used by enterprise applications
- ❌ **Complex:** Requires iframe messaging code on both sides
- ❌ **Timing:** Must wait for iframe load before sending

### Recommendation

**Phase 1 (Now):** Use **Option A** (Query Parameter)
- Fastest path to working prototype
- Easy for both teams to test independently
- Security acceptable with short-lived tokens

**Phase 2 (Later):** Migrate to **Option B** (PostMessage)
- Upgrade after MVP validates the approach
- Better security posture for production
- No architectural changes needed (same token flow)

---

## 4. Our Implementation

### LibreChat Modifications

**Client-Side (React/TypeScript):**
1. **Extract Token**
   - `useQueryParams.ts` - Parse `userToken` from URL query parameter
   - Or: Event listener for postMessage token reception

2. **Store Token**
   - Recoil atom for session persistence
   - Survives component re-renders
   - Cleared on logout/session end

3. **Include in Requests**
   - `useSSE.ts` - Add userToken to request payload
   - Sent with every chat message/tool call

**Backend (Node.js):**
1. **Allow Token Field**
   - `env.ts` - Add "userToken" to `ALLOWED_BODY_FIELDS` array
   - Enables placeholder system to process token

2. **MCP Configuration**
   - `librechat.yaml` - Configure header with placeholder:
   ```yaml
   mcpServers:
     bruce-bem:
       url: "https://archibus-mcp.wilsch-deployment.com/mcp"
       type: "streamable-http"
       headers:
         X-User-Token: "{{LIBRECHAT_BODY_USERTOKEN}}"
   ```

3. **Authentication Bypass**
   - `useAuthRedirect.ts` - Skip redirect to login page
   - Create auto-authentication mechanism (users already authenticated via Bruce BEM)

### MCP Server Refactoring

**Architecture Change (Python/FastMCP):**

1. **Remove Singleton**
   ```python
   # OLD (server.py:25) - REMOVE
   client = BruceBEMClient(settings)  # Shared instance = race condition

   # NEW - Per-request instantiation or Context-only token storage
   ```

2. **Add Middleware**
   ```python
   class TokenExtractionMiddleware(Middleware):
       async def on_request(self, context: MiddlewareContext, call_next):
           # Extract X-User-Token from request headers
           headers = get_http_headers()
           user_token = headers.get("x-user-token")

           # Store in request-scoped Context
           context.fastmcp_context.set_state("user_token", user_token)

           return await call_next(context)
   ```

3. **Modify BruceBEMClient**
   ```python
   class BruceBEMClient:
       def authenticate(self, ctx: Context):
           # Read token from Context (not from .env)
           user_token = ctx.get_state("user_token")
           if not user_token:
               raise ValueError("No user token provided")

           # Use token for API calls
           self.user_token = user_token
           self.bearer_token = self.settings.BEARER_TOKEN  # System-level, from .env
   ```

**Result:**
- No shared state between requests
- Each user's token isolated in their request Context
- Concurrent users safe (no token leakage)

---

## 5. Security Considerations

### Token Isolation (Multi-User Safety)

**Problem:** Multiple concurrent users must not share authentication state.

**Solution:**
- **FastMCP Context:** Request-scoped, automatically isolated per request
- **No Singleton:** BruceBEMClient not shared across requests
- **No Instance Variables:** Tokens stored in Context, not in object attributes

**Result:** User A's token cannot leak to User B's request, even with concurrent access.

### Token Visibility (Query Parameter)

**Problem:** Query parameter tokens visible in browser URL bar and history.

**Mitigation:**
- **Short-lived tokens:** 5-15 minute expiration (limited damage window)
- **HTTPS only:** Encrypted in transit
- **No sensitive data in token:** Token is opaque identifier
- **Future upgrade:** PostMessage removes URL exposure entirely

### Bearer Token Management

**System-Level Token:**
- OAuth client credentials for Bruce BEM system identity
- Shared across all users (represents the application, not individual users)
- Stays in `.env` (not dynamic, not user-specific)

**Security:**
- Never exposed to client
- Server-side only
- Represents authorized application, not user permissions

---

## Summary

**Key Points:**

1. **Ryan's Responsibility:** Deliver userToken to chat interface (query param or postMessage)
2. **Our Responsibility:** Extract token, disable LibreChat auth, refactor MCP for request-scoped authentication
3. **Token Types:** userToken (dynamic, per-user) + bearer token (static, system-level)
4. **Security:** Request-scoped Context prevents multi-user token conflicts
5. **Recommendation:** Start with query parameter, upgrade to postMessage later

**This approach enables:**
- Multiple concurrent users with independent authentication
- No hardcoded credentials
- Seamless user experience (no additional login prompts)
- Secure multi-user API access
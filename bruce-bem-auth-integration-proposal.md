# Bruce BEM AI Authentication Integration Proposal

**For:** Ryan (Rein Suurväli)
**From:** Marius Wilsch
**Date:** 2025-11-17
**Subject:** Dynamic Per-User Authentication Implementation

---

## Executive Summary

This proposal outlines the technical approach to replace hardcoded authentication credentials with dynamic per-user authentication in the Bruce BEM AI chat interface. The solution enables multiple concurrent users to interact with Bruce BEM APIs using their individual credentials.

---

## Current State vs. Desired State

### Current State
- Single hardcoded username/password in environment variables
- All users share the same Bruce BEM identity
- MCP server uses static credentials from `.env`
- No user isolation in API requests

### Desired State
- Dynamic authentication based on logged-in user
- Each user's Bruce BEM credentials used for their requests
- Multi-user concurrent access without token leakage
- No login prompts (auto-authenticated from Bruce BEM session)

---

## Proposed Solution: Query Parameter Token Passing

### Integration Flow

```
User logs into Bruce BEM
        ↓
Ryan generates userToken
        ↓
Iframe opened with ?userToken=xyz
        ↓
LibreChat extracts and forwards token
        ↓
MCP server receives token in headers
        ↓
Bruce BEM API called with user's token
```

---

## Responsibility Split

### Ryan's Responsibilities (Bruce BEM Side)

**1. Token Generation**
- When user opens chat, generate Bruce BEM user token
- Use same authentication flow as current system: `/users/getusertoken`
- Token payload: username + password + clientId

**2. Iframe Integration**
- Pass token via URL query parameter: `?userToken=xyz`
- Example: `https://chat.example.com/?userToken=abc123def456`
- Token is short-lived (security via limited lifetime + HTTPS)

**3. No Authentication Prompts**
- Ensure users don't see LibreChat login/registration screens
- Users already authenticated to Bruce BEM (single sign-on experience)

### Our Responsibilities (Chat/MCP Side)

**1. LibreChat Modifications**
- Extract `userToken` from URL query parameter
- Store token for session persistence
- Include token in backend API requests
- Disable LibreChat authentication flow

**2. MCP Server Refactoring**
- Remove singleton `BruceBEMClient` instance (prevents race conditions)
- Implement request-scoped authentication
- Extract token from HTTP headers
- Use Context for per-request token storage

**3. Bruce BEM API Integration**
- Use extracted `userToken` for `x-user-token` header
- Continue using system-level bearer token from environment
- Both tokens included in all Bruce BEM API calls

---

## Technical Details

### Token Flow Components

**LibreChat Client (React)**
- `useQueryParams.ts` - Extract token from URL
- Recoil atom - Store token in app state
- `useSSE.ts` - Add token to request payload

**LibreChat Backend (Node.js)**
- `env.ts` - Allow `userToken` in request body fields
- Placeholder system: `{{LIBRECHAT_BODY_USERTOKEN}}`

**MCP Configuration**
```yaml
mcpServers:
  bruce-bem:
    url: "https://archibus-mcp.wilsch-deployment.com/mcp"
    type: "streamable-http"
    headers:
      X-User-Token: "{{LIBRECHAT_BODY_USERTOKEN}}"
```

**MCP Server (Python)**
- Middleware extracts `X-User-Token` from request headers
- Stores in FastMCP Context (request-scoped, thread-safe)
- `BruceBEMClient` reads token from Context
- No shared state between concurrent users

---

## Security Considerations

### Token Visibility
- **Query Parameter Approach:** Token visible in URL
- **Mitigation:** Short-lived tokens (minutes, not hours) + HTTPS only
- **Future Enhancement:** PostMessage API (more secure, no URL exposure)

### Multi-User Isolation
- Request-scoped Context prevents token leakage
- Each user's request gets independent authentication
- No race conditions with concurrent users

### Bearer Token Management
- System-level OAuth token stays in `.env` (shared, system identity)
- User token is dynamic (user identity)
- Both required for Bruce BEM API authorization

---

## Testing Strategy

### Phase 1: Manual Testing (Immediate)
1. We manually generate test user token
2. Test with URL parameter: `?userToken=<test_token>`
3. Verify MCP server receives and uses token
4. Confirm API calls succeed with test credentials

### Phase 2: Integration Testing
1. Ryan implements token generation in Bruce BEM
2. Ryan passes token via iframe URL
3. End-to-end testing with real user flow
4. Verify multiple concurrent users work independently

### Phase 3: Production Validation
1. Monitor logs for authentication errors
2. Verify no token leakage between users
3. Test session persistence across page refreshes
4. Confirm auto-authentication (no login prompts)

---

## Implementation Timeline

**Estimated Effort:**

- **LibreChat modifications:** 2-3 days
  - Client token extraction and storage
  - Backend payload extension
  - Authentication bypass

- **MCP server refactoring:** 1-2 days
  - Remove singleton
  - Add middleware
  - Context-based authentication

- **Integration & Testing:** 1-2 days
  - End-to-end flow verification
  - Multi-user concurrency testing

**Total:** ~5-7 days development + testing

---

## Next Steps

1. **Ryan:** Confirm approach and timeline
2. **Us:** Begin LibreChat + MCP implementation
3. **Ryan:** Implement token generation on Bruce BEM side
4. **Both:** Coordinate testing when components ready
5. **Both:** Integration testing with real user flow

---

## Questions for Ryan

1. **Token Lifetime:** How long should user tokens remain valid?
2. **Session Management:** Should tokens refresh automatically?
3. **Error Handling:** What should happen if token expires mid-conversation?
4. **Deployment:** Will chat remain at current URL or move to Bruce BEM subdomain?

---

## Technical Contact

**Marius Wilsch**
Email: marius@veloxforce.ai
Available for technical discussion and clarification.

---

*This proposal is based on comprehensive research of LibreChat architecture, MCP protocol standards, and Bruce BEM authentication requirements.*
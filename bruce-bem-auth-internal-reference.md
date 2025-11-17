# Bruce BEM Dynamic Authentication - Internal Technical Reference

**Purpose:** Implementation reference for dynamic per-user authentication
**Date:** 2025-11-17
**Status:** Research complete, ready for implementation

---

## 1. Architectural Facts

### Component Stack
```
Bruce BEM (Ryan's responsibility)
    ↓ userToken via query param
LibreChat (our modification)
    ↓ token in HTTP headers
MCP Server (our modification)
    ↓ authenticated API calls
Bruce BEM API
```

### Token Architecture
- **userToken:** User identity (dynamic, per-user, passed from Bruce BEM)
- **bearer_token:** System identity (static, OAuth client credentials, stays in .env)
- **Both required:** Bruce BEM API requires both headers for authorization

### Integration Method
LibreChat code modifications + existing placeholder system (`{{LIBRECHAT_BODY_*}}`)

---

## 2. Research Findings

### LibreChat Official Support Status
**Finding:** No official support for external token passing from URL to MCP headers
**Evidence:**
- GitHub Issue #1856: `FORWARD_AUTH_HEADER` requested, not implemented
- GitHub Issue #5419: iframe embedding without auth requested, unimplemented
- URL query params validated against schema, custom params ignored
- `customUserVars` requires manual UI entry (not automatic)

**Conclusion:** Code modifications required (community standard approach)

### Placeholder System Mechanics
**Location:** `packages/api/src/utils/env.ts` (lines 103-195)
**Function:** `processMCPEnv()` resolves placeholders in MCP server config
**Mechanism:**
1. Finds patterns: `{{LIBRECHAT_BODY_*}}`, `{{LIBRECHAT_USER_*}}`, `${ENV_VAR}`
2. Resolves from: request body, user object, environment variables
3. Replaces in: MCP server headers, URLs, environment

**Whitelist:** `ALLOWED_BODY_FIELDS` array (env.ts:33) controls which body fields are accessible
**Current values:** `['conversationId', 'parentMessageId', 'messageId']`
**Required change:** Add `'userToken'` to array

### Community Approach
**Standard pattern:** Code modifications when official support absent
**References:**
- Issue #1856 community patch (auth proxy header forwarding)
- Discussion #7902 (OAuth proxy workaround)
- No configuration-only solutions found

---

## 3. File Locations

### LibreChat Client (React/TypeScript)
```
client/src/hooks/Input/useQueryParams.ts     - Extract token from URL
client/src/store/                             - Create Recoil atom (new file)
client/src/hooks/SSE/useSSE.ts                - Add token to request payload
client/src/routes/useAuthRedirect.ts          - Bypass authentication redirect
```

### LibreChat Backend (Node.js)
```
packages/api/src/utils/env.ts                 - Add to ALLOWED_BODY_FIELDS (line 33)
librechat.yaml                                 - Configure MCP header placeholder
```

### MCP Server (Python/FastMCP)
```
server.py                                      - Remove singleton (line 25)
src/api.py                                     - Modify BruceBEMClient class
                                                - Add token extraction middleware
```

---

## 4. Technical Flow

```
┌─────────────────────────────────────────────────────────────────┐
│ Step 1: Token Arrives                                           │
│ Ryan opens iframe: ?userToken=abc123xyz                         │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 2: Client Extraction (useQueryParams.ts)                   │
│ - Parse URL query parameter                                     │
│ - Extract: userToken = "abc123xyz"                              │
│ - Store in Recoil atom (session persistence)                    │
│ - Remove from URL (cleanup)                                     │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 3: User Sends Message                                      │
│ - User types message, clicks send                               │
│ - useSSE hook constructs request                                │
│ - Retrieves userToken from Recoil                               │
│ - Adds to payload: {text: "...", userToken: "abc123xyz"}        │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 4: Backend Receives Request                                │
│ POST /api/agents                                                 │
│ Body: {text: "...", userToken: "abc123xyz", conversationId...}  │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 5: Field Validation (env.ts)                               │
│ Check: Is 'userToken' in ALLOWED_BODY_FIELDS?                   │
│ Yes → Keep field                                                 │
│ No → Strip field (our change adds it to whitelist)              │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 6: MCP Configuration Read (librechat.yaml)                 │
│ mcpServers:                                                      │
│   bruce-bem:                                                     │
│     headers:                                                     │
│       X-User-Token: "{{LIBRECHAT_BODY_USERTOKEN}}"              │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 7: Placeholder Resolution (env.ts:processMCPEnv)           │
│ - Find: {{LIBRECHAT_BODY_USERTOKEN}}                            │
│ - Extract field name: USERTOKEN → userToken                     │
│ - Lookup: requestBody.userToken = "abc123xyz"                   │
│ - Replace: "{{LIBRECHAT_BODY_USERTOKEN}}" → "abc123xyz"         │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 8: Forward to MCP Server                                   │
│ HTTP POST to MCP server                                          │
│ Headers:                                                         │
│   X-User-Token: abc123xyz                                        │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 9: MCP Middleware Extraction                               │
│ - Extract X-User-Token from request headers                     │
│ - Store in FastMCP Context (request-scoped)                     │
│ - Context: ctx.set_state("user_token", "abc123xyz")             │
└─────────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 10: Bruce BEM API Call                                     │
│ - Retrieve: user_token from Context                             │
│ - Retrieve: bearer_token from .env (system-level)               │
│ - Headers:                                                       │
│     x-user-token: abc123xyz (user identity)                     │
│     Authorization: Bearer <token> (system identity)             │
└─────────────────────────────────────────────────────────────────┘
```

---

## 5. Implementation Points

### Required Modifications

**LibreChat (6 files):**
1. `useQueryParams.ts` - Add token extraction logic
2. `store/userToken.ts` - Create Recoil atom (new file)
3. `useSSE.ts` - Add userToken to request payload
4. `env.ts` - Add 'userToken' to ALLOWED_BODY_FIELDS array
5. `librechat.yaml` - Add header: `X-User-Token: "{{LIBRECHAT_BODY_USERTOKEN}}"`
6. `useAuthRedirect.ts` - Skip redirect for auto-authentication

**MCP Server (3 changes):**
1. `server.py:25` - Remove `client = BruceBEMClient(settings)` singleton
2. `src/api.py` - Add middleware class for token extraction
3. `src/api.py` - Modify BruceBEMClient to read token from Context

### Configuration Changes

**env.ts (line 33):**
```javascript
const ALLOWED_BODY_FIELDS = [
  'conversationId',
  'parentMessageId',
  'messageId',
  'userToken'  // ADD THIS
];
```

**librechat.yaml:**
```yaml
mcpServers:
  bruce-bem:
    url: "https://archibus-mcp.wilsch-deployment.com/mcp"
    type: "streamable-http"
    headers:
      X-User-Token: "{{LIBRECHAT_BODY_USERTOKEN}}"  # ADD THIS
```

### Implementation Patterns

**Pattern 1: Recoil State Management**
```typescript
// client/src/store/userToken.ts
import { atom } from 'recoil';

export const userTokenAtom = atom({
  key: 'userToken',
  default: ''
});
```

**Pattern 2: FastMCP Middleware**
```python
from fastmcp.server.middleware import Middleware
from fastmcp.server.dependencies import get_http_headers

class TokenExtractionMiddleware(Middleware):
    async def on_request(self, context, call_next):
        headers = get_http_headers()
        user_token = headers.get("x-user-token")
        context.fastmcp_context.set_state("user_token", user_token)
        return await call_next(context)
```

**Pattern 3: Request-Scoped Context**
```python
# NO SINGLETON - per-request authentication
def search_assets(ctx: Context, ...):
    user_token = ctx.get_state("user_token")
    bearer_token = settings.BEARER_TOKEN  # System-level from .env

    headers = {
        "x-user-token": user_token,
        "Authorization": f"Bearer {bearer_token}"
    }
```

---

## 6. Critical Implementation Notes

### Multi-User Safety
- **Singleton Bug:** Current `server.py:25` creates shared BruceBEMClient instance
- **Race Condition:** Concurrent users overwrite each other's tokens in shared instance
- **Fix:** Remove singleton, use request-scoped Context for token storage
- **Verification:** FastMCP Context is request-scoped by design (confirmed in research)

### Authentication Bypass
- **Current:** useAuthRedirect redirects unauthenticated users to /login after 300ms
- **Required:** Skip redirect when user already authenticated via Bruce BEM
- **Implementation:** Conditional logic based on external auth presence

### Token Lifetime
- **Consideration:** userToken is short-lived (Ryan controls expiration)
- **No Refresh:** Current design does not handle token refresh
- **Future:** May need token refresh mechanism if sessions > token lifetime

---

## 7. Verification Commands

### Test Token Flow
```bash
# Manual test with query parameter
curl "https://chat.example.com/?userToken=test123"

# Verify token in LibreChat backend logs
docker logs -f LibreChat-dev | grep userToken

# Verify token reaches MCP server
docker logs -f archibus_fastmcp | grep "x-user-token"
```

### Test Multi-User Isolation
```bash
# Simulate concurrent users with different tokens
# (Requires test script - manual verification insufficient)
```

---

## 8. Dependencies

### LibreChat
- React Router (useSearchParams)
- Recoil (state management)
- Existing SSE implementation
- Existing placeholder system

### MCP Server
- FastMCP >= version with Middleware support
- Request-scoped Context (built-in)
- Existing BruceBEMClient class

### External
- Ryan provides userToken generation
- Bruce BEM API unchanged (uses same headers as current)

---

**End of Reference Document**

*This document contains the 20% of research findings needed to implement the 80% of code changes. Refer to conversation history for detailed investigation process and community research sources.*
# Analysis: What Needs Verification from Rain

After reviewing the document, here are the **key assumptions that require Rain's confirmation** (things we cannot figure out ourselves):

## Critical Assumptions Requiring Rain's Input:

### 1. Bruce BEM → Okta Integration
- Document assumes: "Bruce BEM uses Okta for user authentication"
- **Question:** Does Bruce BEM actually use Okta for authentication, or is this an incorrect assumption?

### 2. userToken Generation Capability
- Document assumes: "Ryan generates userToken from Bruce BEM" when user opens chat
- **Question:** Can Bruce BEM's current infrastructure generate a userToken on-demand when a user clicks to open the chat interface?

### 3. userToken Delivery Method
- Document proposes: iframe URL with query parameter `?userToken=abc123xyz`
- **Question:** Is Bruce BEM able to embed LibreChat as an iframe and append the userToken to the URL, or is there a technical constraint preventing this?

### 4. Okta Session Sharing
- Document assumes: Browser will have Okta session cookies when chat loads (from Bruce BEM login)
- **Question:** If Bruce BEM uses Okta, will the Okta session cookies be accessible to LibreChat (same Okta tenant/domain)?

### 5. Okta Admin Access
- Document assumes: "Ryan has access to Okta admin console"
- **Question:** Does Rain have the ability to configure LibreChat as an Okta OAuth client (create new application, set redirect URIs, etc.)?

### 6. Token Lifetime Specification
- Document states: "userToken is short-lived (5-15 minutes)"
- **Question:** What is the actual token lifetime from `/users/getusertoken`? (We know from API it returns `expiresIn: 3600` = 1 hour, which conflicts with the 5-15 minute assumption)

### 7. LibreChat Deployment URL
- Document assumes: "LibreChat deployment accessible at defined URL"
- **Question:** What URL should be used for LibreChat deployment and Okta redirect URI configuration? (Is it the current `https://archibus-mcp.wilsch-deployment.com` or a different domain?)

## Additional Clarifications Needed:

### 8. Bypassing LibreChat Authentication
- Document proposes: Using `OPENID_AUTO_REDIRECT=true` to bypass LibreChat login screen
- **Question:** Is the goal to have users NEVER see any login screen (leveraging Okta SSO), or is there a different authentication bypass approach Rain prefers?

### 9. User Context for Token Generation
- Document doesn't specify HOW Bruce BEM knows which user's token to generate
- **Question:** When Bruce BEM generates the userToken for the iframe, how does it know which user is opening the chat? (Based on Bruce BEM session? Okta session? Explicit user context?)

### 10. Bearer Token vs userToken Relationship
- Document treats bearer token (OAuth client_credentials) as separate from userToken
- **Question:** Should the bearer token remain static (application-level from `.env`), or does it need to become user-specific as well?

---

## What We CAN Figure Out Ourselves:

- **FastMCP Context architecture**: Already confirmed to be request-scoped (safe for multi-user)
- **LibreChat placeholder system**: Documented feature, we can implement `{{LIBRECHAT_BODY_USERTOKEN}}`
- **Token refresh endpoint**: Bruce BEM API has `/users/refreshtoken` available
- **Current token lifetime**: API returns `expiresIn: 3600` (1 hour, not 5-15 minutes as document states)
- **MCP server modifications**: We know what code changes are needed (remove singleton, use Context)

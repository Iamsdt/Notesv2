
Endpoint 1: Initiate Authorization

```
GET /api/auth/authorize

Query Parameters:
- client_id (required)
- redirect_uri (required)
- response_type=code (required)
- scope (optional)
- state (recommended)
- code_challenge (required for PKCE)
- code_challenge_method=S256 (required for PKCE)

Server Actions:
1. Validate client_id and redirect_uri
2. Store code_challenge temporarily (Redis/DB with TTL ~10 min)
3. Check if user is authenticated (session/cookie)
4. If NOT authenticated: redirect to /login
5. If authenticated: show consent screen (Based on Cookie in session id)
6. After consent: generate authorization_code
7. Link authorization_code to stored code_challenge
8. Redirect: {redirect_uri}?code={authorization_code}&state={state}

Response:
- 302 Redirect to login page OR
- 302 Redirect to consent page OR
- 302 Redirect to redirect_uri with code
```

Endpoint 2: User Login (if needed)

```
POST /api/auth/login

Request Body:
{
  "email": "user@example.com",
  "password": "password123",
  "client_id": industrypilot
}

Server Actions:
1. Validate credentials
2. Create user session (JWT/cookie)
3. Continue authorization flow from /authorize
   
Response:
{
  "success": true,
  "redirect": "/authorize?continue=true"
}
```

Note: Generate cookie and keep in session_id for this page, for auth.10xscale.ai. This cookie will be used only for auth, to check session is available or not....

Endpoint 3: Token Exchange (Will Happen in APP level and write inside cookie)
```
POST /api/auth/token

Request Body (x-www-form-urlencoded):
- grant_type=authorization_code
- code (required)
- client_id (required)
- redirect_uri (required)
- code_verifier (required for PKCE)

Server Actions:
1. Retrieve stored code_challenge using authorization code
2. Compute SHA256(code_verifier)
3. Verify computed hash == stored code_challenge
4. If valid: generate access_token + refresh_token
5. Delete used authorization code (one-time use)
6. Delete used code_challenge

Response:
{
  "access_token": "eyJhbGc...",
  "refresh_token": "refresh_xyz",
  "token_type": "Bearer",
  "expires_in": 3600
}

Error Response:
{
  "error": "invalid_grant",
  "error_description": "Code verifier validation failed"
}
```


Endpoint 4: Refresh Token
```
POST /api/auth/token

Request Body:
- grant_type=refresh_token
- refresh_token (required)
- client_id (required)

Response:
{
  "access_token": "new_access_token",
  "token_type": "Bearer",
  "expires_in": 3600,
  "scopes": [industrypilot, resumepilot]
}
```


Minimal Code for PKCE:
```
// utils/pkce.js

// Generate random code verifier (43-128 characters)
export function generateCodeVerifier() {
  const array = new Uint8Array(32);
  crypto.getRandomValues(array);
  return base64URLEncode(array);
}

// Generate code challenge from verifier
export async function generateCodeChallenge(verifier) {
  const encoder = new TextEncoder();
  const data = encoder.encode(verifier);
  const hash = await crypto.subtle.digest('SHA-256', data);
  return base64URLEncode(new Uint8Array(hash));
}

// Base64 URL encoding (without padding)
function base64URLEncode(buffer) {
  const base64 = btoa(String.fromCharCode(...buffer));
  return base64
    .replace(/\+/g, '-')
    .replace(/\//g, '_')
    .replace(/=/g, '');
}
```

usages
```
// LoginPage.jsx or AuthFlow.js

import { generateCodeVerifier, generateCodeChallenge } from './utils/pkce';

async function startOAuthFlow() {
  // 1. Generate PKCE pair
  const codeVerifier = generateCodeVerifier();
  const codeChallenge = await generateCodeChallenge(codeVerifier);
  
  // 2. Store verifier in localStorage (to use later in callback)
  localStorage.setItem('code_verifier', codeVerifier);
  
  // 3. Generate random state for CSRF protection
  const state = generateCodeVerifier(); // reuse same random function
  localStorage.setItem('oauth_state', state);
  
  // 4. Build authorization URL
  const params = new URLSearchParams({
    client_id: 'your_client_id',
    redirect_uri: 'http://localhost:3000/callback',
    response_type: 'code',
    scope: 'read write',
    state: state,
    code_challenge: codeChallenge,
    code_challenge_method: 'S256'
  });
  
  // 5. Redirect to authorization server
  window.location.href = `http://localhost:8000/api/auth/authorize?${params}`;
}

// Call this when user clicks "Login"
<button onClick={startOAuthFlow}>Login with OAuth</button>
```

Backend side:
```
# utils/pkce.py

import hashlib
import base64

def verify_code_challenge(code_verifier: str, code_challenge: str) -> bool:
    """
    Verify that code_verifier matches the code_challenge
    using SHA256 hashing
    """
    # Hash the verifier
    verifier_hash = hashlib.sha256(code_verifier.encode('utf-8')).digest()
    
    # Base64 URL encode (no padding)
    computed_challenge = base64.urlsafe_b64encode(verifier_hash).decode('utf-8').rstrip('=')
    
    # Compare
    return computed_challenge == code_challenge
```


Frontend:
Cookies
1. APP Based cookies -> .10xscale.ai
	1. access_token
	2. refresh_token
	3. scopes [IndustryPilot, ResumePilot]
Save
[hire10x] -> {access_token: access_token}
[industrypilot, Resume Pilot] -> {access_token: access_token}

2. Auth.10xscale.ai
	1. session_id



# Flow
1. Industry Pilot: 
	1. Check using logedin using cookies
	2. if not there redirect to auth.10xscale.ai
	3. Once back from auth continue with the app
2. Career Pilot:
	1. Check cookies and its available
	2. Check scope: is it supported
	3. Reuse access token no need to redirect
3. Hire10x:
	1. Check cookies and its available
	2. Now check scope and scope not there
	3. Page: Using this login, you dont have accces for this app
	4. Login-> redirect to auth
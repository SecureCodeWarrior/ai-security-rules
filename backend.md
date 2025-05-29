## General Secure Coding Practices  
- Validate and sanitize all user inputs to prevent injection attacks.  
- Use error handling without revealing sensitive information.  
- Avoid exposing sensitive data in API responses.  
- Do not hardcode any secrets (credentials, API keys, etc) in the source code or configuration files.

## HTTP Security headers and Cookies
- Use a Content Security Policy (CSP) to protect against XSS and clickjacking attacks.
- Set cookies with `HttpOnly`, `Secure`, and `SameSite` attributes.
- Enforce strict CORS policies for cookies. 

### CSRF Protection
Apply the following rules only if authentication relies on cookies instead of tokens.
- Use anti-CSRF tokens for state-changing operations.  
- Validate `Origin` and `Referer` headers for non-GET requests.  
- Require re-authentication before performing sensitive actions.  

## Output Rendering  
- Ensure output is encoded correctly for the corresponding context.  
- Escape special characters in output to prevent injection attacks.

## Database  
- Use parameterized queries or ORM to prevent injections.  
- Implement proper authentication and authorization.  
- Handle sensitive data properly.  
- Monitor security issues.
- Apply the principle of least privilege to database users.  

## API Security  
- Apply authentication and integrity checks on all API requests.  
- Configure CORS policies to restrict cross-origin access to trusted domains only.  
- Apply rate limiting to manage traffic.  
- Enforce security headers.  
- Handle errors securely without revealing sensitive details to end users.  
- Log access and actions for monitoring, auditing, and detecting abnormal activity.  

## External Requests  
- Restrict outbound requests to only necessary external services and internal endpoints.  
- Use allowlists to define permitted destinations instead of blocking known bad domains.  
- Disable unnecessary URL fetching capabilities in your application.  
- Validate and sanitize all user-supplied URLs before making requests.  
- Implement request timeouts and rate limits to prevent abuse.
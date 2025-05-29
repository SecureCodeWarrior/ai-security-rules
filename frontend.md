## Output Handling  
- Always prefer `textContent` or `setAttribute` over `innerHTML`, `outerHTML`, or `document.write`.  
- Sanitize dynamic content with libraries such as `DOMPurify` before DOM insertion.  
- Use Content Security Policy (CSP) headers to restrict script sources and disable unsafe inline scripts.  
- Apply strict input validation using allow-lists and well-defined patterns.

## CSS Handling
- Sanitize all user inputs before applying them to style properties.  
- Avoid dynamic inline styles where possible.  
- Use CSP with style nonces or hashes to validate inline CSS securely.  

## Clickjacking Protection
Apply these rules only in production or when generating a standalone application. Disable or relax them during development if you're embedding the app in iframes.
- Use the `Intersection Observer API` to detect UI overlays or clickjacking attempts.  
- Add frame-busting logic using JavaScript (`if (top !== self) top.location = self.location`).  
- Set `X-Frame-Options` header to `DENY` or use `Content-Security-Policy: frame-ancestors 'none';`  
- Use `SameSite` cookie attributes to reduce CSRF exposure across frames.

## Redirects
- Avoid using user input directly in redirects or forwards.  
- Use fixed URLs or allow-listed destinations based on internal logic.  
- Use URL identifiers (IDs) instead of full paths in parameters.  
- Validate redirect URLs to ensure they lead to trusted locations.  
- Implement an allowlist for allowed redirections.  
- Log all URL redirects for monitoring.  
- Use `rel="noopener noreferrer"` for external links to prevent reverse tabnabbing.
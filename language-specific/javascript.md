## General Coding Practices
- Enforce strict equality (`===` and `!==`) exclusively; never use loose equality (`==` or `!=`) to prevent type coercion bypasses.
- Apply `Object.freeze()` or `Object.seal()` to shared configuration objects and prototypes to prevent state tampering.
- Strictly attach `.catch()` to any un-awaited ("floating") Promises to avoid unwanted process termination.
- Sanitize objects before logging; explicitly remove sensitive fields (PII, tokens) rather than dumping entire objects via `console.log` or `JSON.stringify` to prevent sensitive data leakage.
- Set the `Content-Security-Policy: frame-ancestors 'none'` (or `'self'`) header on all HTTP responses to prevent clickjacking; strictly avoid legacy JS frame-busting (bypassable via sandbox) and use `X-Frame-Options` only in addition to `frame-ancestors` for legacy browser support.

## Database
- Use parameterized queries and pass parameters as a separate array argument to the execution method (e.g., `db.query(sql, [params])` or `db.execute(sql, [params])`).
- Strictly ban building SQL queries via template literals (`` ` ``) or string concatenation (`+`) to prevent SQL injection; variables must never be part of the query string itself.
- For ORMs and Query Builders (Prisma, Sequelize, TypeORM, Knex), use built-in methods (e.g., `User.findOne()`) and avoid raw SQL with string formatting.
- For NoSQL databases (MongoDB, etc.), validate that user inputs are the expected primitive types; object inputs can enable NoSQL injection (e.g., `{ $ne: null }`).
- Apply `LIMIT` clauses to user-facing queries to prevent mass data exfiltration.

## Code Execution
- Pass function references (not strings) to `setTimeout` and `setInterval`, and ban `eval()`/`new Function()` to prevent dynamic code execution.

## Cryptography & Secrets Management
- Use `crypto.getRandomValues()` for ID/token generation; strictly ban `Math.random()` for any security-critical logic.
- Strictly ban `crypto.createHash` (SHA-256/MD5) for password storage. Use memory-hard functions like `crypto.scrypt` (native) or `Argon2` to resist GPU cracking; downgrade to `crypto.pbkdf2` only when explicitly requested for FIPS/NIST compliance.
- When using `crypto.createCipheriv`, enforce authenticated encryption modes (e.g., `aes-256-gcm`) and strictly avoid unauthenticated modes (CBC, ECB, CTR).

## File System and I/O
- When resolving file paths, use `path.normalize()` and verify the result `startsWith()` the intended base directory; never use string concatenation to build file paths.
- Generate unique, random filenames (e.g., using `crypto.randomUUID()`) for all uploaded files; strictly ban using the user-supplied filename.
- Validate file types by inspecting binary "magic numbers" in the file `Buffer`; never rely on `req.file.mimetype` or file extensions, which can be easily spoofed.

## Networking
- When dynamically loading external scripts, explicitly set `script.integrity` and `script.crossOrigin` to enforce Subresource Integrity (SRI).
- Validate `window.location` assignments against a strict allow-list or map; never assign user-controlled strings directly to the URL to prevent open redirects and phishing.
- Restrict outbound requests to a strict domain allow-list; if arbitrary URLs are required, resolve and validate the destination IP against private ranges (e.g., `127.0.0.1`, `169.254.x.x`) to prevent SSRF and metadata exposure.

## Untrusted Data Handling
- When using objects as dictionaries to store dynamic, user-supplied keys, strictly use `new Map()` or `Object.create(null)`. Never use plain object literals (`{}`) for arbitrary input, as they inherit from `Object.prototype` and expose the application to `__proto__` pollution attacks.
- Strictly ban insecure "deep merge" patterns and "recursive extend" functions that do not explicitly filter `__proto__`, `constructor`, and `prototype` keys during recursive operations to prevent Prototype Pollution.
- Use explicit property assignment or allow-lists when copying data to models, persistent objects, session objects, or security-sensitive structures; strictly avoid `Object.assign(target, input)` or spread syntax (`{...input}`) to prevent Mass Assignment vulnerabilities.
- Iterate objects using `Object.keys()`, `Object.entries()`, or wrap `for...in` loops with `Object.hasOwn()` checks to avoid processing inherited prototype properties.
- Avoid nested quantifiers in RegExp (e.g., `(a+)+`) and enforce input length limits to prevent Event Loop blocking (ReDoS) and Denial of Service.
- Avoid using ES6 Template Literals (`\`${input}``) to interpolate untrusted strings into SQL queries or HTML output.
- Use standard `JSON.parse()` exclusively for data interchange; strictly ban serialization libraries that support custom types or functions (e.g., `js-yaml` with unsafe schema) to prevent remote code execution.

## DOM & UI Handling
- Use `textContent` or `innerText` for DOM insertion; strictly avoid `innerHTML` or `document.write` unless content is explicitly sanitized to prevent DOM-based XSS.
- Select DOM elements using explicit methods (`document.getElementById`, `querySelector`); never access elements via global window properties to prevent DOM clobbering.
- Validate user-provided styles against an allow-list of properties before assigning to `style.innerHTML` or `cssText` to prevent CSS Injection.


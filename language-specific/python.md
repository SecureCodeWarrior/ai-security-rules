## General Coding Practices
- Do not use `assert` statements for security checks or input validation.

## Database
- Use parameterized queries and parameters as a second argument to `cursor.execute()` (e.g., `cursor.execute(sql, (param,))`).
- For ORMs (SQLAlchemy, Django), use ORM methods and avoid raw SQL with string formatting.

## Code Execution
- Do not use `eval()` or `exec()` with data from untrusted sources.
- Always use `subprocess.run()` with `shell=False` (the default). Pass commands and arguments as a list (e.g., `subprocess.run(['ls', '-l', a_variable])`).

## Cryptography & Secrets Management
- Use the `secrets` module for generating all security-sensitive tokens, keys, or passwords. Do not use the `random` module.
- Use `hmac.compare_digest()` to compare secrets. Do not use the `==` operator for secrets like API keys or tokens.
- When working with secret or sensitive information in variables, after use set the variable to `None` and force garbage collection.

## File System and I/O
- Validate all file paths built from user input. Use `os.path.abspath()` to canonicalize the path, then verify it is inside the intended base directory using `os.path.commonpath([full_path, base_dir]) == os.path.abspath(base_dir)`.
- Use secure functions for creating temporary files. Prefer `tempfile.mkstemp()` or `tempfile.NamedTemporaryFile` over `tempfile.mktemp()`.

## Networking
- Configure secure TLS/SSL contexts. Use `ssl.create_default_context()` or `ssl.SSLContext` with modern protocols (e.g., `ssl.PROTOCOL_TLS_CLIENT`).
- Validate URLs with `ipaddress` before connecting to prevent SSRF.

## Deserialization and Data Parsing
- Never use `pickle`, `cPickle`, or `dill` to deserialize data from untrusted sources.
- Do not use `shelve` or `marshal` to deserialize untrusted data.
- When parsing YAML, always use `yaml.safe_load()`. Never use `yaml.load()`.
- When parsing XML, disable external entity resolution. Use `xml.etree.ElementTree.XMLParser` with `resolve_entities=False`.
- When parsing data with `json`, limit the size of the input.
- Validate regex patterns for ReDoS vulnerabilities. Avoid nested quantifiers like `(a+)+` or `(a*)*`.




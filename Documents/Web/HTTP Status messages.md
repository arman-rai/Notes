
**Source:** HTTP Messages guide (HTTP/1.1 examples) ([GitHub](https://github.com/mdn/mdn-http-observatory?utm_source=chatgpt.com "Backend for HTTP Observatory on MDN"))

## Web Pentesting

- **Manipulate start-line**: change methods, target forms
- **Header tampering**: e.g., Host, Referer, User‑Agent, cookies
- **Body payloads**: inject SQL/XSS/Payload-only in body methods    
- **Observe status codes**: e.g., 30x redirects, 401 auth, 500 errors
- **HTTP/2 inspection**: use tools like [`nghttp`](https://github.com/nghttp2/nghttp2) or Burp with HTTP/2 support

---
### 1. Anatomy Overview

- **Start‑line**: Request‑line or status‑line
- **Headers** (metadata)
- **Blank line** separating head and body
- **Body**: optional payload (form data, JSON, HTML, etc.)  
	- Remember head vs. body—essential for parsing and fuzzing.

---
### 2. Request Structure

```http
<method> <request-target> <protocol>
Headers…
<blank line>
<body?>
```

- **Methods**: GET, POST, PUT, DELETE, OPTIONS, CONNECT, PATCH, TRACE
- **Targets**:
    - origin-form (normal): `/path?query`
    - absolute-form (proxies): `https://…`
    - authority-form: `host:port` (CONNECT)
    - asterisk-form: `*` (OPTIONS)
- **Headers**: Case-insensitive, `Name: Value` format
- **Body**: only with POST/PUT/PATCH (e.g., form-encoded, JSON, multipart)

---
### 3. Response Structure

```http
HTTP/1.1 <status-code> <status-text>
Headers…
<blank line>
<body?>
```

- Status codes: 1xx (info), 2xx (success), 3xx (redirect), 4xx (client error), 5xx (server error) ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages?utm_source=chatgpt.com "HTTP messages - MDN Web Docs - Mozilla"), [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status?utm_source=chatgpt.com "HTTP response status codes - MDN Web Docs - Mozilla"))
- Headers: metadata about content, caching, cookies, security, etc.

---
### 4. HTTP/2 Differences

- Binary framing, not plain text
- Uses pseudo‑headers (`:method`, `:path`, `:status`, etc.) ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages?utm_source=chatgpt.com "HTTP messages - MDN Web Docs - Mozilla"))
- Same semantics—head/body separation unchanged

---

# Security Best Practices (XSS, CSRF)

Web application security is crucial to protect users and their data from malicious attacks. Two common security vulnerabilities are Cross-Site Scripting (XSS) and Cross-Site Request Forgery (CSRF). Implementing security best practices helps in mitigating these and other threats.

## Cross-Site Scripting (XSS)

XSS is a type of security vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users. These scripts can steal information, hijack user sessions, or redirect users to malicious websites.

### Types of XSS

1. **Stored XSS**: Malicious script is stored on the server and served to users.
2. **Reflected XSS**: Malicious script is reflected off a web server, such as in an error message or search result.
3. **DOM-based XSS**: Malicious script manipulates the DOM of the page directly on the client side.

### Prevention Techniques

1. **Input Validation and Sanitization**: Validate and sanitize all user inputs to remove any malicious code.

   ```javascript
   function sanitize(input) {
     return input.replace(/</g, "&lt;").replace(/>/g, "&gt;");
   }
   ```

2. **Output Encoding**: Encode data before rendering it in the browser to prevent execution of malicious scripts.

   ```javascript
   function encodeForHTML(str) {
     return str
       .replace(/&/g, "&amp;")
       .replace(/</g, "&lt;")
       .replace(/>/g, "&gt;")
       .replace(/"/g, "&quot;")
       .replace(/'/g, "&#039;");
   }
   ```

3. **Content Security Policy (CSP)**: Implement CSP to restrict sources from which scripts can be loaded.

   ```html
   <meta
     http-equiv="Content-Security-Policy"
     content="default-src 'self'; script-src 'self';"
   />
   ```

4. **Use Secure Libraries**: Use libraries and frameworks that are designed to prevent XSS, such as React, Angular or Svelte.

## Cross-Site Request Forgery (CSRF)

CSRF is an attack that tricks a user into performing actions on a web application where they are authenticated. It exploits the trust that a site has in the user's browser.

### Prevention Techniques

1. **CSRF Tokens**: Use CSRF tokens to ensure that requests made on behalf of a user are intentional.

   ```html
   <input type="hidden" name="csrf_token" value="GENERATED_CSRF_TOKEN" />
   ```

2. **SameSite Cookies**: Use SameSite attribute in cookies to restrict cross-site request.

   ```http
   Set-Cookie: sessionId=abc123; SameSite=Strict
   ```

3. **Double Submit Cookie**: Send CSRF token both as a cookie and as a request parameter.

   ```javascript
   function getCSRFToken() {
     return document.cookie
       .split("; ")
       .find((row) => row.startsWith("csrf_token"))
       .split("=")[1];
   }

   fetch("/api/data", {
     method: "POST",
     headers: {
       "CSRF-Token": getCSRFToken(),
     },
     body: JSON.stringify(data),
   });
   ```

4. **Referer Header Check**: Validate the referer header to ensure that the request originates from the same site.

   ```javascript
   function checkReferer(req) {
     const referer = req.headers.referer;
     if (!referer || !referer.startsWith("https://yourdomain.com")) {
       throw new Error("Invalid referer");
     }
   }
   ```

### Additional Security Best Practices

1. **HTTPS**: Use HTTPS to encrypt data in transit, protecting it from interception and tampering.
2. **Security Headers**: Implement security headers like X-Content-Type-Options, X-Frame-Options, and X-XSS-Protection.

   ```http
   X-Content-Type-Options: nosniff
   X-Frame-Options: DENY
   X-XSS-Protection: 1; mode=block
   ```

3. **Access Control**: Implement proper access controls to ensure that users can only access resources they are authorized to.

4. **Regular Security Audits**: Conduct regular security audits and vulnerability assessments to identify and fix potential security issues.

### Summary

- **XSS**: Prevent by input validation, output encoding, CSP, and using secure libraries.
- **CSRF**: Prevent by using CSRF tokens, SameSite cookies, double submit cookies, and referer header checks.
- **General Security Best Practices**: Use HTTPS, implement security headers, enforce access controls, and conduct regular security audits.

# Cross-Site Scripting (XSS)

Labs from PortSwigger's Web Security Academy, both injecting script into an HTML context where the application applies no output encoding

## Lab 1: Reflected XSS, nothing encoded

**Goal:** execute JavaScript via the search feature

The search term is echoed straight back into the response HTML. Submitting:

```
<script>alert(1)</script>
```

in the search box runs the script immediately in the response page

**Root cause:** the search input is reflected into the page without output encoding. The payload is delivered per-request, so an attacker would weaponize it by getting a victim to click a crafted link containing the script

## Lab 2: Stored XSS, nothing encoded

**Goal:** execute JavaScript that fires for anyone viewing a blog post

Submitting a comment of:

```
<script>alert(1)</script>
```

stores the payload. It then executes in the browser of every user who loads that post

**Root cause:** the comment is saved and later rendered without output encoding. Stored XSS is more dangerous than reflected because it is persistent and needs no interaction beyond viewing the affected page

## Remediation

- **Context-aware output encoding** at the point the data is written into the page (HTML-encode `<`, `>`, `"`, `'`, `&` for an HTML context). This is the primary defense
- **Content Security Policy (CSP)** as defense-in-depth. A policy that blocks inline script would stop `<script>alert(1)</script>` from running even if the encoding were missed. This is the same `Content-Security-Policy` header I now enforce on my client sites, verified by my domain-scanner

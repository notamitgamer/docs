# Cryptography & Security Model

## Zero-knowledge cloud password protection

When a user applies a password to a Cloud Share snippet, the plaintext password is **never** transmitted to Firebase. Veyrix uses the native Web Crypto API to generate a SHA-256 hash locally instead:

```javascript
// Internal Utility Method
async function hashPassword(password) {
    const msgBuffer = new TextEncoder().encode(password);
    const hashBuffer = await crypto.subtle.digest('SHA-256', msgBuffer);
    const hashArray = Array.from(new Uint8Array(hashBuffer));
    return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}
```

## Threat model assumptions

### 1. Physical security

Veyrix relies completely on the local OS and browser profile. If an attacker gains physical, unlocked access to the device, or compromises the browser profile (e.g. via a malicious extension), the IndexedDB store is considered compromised.

### 2. Cross-Site Scripting (XSS)

Veyrix is an editor, not an evaluator. The Ace Editor parses content into Abstract Syntax Trees (ASTs) for highlighting — it does not execute code within the DOM. DOM string interpolations are secured via native `textContent` mappings.

### 3. Cloud anonymity

Firebase interactions use `signInAnonymously()`. Data is tied to a temporary, anonymous session UID. Firebase Security Rules are assumed to enforce read/write access correctly based on the snippet UID, but shared URLs are considered semi-public unless protected with the SHA-256 password hash described above.

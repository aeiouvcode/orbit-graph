# Orbit security model

Orbit is a static, local-first app. There are no analytics, cookies, accounts, servers, API keys, or network calls. The Content Security Policy blocks scripts outside the app, frames, objects, media, forms, and outbound connections.

## Encryption
When enabled by the user, project state is encrypted before being written to localStorage and exports are encrypted too. Orbit derives an AES-256-GCM key from the user's passphrase with PBKDF2-HMAC-SHA-256, a random 128-bit salt, and 310,000 iterations. Every encryption uses a new random 96-bit IV. The passphrase and CryptoKey are never persisted and disappear when the tab closes. AES-GCM authenticates ciphertext, so a wrong passphrase or modified file fails closed.

This is encryption at rest on one device, not multi-party end-to-end messaging. A compromised browser, malicious extension, or script running in the open tab can read unlocked data. Lost passphrases cannot be recovered.

Imported files are capped at 2 MB and project shape, types, limits, and values are checked before rendering. User text inserted into markup is escaped.

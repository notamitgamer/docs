---
label: Mojic
icon: lock
order: 750
---

# Mojic

**Operation Ironclad: obfuscate C source code into a randomized, password-seeded stream of emojis.**

Mojic (Magic + Emoji + Logic) is a CLI tool that transforms readable C code into an unrecognizable, chaotic stream of emojis. Unlike a simple substitution cipher, Mojic uses your password to seed a cryptographically strong PRNG, creating a unique "Emoji Universe" and rolling cipher for every session.

!!!danger Project discontinued (v2.1.5)
Mojic is discontinued. v2.1.5 is the final patch to the GitHub repository.

The maintainer lost access to the npm account (forgotten password, and the recovery passcode file was lost during a Linux migration), so `npm install mojic` currently fails with a 404 — the published `@notamitgamer/mojic` dependency can no longer be patched.

**To keep using it, install from source instead:**
```bash
git clone https://github.com/notamitgamer/mojic.git
cd mojic
npm install
npm link
```
This makes the `mojic` command available globally, same as an npm install would.
!!!

## Key features

- **AES-256-CTR PRNG** — a cryptographically secure PRNG (seeded via Scrypt) drives shuffling and polymorphism
- **Polymorphic keywords** — common C keywords (`int`, `void`, `return`) map to emojis that change every time they appear, based on PRNG state — frequency analysis doesn't work
- **XOR whitening** — raw data (whitespace, variable names) is XORed with the AES keystream before encoding, so repeating patterns like 4-space indentation never produce the same emoji sequence twice
- **Base-1024 compression** — non-keyword code is compressed with a custom scheme (5 bytes → 4 emojis) to keep file size manageable
- **Integrity sealed** — every file ends with an HMAC-SHA256 signature; tampering triggers an immediate `FILE_TAMPERED` error
- **Moon Header Protocol** — metadata (salt + auth check) is encoded with a Moon/Clock phase alphabet (`🌑🌒🕐`), so an incorrect password is detected instantly, before decryption even starts
- **Stream architecture** — built on Node.js `Transform` streams for large files with minimal memory footprint

## Get started

- [Installation](installation.md)
- [CLI Usage](usage.md)
- [How It Works (Operation Ironclad)](algorithm.md)

---
label: CLI Usage
order: 730
---

# CLI Usage

## 1. Encrypting code (`encode`)

Transforms a `.c` file into a `.mojic` file. You'll be prompted to create a password — it's required to decrypt.

```bash
# Encrypt a single file
mojic encode main.c

# Encrypt an entire directory recursively
mojic encode ./src -r

# Flatten/minify code structure before encryption (removes newlines/indentation)
mojic encode main.c --flat
```

## 2. Decrypting code (`decode`)

Restores the original C code from a `.mojic` file.

```bash
# Decrypt a single file
mojic decode main.mojic

# Decrypt an entire directory recursively
mojic decode ./src -r
```

## 3. Security & rotation tools (`srt`)

Manage encrypted files without ever revealing their plaintext contents.

```bash
# Rotate password: changes the password of an encrypted file
mojic srt --pass secret.mojic

# Re-encrypt: re-shuffles the entropy (new salt) with the SAME password
# useful to change the visual emoji pattern without changing the password
mojic srt --re secret.mojic
```

Continue to [How It Works](algorithm.md).

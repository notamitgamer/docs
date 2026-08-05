# Under the Hood: Operation Ironclad

Mojic v2.1.0 implements a custom crypto-system dubbed "Operation Ironclad."

## 1. Derivation phase

- **Input:** user password + 32-byte random salt
- **KDF:** `Scrypt` (N=16384, r=8, p=1)
- **Output:** 80 bytes — 32 bytes AES key, 16 bytes AES IV, 32 bytes HMAC auth key

## 2. The Emoji Universe

The engine generates a universe of roughly 1,100 valid unicode characters (emoticons, transport, symbols), then **shuffles** it using the AES-256-CTR CSPRNG initialized with the derived key.

## 3. Polymorphic encryption

- **C keywords:** the engine detects C keywords (e.g. `while`) and assigns each one a "base emoji" from the shuffled universe.
- **The twist:** it doesn't just print the base emoji — it calculates a random offset using the PRNG to pick a *different* emoji that still maps back to the keyword. That means `int` might render as 🚀 on line 1 and 🌮 on line 5, making frequency analysis useless.

## 4. XOR whitening

Before encoding non-keyword data (variable names, strings, whitespace), the engine generates a random mask from the AES stream and XORs the raw data with it. This turns repetitive patterns — like indentation or common variable names — into white noise before they're converted to emojis.

## 5. Base-1024 encoding

The whitened data is buffered into 5-byte chunks, treated as a single large integer, and converted into 4 base-1024 digits, each mapped to an emoji.

## 6. The header

The salt and a 4-byte auth check are written to the file header using the Moon/Clock alphabet (`🌑🌒🌓🌔...`). This lets Mojic report "Incorrect Password" instantly, rather than churning out garbage data first.

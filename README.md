# Secure Communications – Lab 11: Decoding an Intercepted Message

## Input
- `encryptme.py` – damaged encoder script (secret and `count` unknown)
- `intercepted.txt` – intercepted encoded message (35,138 bytes)

## Encoding scheme (from `encryptme.py`)
- Start: `'2' + base64(secret)`
- Each round, a random step is applied and its number (1/2/3) is prepended:
  - **step1** – ROT13
  - **step2** – Base64 encode
  - **step3** – Caesar shift +4 (lowercase only)

## Decoding (`decryptme.py`)
1. Read the leading digit and strip it
2. Undo that step: 1 → ROT13, 2 → Base64 decode, 3 → Caesar shift −4
3. Repeat until the text no longer decodes as a layer

Run: `python3 decryptme.py -v -f intercepted.txt`

## Result
- Layers decoded: **68** → `count = 67`
- Plaintext: **"Why do elephants have big ears?"**

## Takeaway
This is encoding, not encryption: no key, every step is public and reversible,
and each layer is labelled with the step used.

# Blaze Letters — sealed letters on Bitcoin Cash

**BCH BLAZE 2026 — Mainnet Track.** Write a short letter, seal it on-chain, and anyone
who pays your price gets the decryption key. One static page, no server, no account.

Live demo: https://arukh89.github.io/bch-blaze-mainnet/
(Chipnet test build: the same URL with `?net=chipnet`.)

## How it works

1. **Seal.** The author writes a letter (max 100 chars, max 150 UTF-8 bytes so it fits in
   one OP_RETURN). The browser encrypts it with a fresh AES-256-GCM key and posts a
   transaction: `OP_RETURN [ciphertext, sha256(key)]` + a 546-sat dust output to the
   author's address. The key never leaves the author's browser.
2. **Pay.** A reader pays the author's price to the author's address, with
   `OP_RETURN [sha256(key)]` — a public, on-chain receipt for that letter.
3. **Reveal.** The author's open tab detects the payment and broadcasts
   `OP_RETURN [key]`. The reader verifies `sha256(key)` against the seal, then decrypts
   the letter locally. Every step is a real mainnet transaction (plain P2PKH + OP_RETURN).

## Wallets

- **Built-in wallet** — a fresh in-browser wallet (mainnet.cash), created per tab.
  Fund it with a small amount first. No seed phrase is ever asked for or stored.
- **WizardConnect** — connect Paytaca or Cashonize by scanning the QR code. The wallet
  signs each transaction (CashScript `TransactionBuilder` + `generateWcTransactionObject`
  + `inputPaths`); the dapp never sees a key or a seed.

## Limits, stated plainly

- Letters are short on purpose (one OP_RETURN, max 220 bytes).
- The author's tab must stay open to reveal. If it closes, the letter stays sealed
  until the author re-opens the Watch tab with the saved key (the key is shown after
  sealing and stored in that browser's localStorage).
- A full seal → pay → reveal loop costs well under $1 in fees (about 1 sat/byte).

## Files

- `index.html` — the whole app (mainnet.cash 3.0.0 + CashScript 0.14.0 + WizardConnect
  0.2.8/0.2.11 via CDN; no build step).
- `CHIPNET-TEST.md` — the chipnet test plan.

## Links

- Presentation: https://docs.google.com/presentation/d/1HbALM9_lGp8_zHpxacGp5PkfLw4vmmKOTYjSIGYVapk/edit?usp=sharing
- CashTokens donation address: `bitcoincash:qpsrfdv7rsaxafweujqe56t3avzeuuj5fyz2xsm762`
- BCH BLAZE 2026: https://dorahacks.io/hackathon/bchblaze2026/detail

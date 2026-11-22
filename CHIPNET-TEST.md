# Chipnet test plan (Blaze Letters)

1. Open the demo with `?net=chipnet` (pill must read CHIPNET).
2. Connect the built-in wallet; copy its address.
3. Fund it: https://tbch.googol.cash (select chipnet) or https://apecs.dev/bch/faucets (PoW claim, 10,000 sats).
4. Seal a letter (price 2000 sats) → note the seal txid + letter link + key.
5. In a second tab (or second wallet), open the letter link → pay 2000 sats.
6. First tab (Watch) must auto-detect the payment and broadcast the reveal tx.
7. Second tab must show the decrypted letter with the on-chain verification badge.
8. Confirm all three txids on https://chipnet.chaingraph.cash/.
9. Also test "Reveal now" with a pasted payment txid (covers payments made before the tab opened).
10. If any step fails, note the exact error + txid before changing code.

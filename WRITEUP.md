
## Lab 4.4: Evidence Management and Chain of Custody

Signed run: 36329871614, vault `cgep-lab-grc-evidence-vault-67bbfb2f`, receipt at `evidence/lab-4-4/receipt.json`.

| Property | Artifact that proves it | How it's checked |
|---|---|---|
| Authenticity | `.sig.bundle` (Fulcio cert bound to this repo's GitHub Actions OIDC identity) | `cosign verify-blob` → `Verified OK` |
| Integrity | `.sha256` sidecar and the `sha256` in `receipt.json` | `verify-evidence.sh` recomputes SHA-256 and compares |
| Timeliness | Rekor transparency-log entry referenced in `.sig.bundle` | `cosign verify-blob` confirms the logged timestamp |
| Preservation | S3 Object Lock retention on the bundle (vault from Lab 2.5) | `verify-evidence.sh` checks `RetainUntilDate` is in the future |

Result: `verify-evidence.sh 36329871614` printed `CHAIN INTACT`.

Tamper test: appending one line to a downloaded copy changed its SHA-256 from `8b61031e…29eb4` to `08f83b14…9617e`, so the integrity check fails. The vault copy cannot be overwritten because of Object Lock.

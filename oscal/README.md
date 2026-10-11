# OSCAL layer

| File | Describes | Evidence |
|---|---|---|
| `components/compliant-s3.json` | `terraform/primitives/compliant-s3`: NIST 800-53 Rev 5 controls sc-28, ac-3, au-3, cm-6 | Signed bundle in `s3://cgep-lab-grc-evidence-vault-67bbfb2f/runs/38115197838/` produced by the `grc-gate` workflow |
| `profiles/cge-p-minimum.json` | Selection of the four controls claimed above from the NIST 800-53 Rev 5 catalog | — |

## Verify the chain

```bash
EVIDENCE_VAULT=cgep-lab-grc-evidence-vault-67bbfb2f bash scripts/verify-evidence.sh 38115197838 --profile <your-aws-profile>
```

Expected output: `Verified OK` then `CHAIN INTACT`.

**Note:** the vault uses 1-day GOVERNANCE Object Lock retention. A bundle fails the retention check 24 hours after upload. Rerun the `grc-gate` workflow and update the evidence `href`s to the newest run before verifying.

Validation output: `evidence/lab-6-1/trestle-validate.txt` · Verify output: `evidence/lab-6-1/verify-evidence.txt`

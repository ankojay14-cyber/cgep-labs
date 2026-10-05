# AWS Security Services Baseline (Lab 5.2)

Account-level, always-on evidence sources deployed with Terraform.

## Control mapping

| Service | NIST 800-53 Rev 5 controls | How it satisfies them |
|---|---|---|
| CloudTrail (`cgep-lab-mgmt`) | AU-2, AU-12 | Multi-region trail records all management events, including global services |
| CloudTrail log-file validation | AU-10 (also supports AU-9) | Hourly signed digest files make after-the-fact log tampering detectable |
| S3 trail bucket | AU-9 | SSE (AES256) encryption, all public access blocked, bucket policy scoped by `aws:SourceArn` |
| Security Hub (NIST 800-53 + FSBP) | RA-5, SI-4 | Continuous automated checks; findings normalized and mapped to controls |
| AWS Config | CM-2, CM-6, CM-8 | **Not deployed in this lab.** See the gap below |

## Documented gap: AWS Config

Config was intentionally not deployed, to limit cost. Security Hub reports the gap itself,
as a CRITICAL finding: "AWS Config should be enabled and use the service-linked role for
resource recording." This finding is in the evidence file and serves as machine-generated
documentation of the CM-family gap.

## Evidence

- `evidence/lab-5-2/security-hub-findings.json`: Security Hub findings captured 2026-10-03
  (account 804450520828, us-east-1)
- Vault: `cgep-lab-grc-evidence-vault-67bbfb2f`, key `runs/lab-5-2/security-hub-findings.json`
- Vault VersionId: 1_P6ZcFUzCSspopsD9ggi5beoFWyPfaA
- Object Lock: GOVERNANCE mode, retained until 2026-10-05T00:10Z (applied by bucket default on upload)

## Deploy / teardown

    terraform init && terraform apply
    terraform destroy    # standards checks bill while running; tear down same day
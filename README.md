# CGEP Labs

Hands-on GRC Engineering labs that translate NIST 800-53 requirements into infrastructure-as-code, Policy-as-Code, automated compliance testing, and tamper-resistant evidence collection. Each lab produces machine-readable JSON evidence rather than relying on screenshots.

| Lab | What it built | Evidence |
|---|---|---|
| 2.3 | Compliant AWS S3 bucket (primary + log bucket) enforcing SC-28, AC-3, AU-3, AU-6, CM-6 | [evidence/lab-2-3](evidence/lab-2-3) |
| 2.4 | Reusable GCP GCS bucket module (`compliant-gcs-bucket`) with dev/prod consumers and a negative test, enforcing SC-12, SC-13, SC-28, AC-3, AU-11, CM-6 | [evidence/lab-2-4](evidence/lab-2-4) |
| 2.5 | Object Lock evidence vault (AWS) and `capture-evidence.sh`, hashing and archiving Terraform plan/state as tamper-resistant evidence | [evidence/lab-2-5](evidence/lab-2-5) |
| 3.3 | Rego compliance policies (GCP) for SC-28, AC-3, CM-6, with OPA unit tests and a Terraform-plan fixture | [evidence/lab-3-3](evidence/lab-3-3) |
| 3.4 | AWS variants of the same three policies, plus `policy-gate.sh` wiring the full six-policy library into a Conftest CI gate | [evidence/lab-3-4](evidence/lab-3-4) |
| 4.4 | Keyless Cosign/Sigstore signing of each run's evidence bundle, uploaded to the Object Lock vault with a receipt, plus `verify-evidence.sh` proving authenticity, integrity, timeliness and preservation (`CHAIN INTACT`), enforcing AU-9, AU-10, SI-7 | [evidence/lab-4-4](evidence/lab-4-4) |
| 5.2 | AWS security services baseline in Terraform (`terraform/baselines/aws`), mapped to AU-2, AU-9, AU-10, AU-12, RA-5, SI-4. Captured Security Hub findings as JSON, including a CRITICAL "AWS Config should be enabled" finding documented as a CM-family gap, and stored the findings in the Object Lock vault with the VersionId recorded for chain of custody | [evidence/lab-5-2](evidence/lab-5-2) |
| 5.4 | GCP security services baseline in Terraform (`terraform/baselines/gcp`): Workload Identity Federation scoped to this repo so GitHub Actions authenticates with no service-account keys (AC-2, IA-5), proven by a `wif-demo` workflow; Data Access audit logs, which are off by default, enabled for Storage, KMS and IAM (AU-2, AU-12). Org Policy constraints (CM-6, AC-2, AC-3) are defined but documented as a gap because they require a GCP Organization, with WIF as the compensating control | [evidence/lab-5-4](evidence/lab-5-4) |
| 6.1 | OSCAL component definition for `compliant-s3` (SC-28, AC-3, AU-3, CM-6) and a minimum control profile against the NIST 800-53 Rev 5 catalog, validated and resolved with compliance-trestle. Each control names its enforcing Terraform resource and links to the signed vault bundle, so an assessor can go from control claim to evidence to `CHAIN INTACT` without access to the environment | [oscal](oscal) · [evidence/lab-6-1](evidence/lab-6-1) |

# CGEP Labs

Hands-on labs mapping infrastructure-as-code to NIST 800-53 controls, building toward a Policy-as-Code capstone. Each lab's evidence is captured as JSON, not screenshots.

| Lab | What it built | Evidence |
|---|---|---|
| 2.3 | Compliant AWS S3 bucket (primary + log bucket) enforcing SC-28, AC-3, AU-3, AU-6, CM-6 | [evidence/lab-2-3](evidence/lab-2-3) |
| 2.4 | Reusable GCP GCS bucket module (`compliant-gcs-bucket`) with dev/prod consumers and a negative test, enforcing SC-12, SC-13, SC-28, AC-3, AU-11, CM-6 | [evidence/lab-2-4](evidence/lab-2-4) |
| 2.5 | Object Lock evidence vault (AWS) and `capture-evidence.sh`, hashing and archiving Terraform plan/state as tamper-resistant evidence | [evidence/lab-2-5](evidence/lab-2-5) |
| 3.3 | Rego compliance policies (GCP) for SC-28, AC-3, CM-6, with OPA unit tests and a Terraform-plan fixture | [evidence/lab-3-3](evidence/lab-3-3) |
| 3.4 | AWS variants of the same three policies, plus `policy-gate.sh` wiring the full six-policy library into a Conftest CI gate | [evidence/lab-3-4](evidence/lab-3-4) |
| 4.4 | Keyless Cosign/Sigstore signing of each run's evidence bundle, uploaded to the Object Lock vault with a receipt, plus `verify-evidence.sh` proving authenticity, integrity, timeliness and preservation (`CHAIN INTACT`), enforcing AU-9, AU-10, SI-7 | [evidence/lab-4-4](evidence/lab-4-4) |
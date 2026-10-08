# Lab 5.4: GCP Security Services Baseline

Project: `project-ac718b3e-a9c2-49e8-9ee` (standalone, no Organization)

## What's deployed
| Control | Status | Evidence |
|---|---|---|
| Workload Identity Federation (AC-2, IA-5) | Deployed | Pool `github-actions` ACTIVE; provider condition locked to `ankojay14-cyber/cgep-labs` |
| Data Access audit logs (AU-2, AU-12) | Deployed | `evidence/lab-5-4/iam-policy.json` |
| Org Policy constraints (CM-6, AC-2, AC-3) | **Not deployable** | `evidence/lab-5-4/org-policies.txt` |

## Key lesson: Data Access logs are off by default
GCP records Admin Activity logs automatically, but Data Access logs (DATA_READ,
DATA_WRITE, ADMIN_READ) are disabled by default for most services. This is the
most common GCP audit finding. `audit_logs.tf` enables them for storage, cloudkms
and iam.

## Org Policy gap
The three constraints (`storage.uniformBucketLevelAccess`,
`iam.disableServiceAccountKeyCreation`, `compute.requireOsLogin`) are defined in
`org_policy.tf.disabled`. Applying them failed with `orgpolicy.policies.create`
PERMISSION_DENIED: Org Policy requires a GCP Organization, and this project has
none. `roles/orgpolicy.policyAdmin` can only be granted at the Organization level.

Impact: the preventive layer is missing, so service account key creation is
not blocked at the API. Compensating control: WIF removes the need for keys.
Remediation: rename the file to `org_policy.tf` in a project under an Organization.

## WIF
GitHub Actions authenticates with a short-lived OIDC token exchanged for a
temporary access token. No service account JSON key exists anywhere in the repo.

# Deployment and Teardown Runbook

**Template only. Complete against the verified hosting architecture before deployment.**

## Preconditions
Approved service/region, reviewed cost and account limits, least-privilege IAM, secret storage, dataset/model licensing, health checks, safe errors, reset/rollback, and public endpoint threat model.

## Deployment sequence
1. Confirm target commit and PR review.
2. Run available unit, contract, integration, security, and build checks.
3. Verify no secrets/raw datasets in artifacts.
4. Deploy scoring service; verify health and model version.
5. Deploy MCP server; verify exposed tools and auth.
6. Configure persistence and synthetic fixtures.
7. Deploy dashboard/client adapter.
8. Run end-to-end demo.
9. Verify denial, confirmation, cancellation, failure behavior, and simulation disclosure.
10. Record commit, deployment timestamp, service configuration, verification evidence, and limitations without credentials.

Do not follow this until service selection, terms, cost, and deployment constraints are researched and approved.

## Rollback
Disable public access or revert to last known working commit. Do not silently migrate/delete persistent data. Revoke/rotate exposed credentials. Record incident and recovery without secrets in issues. Verify safe behavior before reopening.

## Cost/security
Prefer minimal short-lived resources; restrict public writes; configure budget alerts where available but do not assume alerts prevent all charges. Avoid cloud credentials in untrusted PR workflows. Remove unused endpoints/resources.

## Teardown
- [ ] Public endpoints disabled or explicitly approved to remain.
- [ ] Temporary cloud resources removed.
- [ ] Data/model artifacts handled according to license/retention.
- [ ] Unneeded secrets revoked/rotated.
- [ ] Usage/cost checked.
- [ ] README reflects what remains live.
- [ ] Evidence added to build journal.

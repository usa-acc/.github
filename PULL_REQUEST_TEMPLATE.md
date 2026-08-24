## Purpose and change summary

Describe the problem, intended and user-visible behavior, owning repository,
affected components, compatibility impact, staged rollout, and rollback path.
Mark non-applicable checks as `N/A` with a reason.

## Review path

- [ ] All commits are on a non-default topic branch and this pull request is the only proposed path into the protected default branch.
- [ ] No generated tool, bot, migration runner, or deployment process writes directly to `main`, `master`, or another protected default branch.
- [ ] The change is small enough to review, or its staged rollout and follow-up pull requests are identified.

## Scope, contracts, and dependencies

- [ ] The change is focused and does not silently cross repository ownership boundaries.
- [ ] Cross-repository dependencies are pinned by immutable commit, lockfile, or released Zed package.
- [ ] Shared functionality is imported from its owning repository, and no `*-infra` repository is introduced as a `*-monorepo/apps` submodule.
- [ ] Public contracts are generated from their canonical schema/interface source and consumer compatibility was checked.
- [ ] Breaking changes document migration, failure behavior, rollback, and staged rollout.

## SQL, persistence, and state

- [ ] No SQL changes exist, or every declaration has a registered `<organization>.<domain>` identity, stable object prefix where needed, and explicit owner.
- [ ] Domain SQL may remain with its owner, while ordering, checksums, drift detection, and promotion are registered through `declarative-migrations`.
- [ ] JSON Schema, generated interfaces, ORM models, fixtures, and migration declarations were updated and checked deterministically together.
- [ ] Application startup validates schema compatibility and does not apply production DDL.
- [ ] Destructive changes, backfills, tenant isolation, RLS/authorization, idempotency, and state-machine invariants have evidence.

## Infrastructure and security

- [ ] App manifests remain app-owned; cluster composition uses `oresoftware/k8s-cluster` and shared components use `oresoftware/k8s-libs-and-shared-defs`.
- [ ] Workload identity, restricted Pod Security, default-deny networking, explicit egress, non-root execution, probes, resources, secrets, and immutable references were considered.
- [ ] Authentication and authorization failures are fail-closed and sensitive operations are auditable.
- [ ] Secrets, credentials, personal data, user content, and private-repository inventory are excluded from source, logs, fixtures, and artifacts.

## Verification and observability

- [ ] Zed lifecycle hooks run deterministic format, lint, build, contract, and publish checks without replacing language-native validation.
- [ ] Unit, integration, adversarial, migration, destructive, and end-to-end tests run in the appropriate isolated environment or test organization, with teardown evidence where applicable.
- [ ] ORES OTEL trace/correlation propagation is present where applicable; secrets and user content are excluded by default and tenant boundaries are preserved.
- [ ] Conflicts were resolved semantically with relevant history and cross-repository contracts; no force push, history rewrite, or destructive recovery was used.

## Validation evidence and residual risk

List exact commands, checks, fixtures, test-org and hosted-CI links, migration or
drift results, manual verification, known limitations, deferred repositories,
and follow-up work.

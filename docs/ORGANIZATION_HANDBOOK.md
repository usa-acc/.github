# usa-acc organization handbook

> Shared operating defaults for repositories maintained under **usa-acc**. Repository-local policy may strengthen these rules but should not silently weaken them.

## Mission

usa-acc maintains the software, services, libraries, and documentation published under the USA ACC project. This `.github` repository is the canonical home for shared policy, reusable templates, community health files, and planning links. Product-specific claims and requirements belong in the repository that owns them and should be supported by current implementation or approved planning records.

## Repository contract

Each active repository must document purpose, ownership boundary, maturity, supported environments, development and test commands, authoritative interfaces and data, release and rollback procedures, compatibility policy, and GitHub Project/Linear links. Assumptions, external integrations, generated artifacts, data-classification boundaries, accessibility requirements, and operational limitations must be explicit.

## Change workflow

1. Anchor work in an issue, Linear item, or documented maintenance objective.
2. Keep branches and pull requests focused.
3. Explain motivation, scope, user and operational impact, validation, compatibility, migration, and rollback.
4. Test success, invalid input, permission, accessibility, timeout, partial failure, and recovery paths as relevant.
5. Resolve conflicts semantically by reconstructing both sides' intent.
6. Prefer squash merges for focused work unless commit structure materially improves auditability.

## Evidence, security, and documentation

Pull requests should include reproducible commands, approved fixtures, expected and observed results, negative-path coverage, documentation updates, and CI or local-equivalent evidence. Never commit credentials, private keys, production data, or sensitive logs. Follow `SECURITY.md` for private reporting. Keep examples executable, links current, assumptions explicit, and consequential architectural, compatibility, accessibility, privacy, and operational decisions recorded.

## Planning ownership

GitHub owns code, reviews, checks, releases, and delivery evidence. Linear owns priority, dependencies, sequencing, and cross-project planning. The organization GitHub Project is the cross-repository execution view; see `PROJECTS.md` for routing details.

## Organization health

- [ ] Profiles, descriptions, topics, and READMEs accurately describe current scope.
- [ ] Community health files and reusable issue/PR guidance are present.
- [ ] Repository boundaries, interfaces, data classes, integrations, and operational limits are explicit.
- [ ] Required checks reflect correctness, security, privacy, accessibility, and supply-chain risk.
- [ ] Stale repositories are archived or clearly marked.
- [ ] GitHub Project and Linear links resolve and reflect completed work.

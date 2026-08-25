# USA Accounting web/API connection patterns

Status: organization architecture guidance, tracked by [DEN-4260](https://linear.app/denman/issue/DEN-4260/document-usa-acc-webapi-connection-patterns).

This policy applies to traditional customer/admin web/BFF, accounting/ledger API, reporting, payment, reconciliation, and background services. Financial correctness and audit evidence take precedence over transport convenience.

## Four supported avenues

| Avenue | Appropriate use | Boundary |
| --- | --- | --- |
| Direct database read | Named public/reference or independently rebuilt reporting projection with a measured need | Never customer-private accounting data, accounts, balances, journals, tax data, payments, authorization, or writes; require distinct `SELECT`-only, `READ ONLY`, non-owner, `NOBYPASSRLS` access |
| Stateless HTTP/JSON | Default synchronous web-to-API path | Required for private reads, accounting/ledger work, posting, closing, reconciliation commands, payments, and every mutation |
| Stateful TCP | Measured authorized reference/status stream without accounting authority | Never posting, closing, reconciliation, payment, persistence, or authorization authority; require ADR, mTLS/delegated identity, bounded frames, deadlines, backpressure, and reconnect policy |
| NATS/message queue | Durable post-commit exports, reconciliation work, notifications, and downstream effects | Never login, posting approval, ledger commit, payment approval, or immediate response; require transactional outbox and idempotent consumers |

HTTP is the default. Accounting and ledger writes plus all customer-private reads go through the API; direct reads are restricted to public/reference or independently reproducible projections.

## Decision and ownership

1. Customer-private data, authorization, accounts, balances, journals, posting, closing, tax data, reconciliation, payments, and every mutation use HTTP.
2. Immediate authoritative answers use HTTP with typed/versioned interfaces, bounded bodies/timeouts, correlation context, and idempotency keys.
3. Durable post-commit effects publish from the authoritative transaction through an outbox to NATS.
4. A measured non-authoritative reference/status stream may use TCP after an ADR and API authorization.
5. Direct reads remain limited to documented public/reference or reproducible projections under a restricted role.

The web/BFF owns HTML, secure opaque sessions, CSRF, and authorization-code plus PKCE. The API owns product authorization, accounting state transitions, payments, and audit decisions. A core/data package owns typed mappings, queries, and transaction helpers. The canonical migration repository owns DDL; services verify compatibility and never migrate production at startup.

Shared Auth proves identity and assurance, not account, ledger, tax, or payment permission. Validate realm, issuer, audience, tenant, app/client, scopes, session, freshness, and assurance. Protected introspection keeps the service credential and user's token separate. Never log tokens, cookies, codes, PKCE verifiers, account/tax/payment data, or raw introspection results.

Use immutable dependency revisions. `opto-sync` supports declared synchronization/outbox workflows, `ores-otel` provides bounded redacted telemetry and trace propagation, and `zed-pkg` records dependency provenance. None may bypass API authorization or ledger ownership.

## Accounting and payment invariants

- Posting and outbox insertion share one transaction; consumers tolerate duplicate delivery and cannot rewrite ledger history.
- A redirect or queue acknowledgement is not settlement evidence. Only signature-verified, replay-safe, deduplicated provider events may advance payment state.
- Fail closed; never replace a failed API authorization or accounting decision with a direct query.
- Code comments identify the avenue and the accounting invariant it preserves.
- Every TCP or direct-read exception has an ADR, owner, measurements, and review/expiry date.

This document is the durable organization policy; repository ADRs may impose stricter controls.

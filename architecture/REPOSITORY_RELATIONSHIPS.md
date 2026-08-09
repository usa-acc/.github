# `usa-acc` repository relationships

Generated from reviewed policy and the current **public** repository inventory.

- Public repositories declared: **2**
- Private repository names withheld: **3**
- Relationship edges: **2**

## Repository roles

| Repository | Role | Lifecycle |
|---|---|---|
| [`.github`](https://github.com/usa-acc/.github) | `organization_governance` | `active` |
| [`usa-acc.github.io`](https://github.com/usa-acc/usa-acc.github.io) | `site` | `active` |

## Declared edges

| From | Relationship | To | Status/basis |
|---|---|---|---|
| `organization://usa-acc` | `researches_with` | `organization://akrion-sim` | `declared` / `explicit-product-decision`: simulation and control-system model exchange |
| `usa-acc/.github` | `governs` | `usa-acc/usa-acc.github.io` | `inferred` / `role-convention`: organization defaults, safety, and relationship declarations |

## Composition, service, and observability contract

Git submodules compose editable source; Zed packages resolve packages/artifacts; dual-managed commits must match. Production deploys immutable image digests, not runtime source builds. Cross-service access uses APIs/SDKs/events rather than another service database. MCP uses the product API/SDK. Services emit OpenTelemetry traces, bounded metrics, and correlated structured logs.

## Privacy boundary

This public registry deliberately omits private repository names and edges; the count above makes the boundary explicit.

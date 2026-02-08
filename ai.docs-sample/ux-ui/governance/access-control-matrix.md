# Access Control Matrix (RBAC) — MVP Contract

This document defines access rules for:
- Routes
- Actions
- Data visibility
- Tenant isolation

No screen/route may be implemented without mapping it here.

---

## 1) Roles (Canonical)

### Company (Tenant) Roles
- **COMPANY_OWNER**: Full control within tenant (billing, users, API, projects)
- **COMPANY_ADMIN**: Same as owner except ownership-critical actions (optional)
- **COMPANY_OPERATOR**: Operational usage (projects, exports, review requests) but no billing or security-sensitive settings

### Reviewer Roles
- **REVIEWER**: Can access review queue and review items assigned/available
- **REVIEWER_LEAD** (optional, v2): reviewer manager

### Platform Roles
- **PLATFORM_ADMIN**: Full platform control
- **PLATFORM_SUPPORT** (optional, v2): limited ops/read-only + tenant support tooling

---

## 2) Global Security Rules (Mandatory)

### Tenant Isolation
- All `/app/*` routes MUST be scoped to `company_id` (tenant).
- A company user MUST NEVER access another company’s projects, assets, exports, billing, or tokens.
- API tokens are company-scoped and enforce tenant isolation at the API layer.

### Reviewer Isolation
- Reviewers do not belong to a tenant by default.
- Reviewers access only:
  - Items assigned to them OR
  - Items available in the global queue
- Reviewers must not access tenant billing, API tokens, or user lists.

### Platform Admin Isolation
- Platform Admin can access all tenants.
- All admin actions must be logged in audit logs.

### Logging / Audit
Audit logs are mandatory for:
- Billing & credit adjustments
- Token creation/revocation
- Tenant suspension/reactivation
- Review approvals/returns
- Export generation and downloads

---

## 3) Route-Level Access Matrix (MVP)

Legend:
- R = Read
- W = Write/Create/Update
- A = Admin action (dangerous/privileged)
- N/A = not allowed

### 3.1 Public Routes
| Route | Access |
|------|--------|
| GET / | Public |
| GET /pricing | Public |
| GET /docs/api | Public |
| GET /contact | Public |
| GET /legal/terms | Public |
| GET /legal/privacy | Public |

### 3.2 Auth & Onboarding
| Route | COMPANY_OWNER | COMPANY_ADMIN | COMPANY_OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|---------------|---------------|------------------|----------|----------------|
| /auth/* | R/W | R/W | R/W | R/W | R/W |
| /onboarding/* | R/W | R/W | N/A | N/A | N/A |

Notes:
- Onboarding is only for newly created tenants.
- Operators cannot run onboarding.

### 3.3 Client App — Dashboard
| Route | OWNER | ADMIN | OPERATOR |
|------|-------|-------|----------|
| GET /app/dashboard | R | R | R |

### 3.4 Client App — Projects / Batches
| Route | OWNER | ADMIN | OPERATOR |
|------|-------|-------|----------|
| GET /app/projects | R | R | R |
| GET /app/projects/new | W | W | W |
| POST /app/projects | W | W | W |
| GET /app/projects/{id} | R | R | R |
| GET /app/projects/{id}/items | R | R | R |
| GET /app/projects/{id}/items/{item_id} | R | R | R |
| POST /app/projects/{id}/export | W | W | W |

Additional rules:
- Only users within the same tenant can access the project.
- Export creation must validate credits / permissions.

### 3.5 Client App — Exports
| Route | OWNER | ADMIN | OPERATOR |
|------|-------|-------|----------|
| GET /app/exports | R | R | R |
| GET /app/exports/{export_id} | R | R | R |
| GET /app/exports/{export_id}/download | R | R | R |

Rules:
- Downloads must use signed URLs with expiration.
- Export access is tenant-scoped.

### 3.6 Client App — Human Review Requests
| Route | OWNER | ADMIN | OPERATOR |
|------|-------|-------|----------|
| GET /app/reviews | R | R | R |
| POST /app/projects/{id}/review | W | W | W |
| GET /app/reviews/{request_id} | R | R | R |

Rules:
- Requesting review must show cost and confirm credit debit.
- Review status visible to tenant users only.

### 3.7 Client App — API Access (Security-Sensitive)
| Route | OWNER | ADMIN | OPERATOR |
|------|-------|-------|----------|
| GET /app/api | R | R | R |
| GET /app/api/tokens | R/W | R/W | N/A |
| POST /app/api/tokens | A | A | N/A |
| DELETE /app/api/tokens/{id} | A | A | N/A |
| GET /app/api/webhooks | R/W | R/W | N/A |
| POST /app/api/webhooks | A | A | N/A |
| DELETE /app/api/webhooks/{id} | A | A | N/A |

Rules:
- Token and webhook actions are privileged.
- Every creation/revocation must be audit-logged.
- Operators can view API overview but cannot manage tokens/webhooks.

### 3.8 Client App — Team & Permissions
| Route | OWNER | ADMIN | OPERATOR |
|------|-------|-------|----------|
| GET /app/team | R/W | R/W | R |
| POST /app/team/invite | A | A | N/A |
| PATCH /app/team/members/{user_id} | A | A | N/A |
| DELETE /app/team/members/{user_id} | A | A | N/A |

Rules:
- Operators can view team list only.
- Invites and role changes require privileged roles.

### 3.9 Client App — Billing & Credits (Highly Sensitive)
| Route | OWNER | ADMIN | OPERATOR |
|------|-------|-------|----------|
| GET /app/billing | R/W | R/W | N/A |
| GET /app/billing/packs | R | R | R |
| POST /app/billing/checkout | A | A | N/A |
| GET /app/billing/history | R | R | N/A |
| GET /app/billing/ledger | R | R | N/A |

Rules:
- Only privileged roles can initiate checkout.
- Ledger is read-only and must be auditable.
- Operators may see pack offerings (read-only).

---

## 4) Reviewer App — Access Matrix

| Route | REVIEWER | PLATFORM_ADMIN |
|------|----------|----------------|
| GET /review/queue | R | R |
| GET /review/items/{item_id} | R/W | R/W |
| POST /review/items/{item_id}/approve | W | W |
| POST /review/items/{item_id}/return | W | W |
| GET /review/profile | R/W | R/W |
| GET /review/stats | R | R |

Rules:
- A reviewer must see only items:
  - assigned to them OR
  - unassigned but available in the queue
- All reviewer actions are audit-logged with timestamps.

---

## 5) Platform Admin — Access Matrix

| Route | PLATFORM_ADMIN |
|------|----------------|
| GET /admin/dashboard | R |
| GET /admin/tenants | R |
| GET /admin/tenants/{tenant_id} | R |
| POST /admin/tenants/{tenant_id}/suspend | A |
| POST /admin/tenants/{tenant_id}/reactivate | A |
| POST /admin/tenants/{tenant_id}/credits/adjust | A |
| GET /admin/tenants/{tenant_id}/usage | R |
| GET /admin/billing | R |
| GET /admin/billing/webhooks | R |
| GET /admin/billing/transactions | R |
| GET /admin/review | R |
| GET /admin/review/reviewers | R/W |
| GET /admin/jobs | R |
| GET /admin/errors | R |
| GET /admin/audit | R |

Rules:
- All admin actions must require confirmation UI.
- All admin actions must be audit-logged.
- Credit adjustments require a reason field.

---

## 6) Action-Level Rules (Critical)

### Credits Debit Rules
- Credits are debited on:
  - job start (reserved) OR job completion (final debit) — must be defined in billing spec.
- Human review debits additional credits per reviewed item.
- Any debit must be idempotent.

### Export Rules
- Exports are generated asynchronously.
- Download links must be signed, expiring, and tenant-scoped.
- Export generation must be logged.

### Human Review Rules
- Reviewer cannot change tenant settings.
- Reviewer edits must keep version history:
  - IA output version
  - human-edited version
- Approve returns "final" status; return requires comment.

---

## 7) Future (Out of MVP)
- PLATFORM_SUPPORT (read-only ops with limited actions)
- REVIEWER_LEAD (assign reviewers, prioritize queue)
- Enterprise roles (compliance officer)

---

## 8) Implementation Notes (Non-Functional)
- RBAC must be enforced at:
  - Route middleware
  - Query scoping
  - Service layer
- Never trust client-side gating.
- Always log privileged actions.

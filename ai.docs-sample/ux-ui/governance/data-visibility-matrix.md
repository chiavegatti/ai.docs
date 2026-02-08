# Data Visibility Matrix — MVP Contract

This document defines what data fields are visible to each role.
It complements RBAC (route/action permissions) by preventing sensitive data leakage
even when a user has access to a screen.

Roles:
- COMPANY_OWNER
- COMPANY_ADMIN
- COMPANY_OPERATOR
- REVIEWER
- PLATFORM_ADMIN

Rules:
- Tenant data is isolated by default.
- “Need-to-know” principle applies.
- If a field is not explicitly allowed, it must be hidden.

---

## 1) Company / Tenant Profile

### Fields
- company_id (internal)
- company_name
- company_branding (logo/colors, if any)
- primary_contact_email
- billing_contact_email
- default_language
- output_profile_defaults
- created_at
- status (active/suspended)

### Visibility
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| company_name | Yes | Yes | Yes | Limited* | Yes |
| primary_contact_email | Yes | Yes | No | No | Yes |
| billing_contact_email | Yes | Yes | No | No | Yes |
| default_language | Yes | Yes | View-only | No | Yes |
| output_profile_defaults | Yes | Yes | View-only | No | Yes |
| status | Yes | Yes | Yes | Limited* | Yes |
| company_id | No (UI) | No (UI) | No (UI) | No | Yes |

*Reviewer: may see company_name and status only as needed for queue context (no contacts).

---

## 2) Users (Team)

### Fields
- user_id (internal)
- name
- email
- role
- last_login_at
- invited_at
- status (active/invited/disabled)

### Visibility
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| name | Yes | Yes | Yes (read-only list) | No | Yes |
| email | Yes | Yes | No | No | Yes |
| role | Yes | Yes | Yes (read-only) | No | Yes |
| last_login_at | Yes | Yes | No | No | Yes |
| invited_at | Yes | Yes | No | No | Yes |
| status | Yes | Yes | Yes (read-only) | No | Yes |
| user_id | No (UI) | No (UI) | No (UI) | No | Yes |

Notes:
- Operators can view team list but should not see emails or privileged metadata.

---

## 3) Projects / Batches

### Fields
- project_id
- company_id
- project_name
- description
- created_by (user reference)
- created_at
- status (queued/processing/done/error)
- total_items
- processed_items
- failed_items
- credits_estimated
- credits_reserved
- credits_final
- flags (ocr_enabled, embed_metadata_enabled, human_review_requested)

### Visibility
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| project_name | Yes | Yes | Yes | Limited* | Yes |
| description | Yes | Yes | Yes | Limited* | Yes |
| created_by | Yes | Yes | No | No | Yes |
| created_at | Yes | Yes | Yes | Limited* | Yes |
| status | Yes | Yes | Yes | Limited* | Yes |
| totals (items/progress) | Yes | Yes | Yes | Limited* | Yes |
| credits_* | Yes | Yes | Limited** | No | Yes |
| flags | Yes | Yes | Yes | Limited* | Yes |
| project_id | No (UI) | No (UI) | No (UI) | No | Yes |

*Reviewer sees only what’s necessary: project_name, status, created_at, priority/SLA related.
**Operator: may see credits_estimated (before processing) and credits_final for awareness, but not ledger-level detail.

---

## 4) Assets / Items (Images)

### Fields
- item_id
- project_id
- filename
- filesize
- mimetype
- image_preview_url (signed)
- status
- error_reason (sanitized)
- generated_alt_short
- generated_long_description
- language
- confidence_score (internal)
- processing_metadata (internal)
- created_at
- updated_at

### Visibility
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| filename | Yes | Yes | Yes | Yes | Yes |
| preview_url | Yes | Yes | Yes | Yes | Yes |
| status | Yes | Yes | Yes | Yes | Yes |
| error_reason | Yes | Yes | Yes (sanitized) | Yes (sanitized) | Yes |
| generated_alt_short | Yes | Yes | Yes | Yes | Yes |
| generated_long_description | Yes | Yes | Yes | Yes | Yes |
| language | Yes | Yes | Yes | Yes | Yes |
| confidence_score | Yes (optional UI) | Yes (optional UI) | No | Limited* | Yes |
| processing_metadata | No | No | No | No | Yes |
| item_id | No (UI) | No (UI) | No (UI) | No (UI) | Yes |

*Reviewer may see a simplified confidence indicator or “needs attention” label, not raw internals.

---

## 5) Human Review (Requests + Review Actions)

### 5.1 Review Requests (Client View)
Fields:
- review_request_id
- project_id
- requested_by
- requested_at
- priority
- status
- items_count
- cost_credits
- sla_due_at

Visibility:
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| requested_by | Yes | Yes | No | No | Yes |
| requested_at | Yes | Yes | Yes | Yes (queue context) | Yes |
| priority/status/items_count | Yes | Yes | Yes | Yes | Yes |
| cost_credits | Yes | Yes | Limited* | No | Yes |
| sla_due_at | Yes | Yes | Yes | Yes | Yes |
| review_request_id | No (UI) | No (UI) | No (UI) | No (UI) | Yes |

*Operator can see cost summary for the request but not billing/ledger detail.

### 5.2 Reviewer Actions (Reviewer View)
Fields:
- reviewer_id (internal)
- assigned_at
- started_at
- completed_at
- reviewer_comments
- decision (approved/returned)
- versions (IA → human)

Visibility:
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| reviewer_comments | Yes | Yes | Yes (read-only) | Yes | Yes |
| decision + timestamps | Yes | Yes | Yes | Yes | Yes |
| reviewer_identity | Limited** | Limited** | No | Yes (self) | Yes |
| versions | Yes | Yes | Yes | Yes | Yes |

**Owner/Admin may see “reviewed by: internal reviewer” or reviewer ID masked; do not show personal identity unless contract requires.

---

## 6) API Tokens & Webhooks

### API Tokens Fields
- token_id
- token_name
- token_prefix (masked)
- created_at
- last_used_at
- scopes
- status
- full_secret (only once)

Visibility:
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| token_name/scopes/status | Yes | Yes | No | No | Yes |
| token_prefix (masked) | Yes | Yes | No | No | Yes |
| last_used_at | Yes | Yes | No | No | Yes |
| full_secret | Only once on creation | Only once on creation | No | No | Yes |
| token_id | No (UI) | No (UI) | No | No | Yes |

### Webhooks Fields
- webhook_id
- url
- events
- secret (masked)
- status
- last_delivery_at
- last_status

Visibility:
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| url/events/status | Yes | Yes | No | No | Yes |
| secret (masked) | Yes | Yes | No | No | Yes |
| delivery logs (summary) | Yes | Yes | No | No | Yes |

---

## 7) Billing, Transactions, Ledger (Highly Sensitive)

### Billing Fields
- customer_id (provider)
- invoices
- transactions
- payment_method (masked)
- billing_address (if any)
- tax_id (if any)
- credit_packs purchased
- chargebacks/refunds

Visibility:
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| packs purchased (summary) | Yes | Yes | Limited* | No | Yes |
| invoices/transactions | Yes | Yes | No | No | Yes |
| payment_method (masked) | Yes | Yes | No | No | Yes |
| billing_address/tax_id | Yes | Yes | No | No | Yes |
| chargebacks/refunds | Yes | Yes | No | No | Yes |
| provider customer_id | No (UI) | No (UI) | No | No | Yes |

### Credit Ledger Fields
- ledger_entry_id
- type (credit/debit/reserve/release)
- amount
- reason
- resource_type/resource_id
- actor_id
- created_at
- idempotency_key

Visibility:
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| amount/type/reason/date | Yes | Yes | No | No | Yes |
| resource references | Yes | Yes | No | No | Yes |
| actor_id | Limited** | Limited** | No | No | Yes |
| idempotency_key | No | No | No | No | Yes |

*Operator may see high-level “credits remaining” and job estimated cost, not ledger entries.
**Mask actor identity where appropriate; show “system” / “admin action” without exposing personal data unnecessarily.

---

## 8) Audit Logs

Fields:
- audit_id
- action (permission)
- actor_role
- actor_id
- tenant_id
- resource_type/resource_id
- timestamp
- metadata (reason)

Visibility:
| Field | OWNER | ADMIN | OPERATOR | REVIEWER | PLATFORM_ADMIN |
|------|-------|-------|----------|----------|----------------|
| tenant-level audit view | Yes | Yes | No | No | Yes |
| actor identity | Limited* | Limited* | No | No | Yes |
| metadata | Yes (sanitized) | Yes (sanitized) | No | No | Yes |

*For tenant audit logs, avoid exposing personal reviewer identity; keep privacy-friendly.

---

## 9) Implementation Notes (Mandatory)
- Do not rely on UI-only hiding; enforce field filtering server-side (DTO/transformers/resources).
- Prefer explicit serializers per role.
- Default stance: hide sensitive fields unless required.
- Any new data field must be added here with visibility rules.

---

## 10) Privacy & Compliance Notes
- Avoid unnecessary exposure of personally identifiable information (PII).
- Reviewers should not see tenant contact emails or billing details.
- Operators should not see payment history, ledger entries, or API secrets.

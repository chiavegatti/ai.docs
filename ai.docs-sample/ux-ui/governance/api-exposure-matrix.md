# API Exposure Matrix — MVP Contract

This document defines what the public API exposes:
- Endpoints
- Methods
- Fields returned
- Fields accepted (write)
- Authentication scope
- Rate limits (high level)
- What is INTERNAL ONLY (never exposed publicly)

The public API must never expose more data than the UI.
Any new endpoint or field requires updating this document.

---

## 1) API Principles

- All API requests are tenant-scoped via API token.
- API tokens have scopes mapped to permissions (see permission-glossary.md).
- No API endpoint returns billing PII or secrets.
- All write operations must be idempotent where applicable.
- Responses must be versioned (`/v1`).

Base URL:
- `POST /api/v1/*`

Auth:
- Bearer token (API Token)
- Scopes enforced server-side

---

## 2) Public API — Endpoints (MVP)

### 2.1 Projects / Batches

#### Create Batch
- `POST /api/v1/projects`
- Scope required:
  - projects.batch.create
- Accepts:
  - project_name
  - description (optional)
  - options:
    - language
    - output_profile
    - embed_metadata (bool)
    - human_review (bool)
- Returns:
  - project_id (public)
  - status
  - estimated_credits
- Exposed Fields:
  - project_id
  - project_name
  - status
  - created_at
- INTERNAL ONLY (never return):
  - credits_reserved
  - internal_flags
  - cost_breakdown_raw

#### Upload Items (Multipart)
- `POST /api/v1/projects/{project_id}/items`
- Scope required:
  - projects.batch.create
- Accepts:
  - files[] (multipart)
  - urls[] (optional)
- Returns:
  - accepted_count
  - rejected_count
  - items (public ids + status)
- Exposed Fields:
  - item_id (public)
  - filename
  - status
- INTERNAL ONLY:
  - storage_path
  - internal_processing_ids

#### Get Project Status
- `GET /api/v1/projects/{project_id}`
- Scope required:
  - projects.view
- Returns:
  - project_id
  - project_name
  - status
  - totals (items, processed, failed)
- INTERNAL ONLY:
  - credits_reserved
  - internal_job_ids

---

### 2.2 Results / Items

#### List Items
- `GET /api/v1/projects/{project_id}/items`
- Scope required:
  - projects.items.list
- Returns:
  - item_id
  - filename
  - status
  - language
- INTERNAL ONLY:
  - processing_metadata
  - confidence_score_raw

#### Get Item Result
- `GET /api/v1/projects/{project_id}/items/{item_id}`
- Scope required:
  - results.view
- Returns:
  - item_id
  - filename
  - generated_alt_short
  - generated_long_description
  - language
  - status
  - version (ia | human)
- INTERNAL ONLY:
  - internal_model_names
  - prompt_templates
  - raw_scores

---

### 2.3 Exports

#### Create Export
- `POST /api/v1/exports`
- Scope required:
  - exports.create
- Accepts:
  - project_id
  - format (json | csv | md | zip)
- Returns:
  - export_id
  - status (queued)
- INTERNAL ONLY:
  - storage_bucket
  - internal_job_id

#### Get Export Status
- `GET /api/v1/exports/{export_id}`
- Scope required:
  - exports.view
- Returns:
  - export_id
  - status
  - format
  - created_at

#### Download Export
- `GET /api/v1/exports/{export_id}/download`
- Scope required:
  - exports.download
- Returns:
  - signed_url (short-lived)
- INTERNAL ONLY:
  - direct storage URLs
  - bucket names

---

### 2.4 Human Review (Client API)

#### Request Review
- `POST /api/v1/reviews`
- Scope required:
  - review.request.create
- Accepts:
  - project_id
  - item_ids[] (optional)
  - priority (optional)
- Returns:
  - review_request_id
  - status
  - estimated_additional_credits
- INTERNAL ONLY:
  - reviewer_assignment
  - internal SLA calculations

#### Get Review Status
- `GET /api/v1/reviews/{review_request_id}`
- Scope required:
  - review.request.view
- Returns:
  - review_request_id
  - status
  - counts (pending/approved/returned)
  - sla_due_at

---

### 2.5 API Usage & Quotas

#### Usage Summary
- `GET /api/v1/usage`
- Scope required:
  - api.usage.view
- Returns:
  - credits_remaining
  - credits_used_this_month
  - jobs_count
- INTERNAL ONLY:
  - ledger entries
  - cost breakdown per model/provider

---

## 3) Rate Limits (High Level)

Per API token:
- Default: 60 req/min
- Burst: 120 req/min
- Batch upload endpoints: custom limits per tenant plan

Rules:
- 429 on limit exceeded
- Include rate limit headers

---

## 4) Webhooks (Outbound)

Supported events:
- project.completed
- project.failed
- export.ready
- review.completed

Payload (public fields only):
- event_type
- timestamp
- tenant_id (public)
- resource_id
- status
- summary fields

Never include:
- PII
- billing data
- secrets
- internal job ids

---

## 5) Error Model (Public)

Standard error response:
- code
- message (user-safe)
- details (optional, sanitized)
- request_id

Never expose:
- stack traces
- internal exception messages
- provider errors verbatim

---

## 6) Versioning & Deprecation

- API version in URL: `/api/v1`
- Deprecations require:
  - 90-day notice
  - documentation update
  - changelog entry
- Breaking changes require new version (`/v2`)

---

## 7) Security Notes

- Tokens are tenant-scoped and permission-scoped.
- All endpoints validate tenant ownership of `project_id`, `item_id`, `export_id`.
- Signed URLs must expire (e.g., 5–15 minutes).
- Webhook signatures must be verified by clients.

---

## 8) Internal-Only APIs (Not Public)
- Admin ops
- Reviewer assignment
- Billing provider callbacks
- Ledger manipulation
- Model orchestration endpoints
- Internal job queue controls

These endpoints must be on a private network / protected route group.

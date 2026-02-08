# Permission Glossary (Atomic Permissions) — MVP Contract

This document defines canonical, atomic permissions used across:
- Laravel policies/middleware
- UI gating (secondary)
- API authorization
- Audit logging rules

Roles must map to permissions explicitly.
No route/action may exist without a corresponding permission.

---

## 1) Naming Convention
Permissions follow the format:

<domain>.<resource>.<action>

Examples:
- projects.batch.create
- api.tokens.manage
- billing.checkout.create

Actions:
- view
- list
- create
- update
- delete
- manage (dangerous / privileged)
- approve (review actions)
- download (exports)

---

## 2) Domains & Permissions

### 2.1 Tenant / Company
- company.profile.view
- company.profile.update
- company.settings.view
- company.settings.update

### 2.2 Team & Roles
- team.members.list
- team.members.view
- team.members.invite
- team.members.update_role
- team.members.remove

### 2.3 Projects / Batches
- projects.list
- projects.view
- projects.batch.create
- projects.batch.update
- projects.batch.cancel
- projects.items.list
- projects.items.view

### 2.4 Processing / Jobs
- jobs.list
- jobs.view
- jobs.retry_item
- jobs.retry_batch
- jobs.cancel

### 2.5 Results / Descriptions
- results.view
- results.update_manual (optional, v2 — allow client edits)
- results.history.view

### 2.6 Exports
- exports.list
- exports.create
- exports.view
- exports.download

### 2.7 Human Review (Client Side)
- review.request.create
- review.request.view
- review.request.cancel (optional)
- review.request.priority.set (optional, v2)

### 2.8 API & Webhooks (Security-Sensitive)
- api.view
- api.tokens.list
- api.tokens.manage
- api.webhooks.list
- api.webhooks.manage
- api.usage.view

### 2.9 Billing & Credits (Highly Sensitive)
- billing.view
- billing.packs.view
- billing.checkout.create
- billing.history.view
- billing.ledger.view
- billing.invoices.view (optional)
- billing.refunds.request (optional, v2)

### 2.10 Audit & Logs (Tenant)
- audit.view (tenant-level audit for own company)

---

## 3) Reviewer Permissions (Human Review App)

### 3.1 Review Queue
- reviewer.queue.view
- reviewer.queue.filter

### 3.2 Review Item Actions
- reviewer.item.view
- reviewer.item.edit
- reviewer.item.approve
- reviewer.item.return_with_comment

### 3.3 Reviewer Profile
- reviewer.profile.view
- reviewer.profile.update
- reviewer.stats.view

---

## 4) Platform Admin Permissions (Operations)

### 4.1 Platform Overview
- platform.dashboard.view
- platform.audit.view

### 4.2 Tenants Management
- platform.tenants.list
- platform.tenants.view
- platform.tenants.suspend
- platform.tenants.reactivate
- platform.tenants.credits.adjust
- platform.tenants.usage.view

### 4.3 Platform Billing Ops
- platform.billing.view
- platform.billing.transactions.view
- platform.billing.webhooks.view

### 4.4 Review Ops
- platform.review.view
- platform.review.reviewers.manage (optional, if reviewer management is in MVP)

### 4.5 System Ops
- platform.jobs.view
- platform.errors.view

---

## 5) Role → Permissions Mapping (MVP)

### 5.1 COMPANY_OWNER
Grants everything within tenant scope, including security-sensitive and billing:
- All `company.*`
- All `team.*`
- All `projects.*`
- All `jobs.*`
- All `results.*` (except v2 manual edits)
- All `exports.*`
- All `review.request.*`
- All `api.*`
- All `billing.*`
- audit.view

### 5.2 COMPANY_ADMIN
Same as owner for MVP (can be identical), except optionally:
- cannot change ownership (not in MVP UI)
Suggested: identical to COMPANY_OWNER for simplicity in MVP.

### 5.3 COMPANY_OPERATOR
Operational permissions only:
- company.profile.view
- company.settings.view
- team.members.list
- team.members.view
- projects.list
- projects.view
- projects.batch.create
- projects.items.list
- projects.items.view
- jobs.list
- jobs.view
- results.view
- results.history.view
- exports.list
- exports.create
- exports.view
- exports.download
- review.request.create
- review.request.view
- api.view
- api.usage.view
- billing.packs.view

Explicitly NOT allowed:
- team.members.invite / update_role / remove
- api.tokens.manage / api.webhooks.manage
- billing.checkout.create / billing.history.view / billing.ledger.view

### 5.4 REVIEWER
Only human review scope:
- reviewer.queue.view
- reviewer.queue.filter
- reviewer.item.view
- reviewer.item.edit
- reviewer.item.approve
- reviewer.item.return_with_comment
- reviewer.profile.view
- reviewer.profile.update
- reviewer.stats.view

### 5.5 PLATFORM_ADMIN
Full platform control:
- All `platform.*`

---

## 6) Audit Logging Rules (Mandatory)

Any action requiring audit logs:
- api.tokens.manage
- api.webhooks.manage
- billing.checkout.create
- billing.ledger.view (access logging optional but recommended)
- platform.tenants.suspend / reactivate / credits.adjust
- reviewer.item.approve / return_with_comment
- exports.download (at least per-export download event)

Audit entry minimum fields:
- actor_id
- actor_role
- tenant_id (when applicable)
- action (permission name)
- resource_type + resource_id
- timestamp
- metadata (reason, notes)

---

## 7) Notes
- UI gating is secondary; authorization must be enforced server-side.
- Every route/action must map to one or more permissions above.
- New permissions require updating this file + PRD if scope changes.

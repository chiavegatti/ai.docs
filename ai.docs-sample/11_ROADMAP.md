# Product Roadmap
## Reference Evolution — Mini CRM

Version: 1.0  
Status: Reference  
Owner: Product / Tech Lead  

---

## 1. Purpose

This roadmap describes the **possible evolution paths** of the reference mini CRM.

It is **not a delivery plan** and **not a sprint backlog**.
Its purpose is to:
- communicate future intent
- define what is explicitly deferred
- avoid scope creep in the MVP

---

## 2. Roadmap Philosophy

- MVP first, extensions later
- Functionality grows only on validated foundations
- No feature enters without:
  - PRD update
  - schema impact analysis
  - API contract definition
  - UX mapping
  - ADR if architectural impact exists

---

## 3. MVP Scope (Baseline)

The MVP includes:
- multi-tenant support
- user and role management
- client management
- contact and interaction tracking
- RBAC enforcement
- API-first access
- basic dashboards

This scope is defined in:
- `03_PRD.md`

Anything not listed there is **out of MVP**.

---

## 4. Near-Term Evolution (Post-MVP)

Potential additions after MVP validation:

### 4.1 Advanced Client Management
- Client segmentation
- Tags and categories
- Status workflows

### 4.2 Extended User Permissions
- Custom roles
- Fine-grained permissions
- Delegated administration

### 4.3 Reporting & Insights
- Basic usage reports
- Activity history
- Audit summaries

---

## 5. Mid-Term Evolution

Possible mid-term extensions:

### 5.1 Integrations
- Webhooks
- External system sync
- Import/export tools

### 5.2 Automation
- Rule-based actions
- Scheduled tasks
- Notifications

---

## 6. Long-Term Possibilities

Ideas explicitly **out of current scope**:

- AI-assisted insights
- Predictive analytics
- Marketplace extensions
- White-labeling
- Enterprise-grade workflow engines

These are **not commitments**, only possibilities.

---

## 7. Out of Scope by Design

The roadmap explicitly excludes:
- implementation timelines
- sprint definitions
- infrastructure decisions
- provider selection
- cost projections

Those belong to execution planning, not to this document.

---

## 8. Governance

Any roadmap change MUST:
- respect MVP boundaries
- update the PRD if scope changes
- be traceable via ADR if architectural impact exists

## Roadmap → Tasks Alignment (Mandatory)

This roadmap defines **high-level milestones and phases**.
Execution happens exclusively through tasks defined in:

ai.docs/tasks/

### Mapping Rules

- Each roadmap item MUST be executed through one or more tasks
- Tasks MUST reference the roadmap item they implement
- Roadmap items MUST NOT contain implementation details
- Tasks MUST NOT redefine roadmap scope

Relationship model:

Roadmap Item
  └── Task 1 (atomic)
  └── Task 2 (atomic)
  └── Task N (atomic)

### Execution Rule

If a roadmap item exists but no tasks are defined:
- the item is NOT in execution yet

If a task exists without a roadmap reference:
- the task is INVALID and must be removed or linked

### Completion Rule

A roadmap item is considered:
- **In Progress** → when at least one linked task exists
- **Completed** → when all linked tasks meet their acceptance criteria

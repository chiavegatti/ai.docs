# UX / UI Index
## Functional Contract — Mini CRM Reference

## 1. Purpose

This document defines the **UX/UI layer as a functional contract** for the reference mini CRM.

It does not contain wireframes or visual design.
It defines:
- which screens may exist
- which actions are allowed per role
- what data may be visible
- how UX maps to APIs and permissions

If a screen or action is not documented here, it must not exist.

---

## 2. UX as a Contract (Mandatory)

The UX/UI layer MUST:
- reflect documented business rules
- respect tenant isolation
- enforce role-based visibility
- map explicitly to API endpoints

UX is not decorative.  
UX is a **controlled interface to system behavior**.

---

## 3. Canonical UX Documentation Location

All UX-related documentation MUST live under: ai.docs/ux-ui/


Recommended structure:

ai.docs/ux-ui/
├── routes.md
├── access-control-matrix.md
├── screen-permission-mapping.md
├── data-visibility-matrix.md
├── api-exposure-matrix.md
└── wireframes/ # optional


Each file has a specific role described below.

---

## 4. Screens & Routes

### 4.1 Routes Definition

All application routes MUST be defined in: ai.docs/ux-ui/routes.md


Each route MUST specify:
- route path
- screen name
- required role(s)
- associated API endpoints

No route may exist without an entry in `routes.md`.

---

## 5. Roles & Access Control

### 5.1 Role Definitions

Roles are defined in:
- `03_PRD.md`

UX enforcement rules are defined in:
- `ai.docs/ux-ui/access-control-matrix.md`

This matrix MUST define:
- which roles can access which screens
- which actions are allowed per role

---

## 6. Screen ↔ Permission Mapping

Each screen MUST be mapped to:
- required permissions
- allowed actions (view, create, edit, delete)

This mapping is documented in: ai.docs/ux-ui/screen-permission-mapping.md

No screen may expose an action without an explicit permission rule.

---

## 7. Data Visibility Rules

UX MUST respect data visibility constraints.

Data visibility rules are documented in: ai.docs/ux-ui/data-visibility-matrix.md


This matrix defines:
- which fields are visible per role
- which entities are visible per tenant
- which data is hidden or masked

UX must not infer visibility dynamically.

---

## 8. UX ↔ API Relationship

Every screen MUST be backed by:
- at least one documented API endpoint
- a clear API exposure rule

This relationship is documented in: ai.docs/ux-ui/api-exposure-matrix.md


UX must not call undocumented APIs.
APIs must not exist without a UX or integration use-case.

---

## 9. Multi-Tenant UX Constraints

UX MUST:
- always operate within a tenant context
- never expose cross-tenant data
- clearly indicate tenant scope where applicable

Tenant rules are defined in:
- `02_CONTEXT.md`
- `05_SECURITY_AND_COMPLIANCE.md`

---

## 10. Notes for AI (Mandatory)

When generating UX-related artifacts:

- Do not invent screens or flows
- Do not assume permissions
- Always consult:
  - PRD
  - API contracts
  - data schemas
  - access matrices
- If UX requirements are incomplete, request clarification

---

## 11. Governance

Any change affecting UX MUST update:
- this index file (if structure changes)
- routes documentation
- access control matrices
- API exposure mappings
- ADRs (`09_DECISIONS_ADR.md`) if behavior changes

---

## 12. Scope Reminder

This document defines **UX structure and rules**, not visual design.

Visual design systems, styling and branding are out of scope.





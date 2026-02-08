# Product Requirements Document (PRD)
## Mini CRM — Reference Example

Version: 1.0  
Status: Reference – Ready for Execution  
Owner: Product / Tech Lead  
Date: 2026-02  

---

## 1. Overview

### 1.1 Problem Statement

Many internal tools and small B2B systems fail due to:
- unclear scope,
- poorly defined data models,
- inconsistent permission rules,
- UX built before rules exist.

This PRD defines a **minimal, well-scoped mini CRM** to demonstrate how requirements should be documented for reliable AI-assisted execution.

---

### 1.2 Proposed Solution

A **B2B, multi-tenant mini CRM** that allows companies to:

- manage clients and contacts,
- track basic interactions,
- control access via roles and permissions,
- expose a stable API for integration,
- maintain auditability and traceability.

This system is intentionally limited to remain executable and easy to reason about.

---

## 2. Target Users

- Internal business teams
- Small B2B operations
- Agencies managing multiple clients
- Product and engineering teams using AI-assisted development

---

## 3. MVP Goals

The MVP MUST:

- Support multiple companies (tenants)
- Allow user management per tenant
- Manage clients and contacts
- Record basic interactions (notes / events)
- Enforce role-based access control (RBAC)
- Expose a documented API
- Provide a simple web interface
- Maintain audit logs for sensitive actions

---

## 4. Core Functional Requirements

### 4.1 Tenant Management

- Create and manage companies (tenants)
- Isolate all data per tenant
- Assign users to tenants with roles

---

### 4.2 User & Role Management

Roles (initial set):
- COMPANY_OWNER
- COMPANY_ADMIN
- COMPANY_USER
- PLATFORM_ADMIN

Requirements:
- A user may belong to multiple tenants
- Permissions are role-based
- Sensitive actions must be auditable

---

### 4.3 Client Management

- Create, update and archive clients
- Store basic client data:
  - name
  - contact information
  - status
- Clients belong to exactly one tenant

---

### 4.4 Contact & Interaction Tracking

- Add contacts linked to clients
- Record interactions:
  - notes
  - timestamps
  - author
- Interactions are immutable once created

---

### 4.5 API Access

The platform MUST expose an API to:

- authenticate users
- list and manage clients
- manage contacts
- create and read interactions

API behavior must be:
- versioned
- tenant-aware
- permission-aware

---

### 4.6 Dashboards

The system provides basic dashboards for:

- Company users
- Company admins
- Platform admins

Dashboards must respect:
- RBAC rules
- data visibility constraints

---

## 5. UX / Navigation Contract

UX is treated as a **functional contract**, not decoration.

All screens, routes and flows MUST be documented in:

- `ux-ui/routes.md`
- `ux-ui/access-control-matrix.md`
- `ux-ui/screen-permission-mapping.md`
- `ux-ui/data-visibility-matrix.md`
- `ux-ui/api-exposure-matrix.md`

No UI element may exist without a corresponding permission rule.

---

## 6. Security & Access Rules (High-Level)

- Strict tenant isolation
- Role-based access control
- Authenticated access only
- Audit logging for:
  - role changes
  - deletions
  - data exports (if any)

Detailed rules are defined in:
- `05_SECURITY_AND_COMPLIANCE.md`

---

## 7. Non-Functional Requirements

- Predictable behavior over “smart” behavior
- Deterministic data access
- Clear error handling
- Logs suitable for auditing
- Documentation updates required for behavior changes

---

## 8. Out of Scope (MVP)

- Advanced analytics
- Automation workflows
- AI features
- Email campaigns
- External CRM integrations

---

## 9. Success Criteria

- All entities and relationships are explicitly defined
- No undocumented permissions
- API contracts match data schemas
- UX flows reflect business rules
- AI models can generate code without inventing requirements

---

## 10. Change Governance

Any change to scope or behavior MUST update:

- this PRD
- related UX documents
- API contracts
- data schemas
- decision records (`09_DECISIONS_ADR.md`)

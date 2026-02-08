# Security and Compliance
## Reference Guidelines — Mini CRM

## 1. Purpose

This document defines the **mandatory security and compliance guidelines** for the reference mini CRM.

These rules are **constraints**, not suggestions.  
They influence architecture, data models, APIs, UX and operational decisions.

---

## 2. Security Principles (Baseline)

The system MUST adhere to the following principles:

- Least privilege by default
- Explicit permissions over implicit access
- Separation of concerns
- Secure-by-default configuration
- No trust based on client-side validation

---

## 3. Authentication

- All access MUST be authenticated
- Token-based authentication for APIs
- Tokens must be:
  - scoped
  - revocable
  - time-bound where applicable

Anonymous access is forbidden.

---

## 4. Authorization (RBAC)

- Role-based access control (RBAC) is mandatory
- Roles are defined in `03_PRD.md`
- Permissions must be enforced at the API layer
- UI-level checks are defensive only

No API endpoint may exist without an explicit permission rule.

---

## 5. Multi-Tenant Isolation

- All core entities MUST belong to a tenant
- Tenant context is mandatory for every request
- Cross-tenant access is forbidden by default
- Platform-level access operates in a separate scope

Tenant isolation must be enforced at:
- query level
- authorization layer
- API contracts

---

## 6. Data Protection

### 6.1 Data Classification

Data should be treated as:
- Internal
- Sensitive (user data, audit logs)

Sensitive data MUST:
- be minimized
- never be exposed unnecessarily
- be protected by access controls

---

### 6.2 Data Integrity

- Strong relational integrity is required
- Deletions should be soft only when explicitly justified
- Audit data is append-only

---

## 7. Audit & Traceability

The system MUST record audit events for:

- authentication events
- role or permission changes
- data creation, update or deletion
- access to sensitive data

Audit logs must be:
- immutable
- timestamped
- attributable to an actor

---

## 8. API Security

- All APIs must be versioned
- Input validation is mandatory
- Consistent error responses (no sensitive leakage)
- Rate limiting may be applied where necessary

API contracts are defined in:
- `07_API_CONTRACTS.md`

---

## 9. UX & Data Visibility Constraints

- UX must reflect permission rules
- Data visibility must align with tenant and role
- No screen may expose data without an explicit rule

UX rules are documented in:
- `10_UX_UI_INDEX.md`

---

## 10. Compliance Awareness

This reference system acknowledges common compliance principles, such as:

- data minimization
- access traceability
- accountability

This document does **not** replace legal or regulatory assessments.

---

## 11. Non-Goals

This document does not cover:
- legal interpretations of regulations
- infrastructure hardening details
- penetration testing procedures
- organization-specific compliance requirements

Those concerns belong to project-specific extensions.

---

## 12. Governance

Any change affecting security or data access MUST update:

- this document
- related API contracts
- UX permission matrices
- relevant ADRs (`09_DECISIONS_ADR.md`)
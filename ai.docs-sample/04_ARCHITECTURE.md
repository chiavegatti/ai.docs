# System Architecture
## Mini CRM — Reference Architecture

## 1. Overview

This document defines the **high-level system architecture** for the reference mini CRM.

The architecture is intentionally:
- simple,
- deterministic,
- multi-tenant,
- API-first,
- and suitable for AI-assisted implementation.

It focuses on **responsibilities and boundaries**, not on framework-specific details.

---

## 2. Architectural Principles

- API-first: all functionality is accessible via API
- Multi-tenant isolation by design
- Clear separation of concerns
- Stateless application layer
- Deterministic behavior over “smart” behavior
- Infrastructure simplicity over premature optimization

---

## 3. High-Level Components

### 3.1 Application API

Responsibilities:
- Authentication and authorization
- Tenant management
- User and role management
- Client and contact management
- Interaction recording
- Audit logging
- API exposure for integrations

This is the **single source of truth** for business rules.

---

### 3.2 Web Interface

Responsibilities:
- Provide dashboards for users, admins and platform admins
- Consume the same APIs exposed publicly
- Enforce permissions at the UI level (defensive layer)

The UI does **not** implement business logic.

---

### 3.3 Database Layer

Responsibilities:
- Persist all core entities
- Enforce relational integrity
- Support audit and traceability

Characteristics:
- Relational database
- Strong consistency
- Explicit schemas and constraints

---

### 3.4 Authentication & Authorization

Responsibilities:
- User authentication
- Role-based access control (RBAC)
- Token-based API access

Authorization rules must be enforced:
- at the API level (mandatory)
- optionally reinforced at the UI level

---

### 3.5 Audit & Logging

Responsibilities:
- Record sensitive actions
- Track changes affecting security or data ownership
- Provide traceability for debugging and compliance

Audit data is **append-only**.

---

## 4. Data Flow (Conceptual)

1. User authenticates
2. API validates tenant context and permissions
3. Request is processed by application logic
4. Data is persisted
5. Audit events are recorded
6. Response is returned

No implicit side effects are allowed.

---

## 5. Multi-Tenancy Model

- Every core entity belongs to a tenant
- Tenant context is mandatory in every request
- Cross-tenant access is forbidden by default
- Platform-level users operate in a separate scope

Tenant isolation must be enforced at:
- query level
- authorization layer
- API contracts

---

## 6. API Architecture

- Versioned APIs (e.g. `/api/v1`)
- Token-based authentication
- Explicit request and response schemas
- Consistent error handling

API contracts are defined in:
- `07_API_CONTRACTS.md`

---

## 7. Data Architecture

- Normalized relational schemas
- Explicit relationships
- No polymorphic “magic” fields
- Soft deletes only where explicitly required

Data schemas are defined in:
- `08_DATA_SCHEMA.md`

---

## 8. Security Boundaries

This architecture enforces:

- Strict tenant isolation
- Role-based access control
- No direct database access from UI
- No implicit permissions

Detailed security rules are defined in:
- `05_SECURITY_AND_COMPLIANCE.md`

---

## 9. Scalability & Evolution (Conceptual)

The architecture allows future evolution via:
- horizontal scaling of the application layer
- read replicas for the database (if required)
- API versioning

These are **design allowances**, not MVP requirements.

---

## 10. Out of Scope

This architecture does not cover:
- infrastructure provisioning
- CI/CD pipelines
- cloud-specific services
- performance tuning

Those concerns belong to implementation phases, not to this document.

---

## 11. Architecture Governance

Any architectural change MUST:
- be documented here
- reference an ADR in `09_DECISIONS_ADR.md`
- respect existing API and data contracts

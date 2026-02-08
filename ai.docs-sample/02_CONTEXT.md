# Project Context — Mini CRM (Reference Example)

## 1. Purpose

This project exists to serve as a **reference context** for applying the ai.docs methodology.

The example system used throughout this documentation is a **mini CRM**, designed to illustrate how to define scope, constraints, data, APIs, UX and decisions in a clear, executable way when working with AI-assisted software development.

The focus is not the CRM itself, but the **documentation discipline** used to describe it.

---

## 2. What This System Is (Conceptual)

The reference system represents a **B2B, multi-tenant mini CRM** with the following conceptual goals:

- Manage companies (tenants) and their users
- Track clients, contacts and basic interactions
- Support role-based access control
- Expose a stable API for integration
- Provide a simple, auditable operational flow

This is intentionally **limited in scope** to remain understandable and reproducible.

---

## 3. Core Principles

- Documentation-first, execution-oriented
- B2B and multi-tenant by design
- API-first mindset
- Explicit data models and contracts
- Traceability over convenience
- Simplicity over feature abundance

---

## 4. Priorities

1. Clear scope and boundaries
2. Well-defined data schemas
3. Stable and explicit API contracts
4. Predictable authorization rules
5. UX aligned with permissions and data visibility
6. Decisions documented and traceable

---

## 5. Constraints & Boundaries

- This is **not** a full-featured enterprise CRM
- This is **not** a low-code/no-code tool
- This is **not** a UI showcase
- Advanced automations, AI features and analytics are out of scope
- Scalability concerns are addressed conceptually, not by implementation detail

The goal is clarity, not completeness.

---

## 6. Design Philosophy

- Admin-driven and permission-aware
- CRUD-focused, not workflow-heavy
- Deterministic behavior preferred over “smart” behavior
- UX treated as a functional contract
- No implicit behavior — everything must be defined

---

## 7. Important Notes for AI (Mandatory)

When using AI models in this project context:

- Do not invent entities, fields or relationships
- Do not assume business rules not explicitly documented
- If information is missing, request clarification
- Follow the documentation order strictly
- Treat schemas, APIs and UX documents as contracts

---

## 8. Engineering Governance (Mandatory)

This project adopts strict engineering practices to reinforce predictability and quality:

- No feature may be implemented without a documented requirement
- Data models must be defined before API contracts
- API contracts must be defined before UX flows
- Changes must be incremental and traceable
- Decisions must be recorded in `09_DECISIONS_ADR.md`
- Documentation updates are mandatory when behavior changes

---

## 9. Scope Reminder

This file defines **context only**.

Detailed requirements belong in:
- `03_PRD.md`

Architectural decisions belong in:
- `04_ARCHITECTURE.md`

Security rules belong in:
- `05_SECURITY_AND_COMPLIANCE.md`

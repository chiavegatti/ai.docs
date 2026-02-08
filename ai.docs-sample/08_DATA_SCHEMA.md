# Data Schema
## Reference Definition — Mini CRM

## 1. Purpose

This document defines the **data modeling rules** and **schema governance** for the reference mini CRM.

It does not replace the actual schema files.  
It defines **how schemas must be described, validated and evolved**.

---

## 2. Schema-First Rule (Mandatory)

- Data models MUST be defined before:
  - APIs
  - UX flows
  - business logic
- No field may exist without:
  - a defined type
  - a clear purpose
  - ownership (entity)

If data is not modeled, it must not be stored.

---

## 3. Canonical Schema Location

All schemas MUST live in: ai.docs/data-base-schemas/


Recommended structure:
ai.docs/data-base-schemas/
├── tenants.md
├── users.md
├── roles.md
├── clients.md
├── contacts.md
└── interactions.md


---

## 4. Entity Definition Rules

Each entity definition MUST include:
- entity purpose
- fields with types
- primary key
- foreign keys
- constraints (unique, nullable, etc.)
- relationships to other entities

No implicit relationships are allowed.

---

## 5. Multi-Tenant Requirements

- All core entities MUST reference a tenant
- Tenant isolation is mandatory
- Cross-tenant relationships are forbidden

Tenant rules are defined in:
- `02_CONTEXT.md`
- `05_SECURITY_AND_COMPLIANCE.md`

---

## 6. Data Integrity Rules

- Strong relational integrity is required
- Foreign keys must be explicit
- Soft deletes are allowed only when justified
- Audit-related entities are append-only

---

## 7. Schema Evolution

Any schema change MUST:
- be backward compatible, OR
- introduce a new version with migration plan

Schema changes require:
- updated schema docs
- updated API contracts
- an ADR (`09_DECISIONS_ADR.md`)

---

## 8. Schema & API Relationship

- APIs MUST NOT expose fields not defined in schemas
- Schema changes must be reflected in API contracts
- API contracts must not redefine schema rules

Schema is the source of truth.

---

## 9. Notes for AI (Mandatory)

- Never invent fields or entities
- Never infer relationships
- If schema information is missing, request clarification
- Always validate schema alignment before generating code

---

## 10. Governance

Any change to data structure MUST update:
- this document
- affected schema files
- related API contracts
- ADRs (`09_DECISIONS_ADR.md`)

# API Contracts
## Reference Definition — Mini CRM

## 1. Purpose

This document defines the **API contract layer** for the reference mini CRM.

It specifies:
- how APIs must be described
- where contracts live
- how versioning works
- what is mandatory before implementation

This document does **not** define endpoints directly.  
It defines the **rules and structure** that all API definitions must follow.

---

## 2. Contract-First Rule (Mandatory)

- APIs MUST be designed before implementation
- No endpoint may be implemented without:
  - a documented request schema
  - a documented response schema
  - explicit permission rules
- API contracts are treated as **binding agreements**

If an API behavior is not documented, it must not exist.

---

## 3. API Versioning

- All APIs MUST be versioned
- Versioning is explicit in the URL path

Example:

/api/v1/clients
/api/v1/contacts


Breaking changes require:
- a new version
- an ADR (`09_DECISIONS_ADR.md`)
- updated documentation

---

## 4. Authentication & Authorization

All API requests MUST:
- be authenticated
- include tenant context
- be permission-aware

Authorization rules MUST be documented per endpoint.

Security rules are defined in:
- `05_SECURITY_AND_COMPLIANCE.md`

---

## 5. API Contract Structure (Normative)

API contracts MUST be documented using **one** of the following formats:

### Option A — OpenAPI (Recommended)

ai.docs/api/openapi.v1.yaml


### Option B — Structured Markdown (Minimal)

ai.docs/api/endpoints/
├── clients.md
├── contacts.md
└── interactions.md


Each endpoint definition MUST include:
- HTTP method
- Path
- Required permissions
- Request schema
- Response schema
- Error cases

---

## 6. Request & Response Rules

### Requests
- Must be validated strictly
- Must not accept undocumented fields
- Must include tenant context implicitly or explicitly

### Responses
- Must be deterministic
- Must not leak sensitive data
- Must follow documented schemas exactly

No “best-effort” or dynamic responses are allowed.

---

## 7. Error Handling

- Errors MUST follow a consistent structure
- Error responses must include:
  - error code
  - human-readable message
- Internal details must never be exposed

---

## 8. API & UX Relationship

Every API endpoint MUST be mapped to:
- at least one UX screen or flow, OR
- an explicit integration use-case

This mapping is documented in:
- `10_UX_UI_INDEX.md`
- `ux-ui/api-exposure-matrix.md`

---

## 9. Governance

Any change to API behavior MUST update:
- API contract definitions
- related UX documentation
- related data schemas (if applicable)
- ADRs (`09_DECISIONS_ADR.md`)

# Technical Contracts (API & Data Governance)
## ⚡ STRICT CONSTRAINTS FOR AI (MANDATORY)
- **Schema-First:** Define data models in `05_DATA_MODELS.md` before APIs.
- **Contract-First:** No API endpoint exists without a documented request/response.
- **No Hallucination:** Do not invent fields not defined in the schema.
- **Tenant Context:** All APIs must include and validate tenant context.

---

## 1. Data Modeling Governance
- Use **ULIDs** (`public_id`) for public exposure; internal `ids` (bigint) for joins.
- All tenant entities MUST have `company_id`.
- Entities must have `created_at` and `updated_at`.
- Relational integrity must be explicit (Foreign Keys).

---

## 2. API Design Rules
- **Versioning:** Always prefix with `/api/v1/`.
- **Statelessness:** Use Bearer Tokens.
- **Deterministic Responses:** No dynamic fields. Structure must be predictable.

### 2.1 Error Handling
Errors must return:
- `error_code`: String (e.g., `UNAUTHORIZED_ACCESS`).
- `message`: User-friendly string.
- (Internal details are strictly forbidden in responses).

---

## 3. Relationship: Schema ↔ API ↔ UX
- **Alignment:** Schema is the source of truth. APIs must not expose undocumented fields.
- **Mapping:** Every API endpoint must serve a specific screen or integration use-case defined in `06_UX_UI_CONTRACT.md`.

---

## 4. Governance
- Breaking changes require a new version and an ADR in `07_GOVERNANCE_AND_ROADMAP.md`.
- Documentation updates are mandatory BEFORE code modification.

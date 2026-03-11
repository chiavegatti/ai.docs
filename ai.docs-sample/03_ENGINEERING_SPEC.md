# Engineering Specification
## ⚡ STRICT CONSTRAINTS FOR AI (MANDATORY)
- **Tenant Isolation** is non-negotiable. Every query MUST include a tenant filter.
- **Security First:** If a feature violates a security boundary, it MUST be rejected.
- **Structure:** Do not move files or create top-level directories without an ADR.
- **Testing:** No code without Pest tests. 90% coverage is the gate.

---

## 1. Architectural Architecture
This is a **Stateless, API-First, Multi-Tenant** architecture.

### 1.1 Components
- **Application API:** Single source of truth for business logic.
- **Web Interface:** Functional consumer of the API; no business logic in UI.
- **Database Layer:** Relational integrity with explicit multi-tenant `company_id`.

### 1.2 Data Flow
1. Auth -> 2. Tenant Context -> 3. Permissions -> 4. Logic -> 5. Audit -> 6. Response.

---

## 2. Security & Compliance Rules

### 2.1 Authentication & RBAC
- All access must be authenticated (Token-based).
- **Least Privilege:** Roles must be strictly enforced at the API layer.
- **Audit:** sensitive actions (deletions, role changes) are recorded in `audit_logs`.

### 2.2 Tenant Isolation
- **Forbidden:** Cross-tenant joins or updates.
- Isolation must be enforced at: 1. DB Query level, 2. Auth layer, 3. API Contract.

---

## 3. Repository Structure (Structural Contract)

### 3.1 Canonical Layout
```text
/
├── ai.docs/             # Canonical Documentation (Root)
├── apps/                # Application Code
│   ├── api/             # Backend (Laravel/PHP)
│   └── web/             # Frontend
└── ops/                 # Infrastructure & CI/CD
```

### 3.2 Placement Rules
- All code MUST live inside `apps/`.
- All contracts remain in `ai.docs/`.
- No generated code outside `apps/`.

---

## 4. Engineering Standards
- **Atomic Commits:** Small, descriptive commits.
- **Branching:** `feature/*`, `fix/*`, `chore/*`. No direct commits to `main`.
- **Testing (Mandatory):** Use **Pest** for all PHP testing suite.
- **Definition of Done:** Logic + Tests + Documentation updated.

# UX / UI Contract
## ⚡ STRICT CONSTRAINTS FOR AI (MANDATORY)
- **Functional only:** UX is an access and behavior contract, not "design".
- **Zero Hallucination:** No screen, route, or button exists without an entry in the Access Control Matrix.
- **Permission Mapping:** Every UI element must map to a specific API permission.
- **No Implicit Data:** Do not display data fields not defined in `05_DATA_MODELS.md`.

---

## 1. UX Design Philosophy
- **Deterministic:** The UI is a controlled interface to specific system behaviors.
- **Tenant-Aware:** The UI must always clearly indicate and enforce the current tenant context.
- **RBAC Focused:** Components must conditionally render based on documented roles.

---

## 2. Routes & Access Matrix
All routes and their corresponding roles MUST be documented here:

| Screen | Route | Allowed Roles | API Backing |
| :--- | :--- | :--- | :--- |
| **Login** | `/login` | `GUEST` | `POST /auth/login` |
| **Clients List** | `/clients` | `COMPANY_USER`+ | `GET /v1/clients` |
| **Client Details**| `/clients/{id}`| `COMPANY_USER`+ | `GET /v1/clients/{id}` |
| **Admin Panel** | `/admin` | `PLATFORM_ADMIN` | `GET /v1/admin/stats` |

---

## 3. Data Visibility Rules
- **COMPANY_USER:** sees clients and interactions within their tenant.
- **COMPANY_OWNER:** sees everything in their tenant + user management.
- **PLATFORM_ADMIN:** sees global stats and tenant lists (no tenant-specific data unless invited).

---

## 4. UI ↔ API Relationship
- No screen may exist without a documented API endpoint in `04_TECHNICAL_CONTRACTS.md`.
- No response fields from the API may be used if not defined in the schema.

---

## 5. Governance
- New screens require: 1. PRD entry, 2. API endpoint, 3. Entry in this contract.
- UI changes affecting permissions require an ADR in `07_GOVERNANCE_AND_ROADMAP.md`.

# Product Definition
## ⚡ STRICT CONSTRAINTS FOR AI (MANDATORY)
- Do not invent target users or problems beyond what is listed here.
- If a requirement is not in the MVP Goals, do not implement it.
- All functional requirements here MUST have a corresponding Data Model and API Contract before implementation.

---

## 1. Vision & Purpose
This project serves as a **reference context** for the `ai.docs` methodology, using a **B2B, multi-tenant mini CRM** as the example system.
The focus is **documentation discipline** and **reliable AI execution**.

### 1.1 Problem Statement
Many B2B systems fail due to:
- Unclear scope and boundary leakage.
- Poorly defined multi-tenancy (data leakage risks).
- UX built before permission rules are defined.

### 1.2 Proposed Solution
A minimal, well-scoped CRM that allows companies (tenants) to manage clients and contacts with strict isolation and auditable roles.

---

## 2. Target Users
- **Company Owners:** Manage their own tenant and users.
- **Company Admins/Users:** Manage clients and interactions within their tenant.
- **Platform Admins:** Manage the entire multi-tenant infrastructure.

---

## 3. MVP Goals (Scope Boundary)
The system MUST:
- Isolate all data per **Tenant (Company)**.
- Enforce **Role-Based Access Control (RBAC)**.
- Manage **Clients** and **Contacts** within a tenant.
- Record immutable **Interactions** (notes).
- Expose a documented **API**.
- Provide a simple **Dashboards** per role.
- Maintain **Audit Logs** for sensitive actions.

---

## 4. Functional Requirements

### 4.1 Tenant & User Management
- Create/Manage companies.
- Isolate data: A user from Company A never sees data from Company B.
- Roles: `COMPANY_OWNER`, `COMPANY_ADMIN`, `COMPANY_USER`, `PLATFORM_ADMIN`.

### 4.2 Client Management
- CRUD and archive operations for clients.
- Clients belong to exactly one tenant.

### 4.3 Interaction Tracking
- Add notes/events to clients.
- Timestamps and authorship are mandatory.
- Records are immutable (no edits to interactions).

### 4.4 Dashboards
- Respect RBAC and data visibility constraints.

---

## 5. Out of Scope (MVP)
- Advanced analytics, automation workflows.
- AI features (in the CRM itself).
- Email campaigns or external integrations.

---

## 6. Success Criteria
- No undocumented permissions or data access.
- API contracts match implementation 100%.
- AI generates code without asking "what field should I use?".

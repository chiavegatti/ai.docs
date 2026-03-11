# Governance, Roadmap & Checklist
## ⚡ STRICT CONSTRAINTS FOR AI (MANDATORY)
- **ADR First:** Any architectural change or structural decision REQUIRES a new ADR entry here. Do not propose code before the decision is recorded.
- **Roadmap:** Do not implement features listed in "Post-MVP" or "Mid-Term" without explicit PRD approval.
- **Checklist:** No merge to `main` without passing the Release Checklist 100%.

---

## 1. Architectural Decisions (ADR)
| ID | Date | Status | Decision |
| :--- | :--- | :--- | :--- |
| **001** | 2026-02-07 | Accepted | B2B Multi-Tenant, API-First |
| **002** | 2026-02-07 | Accepted | RBAC as mandatory auth model |
| **003** | 2026-02-07 | Accepted | Canonical `ai.docs/` directory at root |
| **004** | 2026-03-11 | Accepted | **Structure Consolidation:** High-density 7-file model |

### ADR-004: Structure Consolidation
- **Context:** Previous 12-file model caused context fragmentation and LLM hallucination.
- **Decision:** Consolidate into 7 high-density files; move constraints to the TOP.
- **Consequences:** Easier for LLMs to maintain state. Requires strict adherence to Consolidated Execution Order in File 01.

---

## 2. Product Roadmap

### 2.1 MVP Goals (Current)
- Multi-tenancy, Users/Roles, Clients, Contacts, Interactions, Basic Dashboards.

### 2.2 Post-MVP (Deferred)
- Advanced Analytics, Automation Workflows, AI insights, External Integrations.

---

## 3. Release Checklist (Production Gate)
- [ ] Release matches `02_PRODUCT_DEFINITION.md`.
- [ ] Code follows `03_ENGINEERING_SPEC.md` (Pest Tests pass, Coverage > 90%).
- [ ] Documents updated (ADR, Schema, API).
- [ ] Tenant isolation verified via tests.
- [ ] Security boundaries respected.

---

## 4. Notes for AI
- Use ADRs to document "Why".
- Use the Roadmap to understand "What's next" but focus on "Now".
- Use the Checklist as the final validation before confirming "Done".

# Boilerplate Structure — Project Rules

## 1. Purpose

Define a clear and enforceable repository structure for:
- application code
- documentation (ai.docs startkit)
- operational scaffolding (optional)

This document is a **structural contract**.  
LLMs and contributors must not invent folders or move files without recording decisions.

---

## 2. Repository Rules (Mandatory)

- Any scope change MUST update the PRD and (if needed) create/update an ADR.
- Do not generate code before validating scope impact in `03_PRD.md`.
- The canonical execution order is defined by the numbered `.md` files in the repository root.
- Do NOT create new top-level directories without updating `09_DECISIONS_ADR.md`.

---

## 3. Engineering Rules (Mandatory)

- It is forbidden to commit code without automated tests.
- Minimum global test coverage required: **90%**.
- Every change must occur in a dedicated branch:
  - `feature/<short-name>`
  - `fix/<short-name>`
  - `chore/<short-name>`
- The `main` branch must remain stable and production-ready.
- Direct commits to `main` are forbidden.
- Merges to `main` only via Pull Request with review.
- Commits must be small, descriptive and focused (atomic commits).
- CI must block merges if:
  - tests fail, or
  - coverage < 90%.

---

## 4. Notes for AI (Mandatory)

- Never invent requirements, schemas or permissions.
- If a file is missing required definitions, request clarification.
- Always propose tests alongside any generated code.
- Never suggest direct edits to `main`.
- Respect multi-tenant assumptions defined in `02_CONTEXT.md`, `03_PRD.md` and `05_SECURITY_AND_COMPLIANCE.md`.

---

# Repository Structure Reference (Contract for LLMs)

## 5. Root Structure (Normative)

/
├── README.md
├── ai.docs/
│   ├── 01_README_AI.md
│   ├── 02_CONTEXT.md
│   ├── 03_PRD.md
│   ├── 04_ARCHITECTURE.md
│   ├── 05_SECURITY_AND_COMPLIANCE.md
│   ├── 06_BOILERPLATE_STRUCTURE.md
│   ├── 07_API_CONTRACTS.md
│   ├── 08_DATA_SCHEMA.md
│   ├── 09_DECISIONS_ADR.md
│   ├── 10_UX_UI_INDEX.md
│   ├── 11_ROADMAP.md
│   └── 12_RELEASE_CHECKLIST.md
├── apps/
│   ├── app-laravel/        (ou api/ + web/)
│   └── worker-python/      (se existir no projeto)
└── ops/
    ├── docker/
    ├── nginx/
    └── ci/


Notes:
- If `apps/` and `ops/` do not exist yet, they may be created during implementation,
  but only if recorded in `09_DECISIONS_ADR.md` (ADR: repo layout decision).
- Top-level numbered documents MUST remain in the repository root.

---

## 6. Placement Rules (Mandatory)

- All application code MUST live inside `apps/` (or an explicitly documented equivalent).
- Documentation and contracts remain in the repository root as the canonical startkit.
- No generated code is allowed outside `apps/`.
- No infrastructure files are allowed outside `ops/` (if used).

---

## 7. Change Control

Any change to repository structure MUST:
- be documented in `09_DECISIONS_ADR.md`
- keep the canonical documentation flow intact
- avoid breaking links referenced by README and numbered docs

---

## 8. Scope Reminder

This file defines **where things live**, not product behavior.

Behavior belongs in:
- `03_PRD.md`

Security constraints belong in:
- `05_SECURITY_AND_COMPLIANCE.md`

API details belong in:
- `07_API_CONTRACTS.md`

Schemas belong in:
- `08_DATA_SCHEMA.md`

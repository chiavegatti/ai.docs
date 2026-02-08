# ai.docs

**ai.docs** is a structured, documentation-first system designed to guide AI-assisted software development from intent to execution — without ambiguity.

It provides a clear, ordered documentation flow that helps humans and AI models collaborate reliably when designing, planning and building software systems.

---

## Why this exists

AI-assisted development often fails not because of code quality, but because of **missing definitions**:
- unclear scope
- undefined data models
- vague API contracts
- undocumented decisions
- UX disconnected from rules and permissions

**ai.docs** addresses this by enforcing:
- explicit schemas and contracts
- a strict execution order
- separation between intent, constraints and implementation
- traceable and reviewable decisions

The result is a system that can be **executed**, not guessed.

---

## What this repository is

This repository is a **startkit / reference implementation** of the **ai.docs methodology**.

It demonstrates how to structure and use an **`ai.docs/` directory** as the **canonical source of truth** for:
- product intent
- requirements
- architecture
- security constraints
- execution rules

It is **not** a code boilerplate.  
It is a **documentation and reasoning framework** designed to be embedded into real projects.

The example used throughout the documentation represents a small system (e.g. a mini CRM), but the methodology applies to projects of any size.

---

## How to use

1. Clone or copy this repository into your project.
2. Ensure the **`ai.docs/` directory exists at the root of your project**.
3. Follow the documentation **in order**, starting from:
4. Complete each document before moving to the next.
5. Treat the documentation as a **contract**, not as optional notes.

The numbered files inside `ai.docs/` represent the **canonical execution order**.

---

## Documentation flow (canonical order)

All documents below live inside the **`ai.docs/` directory**:

1. `01_README_AI.md` — Operational contract for AI / LLMs  
2. `02_CONTEXT.md` — Purpose, scope and boundaries  
3. `03_PRD.md` — Product requirements and rules  
4. `04_ARCHITECTURE.md` — System architecture  
5. `05_SECURITY_AND_COMPLIANCE.md` — Security and compliance constraints  
6. `06_BOILERPLATE_STRUCTURE.md` — Project structure and conventions  
7. `07_API_CONTRACTS.md` — API contracts and versioning  
8. `08_DATA_SCHEMA.md` — Data models and relationships  
9. `09_DECISIONS_ADR.md` — Architectural decisions and rationale  
10. `10_UX_UI_INDEX.md` — UX/UI flows, permissions and routes  
11. `11_ROADMAP.md` — Future evolution  
12. `12_RELEASE_CHECKLIST.md` — Release and delivery gate

---

## Important principles

- Documentation comes **before** code.
- If something is not defined, it must not be implemented.
- AI models must not invent schemas, rules or behavior.
- Decisions must be recorded, not remembered.
- UX is a contract, not decoration.

---

## Contributions

This repository is open to improvements and refinements.

If you contribute:
- respect the canonical execution order
- keep examples consistent
- update related documents when changing templates

Any structural or behavioral change must be reflected inside `ai.docs/`.

---

## License

Open-source. Use, adapt and improve freely.


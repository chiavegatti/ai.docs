# Contributing to ai.docs

Thank you for your interest in contributing to **ai.docs**.

This project is a **documentation-first, contract-driven framework**.  
Contributions are welcome — but they must respect the execution order, governance rules and core principles of the system.

---

## What This Project Values

ai.docs prioritizes:

- Clarity over cleverness
- Explicit contracts over assumptions
- Documentation before implementation
- Traceability over convenience
- Deterministic behavior over “smart” behavior

If a change reduces ambiguity, improves consistency, or strengthens execution reliability, it is likely welcome.

---

## Canonical Structure (Mandatory)

All canonical documentation lives inside the **`ai.docs/`** directory.

The execution order is defined by numbered files:

ai.docs/
├── 01_README_AI.md
├── 02_CONTEXT.md
├── 03_PRD.md
├── 04_ARCHITECTURE.md
├── 05_SECURITY_AND_COMPLIANCE.md
├── 06_BOILERPLATE_STRUCTURE.md
├── 07_API_CONTRACTS.md
├── 08_DATA_SCHEMA.md
├── 09_DECISIONS_ADR.md
├── 10_UX_UI_INDEX.md
├── 11_ROADMAP.md
└── 12_RELEASE_CHECKLIST.md


**Do not change this order** without an approved ADR.

---

## Types of Contributions

We welcome:

- Improvements to documentation clarity
- Fixes for inconsistencies or ambiguities
- Better examples that reinforce execution
- Refinements to governance, contracts or rules
- New templates that follow existing conventions

We do **not** accept:

- Opinionated rewrites without justification
- Undocumented structural changes
- Product-specific assumptions
- Additions that bypass existing contracts

---

## Rules for Changes (Mandatory)

### 1. Respect the Execution Order
If you change a document:
- verify upstream documents still make sense
- update downstream documents if impacted

Example:
- changing `03_PRD.md` may require updates to:
  - `04_ARCHITECTURE.md`
  - `07_API_CONTRACTS.md`
  - `08_DATA_SCHEMA.md`
  - `10_UX_UI_INDEX.md`

---

### 2. Contract-First Principle

No contribution should introduce:
- implicit behavior
- inferred rules
- undocumented permissions
- undefined schemas or APIs

If something is required, it must be documented explicitly.

---

### 3. Architectural Decisions (ADR)

Any change that affects:
- architecture
- repository structure
- execution order
- security posture
- governance rules

**MUST** include a new entry in: ai.docs/09_DECISIONS_ADR.md


ADRs are append-only.  
Do not edit accepted decisions — supersede them.

---

## Pull Request Guidelines

All contributions must be submitted via Pull Request.

Your PR must include:
- a clear description of **what** changed
- a clear explanation of **why** it changed
- references to affected documents
- an ADR, if applicable

PRs may be rejected if they:
- break the canonical order
- introduce ambiguity
- bypass documentation rules
- are inconsistent with existing principles

---

## Style Guidelines

- Write in clear, direct English
- Prefer declarative language (“MUST”, “MUST NOT”, “SHOULD”)
- Avoid vague or promotional language
- Keep documents focused on their defined responsibility

---

## Notes for AI-Assisted Contributions

If you use AI to help generate content:

- Review all output manually
- Ensure no rules, schemas or behaviors are invented
- Ensure consistency with existing documents
- Treat AI output as a draft, not an authority

AI assistance does not exempt contributors from responsibility.

---

## Code of Conduct

Be respectful, constructive and professional.

Discussions should focus on:
- improving execution reliability
- reducing ambiguity
- strengthening contracts

Personal attacks, dismissive language or low-effort contributions are not acceptable.

---

## Final Note

ai.docs is designed to scale **clarity**, not complexity.

If your contribution makes the system easier to understand, reason about and execute — it is welcome.

Thank you for contributing.

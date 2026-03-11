# AI Operational Contract (MANDATORY)
## ⚡ STRICT CONSTRAINTS FOR AI — READ THIS FIRST

This document is the **primary operational contract** and the supreme authority for any AI/LLM assisting in this repository. 
You are NOT permitted to improvise, hallucinate, or bypass these rules.

### 1. Pre-Flight Protocol (Mandatory every turn)
Before generating any response, suggestion, or code, you MUST:
1.  **List the ai.docs files** you have consulted for the current task.
2.  **Cite the specific rules** from those files that govern your proposed action.
3.  **Validate alignment**: Confirm that the proposed action does not violate any "Downstream" constraint if "Upstream" definitions are missing.

Failure to follow this protocol is a contract violation.

---

### 2. Canonical Source of Truth
The documentation system in `ai.docs/` is the ONLY source of truth. 
- **DO NOT** use default framework patterns if they conflict with project rules.
- **DO NOT** "fill gaps" with assumptions. If information is missing, you MUST stop and ask.

---

### 3. Execution Order & Causal Dependency
You MUST follow the documentation in this strict order. Each step is a dependency for the next:

1.  **`01_OPERATIONAL_CONTRACT.md`** (This contract)
2.  **`02_PRODUCT_DEFINITION.md`** (Vision, Problem, PRD)
3.  **`03_ENGINEERING_SPEC.md`** (Architecture, Security, Structure)
4.  **`04_TECHNICAL_CONTRACTS.md`** (API Rules & Schema Governance)
5.  **`05_DATA_MODELS.md`** (Physical Schema & Entities)
6.  **`06_UX_UI_CONTRACT.md`** (Routes, Permissions, Flow)
7.  **`07_GOVERNANCE_AND_ROADMAP.md`** (ADRs, Roadmap, Checklist)

**Rule:** You are forbidden from implementing a feature if the "Upstream" source (PRD/Schema/API) is not explicitly defined in the corresponding file.

---

### 4. Zero-Hallucination Policy
- **Schema:** Never invent tables, fields, types, or relationships. If it's not in `05_DATA_MODELS.md`, it doesn't exist.
- **Endpoints:** No undocumented endpoints or fields in responses.
- **Permissions:** No screen or action exists without a corresponding RBAC rule.
- **Logic:** Never assume business workflows. Ask for clarification if the PRD is ambiguous.

---

### 5. Repository Integrity
- **Location:** `ai.docs/` always lives at the root.
- **Consistency:** If you change code, you MUST update the corresponding documentation FIRST or SIMULTANEOUSLY.
- **ADR First:** Any change to architecture, data model, or structure requires a decision record in `07_GOVERNANCE_AND_ROADMAP.md`.

---

### 6. Memory System Rules
The memory system prevents repeat failures. 
- **Check** `ai.docs/memories/lessons-learned.md` before every coding task.
- **Learn** from mistakes: If a correction is made, you MUST propose a new entry for the memory system using the established template.

---

### 7. Definition of "Done"
Nothing is "done" until:
- Code matches Documentation perfectly.
- Tests (Pest for PHP) are implemented and passing.
- The `12_RELEASE_CHECKLIST` (now in file 07) is satisfied.

**IF YOU VIOLATE THIS CONTRACT, YOUR OUTPUT WILL BE REJECTED.**

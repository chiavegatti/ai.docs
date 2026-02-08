# Architectural Decisions (ADR)
## Decision Records — Mini CRM Reference

## Purpose

This document records **architectural and structural decisions** made during the design of the reference mini CRM.

ADRs exist to capture:
- what was decided
- why it was decided
- what alternatives were considered
- what consequences are expected

ADRs prevent decisions from being lost, re-debated or implicitly changed.

---

## How to Use ADRs (Mandatory)

- Every significant architectural or structural decision MUST be recorded here
- Decisions must be added sequentially
- Decisions must not be edited after acceptance
- Superseded decisions must reference the new decision

If a decision impacts:
- architecture
- data model
- API contracts
- repository structure
- security posture

…it **requires an ADR**.

---

## ADR Format (Normative)

Each decision MUST follow this structure:

- **ID**: incremental number
- **Date**
- **Status**: Proposed | Accepted | Superseded
- **Decision**
- **Context**
- **Alternatives Considered**
- **Consequences**

---

## ADR-001 — B2B, Multi-Tenant, API-First Architecture

- **Date**: 2026-02-07  
- **Status**: Accepted  

### Decision  
The system will be designed as a **B2B, multi-tenant, API-first platform**.

### Context  
The reference system must demonstrate clear tenant isolation, permission boundaries and integration readiness.

### Alternatives Considered  
- Single-tenant architecture  
- B2C-oriented design  

### Consequences  
- Increased architectural rigor  
- Mandatory tenant context in all requests  
- Clear separation between platform and tenant scopes  

---

## ADR-002 — Role-Based Access Control (RBAC)

- **Date**: 2026-02-07  
- **Status**: Accepted  

### Decision  
The system will enforce **role-based access control (RBAC)** for all actions.

### Context  
Explicit permission rules are required to avoid implicit or undocumented access paths.

### Alternatives Considered  
- Attribute-based access control (ABAC)  
- Hardcoded permission checks  

### Consequences  
- Roles must be documented in the PRD  
- All APIs must declare required permissions  
- UX must reflect permission rules  

---

## ADR-003 — Monorepo with Canonical ai.docs Directory

- **Date**: 2026-02-07  
- **Status**: Accepted  

### Decision  
The project will use a **single repository (monorepo)** containing:
- application code
- operational scaffolding
- a canonical `ai.docs/` directory at the root

### Context  
A unified repository simplifies coordination between documentation, architecture and implementation.

### Alternatives Considered  
- Multiple repositories per service  
- External documentation repositories  

### Consequences  
- `ai.docs/` becomes the single source of truth  
- Structural changes require ADR updates  
- CI must support multiple stacks if applicable  

---

## ADR-004 — Documentation-First and Contract-Driven Development

- **Date**: 2026-02-07  
- **Status**: Accepted  

### Decision  
All development will follow a **documentation-first, contract-driven approach**.

### Context  
AI-assisted development requires explicit definitions to avoid hallucination and ambiguity.

### Alternatives Considered  
- Code-first development  
- Informal documentation  

### Consequences  
- PRD, schemas and API contracts must exist before code  
- Changes require synchronized documentation updates  
- AI models are constrained by documented contracts  

---

## ADR-005 — Engineering Governance and Quality Gates

- **Date**: 2026-02-07  
- **Status**: Accepted  

### Decision  
Strict engineering governance rules will be enforced.

### Context  
Predictability, auditability and reliability are required even in small systems.

### Alternatives Considered  
- Direct commits to main  
- No minimum test coverage  

### Consequences  
- Branch-based development  
- Mandatory code reviews  
- Minimum 90% test coverage  
- CI-enforced quality gates  

---

## ADR Lifecycle

- New decisions append new ADRs
- Superseded decisions remain for historical reference
- ADRs must be referenced in:
  - PRs
  - architecture changes
  - schema or API evolution

---

## Scope Reminder

This document records **decisions**, not implementation details.

Implementation belongs in:
- code
- migrations
- configuration

Rationale belongs here.

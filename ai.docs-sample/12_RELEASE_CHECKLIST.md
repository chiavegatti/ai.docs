# Release Checklist
## Production Gate — Mandatory

This checklist MUST be completed before any release to production.
No exceptions.

If an item is not applicable, it must be explicitly marked and justified.

---

## 1. Scope & Readiness

- [ ] Release scope matches `03_PRD.md`
- [ ] No undocumented scope changes
- [ ] All features in this release are fully implemented
- [ ] No partial, experimental or placeholder functionality
- [ ] Feature flags defined for risky or progressive changes (if applicable)

---

## 2. Documentation Consistency

- [ ] PRD reflects the released behavior
- [ ] Architecture document updated if structure changed
- [ ] Security & compliance rules reviewed
- [ ] API contracts updated and versioned
- [ ] Data schemas updated and consistent
- [ ] UX documentation updated (routes, permissions, visibility)
- [ ] ADR created for any significant decision

If behavior changed, documentation MUST have changed first.

---

## 3. Code Quality & Governance

- [ ] All changes developed in branches (no direct commits to `main`)
- [ ] All changes merged via Pull Requests
- [ ] Code review completed
- [ ] Automated tests updated and passing
- [ ] Minimum test coverage threshold met
- [ ] No critical TODOs, debug code or commented logic

---

## 4. Security & Access Control

- [ ] Authentication flows tested
- [ ] Authorization rules tested (RBAC)
- [ ] Tenant isolation validated
- [ ] No secrets committed to repository
- [ ] Sensitive operations audited
- [ ] Error handling does not leak internal details

Security rules must align with:
- `05_SECURITY_AND_COMPLIANCE.md`

---

## 5. Data & Migrations

- [ ] Database migrations reviewed
- [ ] Migrations tested in non-production environment
- [ ] Rollback plan documented
- [ ] Backups verified
- [ ] Schema changes reflected in `08_DATA_SCHEMA.md`

---

## 6. API Stability

- [ ] API contracts respected
- [ ] No undocumented endpoints
- [ ] Breaking changes properly versioned
- [ ] API permissions tested
- [ ] Rate limits reviewed (if applicable)

API behavior must align with:
- `07_API_CONTRACTS.md`

---

## 7. UX & Functional Validation

- [ ] All screens mapped to permissions
- [ ] Data visibility rules validated
- [ ] No UI exposes undocumented data or actions
- [ ] Error and empty states handled
- [ ] UX reflects current business rules

UX rules must align with:
- `10_UX_UI_INDEX.md`

---

## 8. Observability & Reliability

- [ ] Logging enabled and reviewed
- [ ] Error tracking active
- [ ] Health checks validated
- [ ] Timeouts and retries reviewed
- [ ] Monitoring dashboards (if any) updated

---

## 9. Release Notes & Communication

- [ ] Release notes written (user-facing)
- [ ] Internal notes updated (technical / operational)
- [ ] Known limitations documented
- [ ] Support or operations informed (if applicable)

---

## 10. Final Approval Gate

- [ ] Product Owner approval
- [ ] Technical Lead approval
- [ ] Go / No-Go decision recorded

Decision records may reference:
- `09_DECISIONS_ADR.md`

---

## Rollback Conditions

A rollback MUST be executed if any of the following occur:
- security or access control failure
- tenant isolation breach
- data corruption
- critical functionality unavailable
- undocumented behavior detected

Rollback actions and outcomes must be documented.

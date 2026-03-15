# Moderator Checklist

Use this checklist during [Step Review ceremonies](../docs/ceremonies.md) to guide moderation of AI-generated artefacts.

---

## Before You Begin

- [ ] I have read and understood the STEP.md for this step
- [ ] I have the acceptance criteria clearly in mind
- [ ] I have the ARCHITECTURE.md and Domain Language Matrix available for reference
- [ ] I am not under time pressure to accept output I have not fully reviewed

---

## Level 1 — Baseline (all steps)

- [ ] The output matches the scope defined in STEP.md — nothing missing, nothing extra
- [ ] All domain language terms are used correctly (check against the Domain Language Matrix)
- [ ] No hallucinated APIs, libraries, or external references
- [ ] No unresolved TODOs, placeholder comments, or stub implementations
- [ ] No real credentials, API keys, personal data, or sensitive business information

---

## Level 2 — Code Quality (steps producing code)

- [ ] Code follows the patterns and conventions in ARCHITECTURE.md
- [ ] Identifiers (variables, functions, classes, files) use domain language
- [ ] Error paths are handled — not just happy paths
- [ ] No obvious security vulnerabilities:
  - [ ] No SQL / NoSQL injection risks
  - [ ] No hardcoded secrets
  - [ ] No unsafe deserialisation
  - [ ] Input validation is present where needed
- [ ] Code is testable — no hidden global state or untestable side effects

---

## Level 3 — Completeness (feature increment steps)

- [ ] All acceptance criteria from STEP.md are met — evaluate each one explicitly
- [ ] Unit tests are present, meaningful, and pass
- [ ] No existing tests are broken
- [ ] Documentation is updated if any public interfaces changed

---

## Decision

After completing the checklist:

| Decision | Condition | Action |
|---|---|---|
| **Accept** | All applicable criteria pass | Record in REVIEW.md, proceed to QA |
| **Request Revisions** | Minor issues only, clear guidance can be given | Record findings in REVIEW.md, return step to In Progress |
| **Reject** | Fundamental failure or safety concern | Escalate to Tech Lead, record in REVIEW.md |

---

## When in Doubt

- If you are unsure whether a finding is blocking, treat it as blocking.
- If output seems correct but you cannot verify it, escalate to the Tech Lead.
- If the same step fails moderation twice, stop and replan the step.

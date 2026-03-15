# Step Lifecycle

A **step** is the fundamental unit of work in MAID. It represents a bounded, reviewable slice of AI-assisted development. This document describes the full lifecycle of a step from creation to completion.

---

## Step States

```
Planned → In Progress → Under Review → QA → Done
                                  │
                                  └──► Rejected → In Progress (retry)
```

---

## 1. Planned

**Entry criteria:** The step is listed in [ROADMAP.md](../templates/ROADMAP.md) with a defined scope.

**Activities:**
- Tech Lead authors the [STEP.md](../templates/STEP.md) artefact
- Product Owner reviews and approves acceptance criteria
- AI agent and prompt template are identified

**Exit criteria:** STEP.md is complete and approved.

---

## 2. In Progress

**Entry criteria:** STEP.md is approved and the AI work session has started.

**Activities:**
- Tech Lead submits the step's prompt to the AI agent
- AI agent generates output (code, documentation, tests, etc.)
- Tech Lead records prompts and responses
- Iterations may occur if initial output is unsatisfactory

**Exit criteria:** AI output is ready for moderation review.

---

## 3. Under Review

**Entry criteria:** AI output is available for the Moderator to review.

**Activities:**
- Moderator reviews AI output against STEP.md acceptance criteria
- Moderator completes [REVIEW.md](../templates/REVIEW.md)
- Moderator decides: **Accept**, **Request Revisions**, or **Reject**

**If Accepted:** Step moves to QA.  
**If Revisions Requested:** Tech Lead refines the prompt and retries. Step returns to In Progress.  
**If Rejected:** Step is escalated. The team discusses whether to replan the step.

**Exit criteria:** REVIEW.md is complete with an Accept decision.

---

## 4. QA

**Entry criteria:** AI output is accepted by the Moderator.

**Activities:**
- QA / Tester executes the test plan in [QA.md](../templates/QA.md)
- Defects are raised if tests fail

**If all tests pass:** Step moves to Done.  
**If tests fail:** Defects are raised and linked to the step. The step may return to In Progress.

**Exit criteria:** QA.md is complete with all tests passing.

---

## 5. Done

**Entry criteria:** QA is complete and all tests pass.

**Activities:**
- ROADMAP.md is updated to mark the step as Done
- Artefacts (STEP.md, REVIEW.md, QA.md) are committed to the repository
- Team optionally tags the commit (see [annotated-git-tags](../examples/frontend-saved-views/annotated-git-tags.md))

---

## Retry Limit

If a step fails moderation more than twice, the team must hold a brief discussion to determine whether:

- The step scope is too large and should be split
- The prompt needs a fundamental redesign
- The acceptance criteria need clarification
- A different AI agent or model should be tried

# MAID Artefacts

Artefacts are the documents, templates, and records that a MAID team produces and maintains. They provide transparency, traceability, and a shared source of truth.

---

## Project-Level Artefacts

### PRODUCT.md

**Owner:** Product Owner  
**Template:** [templates/PRODUCT.md](../templates/PRODUCT.md)

Describes the product: its purpose, target users, goals, non-goals, and high-level requirements. Serves as the primary input to the AI Product Owner Agent.

### ARCHITECTURE.md

**Owner:** Tech Lead  
**Template:** [templates/ARCHITECTURE.md](../templates/ARCHITECTURE.md)

Describes the technical architecture: stack, key design decisions, constraints, and patterns. Serves as the primary input to the AI Tech Lead Agent and Development Team Agent.

### ROADMAP.md

**Owner:** Product Owner + Tech Lead  
**Template:** [templates/ROADMAP.md](../templates/ROADMAP.md)

Lists the steps to be completed, their order, and their status. Provides a high-level view of progress.

### DOMAIN_LANGUAGE_MATRIX.md

**Owner:** Tech Lead  
**Template:** [templates/DOMAIN_LANGUAGE_MATRIX.md](../templates/DOMAIN_LANGUAGE_MATRIX.md)

A table of domain terms, their definitions, and their usage in prompts and code. Ensures AI output uses consistent, team-agreed vocabulary.

### AGENTS.md

**Owner:** Tech Lead  
**Template:** [templates/AGENTS.md](../templates/AGENTS.md)

Describes the AI agents used in the project: their roles, the models they run on, and any configuration or context they require.

---

## Step-Level Artefacts

### STEP.md

**Owner:** Tech Lead  
**Template:** [templates/STEP.md](../templates/STEP.md)  
**Naming:** `STEP-01.md`, `STEP-02.md`, etc.

Defines a single unit of AI-assisted work: its scope, inputs, expected outputs, acceptance criteria, assigned AI agent, and quality gate.

### REVIEW.md

**Owner:** Moderator  
**Template:** [templates/REVIEW.md](../templates/REVIEW.md)

Records the moderation of AI output for a step: what was reviewed, the criteria applied, decisions made, and any concerns noted.

### QA.md

**Owner:** QA / Tester  
**Template:** [templates/QA.md](../templates/QA.md)

Describes the test plan for a step and records test results. Confirms that accepted AI output behaves correctly end-to-end.

---

## Artefact Lifecycle

```
PRODUCT.md ──► ROADMAP.md ──► STEP.md ──► [AI Work Session]
                                              │
                                              ▼
                                          REVIEW.md ──► (accepted)
                                              │
                                              ▼
                                           QA.md ──► Done
```

See [step-lifecycle.md](step-lifecycle.md) for a detailed walkthrough.

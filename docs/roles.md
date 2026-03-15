# MAID Roles

MAID defines a small set of human roles and AI agent roles. Clear role boundaries prevent confusion and ensure accountability.

---

## Human Roles

### Product Owner

The Product Owner is responsible for defining *what* is built and *why*. In MAID, the Product Owner:

- Authors and maintains the [PRODUCT.md](../templates/PRODUCT.md) artefact
- Sets acceptance criteria for each step
- Reviews and approves the [ROADMAP.md](../templates/ROADMAP.md)
- Participates in [ceremonies](ceremonies.md): Kickoff, Step Review, and Retrospective
- Does **not** write prompts or moderate AI output directly

### Tech Lead

The Tech Lead is responsible for *how* the product is built. In MAID, the Tech Lead:

- Authors and maintains the [ARCHITECTURE.md](../templates/ARCHITECTURE.md) artefact
- Defines the [Domain Language Matrix](../templates/DOMAIN_LANGUAGE_MATRIX.md)
- Writes and refines prompts for AI agents
- Moderates AI output for technical correctness
- Authors [STEP.md](../templates/STEP.md) artefacts
- Participates in all ceremonies

### Moderator

The Moderator reviews AI-generated output before it enters the codebase or product. In MAID, the Moderator:

- Reviews each step's AI output against the quality gate criteria
- Records moderation decisions in the [REVIEW.md](../templates/REVIEW.md) artefact
- May be the same person as the Tech Lead on small teams
- Must have sufficient domain and technical expertise to evaluate the output
- Has authority to reject output and request a retry

### QA / Tester

The QA role validates that accepted AI output behaves correctly end-to-end. In MAID, the QA:

- Authors and executes the [QA.md](../templates/QA.md) test plan for each step
- Verifies that quality gates were met in practice
- Raises defects if accepted output later fails in testing

---

## AI Agent Roles

### Product Owner Agent (ChatGPT)

An AI model used to assist the human Product Owner with:

- Drafting user stories and acceptance criteria
- Generating initial PRODUCT.md content from a brief
- Suggesting roadmap breakdowns

See: [prompts/product-owner-chatgpt.md](../prompts/product-owner-chatgpt.md)

### Tech Lead Agent (ChatGPT)

An AI model used to assist the human Tech Lead with:

- Generating ARCHITECTURE.md drafts
- Suggesting domain language terms
- Reviewing technical approaches

See: [prompts/tech-lead-chatgpt.md](../prompts/tech-lead-chatgpt.md)

### Development Team Agent (Claude)

An AI model used to generate implementation artefacts:

- Code, tests, and documentation for a specific step
- Follows instructions from the STEP.md artefact
- Output is always moderated before acceptance

See: [prompts/development-team-claude.md](../prompts/development-team-claude.md)

---

## Role Summary Table

| Role | Human or AI | Primary Artefact | Quality Gate Responsibility |
|---|---|---|---|
| Product Owner | Human | PRODUCT.md | Accepts/rejects step scope |
| Tech Lead | Human | ARCHITECTURE.md, STEP.md | Writes prompts, moderates output |
| Moderator | Human | REVIEW.md | Accepts/rejects AI output |
| QA / Tester | Human | QA.md | Validates end-to-end behaviour |
| Product Owner Agent | AI | PRODUCT.md draft | None — output is moderated |
| Tech Lead Agent | AI | ARCHITECTURE.md draft | None — output is moderated |
| Development Team Agent | AI | Code, tests, docs | None — output is moderated |

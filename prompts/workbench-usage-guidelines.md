# Workbench Usage Guidelines

The **workbench** is the environment in which AI work sessions take place. These guidelines apply regardless of which AI model or interface you are using.

---

## Principles

1. **One step, one session.** Start a fresh conversation for each STEP. Carrying context from a previous step increases the risk of the AI making assumptions based on earlier work.

2. **System prompt first.** Always begin a session by pasting the system prompt for the agent role. This sets the AI's behaviour before any content is provided.

3. **Context before task.** Provide architecture, domain language, and relevant source context *before* stating the task. The AI produces better output when it has context before instructions.

4. **Record everything.** Paste the full prompt (including context) into STEP.md or a dedicated prompt log. If the AI's output is accepted, the prompt that produced it is part of the record.

5. **Never include sensitive data.** Before submitting any prompt, review it for:
   - Real API keys or credentials
   - Production data or PII
   - Commercially sensitive algorithms or IP
   - Information your organisation's AI policy prohibits sharing

---

## Starting a Session

1. Open a new conversation (do not reuse an old one).
2. Paste the system prompt from the relevant prompt template.
3. Paste the context block: ARCHITECTURE.md sections, Domain Language Matrix, relevant source files.
4. Paste the STEP.md for the current step.
5. Send the message and wait for any clarifying questions.

---

## During a Session

- Answer clarifying questions directly and concisely.
- If the AI's output is partial or incorrect, provide specific feedback: *"The function does not handle the case where X is null"* is more effective than *"This is wrong"*.
- If the AI introduces terms not in the Domain Language Matrix, correct it immediately: *"Use 'SavedView' not 'Bookmark'"*.
- If the AI extends scope beyond the STEP, redirect it: *"That is out of scope for this step. Please focus on Y only."*

---

## Ending a Session

- Copy all prompts and the final accepted output into the relevant artefacts.
- Do **not** submit AI output directly to a pull request or codebase — it must pass moderation first.
- Close the session.

---

## Choosing an Interface

| Interface | Best for | Notes |
|---|---|---|
| ChatGPT (web) | Product Owner Agent, Tech Lead Agent | Good for document drafting and conversational refinement |
| Claude.ai (web) | Development Team Agent | Good for long-context code generation |
| GitHub Copilot (IDE) | Inline code assistance | Use with caution — output is not always captured in a prompt log |
| API | Automated or reproducible workflows | Requires additional tooling to capture prompt history |

---

## Data Residency and Privacy

Before using any AI workbench, confirm:

- [ ] Your organisation's AI usage policy permits the use of this tool
- [ ] You understand whether the AI provider stores or trains on your input
- [ ] You are not submitting data that violates data residency requirements

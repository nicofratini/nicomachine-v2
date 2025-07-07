# Mailbox Protocol

## 1. Overview

The Mailbox system facilitates direct, asynchronous communication between agents. It is designed for targeted requests and notifications, complementing the global context provided by the Memory Bank.

The system resides in the `.roo/mailbox/` directory.

## 2. Message Structure

Each message is a Markdown file named according to the recipient agent's slug (e.g., `to-tester.md`, `to-architect.md`).

A message MUST contain the following frontmatter headers:

- `from`: The slug of the sending agent.
- `timestamp`: The ISO 8601 timestamp of when the message was sent.
- `id`: A unique identifier for the message (e.g., a UUID).
- `priority`: (Optional) `high` or `normal` (defaults to `normal`).

The body of the message should contain a clear, actionable request or notification.

### Example Message (`.roo/mailbox/to-tester.md`):

```markdown
---
from: nestjs-developer
timestamp: "2025-07-07T11:15:00Z"
id: "msg-a4b1c9e0"
priority: high
---

**Request: Integration Test**

Please run integration tests on the new `auth-service`. The relevant code has been pushed to the `feature/new-auth` branch.

Reference Decision Log: `ADR-004`.
```

## 3. Workflow

1.  **Sending:** An agent creates a message file in the `.roo/mailbox/` directory.
2.  **Checking:** At the beginning of its operational cycle, each agent MUST check the mailbox for messages addressed to it.
3.  **Processing:** If a message is found, the agent MUST prioritize it according to its `priority` and internal logic.
4.  **Archiving:** Once a message has been processed and its task completed, the receiving agent is responsible for deleting the message file from the mailbox directory to prevent re-processing. The action taken should be logged in the `progress.md` file in the Memory Bank, referencing the message `id`.

## 4. State Messages

- When checking the mailbox: `[MAILBOX: CHECKING]`
- When processing a message: `[MAILBOX: PROCESSING MESSAGE id:msg-a4b1c9e0]`
- When archiving a message: `[MAILBOX: ARCHIVING MESSAGE id:msg-a4b1c9e0]`
# Memory Bank Protocol

## Overview
The Memory Bank is a structured set of files in `.roo/memory-bank/` used for persistent context management across sessions and agents.

## Core Files
- `activeContext.md`: Current session state and objectives.
- `productContext.md`: High-level project vision and specs.
- `progress.md`: Task tracking and project status.
- `decisionLog.md`: Architecture Decision Records.
- `systemPatterns.md`: Links to established coding standards.

## Command: Update Memory Bank (UMB)
- The `UMB` is a conceptual command representing a workflow to update the Memory Bank.
- Agents with write permissions can directly modify the files.
- For agents without write access, they must request an update from an agent with the appropriate permissions (e.g., `tester`).

## State Messages
- Agents must use clear status messages when interacting with the Memory Bank.
- `[MEMORY BANK: READING]`
- `[MEMORY BANK: UPDATING]`
- `[MEMORY BANK: ACTIVE]`

## Context Management
- **Transfer:** Sub-task delegation must include a summary of the relevant context from the Memory Bank.
- **Condensation:** When context approaches token limits (90%), agents should summarize the Memory Bank content before proceeding.
- **Persistence:** The Memory Bank is designed to be persistent through VS Code sessions.
# Memory Curation Patterns

## 1. Agent Role: Memory Curator

The Memory Curator is a specialized background agent responsible for the proactive maintenance, optimization, and structuring of the Memory Bank. Its primary goal is to ensure the long-term integrity, performance, and usability of the shared project context.

It operates autonomously and does not typically handle direct development tasks.

## 2. Core Responsibilities

### 2.1. Context Condensation & Summarization
- **Trigger:** When `activeContext.md` or `progress.md` exceed a certain size or complexity threshold.
- **Action:** Generate concise summaries of lengthy entries. Move detailed, but no longer immediately active, context to an archival file (e.g., `memory_archive.md`).
- **Goal:** Keep the active context lean and focused, reducing the token load for other agents.

### 2.2. Decision Log Indexing
- **Trigger:** Periodically (e.g., once per operational cycle or on a time basis).
- **Action:** Analyze `decisionLog.md`. Create and maintain an index or a table of contents at the top of the file for quick navigation of Architecture Decision Records (ADRs).
- **Goal:** Make critical decisions easily searchable and referenceable.

### 2.3. Knowledge Graph Structuring
- **Trigger:** On-going background task.
- **Action:** Parse all Memory Bank files to identify entities (e.g., services, components, technologies) and their relationships. It can maintain a separate file, `knowledge_graph.json` or `knowledge_graph.md`, representing these relationships.
- **Goal:** Transform unstructured text into a structured knowledge base for advanced querying and analysis by other agents.

### 2.4. Integrity Checks
- **Trigger:** Periodically.
- **Action:** Scan for broken links between documents (e.g., a reference to a non-existent ADR in `progress.md`). Check for formatting inconsistencies.
- **Goal:** Ensure the overall health and reliability of the Memory Bank.

## 3. State Messages
- `[CURATOR: SUMMARIZING]`
- `[CURATOR: INDEXING ADRS]`
- `[CURATOR: ARCHIVING CONTEXT]`
- `[CURATOR: RUNNING INTEGRITY CHECK]`
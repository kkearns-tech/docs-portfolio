# Decisions (Lightweight ADR Log)

Use this log to record decisions that affect workflows, terminology, or system design.

## Template
- **Decision:**
- **Context:**
- **Options considered:**
- **Why this option:**
- **Consequences / follow-up:**

---
## 2026-05-13 - add a generated ID property to Batch
- **Decision:** add a generated ID property to batch that is a formula to create an id for tha batch based on the name, date, and time it was produced:
- **Context:** Need a way to refer to a batch that is unique
- **Options considered:** hand-creating a name, unique id, and this metadata aware id
- **Why this option:** unique AND human readable to make sure mistakes don't happen
- **Consequences / follow-up:** easier way to refer to batches with reduced human error

## 2026-05-06 — Track sales closeout at the batch level

- **Decision:** Track units sold, remaining, and waste directly on each Batch record for v0.
- **Context:** Flavor is an attribute of production, not a separate sales entry. Capturing sales by batch avoids duplicate flavor entry and keeps event-day logging simple.
- **Options considered:**
  - Separate sales summary by event/flavor
  - Separate batch closeout database
  - Closeout fields directly on Batch records
- **Why this option:** Batch-level closeout is the simplest model that supports reconciliation without adding unnecessary databases or duplicate fields.
- **Consequences / follow-up:** Revenue estimates are derived from batch closeout data. Event-level payment totals remain on the Event record for actual reconciliation.

## 2026-05-06 — Adopt hybrid iterative + milestone delivery model

- **Decision:** Use an iterative (Agile-style) workflow for execution, with defined milestones (v0.1, v0.2, v1.0) to group and communicate feature delivery.

- **Context:** The project is being developed by a single contributor with evolving requirements based on real-world usage (event operations). A fully predefined plan would be too rigid, but completely unstructured iteration would make progress harder to communicate and evaluate.

- **Options considered:**
  - Pure Agile (no predefined milestones, fully emergent scope)
  - Waterfall (define all requirements and deliver in sequence)
  - Hybrid model (iterative work within milestone targets)

- **Why this option:**
  - Supports incremental progress and adaptation based on actual use
  - Provides clear checkpoints for reviewing progress and communicating status
  - Balances flexibility (iteration) with structure (milestones)
  - Aligns well with a docs-as-code workflow and visible versioning (tags/releases)

- **Consequences / follow-up:**
  - Milestones must remain flexible and may be re-scoped based on learnings
  - Status reports should reference both current work (issues) and milestone progress
  - GitHub Issues will represent execution-level work; roadmap will reflect milestone-level goals

## 2026-03-03 — Establish docs-as-code as source of truth
- **Decision:** Maintain operational and system documentation in a Git repository, published via MkDocs.
- **Context:** Need repeatable, auditable documentation with change history.
- **Options considered:** Notion-only docs; Google Docs; Markdown + MkDocs.
- **Why this option:** Versioning, portability, and portfolio value.
- **Consequences / follow-up:** Keep operational checklists concise; link to supporting references as needed.


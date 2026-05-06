# Project Charter — Popstiche Ops

## Project Purpose
Design and document a lightweight operational system to support event-based retail (Popstiche), including workflows, data model, and reporting.

## Objectives
- Document repeatable event-day workflows
- Define a minimal, usable data model
- Establish a system for reconciliation and restocking decisions
- Publish documentation using a docs-as-code workflow (MkDocs + GitHub Actions)

## Scope (v0–v1)
**In scope**
- Events, batches, sales summaries, inventory
- Workflow documentation (prep, event day, reconciliation)
- Data model and architecture overview

**Out of scope (for now)**
- POS replacement
- Real-time analytics
- Advanced forecasting

## Success Criteria
- Documentation is clear enough to follow during a live event
- Data captured supports reconciliation and restocking decisions
- Site is publicly accessible and versioned

## Constraints
- Must be usable during live events (low friction)
- Limited time and resources (single contributor)
- Notion used as initial system of record

## Stakeholders
- Owner (primary user)
- Event staff (secondary users)
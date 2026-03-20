# Architecture Overview (Conceptual)

## Purpose
This page captures a pragmatic architecture that can support Popstiche operational tracking over time. It is intentionally simple.

## Conceptual components
- **Client**: phone/tablet for event logging and summary entry
- **System of record**: a database (or Notion initially)
- **Reporting**: generate daily summaries and restock signals
- **Exports**: produce CSV/PDF artifacts for review or bookkeeping

## Conceptual diagram
```mermaid
flowchart LR
  User[Owner / Staff] --> Docs[Operational Workflows]
  User --> Record[System of Record]
  Record --> Reports[Daily Summary + Restock Signals]
  
Notes

The operational workflows are the primary source of truth for how data is captured.

System implementation can evolve without changing the documented intent and definitions.
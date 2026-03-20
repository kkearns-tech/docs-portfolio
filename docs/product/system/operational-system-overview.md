# Operational System Overview

Operational workflows (documented in the Product section) define:

What data is captured

When it is captured

Who is responsible

How it is used

These workflows ensure that:

Data entry is consistent

Reporting is reliable

Decisions are based on repeatable processes

## Purpose
This document describes the operational system used to run Popstiche, including how data is captured, stored, and used to support event-based retail operations.

The system is intentionally simple, prioritizing reliability and usability during live events over technical complexity.

---

## System Summary

The Popstiche operational system consists of two layers:

1. **Operational Layer (System of Record)**  
   - Tool: Notion  
   - Purpose: Capture and manage real-time business data

2. **Documentation Layer (System Design & Reference)**  
   - Tool: GitHub + MkDocs  
   - Purpose: Document workflows, data structures, and system design decisions

This separation ensures that operational tasks remain fast and accessible, while documentation remains structured, versioned, and portable.

---

## Operational Layer (Notion)

### Role
Notion serves as the **system of record** for Popstiche operations.

It is used during:
- Event execution
- Prep and inventory management
- End-of-day reconciliation

### Core Data Domains

The operational system is organized around four primary data domains:

#### 1. Events
Tracks where and when sales occur.

**Example fields**
- Date
- Location
- Booth fee
- Staff assigned
- Notes (weather, traffic, anomalies)

---

#### 2. Batches (Production)
Tracks production during events.

**Captured data**
- Flavor
- Event
- Time (optional)
- Units produced (yield)
- Waste (if applicable)

---

#### 3. Sales (Aggregated)
Tracks units sold and revenue at the event level.

**Captured data**
- Event
- Flavor (optional granularity)
- Units sold
- Revenue estimate
- Payment breakdown (optional)

---

#### 4. Inventory (Ingredients & Supplies)
Tracks stock levels and replenishment needs.

**Captured data**
- Ingredient name
- Unit (lbs, oz, count)
- Current quantity
- Par level (minimum threshold)
- Cost per unit (optional)

---

### Design Principles

The operational system is designed to:

- Minimize data entry during live events
- Favor consistency over precision where needed
- Support end-of-day reconciliation
- Enable restocking decisions without complex tooling

---

## Documentation Layer (MkDocs)

### Role
The documentation site serves as the **system design reference**.

It captures:
- Operational workflows
- Data model definitions
- Architecture decisions
- Terminology and constraints

### Purpose

This layer exists to:
- Provide a stable, version-controlled source of truth
- Enable clear communication of system behavior
- Support future system evolution (e.g., API or custom tooling)

---

## Data Flow (Conceptual)

```mermaid
flowchart LR
  Staff[Event Staff] --> Notion[Notion - System of Record]
  Owner[Owner] --> Notion

  Notion --> Review[Reconciliation & Review]
  Review --> Decisions[Restock & Planning Decisions]

  Notion -. informs .-> Docs[Documentation (MkDocs)]
  
  
  Reporting and Outputs

At the end of each event, the system produces:

Sales summary (units and revenue)

Inventory consumption (estimated)

Restock list (based on par levels)

Operational notes (qualitative insights)

These outputs support:

Inventory planning

Cost awareness

Event evaluation

Tradeoffs and Constraints
Chosen Approach

Notion-based system for speed and flexibility

Documentation-first architecture for clarity and scalability

Tradeoffs

Limited automation in v0

Some reliance on manual data entry

Approximate data during high-volume periods

Rationale

This approach prioritizes:

Usability during live events

Low setup and maintenance overhead

Clear upgrade path to more advanced systems

Future Evolution

Potential future enhancements include:

Automated reporting (CSV or dashboard generation)

API layer for integrations (POS, analytics)

Mobile-friendly data entry interface

Real-time inventory tracking

The current documentation structure is designed to support these future transitions without requiring a redesign of core concepts.

Summary

Popstiche’s operational system is designed to be:

Practical — usable in real event conditions

Structured — based on defined workflows and data models

Evolvable — ready to support future automation or system expansion

The combination of a flexible operational tool (Notion) and a structured documentation system (MkDocs) provides both immediate usability and long-term clarity.
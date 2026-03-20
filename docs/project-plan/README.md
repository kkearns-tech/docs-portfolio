# Popstiche Inventory & Event Ops API
 
## Purpose 

Help you track money + inventory
Reduce end-of-event chaos
Make restocking decisions rational instead of vibes-based


## Product Concept

A lightweight SaaS for:

- Tracking inventory (corn, sugar, flavor dust, limeade syrup 🍋)
- Managing event locations
- Recording daily batch yields
- Sales tracking by flavor + event
- Basic forecasting

Admin Guide: “Add event location,” “Reconcile inventory,” “Export daily report”

Architecture: POS → API → database → reporting job queue

REST design

Role-based access (event staff vs admin)

Reporting/export workflows

Async processing (CSV exports)

## Popstiche Ops is a lightweight event-based inventory + production tracking platform.

It handles:

- Event locations
- Batch production (kettle runs)
- Ingredient inventory
- Flavor recipes
- Sales logging
- After action reports
- End-of-day reconciliation
- Reporting exports

## User Roles (Important for portfolio depth)
|Role	| Capabilities|
|-------|-------------------------------|
|Owner	|Full access, financial reporting|
|Event Staff	|Log batches + sales|
|Prep Lead	|Manage inventory + recipes|
|Accountant (future)	|Read-only reporting|

## Core Data Model (Architecture Backbone)
Entities:
- Ingredient
- Flavor
- Recipe
- Batch
- Event
- Sale
- InventoryAdjustment
- User

## Realistic API Surface
- Inventory
  * GET /ingredients
  * POST /ingredients
  * POST /inventory/adjustments
- Production
  * POST /batches
  * GET /batches?event_id=...
- Events
  * POST /events
  * GET /events
- Sales
  * POST /sales
  * GET /sales?event_id=...
- Reporting
  * POST /reports/daily-summary
  * GET /reports/{id}
  
## Architecture Design

Components

- API service — CRUD operations, auth
- Postgres — inventory, sales, events
- Queue (Redis/SQS) — report generation
- Worker — creates CSV summaries
- Object storage — stores exported reports

## Doc set ideas

Home
Getting Started
API Reference
Admin Guide
Production Workflows
Architecture Overview
Data Model

## Possible additions:
Webhook documentation (for POS integration)
Rate limiting section
API versioning section
Audit log section
Data retention policy

## Design Principles 

This system should:
- Work at a folding table with sticky hands.
- Require minimal typing during events.
- Handle offline gaps (spotty WiFi at fairs).
- Make end-of-day reconciliation easy.
- Not over-engineer forecasting yet.

## Events

Track where you are and when.

Fields:
- Name
- Location
- Date
- Expected attendance
- Weather notes
- Booth fee
- Staff assigned

Why it matters:
- You can calculate event profitability later.

## Ingredients (Inventory Backbone)

Track:
- Corn kernels
- Sugar
- Oil
- Flavor mix
- Limeade syrup
- Cups
- Bags

Fields:
- Name
- Unit (lbs, oz, gallons, count)
- Current stock
- Par level (minimum before reorder)
- Cost per unit

This powers:
- Restocking alerts
- Margin calculations
- Batch cost estimation

## Recipes (Flavor Intelligence)

Each flavor has:
- Ingredients + quantities per batch
- Yield per batch (bags produced)
- Target margin

This lets you:
- Predict how much sugar you’ll burn through
- Estimate event needs
- Compare flavor profitability

## Batches (Production Log)

During event:
- Select flavor
- Record batch start time
- Record number of bags yielded
- Mark if waste occurred

This:
- Automatically deducts inventory
- Feeds sales forecasting later
- This is where real operational clarity happens.

## Sales (Simplified)

Track:
- Flavor
- Quantity sold
- Payment type (cash/card/venmo)
- Price per unit

That’s enough for:
- Revenue
- Margin
- Event profit
- Payment reconciliation

## End-of-Day Reconciliation

System should generate:
- Total revenue
- Ingredient consumption
- Estimated profit
- Inventory remaining
- Restock warnings

## Roles (RBAC)

- Owner:
  * Full access
  * Financial visibility
- Event Staff:
  * Can log batches + sales
  * Cannot edit costs or recipes
  
## Key Metrics 

At event:
- Bags per hour
- Revenue per hour
- Most popular flavor

After event:
- Profit after booth fee
- Ingredient depletion
- Restock recommendations

Explain the business reasoning behind each metric.

## Data Model (Clean and Real)

Core tables:
- users
- events
- ingredients
- recipes
- recipe_ingredients (join table)
- batches
- sales
- inventory_adjustments
- report_jobs


# Architecture 
(image)

## Doc Navigation
Home
Getting Started
User Roles & Permissions
Event Workflow
Production Workflow
Inventory Management
API Reference
Data Model
Architecture Overview
Reporting & Reconciliation

# Scope
Before we write anything, answer these:
- Will you track exact cash vs card totals?
- Do you want ingredient cost tracking from day one?
- Do you want forecast logic now or later?
- Are you imagining this as:
  * A Notion-backed prototype first?
  * Or straight conceptual architecture for portfolio?

Once we answer that:
- Define the exact data schema
- Define the API contracts
- Outline your MkDocs page structure

## Two Layers: Ops Brain vs Portfolio Brain

Think of it like this:

|Layer	|Tool	|Purpose|
|-------|-------|-------|
|🛠 Operational System	|Notion (for now)	|Actually run Popstiche|
|📚 Docs-as-Code Site	|MkDocs + GitHub	|Demonstrate architecture + modern skills|


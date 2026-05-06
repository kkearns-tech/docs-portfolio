 
# Data Model (v0 Draft)

This model defines the minimum entities required to support workflows and reconciliation.

## Entities

### Event
- id (implicit)
- name (text)
- date (date)
- location (text)
- booth_fee (number, $)
- notes (text)

### Ingredient
- id
- name (text)
- unit (select: lbs, oz, count, gallons)
- on_hand (number)
- par_level (number)
- cost_per_unit (number, optional)

### Flavor
- id
- name
- notes (optional)

### Recipe (Flavor composition)
- id
- flavor_id
- yield_units_per_batch
- notes (optional)

### Batch
- event (relation → Event)
- flavor (text)
- time (optional)
- yield_units (number)
- waste_units (number, optional)
- notes (text)



### Sales Summary
- event (relation → Event)
- flavor (text, optional)
- units_sold (number)
- revenue (number, optional)
- payment_split (text, optional)

## Relationships (conceptual)
- Event has many Batches
- Event has many Sale Summaries
- Flavor has one Recipe
- Recipe references Ingredients (via a join table in a full implementation)

## System Rules

- Inventory is reduced based on batch production, not sales
- Sales may be approximate; batch production is the primary metric
- Reconciliation compares:
  - batches produced
  - units sold
  - remaining inventory

- Restock decisions are based on:
  - current on_hand vs par_level
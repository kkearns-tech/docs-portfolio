
### `docs/system/data-model.md`
```md
# Data Model (v0 Draft)

This model defines the minimum entities required to support workflows and reconciliation.

## Entities

### Event
- id
- date
- location
- booth_fee (optional)
- notes

### Ingredient
- id
- name
- unit
- on_hand_quantity
- par_level (optional)
- cost_per_unit (optional)

### Flavor
- id
- name
- notes (optional)

### Recipe (Flavor composition)
- id
- flavor_id
- yield_units_per_batch
- notes (optional)

### Batch (Production run)
- id
- event_id
- flavor_id
- started_at
- yield_units
- waste_units (optional)
- waste_reason (optional)

### Sale Summary (Event-level, practical)
- id
- event_id
- flavor_id (optional)
- units_sold
- gross_revenue (optional)
- payment_split (optional)

## Relationships (conceptual)
- Event has many Batches
- Event has many Sale Summaries
- Flavor has one Recipe
- Recipe references Ingredients (via a join table in a full implementation)
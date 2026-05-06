# Data Model (v0 Draft)

This model defines the minimum entities required to support event workflows, batch production, sales closeout, and end-of-day reconciliation.

## Design Principle

Popstiche Ops v0 tracks production first.

A **Batch** represents what was made. Sales and closeout data are captured against the batch so flavor, event, and production data do not need to be duplicated.

---

## Entities

### Event

An Event represents a single sales opportunity, such as a market, fair, festival, or pop-up.

| Property | Type | Required | Notes |
|---|---|---:|---|
| Name | Title | Yes | Example: Frederick Market — 2026-05-09 |
| Date | Date | Yes | Event date |
| Location | Text | Yes | Venue or city |
| Booth Fee | Number | No | Cost to participate |
| Cash Total | Number | No | Actual cash collected |
| Card Total | Number | No | Actual card total |
| Venmo Total | Number | No | Actual Venmo total |
| Gross Collected | Formula | No | Cash + Card + Venmo |
| Notes | Text | No | Weather, traffic, staffing, issues |

---

### Ingredient

An Ingredient represents a consumable item used in production or packaging.

| Property | Type | Required | Notes |
|---|---|---:|---|
| Name | Title | Yes | Example: Popcorn kernels |
| Unit | Select | Yes | lbs, oz, count, gallons |
| On Hand | Number | Yes | Current available amount |
| Par Level | Number | No | Minimum desired amount |
| Cost per Unit | Number | No | Used for future cost calculations |
| Notes | Text | No | Supplier, package size, storage notes |

---

### Flavor

A Flavor represents a sellable popcorn or drink variety.

| Property | Type | Required | Notes |
|---|---|---:|---|
| Name | Title | Yes | Example: Classic Kettle Corn |
| Default Unit Price | Number | No | Used for revenue estimates |
| Notes | Text | No | Flavor description, allergens, prep notes |

---

### Recipe

A Recipe defines the expected production structure for a flavor.

| Property | Type | Required | Notes |
|---|---|---:|---|
| Name | Title | Yes | Usually matches flavor name |
| Flavor | Relation → Flavor | Yes | Flavor this recipe produces |
| Expected Yield per Batch | Number | No | Expected sellable units |
| Notes | Text | No | Prep notes or assumptions |

!!! note
    Recipe ingredients may be added later through a Recipe Ingredients join table. For v0, recipes can remain lightweight until ingredient-level deduction is needed.

---

### Batch

A Batch represents one production run. Flavor is captured here because flavor is a property of what was made.

| Property | Type | Required | Notes |
|---|---|---:|---|
| Name | Title | Yes | Example: Classic Batch 1 |
| Event | Relation → Event | Yes | Event where batch was produced |
| Flavor | Relation → Flavor | Yes | Flavor produced |
| Time Produced | Date/Time | No | Useful during live events |
| Units Produced | Number | Yes | Total units made |
| Waste Units | Number | No | Units lost/spoiled during production |
| Units Available | Formula | No | Units Produced - Waste Units |
| Units Sold | Number | No | Units sold from this batch |
| Units Remaining | Number | No | Units left after event |
| Units Comped/Donated | Number | No | Giveaways, samples, donations |
| Unit Price | Rollup or Number | No | From Flavor default price, or manually entered |
| Revenue Estimate | Formula | No | Units Sold × Unit Price |
| Closeout Variance | Formula | No | Units Available - Units Sold - Units Remaining - Units Comped/Donated |
| Notes | Text | No | Production or sales notes |

---

## Relationships

- Event has many Batches
- Batch belongs to one Event
- Batch has one Flavor
- Flavor may have one or more Recipes
- Recipe belongs to one Flavor
- Ingredient is not directly deducted in v0 unless recipe ingredient tracking is added

---

## System Rules

### Production Tracking

- Batch production is the primary operational record.
- Flavor is captured on the Batch because flavor is determined when the batch is made.
- Sales closeout is recorded on the Batch to avoid duplicating flavor and event data.

### Revenue Tracking

- Batch-level revenue is estimated from units sold and unit price.
- Event-level payment totals are actual collected totals.
- Reconciliation compares estimated batch revenue against gross collected revenue.

### Inventory Tracking

- Inventory is reduced based on batch production, not individual sales.
- Ingredient-level deduction is deferred until recipe ingredient tracking is implemented.
- Restock decisions are based on current On Hand values compared to Par Level.

### Reconciliation

End-of-day reconciliation compares:

- Units produced
- Units wasted
- Units sold
- Units remaining
- Units comped/donated
- Estimated revenue
- Actual gross collected

The goal is not perfect accounting in v0. The goal is consistent operational visibility.

---

## Future Enhancements

Potential future entities:

### Recipe Ingredient

A join table connecting Recipes to Ingredients.

| Property | Type | Notes |
|---|---|---|
| Recipe | Relation → Recipe | Parent recipe |
| Ingredient | Relation → Ingredient | Ingredient used |
| Quantity | Number | Amount used per batch |
| Unit | Rollup or Select | Measurement unit |

### Inventory Adjustment

A manual inventory correction record.

| Property | Type | Notes |
|---|---|---|
| Ingredient | Relation → Ingredient | Adjusted item |
| Adjustment Type | Select | Restock, waste, correction, donation |
| Quantity | Number | Amount added or removed |
| Reason | Text | Why the adjustment happened |
| Date | Date | When adjustment occurred |
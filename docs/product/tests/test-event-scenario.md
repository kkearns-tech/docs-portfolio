# Test 1

## Event situation

We’re going to simulate:

prep
production
sales
reconciliation

🧾 Step 1: Create the Event
Event Record
Property Value
Name Frederick Saturday Market — 2026-05-09
Date 2026-05-09
Location Frederick, MD
Booth Fee 75
Cash Total 214
Card Total 356
Venmo Total 48
Notes Warm weather, high afternoon traffic

Gross Collected formula should give: 618

Step 2: Create Ingredients
Ingredients
Name Unit On Hand Par Level
Popcorn Kernels lbs 50 20
Sugar lbs 25 10
Oil gallons 5 2
Salt oz 40 10
Limeade Syrup gallons 3 1
Medium Bags count 500 200

Step 3: Create Flavors
Flavors
Name Default Unit Price
Classic Kettle Corn 8
Caramel Corn 10
Cheddar Jalapeño 9
Limeade 5

Step 4: Create Batches
Batch 1
Property Value
Name Classic Batch 1
Event Frederick Saturday Market
Flavor Classic Kettle Corn
Units Produced 30
Waste Units 2
Units Sold 25
Units Remaining 2
Units Comped/Donated 1
Unit Price 8
Revenue Estimate 200
Closeout Variance
Should equal: 0 Because: 30 - 2 - 25 - 2 - 1 = 0

Batch 2
Property Value
Name Caramel Batch 1
Event Frederick Saturday Market
Flavor Caramel Corn
Units Produced 20
Waste Units 1
Units Sold 17
Units Remaining 1
Units Comped/Donated 1
Unit Price 10

Batch 3
Property Value
Name Cheddar Jalapeño Batch 1
Event Frederick Saturday Market
Flavor Cheddar Jalapeño
Units Produced 15
Waste Units 0
Units Sold 13
Units Remaining 1
Units Comped/Donated 1
Unit Price 9

## Validation Outcome

Completed first end-to-end operational simulation using sample event data.

Key findings:
- Batch-centric reconciliation model validated
- Event-level payment tracking simplified reconciliation
- Additional reporting rollups identified as future enhancement area
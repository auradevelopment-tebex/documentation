---
description: Register billing in aura_foodtruck - sending bills and getting paid.
---

# Register

Open **Register** on the truck (employees only). Pick the items, pick a nearby player, send the bill.

### How a bill works

1. The cashier builds a bill from the menu — totals are computed from server-side prices.
2. The customer gets a payment prompt with the item list and total.
3. Accept: money is taken from the customer and paid out to the business (society account or directly to the employee, see `sales.account`). Decline: the cashier is told and sees it in the UI.
4. Paid orders appear in the cooking UI so the kitchen knows what to make. Marking them served logs `player_order_completed`.

{% hint style="warning" %}
Bills expire after `bills.ttlSeconds` (default 5 minutes). Totals above `bills.maxTotal` and bills with more than `bills.maxItems` lines are rejected server-side.
{% endhint %}

Next: [NPC Sales](./npc-sales.md)

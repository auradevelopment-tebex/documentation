---
description: NPC walk-up sales in aura_foodtruck - customers, patience and handoff.
---

# NPC Sales

Stand near your truck and run `/sellfoodtruck` (command name in `sales.command`). Random NPC customers walk up, place priced orders from your menu, and wait at the handoff point.

### How a sale works

1. An NPC walks up and an order card appears above their head with the items and total.
2. Cook or grab the matching items, walk to the customer and choose **Hand Over Order**.
3. Items are removed from your inventory first, then the payout lands in the business. The order is logged as `npc_order_served`.

{% hint style="info" %}
Customers have patience — take too long and they curse at you and walk away (`npc_order_expired`). `customerComfort` upgrades make them wait longer.
{% endhint %}

### Tuning the flow

* Go further than `sales.maxDistance` from the truck (or lose the truck) and sales stop automatically.
* `service` upgrades allow more simultaneous customers, `marketing` speeds up arrivals, `signage` grows orders to 2 items, `premiumIngredients` boosts every payout. See [Configuration](../configuration.md).

Next: [Tablet](./tablet.md)

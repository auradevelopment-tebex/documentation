---
description: How players sell items to the pawnshop counter in aura_pawnshop.
---

# Selling at the Counter

Any player **without** the `pawn` job can sell valuables to the shop while it is in **NPC mode**.

### How a player sells

1. Walk up to the pawnbroker NPC behind the counter and use the target option.
2. The sell menu opens with the items from your inventory that the shop buys, sorted into **Collectibles**, **Antiques**, **Tech**, **Plushies** and **Misc**.
3. Pick an item and an amount, or use **sell all valuables** to sell everything the shop buys at once.
4. You are paid in **cash**, straight away.

The items go into **Manager storage**, where managers can list them on the [marketplace](./marketplace-and-deliveries.md).

### What the shop pays

The price for each item is its price in `Marketplace.basePrices`, unless the owner set a lower price in the **Buy List**. The owner can also turn an item off or cap how many the shop buys.

### When the counter refuses

| Message / situation | Why |
| --- | --- |
| "The shop can not cover that buy-in right now." | The shop account doesn't have enough money. A manager must deposit in **Treasury**. |
| The NPC is not there | The shop is in **player mode**. Staff run the counter in person. |
| The item is not in the menu | It is not on the buy list, turned off, over its cap, on the blacklist (`money`, `black_money`, `radio`), or missing from your inventory's item list. |
| Employees get no sell option | By design: staff can't sell to their own shop. |
| Nothing happens at all | `Counter.sellEnabled = false` in `configs/shared/main.lua`, or the inventory can't put items into storage ([Compatibility](../compatibility.md#inventory)). |

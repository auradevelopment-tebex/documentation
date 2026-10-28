---
description: Walk-in NPC customers in aura_pawnshop - opening the door, haggling and regulars.
---

# Walk-in Customers

Walk-ins are NPC customers who come through the shop door for staff to deal with. They need [aura_dialog](../../../free-releases/aura_dialog/README.md) running: without it staff get *"aura_dialog is not running — negotiation unavailable"*.

### Open the door

An employee in the shop types:

```
/pawnsell
```

Every employee sees *"The shop door is open — walk-ins welcome"*. A customer walks in after 30 to 90 seconds, goes to the counter and waits. Type `/pawnsell` again to close the door; the current customer leaves.

You must be inside or near the shop, and your grade needs the `view_market` permission (every grade by default).

### Talk to the customer

Stand near the customer and use the target option to start the conversation. An info card above their head shows who they are.

About 70% of customers come to **sell**, the rest come to **buy**.

**A seller** brings 1 to 3 items:

1. Ask questions about the item's **condition**, **provenance** and **authenticity**. The answers hint at what it is really worth.
2. Make an offer. Some sellers name a price, some wait for yours.
3. If they accept, the shop pays from its account and the items go into **Employee storage**.

**A buyer** wants 1 to 2 items the shop has **listed on the marketplace**:

1. They name what they want and their budget.
2. Make your price. If they accept, the items are taken from the marketplace listings and the money goes into the shop account.

Buyers only ask for items that are listed, so keep stock on the [marketplace](./marketplace-and-deliveries.md).

### Limits on offers

So staff can't drain the shop or give items away:

* You can't offer a seller more than **150%** of the item's normal price (`offerMaxPct`).
* You can't sell to a buyer for less than **50%** of the item's normal price (`offerMinPct`).

### Patience

A customer waits about **6 minutes**. Ask them to **hold on** to get 90 more seconds, up to 3 times. Then they leave.

### Personalities and regulars

Every customer has a personality (gruff, shady, chatty, collector, desperate and more) that changes how they talk and haggle. Customers come back: the **Regulars** tab on the marketplace tablet keeps a file on each one, with their deals so far. With **MugShotBase64** running, the file also has their photo.

### Turning walk-ins off

Set `WalkUps.enabled = false` in `configs/shared/main.lua`. All other features keep working.

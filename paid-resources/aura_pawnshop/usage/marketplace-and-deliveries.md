---
description: Listing items on the marketplace tablet, NPC orders, deliveries and fence offers in aura_pawnshop.
---

# Marketplace & Deliveries

This is how the shop turns stock into money: employees list items, NPC buyers buy them, and an employee delivers the order in the van.

### 1. List an item

1. Put the item in **your own inventory** (take it from a storage first).
2. Use the **Marketplace tablet** and open **Listings**.
3. Choose **Create listing**, pick the item, the amount and your price per item.

The item leaves your inventory when you list it.

* Your price must be between `minListingPrice` and `maxListingPrice`, and at most `maxPriceMultiplier` (5x) the item's normal price.
* Each employee can have up to 10 listings at once (the owner can change this in **Settings**).
* If `playerSetPrices = false`, you can't choose a price: items sell at their normal price with bulk discounts.

Withdraw a listing to get the items back. When a manager withdraws your listing, the items go back to you.

### 2. Wait for a buyer

After 8 to 35 minutes an NPC buyer buys the listing and creates an **order**. Every employee gets a notification: *"Order #12 sold to M. Vance — ready for delivery"*.

* Priced **above** the normal price: it takes longer to sell (up to 60 extra minutes).
* Priced **below**: it sells sooner (up to 20 minutes sooner).
* The **Faster Buyers** upgrade makes every listing sell up to 55% sooner.
* With **Order Bundling**, one order can contain several different items.

### 3. Take the delivery

1. On the tablet, open **Deliveries**. The order board shows every waiting order.
2. Accept an order. *"Order #12 accepted — grab the van and deliver to Legion 24/7"*.
3. The [delivery van](../delivery-van.md) spawns at the pick-up point behind the shop, with keys and fuel. A GPS route on the map shows the drop-off.

### 4. Deliver the goods

1. Drive to the drop-off.
2. Get out and walk to the **rear doors** of the van. Take the package.
3. Carry it to the buyer and hand it over.
4. Drive the van back to the pick-up point and park it there to finish.

You have **10 minutes** from accepting the order (`Delivery.timeoutMinutes`). If the timer runs out, you cancel, disconnect or lose the van, the order goes back on the board for someone else.

### Who gets paid

When the package is handed over:

* The sale value goes into the **shop account**.
* The driver gets **commission** in cash, paid from the shop account: 12% of the sale value plus a `$300` flat fee by default. The owner can change both in **Settings**.

If the shop account can't cover the commission, the hand-over fails with *"Society cannot cover the payout right now"*. Deposit money and try again.

### Premium drop-offs

The **Premium Routes** upgrade unlocks up to 5 premium drop-offs that pay 25% to 100% more. Once unlocked, about a third of orders go there (`Delivery.premiumChancePct`).

### Fence offers

Every 10 minutes there is a chance (25%) that a fence wants something the shop has listed, for **1.6x to 2.8x** its normal price. Employees get a notification:

```
FENCE OFFER: Whisper wants x2 Golden Watch for $4,320 — expires in 8 min!
```

The offer appears on the order board. Accept and deliver it like any order, before it expires. If nobody takes it in time, the items go back on the marketplace.

* The shop needs at least one item listed for a fence to show up.
* The **Fence Connections** upgrade makes offers appear more often.

### Regulars

The **Regulars** tab on the tablet lists walk-in customers you have met before, with notes from past deals. See [Walk-in Customers](./walk-ins.md).

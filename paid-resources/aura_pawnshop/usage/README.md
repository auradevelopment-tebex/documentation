---
description: How aura_pawnshop works in game - who does what and where.
---

# Usage

The shop has three kinds of people:

* **Customers:** any player without the `pawn` job. They sell valuables at the counter.
* **Employees:** the `pawn` job. They list items, deliver orders and deal with walk-in customers.
* **Managers and the owner:** grade `3` and up. They also run the boss menu. The owner (top grade) can do everything.

### Where things are

Every point inside the shop is a target option. Staff only see the ones their grade can use.

| Target | Who | What it does |
| --- | --- | --- |
| Pawnbroker NPC | Customers | Sell items to the shop ([Selling at the Counter](./selling-at-the-counter.md)) |
| Display tray | Everyone | A public stash on the counter, for handing items over in person |
| Employee storage | Employees | Shared staff stash. Items bought from walk-ins land here |
| Manager storage | Managers | Items bought at the counter land here |
| Marketplace tablet | Employees | List items, see regulars, take deliveries ([Marketplace & Deliveries](./marketplace-and-deliveries.md)) |
| Management terminal | Managers | The boss menu ([Boss Menu](./boss-menu.md)) |
| Staff wardrobe | Employees | Save and load up to 5 work outfits |
| Warehouse entrance | Employees | Extra storage, after the upgrade ([Warehouse](./warehouse.md)) |

### How money flows

Everything goes through the **shop account** (the society account, `pawn` by default):

* Counter purchases and walk-in purchases are **paid from** the shop account.
* Marketplace sales, deliveries and walk-in sales **pay into** the shop account.
* Driver commission and upgrades are **paid from** the shop account.
* Managers deposit and withdraw in the boss menu (**Treasury**).

{% hint style="warning" %}
A new shop starts with `$0`. Until someone deposits money, the pawnbroker can't buy anything from players. See [First Setup](./first-setup.md).
{% endhint %}

### Pages

1. [First Setup](./first-setup.md): what the owner does on day one
2. [Selling at the Counter](./selling-at-the-counter.md): customers selling to the shop
3. [Marketplace & Deliveries](./marketplace-and-deliveries.md): listing items, orders, the van, fence offers
4. [Walk-in Customers](./walk-ins.md): opening the door, haggling, regulars
5. [Boss Menu](./boss-menu.md): every tab of the management terminal
6. [Warehouse](./warehouse.md): the extra storage interior

Next: [First Setup](./first-setup.md)

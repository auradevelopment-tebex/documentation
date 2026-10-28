---
description: The aura_pawnshop warehouse - extra storage unlocked by the Warehouse Expansion upgrade.
---

# Warehouse

The warehouse is a separate interior with extra storage. It is **locked** until the owner buys the **Warehouse Expansion** upgrade in the [boss menu](./boss-menu.md#upgrades).

### Going in

1. Use the **warehouse entrance** target near the shop (only employees see it).
2. You are teleported inside: *"Entered Warehouse — 1 of 5 storage units"*.
3. Use the exit inside to come back.

Before the upgrade, the entrance says *"Warehouse not unlocked — purchase the Warehouse Expansion upgrade"*.

### Storage inside

* **Employee and manager crates:** the same stashes as in the shop, so staff can reach their storage from inside.
* **Storage units:** each Warehouse Expansion level adds one unit (5 in total by default). Each unit is its own stash with 80 slots and 300 kg.

After buying a level, staff already inside get *"exit and re-enter to load it"*. The new unit appears the next time they enter.

{% hint style="info" %}
The upgrade does not make the shop's own stashes bigger. It only adds warehouse units. Shop stash sizes are set in `Storage` in `configs/shared/main.lua`.
{% endhint %}

### Moving units or using another interior

Unit positions are in `Warehouse.units`, as offsets from the level's `interior` point. To move one: stand where you want it, take your coords, subtract the `interior` coords, and put the result in the list. See [Configuration](../configuration.md#warehouse-warehouse).

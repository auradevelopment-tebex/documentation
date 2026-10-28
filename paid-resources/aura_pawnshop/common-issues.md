---
description: Common issues with fixes for aura_pawnshop.
---

# Common Issues

Fixes for the most common setup mistakes. Turn on `Debug = true` in `configs/shared/main.lua` to see more detail in the F8 and server console, and turn it off again when you are done.

### `invalid item '...' — not in the items database, skipped` in console

The item is missing from your inventory, so the shop skips it.

Fix: add the items from [Framework Setup](./framework-setup.md) to your **inventory** (ox_inventory uses its own `data/items.lua`, even on ESX), restart the server, then check with `/pawnitems <item>`.

### `item validation skipped: no item database found`

Your inventory or framework starts after `aura_pawnshop`, or isn't running.

Fix: `ensure` your framework and inventory **before** `aura_pawnshop` in `server.cfg`.

### No target options in the shop

The target resource or the framework starts after the shop, or you don't have the job.

Fix: start `ox_target` / `qb-target` and your framework before `aura_pawnshop`. Check your job is exactly `pawn` (or your `JOB_NAME`). Managers-only points (terminal, manager storage) need grade `3` or up.

### Players are standing in an empty building / fall through the floor

The rStudio Pawn Shop MLO is missing or starts after the shop.

Fix: install the MLO and `ensure` it. If you moved the shop elsewhere, move every location in `configs/shared/main.lua` together: `Blip`, `Storage`, `Warehouse.entrance`, `Interactions`, `NPC`, `WalkUps` and `Delivery.pickup`.

### The pawnbroker says "The shop can not cover that buy-in right now."

The shop account doesn't have enough money.

Fix: a manager deposits cash in the boss menu (**Treasury**).

### The pawnbroker NPC is gone

The shop is in **player mode**.

Fix: a manager switches it back to NPC mode in the boss menu (**Settings**).

### `shop storage needs qb-inventory 2.x` in console

You run qb-inventory 1.x. It has none of the stash functions the shop uses.

Fix: update to qb-inventory 2.x, or use ox_inventory.

### Storage won't open on ESX

The ESX built-in inventory has no stashes.

Fix: use `ox_inventory` with ESX. See [Compatibility](./compatibility.md#inventory).

### "aura_dialog is not running — negotiation unavailable"

Staff can't talk to walk-ins without aura_dialog.

Fix: install [aura_dialog](../../free-releases/aura_dialog/installation.md) and `ensure` it before `aura_pawnshop`.

### Walk-in customers never come

The door is closed, or walk-ins are turned off.

Fix: type `/pawnsell` inside the shop, then wait up to 90 seconds. Check `WalkUps.enabled = true`. Buyers only come for items that are listed on the marketplace.

### Listings never sell

A buyer takes 8 to 35 minutes, and longer if your price is above the item's normal price.

Fix: wait, lower the price, or buy the **Faster Buyers** upgrade. You can also lower `buyerDelayMinMinutes` / `buyerDelayMaxMinutes` in `configs/server/main.lua`.

### The delivery van doesn't spawn or is invisible

The resource folder was renamed, or the van files were moved.

Fix: keep the folder name `aura_pawnshop` with `stream/` and `data/aurapawnvan/` inside, then restart the server (not only the resource) so players download the model. To use a GTA van instead, see [Delivery Van](./delivery-van.md#using-a-different-vehicle).

### Drivers can't start the van

Your vehicle key resource isn't detected.

Fix: check the list in [Compatibility](./compatibility.md#other-resources). For another key resource, add it in `bridge/vehiclekey/client.lua`.

### "Society cannot cover the payout right now" at the drop-off

The shop account can't pay the driver's commission.

Fix: deposit money in **Treasury**, then hand the package over again.

### My config change does nothing

Permissions, buy list, mode, policies and upgrades are saved in the database after the first start.

Fix: change them in the boss menu, or [reset the saved setting](./configuration.md#resetting-saved-settings).

### Money is split between two accounts

`StandaloneBank.enabled = true` while your banking resource also works, and the banking resource failed to start once.

Fix: if your banking resource is supported, set `StandaloneBank.enabled = false`.

### Still stuck?

Open a ticket in our [Discord](https://discord.gg/ZWrEnn358r) with: your framework, inventory and target (with versions), your `server.cfg` ensure order, the `[pawnshop]` lines from the server console with `Debug = true`, and what you did before it went wrong.

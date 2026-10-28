---
description: Frequently asked questions for aura_pawnshop.
---

# FAQ

### Do I need the rStudio Pawn Shop MLO?

Yes, [buy it here](https://rstudiomaps.tebex.io/package/6793070). Every location in the config (counter, stashes, boss desk, NPC, walk-in path, van pick-up) is placed for that MLO. With another interior you have to move all of them yourself in `configs/shared/main.lua`.

### Do I need to import an SQL file?

No. The resource creates its own database tables the first time it starts. You only add the job and items ([Framework Setup](./framework-setup.md)). On ESX the job is added with SQL.

### Do I need aura_bridge?

No. Everything aura_pawnshop needs to work with your framework, inventory, target and banking is built in.

### Is aura_dialog required?

Only for walk-in customers. Without it, staff can't talk to walk-ins. Everything else works. It is a [free resource](../../free-releases/aura_dialog/README.md).

### Where does the money go?

Into the shop's society account (`Society.account`, `pawn` by default; `society_pawn` on ESX). Counter purchases, walk-in purchases, driver commission and upgrades are paid from it. Sales are paid into it. See [Usage](./usage/README.md#how-money-flows).

### Why won't the pawnbroker buy anything?

Most likely the shop account is empty. A manager has to deposit money in **Treasury** first. Other reasons are listed in [Selling at the Counter](./usage/selling-at-the-counter.md#when-the-counter-refuses).

### Can employees sell their own items to the counter?

No. Staff can't sell to their own shop. They list items on the marketplace instead.

### How do I hire someone?

The owner or a manager hires them at the **Management terminal** (**Employees** → **Hire**) while the player is in the shop. You don't need `/setjob` for staff.

### I changed the config but nothing changed in game?

Permissions, the buy list, shop mode, policies and upgrades are saved in the database the first time the resource starts, and the owner changes them in game. The config is only the starting value. Change them in the boss menu, or [reset the saved row](./configuration.md#resetting-saved-settings).

### How do I add a new item the shop buys and sells?

1. Add the item to your inventory and restart it.
2. Give it a price in `Marketplace.basePrices` in `configs/server/main.lua`.
3. Optional: add it to `Sell.buyList.items` with a category, and to `WalkUps.sellPool` / `buyPool` for walk-ins.
4. Restart the server. If the item is still missing from your inventory, the console prints a red `invalid item` line for it.

### Can I use a different delivery vehicle?

Yes. Set `Delivery.truckModel` in `configs/shared/main.lua`, for example `` `speedo` ``, and remove the `truckLook` livery. See [Delivery Van](./delivery-van.md).

### Do I have to add the van to my vehicle shop or garage?

No. It is streamed by the resource and only spawns for deliveries.

### Can I hide the shop from the map?

Set `Blip.enabled = false` in `configs/shared/main.lua`.

### Can I rename the resource folder?

No. aura_pawnshop is protected by CFX escrow, and escrowed resources can't be renamed. Keep the folder name `aura_pawnshop`.

### Can I rename the job?

Yes. Change `JOB_NAME` at the top of `configs/shared/main.lua` and use the same name in your framework. Changing it also renames the stashes, so they start empty.

### Which files can I edit?

`configs/`, `bridge/` and `locales/`. The rest is escrowed.

### What language is the resource in?

9 languages ship: `en`, `de`, `fr`, `es`, `pt`, `ru`, `tr`, `zh`, `ar`. Set the server language with `setr ox:locale <code>` in `server.cfg`.

### Does it log to Discord?

No. Activity is shown in game: staff notifications, the **Transactions** and **Orders** tabs.

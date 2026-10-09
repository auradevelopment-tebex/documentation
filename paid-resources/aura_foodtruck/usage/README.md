---
description: How aura_foodtruck works - cooking, register, NPC sales and the tablet.
---

# Usage

Everything runs through the four target points on the truck, gated by job where configured:

1. **Cook Food** — recipe menu, craft timers, live queue ([Cooking](./cooking.md))
2. **Open Register** — bill nearby players, they pay through a prompt ([Register](./register.md))
3. **Sell** (`/sellfoodtruck`) — walk-up NPC customers ([NPC Sales](./npc-sales.md))
4. **Tablet** (item or `/foodtrucktablet`) — dashboard, bank, upgrades, logs ([Tablet](./tablet.md))

The **tray** is public so customers can grab their food; **storage** is employees-only. Each truck gets its OWN tray/storage stashes (named per model + plate), so stock never leaks between trucks.

Next: [Cooking](./cooking.md)

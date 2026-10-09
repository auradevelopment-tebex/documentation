---
description: Cooking food in aura_foodtruck - recipes, craft timers and the queue.
---

# Cooking

Open **Cook Food** on the truck (employees only). Pick a recipe to see its ingredients.

### How a craft works

1. Select a recipe.
2. Press **Craft Item** — ingredients are removed from your inventory **first**, then the timer runs with animation, freeze and smoke.
3. When the timer finishes the finished item lands in your inventory and the craft is logged.

{% hint style="info" %}
Ingredients are removed before the reward is given, and the server re-validates everything — a manipulated client can only get itself an error, never free items.
{% endhint %}

### Craft queue

Every started craft shows in the queue with its live timer. Finished crafts stay in the orders list for `orders.completedTtl` seconds (default 60).

### Eating your work

Anything in `consumables` is usable straight from the inventory: eating/drinking plays an animation with a progress bar, removes 1x item and restores hunger/thirst. `eat`/`alcohol` items also relieve a little stress. See the per-item values in [Menus](../menus.md).

Next: [Register](./register.md)

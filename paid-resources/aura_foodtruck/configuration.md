---
description: Configuring aura_foodtruck - every option in configs/shared/main.lua.
---

# Configuration

All shared options live in `configs/shared/main.lua`. Server-only tuning (cooldowns, bill caps, log retention) lives in `configs/server/main.lua`.

### General

| Option | Default | Description |
| --- | --- | --- |
| `debug` | `false` | Prints debug messages to the server/client consoles. Turn off on live servers. |
| `useConsumables` | `true` | If true, eating/drinking crafted items restores hunger/thirst. |
| `framework.bossGrades` | `{ 'boss', 'chief' }` | ESX `grade_name` values treated as owner/boss grades. Add yours if your ESX names them differently. |

### Interaction points (`target`)

| Option | Default | Description |
| --- | --- | --- |
| `target.offsetRadius` | `0.75` | How close (in meters) the player must stand to a point before its option appears. |
| `target.interactDistance` | `2.0` | How far away (in meters) the player can be to see the option at all. |
| `target.customerInteractDistance` | `2.3` | How close the player must be to a waiting NPC customer to hand over an order. |
| `target.offsets.storage` | `vector3(0.41, -3.20, 0.59)` | Storage attachment offset, relative to the truck model. |
| `target.offsets.register` | `vector3(-1.00, -1.57, 0.89)` | Register attachment offset, relative to the truck model. |
| `target.offsets.tray` | `vector3(-1.10, -0.61, 0.80)` | Tray attachment offset, relative to the truck model. |
| `target.offsets.cooking` | `vector3(0.66, 1.43, 0.82)` | Cooking station attachment offset, relative to the truck model. |
| `target.offsets.handoff` | `vector3(-1.60, -0.92, 0.55)` | Order handoff attachment offset, relative to the truck model. |

Use `/foodtruckoffset` (admin only) in-game to find and print new offsets for custom truck models — aim at a spot and press **E** to save it, **R** toggles fivem-freecam fly mode, **G** prints, **X** clears, **Backspace** exits.

### Offset finder (`offsetFinder`)

| Option | Default | Description |
| --- | --- | --- |
| `offsetFinder.defaultSpeed` | `1.0` | Freecam fly speed when toggled on. |
| `offsetFinder.minSpeed` | `0.10` | Slowest step (fine placement against the truck). |
| `offsetFinder.maxSpeed` | `15.0` | Fastest step. |
| `offsetFinder.speedStep` | `2.0` | Each **Z** / **C** press divides / multiplies the speed. |

### Business tablet (`tablet`)

| Option | Default | Description |
| --- | --- | --- |
| `tablet.item` | `'foodtruck_tablet'` | Inventory item that opens the business tablet. |
| `tablet.command` | `'foodtrucktablet'` | Chat command that opens the business tablet. |
| `tablet.openMode` | `'both'` | How the tablet can be opened: `'item'`, `'command'` or `'both'`. |
| `tablet.defaultProfileImage` | `'./svg/exampleProfileImage.png'` | Avatar used until the owner sets one. |
| `tablet.maxLogs` | `80` | How many recent activity logs the tablet shows. |
| `tablet.ownerGrades` | `{ 3, 4 }` | Job grades allowed to open the tablet — **exact match** (grade 5 can NOT open it). Empty table = everyone in the job. |
| `tablet.useCharacterNames` | `true` | `true` = firstname lastname, `false` = FiveM/Steam name. |

`tablet.jobAliases` maps your server's actual job names to the food truck jobs (`['your_server_job_name'] = 'foodtruck_job_name'`). Names are normalized before matching (lowercased, spaces/dashes removed), so `Burger Shot` and `burger_shot` both match `burgershot`.

### Activity logging (`logging`)

| Option | Default | Description |
| --- | --- | --- |
| `logging.enabled` | `true` | Master switch — `false` disables ALL logging. |
| `logging.types.crafted` | `true` | A player finished cooking an item. |
| `logging.types.order_paid` | `true` | A player paid a register bill. |
| `logging.types.player_order_completed` | `true` | A register order was marked as served. |
| `logging.types.npc_order_created` | `true` | A walk-up NPC placed an order. |
| `logging.types.npc_order_served` | `true` | A walk-up NPC order was handed over. |
| `logging.types.npc_order_expired` | `true` | A walk-up NPC left because the order took too long. |
| `logging.types.upgrade_purchased` | `true` | A business upgrade was bought. |
| `logging.types.bank_deposit` | `true` | Money deposited into the business bank. |
| `logging.types.bank_withdraw` | `true` | Money withdrawn from the business bank. |

The tablet dashboard is computed from these logs: `npc_order_served` + `order_paid` feed order counts, revenue and the 7-day trends, `crafted` feeds crafted items. Logs older than `logs.retentionDays` are pruned nightly.

### Cooking (`cooking`)

| Option | Default | Description |
| --- | --- | --- |
| `cooking.maxQuantity` | `10` | Max items a player can cook at once (also the server-side cap). |
| `cooking.cookingAnim.dict` | `'mini@repair'` | Animation dictionary played while cooking. |
| `cooking.cookingAnim.name` | `'fixing_a_ped'` | Animation name played while cooking. |
| `cooking.cookingAnim.flag` | `49` | Animation flag. |
| `cooking.smoke.enabled` | `true` | `false` skips the smoke particle effect entirely. |
| `cooking.smoke.dict` | `'core'` | Particle dictionary for the cooking smoke effect. |
| `cooking.smoke.ptfx` | `'exp_grd_grenade_smoke'` | Particle effect that puffs from the truck while cooking. |
| `cooking.smoke.scale` | `0.58` | Smoke particle scale. |
| `cooking.smoke.duration` | `6500` | How long one puff lasts (milliseconds). |
| `cooking.smoke.color` | `vector3(1.0, 1.0, 1.0)` | RGB tint (0.0–1.0 per channel). |

### Orders (`orders`)

| Option | Default | Description |
| --- | --- | --- |
| `orders.completedTtl` | `60` | How long a served order stays in the orders list before being removed (seconds). |

### NPC sales (`sales`)

| Option | Default | Description |
| --- | --- | --- |
| `sales.enabled` | `true` | Enables walk-up NPC customers (the `/sellfoodtruck` system). |
| `sales.command` | `'sellfoodtruck'` | Chat command to start/stop selling. |
| `sales.account` | `'society'` | Where sale money goes: `'society'` = the owning job's society/business bank account, `'cash'` or `'bank'` = paid directly to the employee. |
| `sales.societyPrefix` | `false` | Society account naming in your banking resource: `false` = raw job name (e.g. `burgershot`), `true` = `society_` prefixed (e.g. `society_burgershot`). Only used when `account = 'society'`. |
| `sales.defaultPrice` | `35` | Fallback price when neither the recipe nor `sales.prices` sets one. |
| `sales.orderDelay` | `25000` | Milliseconds between NPC customers spawning. |
| `sales.maxActiveCustomers` | `1` | Max NPC customers waiting at the same time (before upgrades). |
| `sales.spawnDistance.min` | `13.0` | Minimum spawn distance from the truck (meters). |
| `sales.spawnDistance.max` | `19.0` | Maximum spawn distance from the truck (meters). |
| `sales.handoffDistance` | `3.5` | How close to the truck NPCs stop and wait (meters). |
| `sales.maxDistance` | `20.0` | Safety leash — going further (or the truck being deleted) stops sales and sends waiting customers away. |

Price fallback chain per item: `recipe.price` → `sales.prices` → `sales.defaultPrice`.

### Sales upgrades (`sales.upgrades`)

Each level costs `baseCost * (currentLevel + 1)`.

| Upgrade | Max Level | Base Cost | Effect per level |
| --- | --- | --- | --- |
| `marketing` | 3 | `$500` | Removes 5000 ms from `orderDelay` (min 8 s gap) |
| `signage` | 2 | `$750` | NPC orders get 2 items instead of 1 at level 2 |
| `service` | 2 | `$1000` | +1 simultaneous waiting customer |
| `premiumIngredients` | 3 | `$1250` | +8% payout on every player and NPC order |
| `expressPrep` | 3 | `$1500` | Cooking is 8% faster |
| `customerComfort` | 2 | `$900` | NPCs wait 20 extra seconds |

### Consumables (`consumables`)

`item_name = hunger/thirst restored (0–100)`. Every listed item is registered as a usable inventory item: using it plays an eating/drinking animation with a progress bar, removes 1x item, then restores the stat. `eat`/`alcohol` also relieve a little stress. See the full per-item table in [Menus](./menus.md).

### Food trucks (`foodTrucks`)

One entry per vehicle model: owning `job`, UI `theme`, `shopName`, `targets` (tray/storage inventories with slots and weight in grams; `jobRestricted` gates employees-only points — the tray stays public so customers can grab food) and `recipes` grouped into menu categories. Each truck gets its OWN tray/storage stashes (named per model + plate), so stock never leaks between trucks.

### Server tuning (`configs/server/main.lua`)

| Option | Default | Description |
| --- | --- | --- |
| `bills.ttlSeconds` | `300` | Unpaid register bills expire after this long. |
| `bills.maxTotal` | `100000` | Bills above this total are rejected server-side. |
| `bills.maxItems` | `25` | Bills with more lines are rejected server-side. |
| `bills.sweepCron` | `'*/5 * * * *'` | Expired-bill cleanup schedule. |
| `npcOrders.sweepCron` | `'*/2 * * * *'` | Expired-NPC-order cleanup schedule. |
| `npcOrders.createCooldownMs` | `2000` | Min gap between NPC orders per employee. |
| `cooking.cookCooldownMs` | `1000` | Min gap between cook requests per player. |
| `cooking.maxPendingPerPlayer` | `8` | Unfinished crafts allowed per player before new cooks are refused. |
| `tablet.transferCooldownMs` | `2000` | Min gap between bank deposits/withdrawals per player. |
| `tablet.upgradeCooldownMs` | `2000` | Min gap between upgrade purchases per player. |
| `tablet.maxDisplayName` | `64` | Tablet profile display-name length cap. |
| `tablet.maxProfileImage` | `512` | Tablet profile-image URL length cap. |
| `consumables.maxStatAmount` | `100` | Hunger/thirst restored per use is clamped to this. |
| `logs.retentionDays` | `90` | Activity logs older than this are pruned nightly (`logs.pruneCron`). |

### Languages (`locales/`)

All notify / progress / target / command strings go through ox_lib locale. 11 languages ship: `en, de, fr, es, pt, it, nl, ru, tr, zh, ar`.

* Server language: `set ox:locale <code>` in `server.cfg`.
* Player language: each player picks it in the ox_lib settings dialog (stored per-player), unless you `set ox:userLocales 0` to force the server convar for everyone.
* Missing keys fall back to English automatically.

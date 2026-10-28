---
description: Configuring aura_pawnshop - every option in configs/shared/main.lua and configs/server/main.lua.
---

# Configuration

There are two config files. Both are fully commented, so you can also read the explanation next to each line.

| File | What is in it |
| --- | --- |
| `configs/shared/main.lua` | The job, blip, locations, storages, warehouse, walk-in customers, delivery van and drop-offs |
| `configs/server/main.lua` | Money: the shop account, permissions, upgrades, the buy list, prices, marketplace, deliveries, fence offers. Players can't read this file |

After any change, restart the resource (`ensure aura_pawnshop` or a server restart).

{% hint style="warning" %}
Some settings are only **starting values**. The first time the resource starts it saves them in the database, and from then on the owner changes them in game: permissions, the buy list, shop mode, policies (commission, delivery fee, listing limit) and upgrade levels. Editing the config later does not overwrite what is saved. See [Resetting saved settings](#resetting-saved-settings).
{% endhint %}

## Shared config (`configs/shared/main.lua`)

### Job

At the very top of the file:

```lua
local JOB_NAME <const> = 'pawn'
local MANAGER_GRADE <const> = 3
local MAX_GRADE <const> = 4
```

| Option | Default | Description |
| --- | --- | --- |
| `JOB_NAME` | `'pawn'` | Job name exactly as it exists in your framework. Also used to name the stashes (`pawn_employee`, `pawn_manager`, ...). |
| `MANAGER_GRADE` | `3` | Lowest grade that counts as management: boss menu and manager storage. |
| `MAX_GRADE` | `4` | Highest grade of the job. Grades above it are treated as this grade. |

### General

| Option | Default | Description |
| --- | --- | --- |
| `Debug` | `false` | Prints extra `[DEBUG]` lines in the F8 and server console. Turn it on when something doesn't work, off on a live server. |
| `DevMode` | `false` | Enables the admin test command `pawn_warehouse_set`. Leave it `false` on a live server. |
| `Sounds` | GTA sounds | Sound played for select, back, purchase, success, error and van arrival. Set one to `false` to mute it. |
| `InventoryImages.baseUrl` | `'nui://ox_inventory/web/images/'` | Backup image folder, only used when the resource can't find an item's image in your inventory or in the images that ship with it. |

### Map blip (`Blip`)

| Option | Default | Description |
| --- | --- | --- |
| `Blip.enabled` | `true` | `false` hides the shop from the map. |
| `Blip.sprite` | `431` | Blip icon ([list](https://docs.fivem.net/docs/game-references/blips/)). |
| `Blip.color` | `46` | Blip colour. |
| `Blip.scale` | `0.75` | Icon size. |
| `Blip.label` | `'Pawn Shop'` | Name on the map. |
| `Blip.coords` | MLO position | Where the blip is. |

### Shop storage (`Storage`)

Three stashes inside the shop:

| Stash | Default size | Who can open it |
| --- | --- | --- |
| `Storage.tray` | 12 slots, 25 kg | Everyone (staff and customers): the display tray on the counter |
| `Storage.employee` | 25 slots, 50 kg | Every employee. Items bought from walk-in sellers go here |
| `Storage.manager` | 35 slots, 80 kg | `MANAGER_GRADE` and up. Items sold at the counter go here |

Each has `id` (stash name), `slots`, `weight` (grams), `coords`, `size` and `heading` (the interaction box). `openCooldownMs` / `denyCooldownMs` (`750`) stop players spamming the stashes.

{% hint style="info" %}
Changing a stash `id` gives you a new, empty stash. The old stash keeps its items in your inventory's database.
{% endhint %}

### Warehouse (`Warehouse`)

A separate interior with extra storage, locked until the owner buys the **Warehouse Expansion** upgrade. Staff interact at the entrance near the shop and are teleported inside.

| Option | Default | Description |
| --- | --- | --- |
| `entrance` | behind the shop | Where staff go in. |
| `warehouseStash` | `pawn_warehouse`, 80 slots, 300 kg | Every storage unit is its own stash: `pawn_warehouse`, `pawn_warehouse_2`, ... |
| `crates` | GTA crate props | Props shown for the employee, manager and warehouse stashes inside. |
| `stashes` | | Label, lowest grade (`minGrade`) and distances for each kind of stash. |
| `levels` | Small warehouse | The interior: map files (`ipls`), the arrival point (`interior`), the exit and the crate positions. |
| `units` | 5 lines | Storage units added by each upgrade level, line 1 for level 1 and so on. |

Positions inside the warehouse are **offsets** from the level's `interior` point. Stand on the spot, take your coords and subtract `interior` to get the offset.

### Interaction points (`Interactions`)

| Option | Who uses it |
| --- | --- |
| `bossDesk` | Management terminal (boss menu), managers only |
| `tablet` | Marketplace tablet, every employee |
| `outfits` | Staff wardrobe, every employee |
| `counter` | Players must be near here to sell to the shop |

`Counter.sellEnabled = false` turns off selling at the counter completely.

### Pawnbroker NPC (`NPC`)

The NPC behind the counter who buys from players while the shop is in `npc` mode. `model`, `coords`, `heading` and `scenario` (idle animation).

### Walk-in customers (`WalkUps`)

NPC customers who walk in for staff to deal with. Staff open the door with `/pawnsell`.

| Option | Default | Description |
| --- | --- | --- |
| `enabled` | `true` | `false` = no walk-ins. |
| `command` | `'pawnsell'` | Command staff use to open and close the door. |
| `spawn`, `counter`, `route` | MLO path | Where customers appear, the path they walk and where they wait. |
| `interactionDistance` | `2.5` | How close staff must be to talk to a customer. |
| `billboardDistance` | `18.0` | How far the info card above a customer shows (`0` = off). |
| `patienceMinutes` | `6` | How long a customer waits before leaving. |
| `holdSeconds` / `holdMax` | `90` / `3` | Extra time gained when staff ask them to hold on, and how many times. |
| `cooldownMinSeconds` / `cooldownMaxSeconds` | `30` / `90` | Wait before the next customer while the door is open. |
| `sellChancePct` | `70` | % of customers who come to sell. The rest come to buy. |
| `sellCountMin` / `sellCountMax` | `1` / `3` | Items a seller brings. |
| `buyCountMin` / `buyCountMax` | `1` / `2` | Items a buyer wants. |
| `offerMaxPct` | `1.50` | Staff can't offer a seller more than 150% of the item's price. |
| `offerMinPct` | `0.50` | Staff can't sell to a buyer for less than 50% of the item's price. |
| `models`, `maleNames`, `femaleNames` | | Customer looks and names. |
| `topics` | 3 questions | Questions staff can ask a seller before an offer. |
| `sellPool` / `buyPool` | 66 items | Items customers bring in / ask for. Every item needs a price in `Marketplace.basePrices`. |
| `waitingTexts` | per personality | What customers say while they wait. Keep `%d` and `%s` in the lines that have them. |

The other options (`valueDrift*`, `ask*`, `buyBudget*`, `*ChancePct`) tune the haggling. The defaults work well.

### Delivery van and drop-offs (`Delivery`)

| Option | Default | Description |
| --- | --- | --- |
| `truckModel` | the included van | Vehicle used for deliveries. See [Delivery Van](./delivery-van.md). |
| `truckLook` | livery `0`, dark paint | Livery and colours applied when the van spawns. Remove the block to keep the model's own look. |
| `platePrefix` | `'PAWN'` | Plate text, 4 random digits are added. |
| `fuelLevel` | `65.0` | Fuel the van starts with. |
| `returnRadius` | `14.0` | How close to the pick-up point the van must be parked to finish the run. |
| `carry` | box prop | The box the driver carries to the buyer. |
| `pickup` | behind the shop | Where the van spawns and must be returned. |
| `dropoffs` | 5 locations | Normal drop-off points. Add as many as you like. |

## Server config (`configs/server/main.lua`)

### Shop bank account (`Society`, `StandaloneBank`)

| Option | Default | Description |
| --- | --- | --- |
| `Society.account` | `'pawn'` | Society/business account in your banking resource, usually the job name. On ESX it becomes `society_pawn`. |
| `Society.allowCommissionEdit` | `true` | Owners can change the driver commission and delivery fee in game. |
| `Society.allowListingCapEdit` | `true` | Owners can change how many listings each employee may have. |
| `Society.maxCommissionPct` | `50` | Highest commission an owner can set. |
| `Society.maxDeliveryFee` | `5000` | Highest delivery fee an owner can set. |
| `Society.requireDuty` | `false` | `true` = staff must be on duty to use the shop. |
| `StandaloneBank.enabled` | `true` | Backup account in the resource's own database table, used when your banking resource can't hold the money. |

{% hint style="warning" %}
If your banking resource is supported and working, set `StandaloneBank.enabled = false`. With both on, money can end up split between the two if your banking resource fails to start once.
{% endhint %}

### Staff permissions (`Permissions`)

Which grades can do what. `'all'` = every grade, or a list like `{ 3, 4 }`. The boss always has every permission. These are starting values: the owner changes them in the boss menu (**Ranks**).

| Permission | Default | Allows |
| --- | --- | --- |
| `view_market` | all | Open the marketplace tablet, open the door to walk-ins |
| `list_items` | all | List items on the marketplace |
| `do_deliveries` | all | Take and drive delivery orders |
| `view_orders` | all | See the order history |
| `view_transactions` | 3, 4 | See the transactions |
| `view_treasury` | 3, 4 | See the shop's balance |
| `deposit_treasury` | 3, 4 | Put their own cash into the shop account |
| `withdraw_treasury` | 4 | Take cash out of the shop account |
| `manage_employees` | 3, 4 | Promote, demote and fire staff below their own grade |
| `hire_employees` | 3, 4 | Hire new staff |
| `edit_buy_list` | 3, 4 | Change what the counter buys and for how much |
| `edit_permissions` | 4 | Change this table, for grades below their own |
| `edit_policies` | 4 | Change commission, delivery fee and listing limit |
| `buy_upgrades` | 4 | Buy upgrades with the shop's money |

### Upgrades (`Upgrades`)

Six tracks, 5 levels each, bought in order from the boss menu with the shop's money.

| Track | Name | Effect per level | Level 1 to 5 cost |
| --- | --- | --- | --- |
| `fence` | Fence Connections | Fence offers appear 20 / 40 / 65 / 90 / 125% more often | 15k, 35k, 75k, 140k, 250k |
| `bulk` | Logistics Contracts | One delivery carries up to 150 / 200 / 300 / 450 / 650 items | 10k, 25k, 60k, 120k, 220k |
| `locations` | Premium Routes | Unlocks 1 / 2 / 3 / 4 / 5 premium drop-offs | 20k, 45k, 90k, 160k, 300k |
| `variety` | Order Bundling | Orders contain up to 2 / 3 / 4 / 5 / 6 different items | 12k, 30k, 70k, 130k, 240k |
| `storage` | Warehouse Expansion | Unlocks the warehouse, each level adds the units in `Warehouse.units` | 18k, 40k, 85k, 150k, 280k |
| `speed` | Faster Buyers | Listings sell 15 / 25 / 35 / 45 / 55% faster | 16k, 35k, 70k, 120k, 220k |

### Shop mode (`Mode`)

| Option | Default | Description |
| --- | --- | --- |
| `Mode.default` | `'npc'` | `'npc'` = the pawnbroker NPC buys at the counter. `'player'` = no NPC, your staff run the counter. |
| `Mode.playerToggle` | `true` | Managers can switch the mode in the boss menu (**Settings**). |

### Selling to the shop (`Sell`)

| Option | Default | Description |
| --- | --- | --- |
| `Sell.blacklist` | `money`, `black_money`, `radio` | Items the counter never buys. |
| `Sell.buyList.enabledByDefault` | `true` | Items with a price that are not in `buyList.items`: `true` = buy them. |
| `Sell.buyList.items` | 66 items | Starting buy list: `item = { buy = true, category = 'misc' }`. Categories: `collectibles`, `antiques`, `tech`, `plushies`, `misc`. |
| `Sell.multiplier` | `0.45` | Leave as is. Only used for items without a price, which the shop doesn't buy. |

The counter pays an item's price from `Marketplace.basePrices`, unless the owner sets a lower price in the **Buy List**. An item without a price in `basePrices` is never bought, even if it is in the buy list.

### Marketplace (`Marketplace`)

| Option | Default | Description |
| --- | --- | --- |
| `playerSetPrices` | `true` | Staff choose their own price. `false` = items always sell at `basePrices` with `bulkTiers` discounts. |
| `minListingPrice` / `maxListingPrice` | `1` / `100000` | Price limits per item. |
| `maxPriceMultiplier` | `5` | Staff can't ask more than 5x the item's price. `false` = no limit. |
| `maxActiveListingsPerEmployee` | `10` | Listings each employee can have at once. |
| `basePrices` | 66 items | **The price list.** Used for the counter, NPC buyers, walk-ins and fence offers. Only items listed here can be sold to the shop or listed. |
| `defaultBasePrice` | `100` | Backup price, rarely used. |
| `bulkTiers` | 0 to 25% | Bulk discounts, only when `playerSetPrices = false`. |
| `buyerDelayMinMinutes` / `buyerDelayMaxMinutes` | `8` / `35` | A buyer shows up after a random time in this range. |
| `demand` | | Overpriced listings take longer (up to +60 min), cheap ones sell sooner (up to -20 min), never faster than 2 min. |
| `commissionPct` | `12` | Driver gets 12% of the sale value. |
| `deliveryFlatFee` | `300` | Plus this amount per delivery. |
| `buyerNames` | 40 names | Names on NPC orders. |

### Deliveries (`Delivery`)

| Option | Default | Description |
| --- | --- | --- |
| `timerEnabled` | `true` | Drivers have a time limit. |
| `timeoutMinutes` | `10` | When it runs out, the order goes back on the board. |
| `defaultMaxUnitsPerDelivery` | `100` | Items one delivery can carry before upgrades. |
| `premiumDropoffs` | 5 locations | Better-paying drop-offs (+25% to +100%), unlocked by **Premium Routes**. |
| `premiumChancePct` | `35` | Once unlocked, % of orders that go to a premium drop-off. |

### Fence offers (`FenceEvents`)

| Option | Default | Description |
| --- | --- | --- |
| `enabled` | `true` | `false` = no fence offers. |
| `checkIntervalMinutes` | `10` | How often the game rolls for an offer. |
| `spawnChancePct` | `25` | Chance of an offer on each roll. |
| `minActiveDelayMinutes` | `20` | At least this long between two offers. |
| `offerExpiryMinutes` | `8` | Time staff have to accept. |
| `valueMultiplierMin` / `valueMultiplierMax` | `1.6` / `2.8` | An offer pays 1.6x to 2.8x the item's price. |
| `maxQuantity` | `3` | Most items a fence asks for. |
| `minStockRequired` | `1` | The shop needs this many items listed before a fence shows up. |
| `dropoffs` | `'normal'` | `'normal'`, `'premium'` or `'custom'` (uses `customDropoffs`). |

### Languages (`locales/`)

9 languages ship: `en`, `de`, `fr`, `es`, `pt`, `ru`, `tr`, `zh`, `ar`. The resource uses the ox_lib language. Set it in `server.cfg`:

```cfg
setr ox:locale en
```

To add a language, copy `locales/en.json` to `locales/<code>.json` and translate the values. Keep the keys and the `%d` / `%s` placeholders.

### Resetting saved settings

The resource saves some settings in the `aura_pawnshop_settings` table. To go back to the config values, delete the row and restart:

| Row (`k`) | What it holds |
| --- | --- |
| `permissions` | Rank permissions |
| `buyList` | Buy list on/off, prices, caps |
| `policies` | Commission, delivery fee, listing limit |
| `mode` | `npc` or `player` |
| `upgrades` | Purchased upgrade levels |

```sql
DELETE FROM aura_pawnshop_settings WHERE k = 'buyList';
```

{% hint style="danger" %}
Deleting `upgrades` removes everything the shop paid for. Refund the shop account yourself if you do this on a live server.
{% endhint %}

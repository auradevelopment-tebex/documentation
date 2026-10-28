---
description: The aura_pawnshop boss menu - every tab of the management terminal.
---

# Boss Menu

Managers (grade `3` and up) open the boss menu at the **Management terminal** in the shop. Each tab is controlled by a [permission](../configuration.md#staff-permissions-permissions); a tab you can't use shows **Restricted**.

### Dashboard

Overview of the shop: orders, sales and staff activity.

### Employees

Everyone with the `pawn` job, online or offline.

* **Hire:** pick a nearby player (within 25 m of the terminal). They must accept the offer. New hires start at the lowest grade.
* **Promote / demote / fire:** only for staff below your own grade. Offline staff can be fired too.

Permissions: `hire_employees`, `manage_employees`.

### Ranks

What each grade may do. Tick or untick a permission per grade. You can only change grades below your own. Changes are saved and replace the config defaults.

Permission: `edit_permissions` (owner only by default).

### Buy List

What the counter buys from players:

* Turn an item on or off.
* Set a **lower** buy price than the item's normal price.
* Set a **cap**: the most of that item the shop buys.

Permission: `edit_buy_list`.

### Upgrades

Six upgrade tracks with 5 levels each, paid from the shop account. Effects apply at once, no restart.

| Upgrade | What it does |
| --- | --- |
| Fence Connections | Fence offers appear more often |
| Logistics Contracts | One delivery can carry more items |
| Premium Routes | Unlocks premium drop-offs that pay more |
| Order Bundling | Orders contain more different items |
| Warehouse Expansion | Unlocks the [warehouse](./warehouse.md) and adds storage units |
| Faster Buyers | Listings sell sooner |

Levels and costs are in [Configuration](../configuration.md#upgrades-upgrades). Permission: `buy_upgrades`.

### Orders

Every marketplace and fence order: buyer, items, driver, status and the money breakdown. Permission: `view_orders`.

### Transactions

The shop's ledger: every buy-in, sale, delivery payout, deposit, withdrawal and upgrade. Permission: `view_transactions`.

### Treasury

The shop account balance and cash flow chart.

* **Deposit** your own cash into the shop. Permission: `deposit_treasury`.
* **Withdraw** shop money as cash. Permission: `withdraw_treasury` (owner only by default).

### Settings

* **Shop mode:** NPC (the pawnbroker buys at the counter) or player (staff run the counter). Needs `Mode.playerToggle = true`.
* **Policies:** driver commission, delivery fee and the listing limit per employee. Needs `edit_policies` and `Society.allowCommissionEdit` / `allowListingCapEdit`. The highest values are capped by `Society.maxCommissionPct` (50%) and `Society.maxDeliveryFee` ($5,000).

### Demo data

Admins can preview the boss menu with fake data using `/pawndemo` ([Commands](../commands.md)). Nothing is written to the database.

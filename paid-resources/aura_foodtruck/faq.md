---
description: Frequently asked questions for aura_foodtruck.
---

# FAQ

### Tablet says "No food truck business job found"?

Your current job doesn't match any truck's `job`. Job names are normalized (lowercased, spaces/dashes removed) and `tablet.jobAliases` maps your server's names — add yours there.

### I'm grade 5 but `ownerGrades` is `{ 3, 4 }` and I can't open the tablet?

Working as intended — grades match **exactly**. Add `5` to `ownerGrades` (or empty the table for everyone in the job).

### Where does the sale money go?

`sales.account`: `'society'` pays the owning job's society/business bank account through your banking resource, `'cash'`/`'bank'` pays the employee directly. If your banking names society accounts `society_<job>`, set `sales.societyPrefix = true`.

### Tray vs storage — what's the difference?

The tray is public (customers grab their food), storage is employees-only. Both are per-truck stashes (model + plate), so stock never leaks between trucks.

### Do I need aura_bridge?

No. Framework, inventory, target, notify, progress and banking integrations live in the resource's own `bridge/` folder and resolve the running providers automatically.

### Which providers are supported?

Frameworks: `qbx_core`, `qb-core`, `es_extended`. Inventories: `ox_inventory`, `qb-inventory`, `ps-inventory`, `qs-inventory`, `codem-inventory`, `origen_inventory`, `tgiann-inventory`, `jpr-inventory`, `core_inventory`, `one_inventory`. Targets: `ox_target`, `qb-target`. Banking: `qb-banking`, `Renewed-Banking`, `okokBanking`, `fd_banking`, `kartik-banking`, `wasabi_banking`, `tgg-banking`, `tgiann-bank`, `DHS-BankingSim`.

### What language is the UI in?

All notify / progress / target / command strings go through ox_lib locale — 11 languages ship (`en, de, fr, es, pt, it, nl, ru, tr, zh, ar`). Server language: `set ox:locale <code>`. Players pick their own in the ox_lib settings dialog unless you `set ox:userLocales 0`. Missing keys fall back to English.

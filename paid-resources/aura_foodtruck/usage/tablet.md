---
description: Business tablet in aura_foodtruck - dashboard, bank, upgrades and logs.
---

# Tablet

Open with the `foodtruck_tablet` item or `/foodtrucktablet` (`tablet.openMode` controls which). Only the owning job can open it, and only `tablet.ownerGrades` — exact grade match — get in.

### Dashboard

Live business profile, order counts, crafted items, revenue and 7-day trends, all computed from the activity logs.

### Bank

Per-job business bank with the last 24 transactions. Deposit from / withdraw to your cash, every movement logged. Withdrawals are atomic — concurrent spends can't overdraw.

### Upgrades

Six upgrades with escalating costs (`baseCost * (currentLevel + 1)`). Pay from the business bank first, your own cash as fallback. Effects apply immediately: faster arrivals, bigger orders, more customers, better margins, faster cooking, more patient NPCs.

### Logs & profile

The last `tablet.maxLogs` events (toggle per-type in `logging.types`) and an editable business profile (name + image).

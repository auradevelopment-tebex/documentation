---
description: Staff and admin commands in aura_pawnshop.
---

# Commands

| Command | Who | What it does |
| --- | --- | --- |
| `/pawnsell` | Employees with `view_market`, in the shop | Opens or closes the door to [walk-in customers](./usage/walk-ins.md) |
| `/pawndemo` | Admins (`group.admin`) | Toggles fake demo data in your own boss menu. Nothing is saved |
| `/pawn_warehouse_set <level>` | Admins (`group.admin`), only with `DevMode = true` | Sets the warehouse level (`0` to `5`) without paying, for testing |

### /pawnsell

```
/pawnsell
```

Run it inside or near the shop. The command name can be changed with `WalkUps.command` in `configs/shared/main.lua`.

### /pawndemo

```
/pawndemo
```

Shows fake staff, charts and ledger in **your** boss menu only, for screenshots or testing the layout. Run it again to go back to live data.

### /pawn_warehouse_set

```
/pawn_warehouse_set 2
```

Only exists when `DevMode = true` in `configs/shared/main.lua`. It changes the shop's real upgrade level and is logged in the transactions.

{% hint style="danger" %}
Set `DevMode = false` on a live server, so the command does not exist there.
{% endhint %}

{% hint style="info" %}
Admin commands use the ACE group `group.admin`. Give your staff access in `server.cfg`, for example `add_principal identifier.fivem:123456 group.admin`.
{% endhint %}

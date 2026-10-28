---
description: How to properly install aura_pawnshop.
---

# Installation

How to properly install aura_pawnshop. Takes about 15 minutes, most of it adding the job and items.

{% stepper %}
{% step %}

### Check what you need first

Install and start these **before** you add aura_pawnshop:

* [**rStudio Pawn Shop MLO**](https://rstudiomaps.tebex.io/package/6793070)
* [**ox_lib**](https://github.com/overextended/ox_lib/releases/latest)
* [**oxmysql**](https://github.com/overextended/oxmysql/releases/latest)
* **A framework:** `qbx_core`, `qb-core` or `es_extended`
* **An inventory with stashes:** `ox_inventory` (recommended), `qb-inventory` 2.x, `qs-inventory`, `origen_inventory`, `tgiann-inventory`, `jpr-inventory` or `core_inventory` ([full list](./compatibility.md#inventory))
* **A target:** `ox_target` or `qb-target`
* [**aura_dialog**](../../free-releases/aura_dialog/installation.md) (free)

Optional:

* **A banking resource** from the [supported list](./compatibility.md#banking-shop-money). Without one, the resource keeps the shop's money in its own database table.
* **MugShotBase64** for photos of regular customers on the tablet.

{% hint style="info" %}
Using the ESX built-in inventory? It has no stashes, so shop storage, counter sales and the warehouse do not work. Use `ox_inventory` with ESX.
{% endhint %}
{% endstep %}

{% step %}

### Get resource

Download `aura_pawnshop` from your [CFX portal](https://portal.cfx.re/assets/granted-assets), then unzip it into your server files, preferably:

```
resources/[aura]/aura_pawnshop
```

{% hint style="danger" %}
Keep the folder name `aura_pawnshop`. The resource is protected by CFX escrow, and escrowed resources can't be renamed: a renamed folder does not start.
{% endhint %}

The download contains:

* `configs/` the two config files you edit
* `bridge/` the framework, inventory and other integrations
* `locales/` the translations
* the custom-made delivery van, loaded automatically
* `_images/` an image for every shop item
* `README.md` the full item and job lists, the same as [Framework Setup](./framework-setup.md)
{% endstep %}

{% step %}

### Add the job and items

The resource needs a `pawn` job with grades `0` to `4`, and the 66 items the shop buys and sells must exist in your inventory.

Follow [Framework Setup](./framework-setup.md). It has ready-to-paste blocks for QBCore/QBOX, ox_inventory and ESX.

{% hint style="info" %}
About 3 seconds after the resource starts, it checks every item in its config against your inventory's item list. An item your inventory doesn't know is **skipped**: it is removed from the counter's buy list, the marketplace price list and the walk-in item lists until the next restart. The rest of the resource keeps working.

Each skipped item prints a red line in the server console, for example `[pawnshop] invalid item 'rolex' in Marketplace.basePrices — not in the items database, skipped`.
{% endhint %}
{% endstep %}

{% step %}

### Startup order

In `server.cfg` (or txAdmin CFG Editor), start aura_pawnshop **after** everything it depends on:

```cfg
ensure oxmysql
ensure ox_lib
# your framework, inventory, target and banking resources
ensure qbx_core
ensure ox_inventory
ensure ox_target
ensure aura_dialog
ensure aura_pawnshop
```

Replace `qbx_core` / `ox_inventory` / `ox_target` with what your server uses. The MLO can start anywhere before `aura_pawnshop`.

{% hint style="info" %}
When `aura_pawnshop` starts, the resource looks for your framework, inventory, target and banking resources. One that starts **after** it may not be detected, and the features that depend on it stay dead: no target options, no stashes, or money not reaching the society account. Fix the order and restart the server.
{% endhint %}
{% endstep %}

{% step %}

### Check the config

Open `configs/shared/main.lua`. The two lines at the top are already set for a live server, leave them like this:

```lua
Debug = false,
DevMode = false,
```

If your job is not called `pawn`, or has more or fewer grades, change `JOB_NAME`, `MANAGER_GRADE` and `MAX_GRADE` at the very top of the same file.

Everything else works with the defaults. See [Configuration](./configuration.md) when you want to change prices, locations or upgrades.
{% endstep %}

{% step %}

### Verify it works

Restart the server and look at the server console. There should be no red `[pawnshop]` lines. A missing item looks like this:

```
[pawnshop] invalid item 'rolex' in Marketplace.basePrices — not in the items database, skipped
```

If you see these, the item is missing from your inventory. Go back to [Framework Setup](./framework-setup.md).

Then in game:

1. Give yourself the job at the top grade: `/setjob <your id> pawn 4`.
2. Go to the pawn shop (the **Pawn Shop** blip on the map).
3. Inside, you should see target options for the **Management terminal**, **Marketplace tablet**, **Staff wardrobe**, **Employee storage**, **Manager storage** and the **display tray**.
4. Without the job (or on a second player), the pawnbroker NPC behind the counter offers to buy your items.

Continue to [Usage](./usage/README.md) to set up the shop for your players.
{% endstep %}
{% endstepper %}

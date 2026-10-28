---
description: How to properly install aura_pawnshop.
---

# Installation

How to properly install aura_pawnshop. Takes about 15 minutes, most of it adding the job and items.

{% stepper %}
{% step %}

### Check what you need first

Install and start these **before** you add aura_pawnshop. The resource does not work without them.

| Requirement | Why it is needed |
| --- | --- |
| **rStudio Pawn Shop MLO** | The shop interior. All counters, stashes, the boss desk and the NPC are placed for this MLO. Without it players stand in an empty building. |
| [**ox_lib**](https://github.com/overextended/ox_lib/releases/latest) | Menus, callbacks, progress bars, languages. |
| [**oxmysql**](https://github.com/overextended/oxmysql/releases/latest) | Database. The shop creates its own tables on first start. |
| **Framework:** `qbx_core`, `qb-core` or `es_extended` | Jobs, money and player data. |
| **Inventory with stashes** | `ox_inventory` (recommended), `qb-inventory` 2.x, `qs-inventory`, `origen_inventory`, `tgiann-inventory`, `jpr-inventory`, `core_inventory`. See [Compatibility](./compatibility.md) for the limits of `ps-inventory` and `codem-inventory`. |
| **Target:** `ox_target` or `qb-target` | Every interaction point in the shop. |
| **Banking resource** | Holds the shop's money (society account). Optional: if you have none, the shop keeps its money in its own table. |
| [**aura_dialog**](../../free-releases/aura_dialog/installation.md) (free) | Conversations with walk-in customers. Everything else works without it, but staff cannot talk to walk-ins. |

Optional: **MugShotBase64** shows a photo of regular customers on the tablet.

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
Keep the folder name `aura_pawnshop`. The interface, the item images and the vehicle files are loaded by that name.
{% endhint %}

The download contains:

* `configs/` the two config files you edit
* `bridge/` framework, inventory and other integrations, editable
* `locales/` the translations
* `stream/` and `data/aurapawnvan/` the delivery van, loaded automatically
* `_images/` an image for every shop item
* `README.md` the full item and job lists, the same as [Framework Setup](./framework-setup.md)
{% endstep %}

{% step %}

### Add the job and items

The shop needs a `pawn` job with grades `0` to `4`, and the 66 items it buys and sells must exist in your inventory.

Follow [Framework Setup](./framework-setup.md). It has ready-to-paste blocks for QBCore/QBOX, ox_inventory and ESX.

{% hint style="info" %}
Items that are missing from your inventory are skipped when the shop starts. Nothing breaks, but those items cannot be sold to the shop or listed.
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

Replace `qbx_core` / `ox_inventory` / `ox_target` with what your server uses. The MLO can start anywhere before the shop.

{% hint style="info" %}
The shop finds your framework, inventory, target and banking when it starts. If one of them starts later, the shop does not see it and interactions stay dead.
{% endhint %}
{% endstep %}

{% step %}

### Check the config

Open `configs/shared/main.lua` and set these two lines at the top for a live server:

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

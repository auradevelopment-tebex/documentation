---
description: How to properly install aura_foodtruck.
---

# Installation

How to properly install aura_foodtruck. Takes about 10 minutes, most of it framework setup.

{% stepper %}
{% step %}

### Get resource

Download `aura_foodtruck` from your [CFX portal](https://portal.cfx.re/assets/granted-assets), then unzip it into your server files, preferably:

```
resources/[standalone]/aura_foodtruck
```
{% endstep %}

{% step %}

### Install dependencies

Make sure these are installed and start **before** `aura_foodtruck`:

* [**ox_lib**](https://github.com/overextended/ox_lib/releases/latest) — required (v3.30.6 or higher)
* [**oxmysql**](https://github.com/overextended/oxmysql/releases/latest) — required (profiles, upgrades, logs, bank)

No external bridge resource is required. Framework, inventory, target, notify, progress and banking integrations live in the resource's own `bridge/` folder and resolve the running providers automatically.
{% endstep %}

{% step %}

### Startup order

In `server.cfg` (or txAdmin CFG Editor):

```cfg
ensure ox_lib
ensure aura_foodtruck
```

{% hint style="info" %}
Without the proper startup order the bridge modules fail to resolve and every interaction stays dead.
{% endhint %}
{% endstep %}

{% step %}

### Framework setup

Add the jobs, items and inventory images for your setup — [Framework Setup](./framework-setup.md) has the ready-to-paste blocks for QBCore, ESX and ox_inventory.
{% endstep %}

{% step %}

### Verify it works

Give yourself one of the truck jobs, spawn the matching truck model (e.g. `sbbm`), and walk up to it. You should see target options for Tray, Cook Food, Storage and Register.

Then continue to [Configuration](./configuration.md).
{% endstep %}
{% endstepper %}

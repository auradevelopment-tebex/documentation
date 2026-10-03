---
description: How to properly install aura_dialog.
---

# Installation

How to properly install aura_dialog. Takes about 2 minutes, no framework steps.

{% stepper %}
{% step %}

### Get resource

Get `aura_dialog` from our [store](https://store.auradevelopment.xyz/products/7646274), then download it from your [CFX portal](https://portal.cfx.re/assets/granted-assets).
{% endstep %}

{% step %}

### Unzip resource

Unzip it into your server files, preferably:

```
resources/[standalone]/aura_dialog
```
{% endstep %}

{% step %}

### Install dependencies

Make sure these are installed and start **before** `aura_dialog`:

* [**ox_lib**](https://github.com/overextended/ox_lib/releases/latest) — required
* **MugShotBase64** — required for the NPC portrait (`exports:GetMugShotBase64`). Dialog still opens if it fails, just without a mugshot.
{% endstep %}

{% step %}

### Startup order

In `server.cfg` (or txAdmin CFG Editor):

```cfg
ensure ox_lib
ensure MugShotBase64
ensure aura_dialog
```

{% hint style="info" %}
Without the proper startup order the example NPC will error on start.
{% endhint %}
{% endstep %}

{% step %}

### Verify it works

With default `config.lua` the Trevor example spawns near Davis impound (`346.31, -1696.43, 47.3`).

Walk within `3.0m`, you will see `[E] Talk to Trevor` — press **E** to open `trevor_main`.

Then continue to [Configuration](./configuration.md).
{% endstep %}
{% endstepper %}

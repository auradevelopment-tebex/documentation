---
description: How to properly install aura_dialog.
---

# Installation

How to properly install aura_dialog. Takes about 2 minutes, no framework steps.

{% stepper %}
{% step %}

### Download resource

Download `aura_dialog` from your [store](https://store.auradevelopment.xyz/) release.
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

* [**ox_lib**](https://github.com/overextended/ox_lib/releases/latest) — required (`lib.points`, init)
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
Without the proper startup order the Trevor example point (`lib.points.new`) will error on start.
{% endhint %}
{% endstep %}

{% step %}

### Verify it works

With default `config.lua` the Trevor example spawns near Davis impound (`346.31, -1696.43, 47.3`).

Walk within `3.0m`, you will see `[E] Talk to Trevor` — press **E** to open `trevor_main`.

Then continue to [Configuration](./configuration.md).
{% endstep %}
{% endstepper %}

The release ships pre-built — `web/build/index.html` is already set as `ui_page`. No extra build step needed.

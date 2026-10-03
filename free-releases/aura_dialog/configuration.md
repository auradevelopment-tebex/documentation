---
description: Configuring aura_dialog - UI styling, example NPC and version check.
---

# Configuration

All configuration lives in `config.lua` at the resource root. Three blocks only.

```lua
Config.Ui = {
    ThreeDEffect = true,  -- 3D panel tilt on/off
    Perspective = 800,    -- lower = more pronounced
    TiltX = 4.0,          -- vertical tilt in degrees
    TiltY = -14.0,        -- horizontal tilt in degrees, negative tilts left
    Shadow = true,        -- panel drop shadow
}

Config.TrevorExample = true  -- bundled example NPC
Config.VersionCheck = true   -- check versions.json on start, console notice if update
```

### UI styling

| Setting | Type | Default | What it does |
| --- | --- | --- | --- |
| `ThreeDEffect` | boolean | `true` | `false` = flat panel, no tilt |
| `Perspective` | number | `800` | Perspective strength, lower = more depth |
| `TiltX` | number | `4.0` | Vertical tilt |
| `TiltY` | number | `-14.0` | Horizontal tilt, negative = left |
| `Shadow` | boolean | `true` | Drop shadow on/off |

Changes apply on the next `ShowDialog` — the UI receives `configure(Config.Ui)` every open. See differences in [Showcase](./showcase.md).

### Example NPC

```lua
Config.TrevorExample = true
```

* `true` — spawns an example NPC with a few example dialogs so you can try it out immediately.
* `false` — disables spawn + interaction entirely. Use this in production once you use your own dialogs.

{% hint style="warning" %}
Disable `TrevorExample` on live servers once you use your own dialogs.
{% endhint %}

### Version check

```lua
Config.VersionCheck = true
```

Checks for updates once on resource start. Set to `false` to silence it.

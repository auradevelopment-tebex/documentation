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

Config.TrevorExample = true  -- demo Trevor NPC + 10 dialogs
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

* `true` — spawns `player_two` (Trevor) at `vector4(346.31, -1696.43, 47.3, 329.85)`, invincible, `WORLD_HUMAN_STAND_IMPATIENT`, `lib.points.new` 10.0m range, `[E]` prompt at 3.0m, registers 10 dialogs (`trevor_main`, `trevor_backstory`, `trevor_early_life`, `trevor_blaine`, `trevor_michael`, `trevor_michael_found`, `trevor_business`, `trevor_oneils`, `trevor_crew`, `trevor_goodbye`).
* `false` — disables spawn + interaction entirely. Use this in production once you use your own dialogs.

{% hint style="warning" %}
Disable `TrevorExample` on live servers. It is only a showcase of [Branching](./usage/branching.md).
{% endhint %}

### Version check

```lua
Config.VersionCheck = true
```

Checks for updates once on resource start. Set to `false` to silence it.

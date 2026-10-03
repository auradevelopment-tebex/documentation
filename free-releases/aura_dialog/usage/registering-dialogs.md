---
description: Registering dialogs with aura_dialog.
---

# Registering Dialogs

Register after the NPC entity exists — for example right after `CreatePed`.

```lua
exports['aura_dialog']:RegisterDialog({
    id = 'npc_main',          -- unique id, used to open
    title = 'John Doe',       -- header name
    subtitle = 'Paleto Bay',  -- subtitle under name
    text = 'Hello there!',    -- typewriter body text
    speed = 35,               -- optional, ms per character
    entity = entity,           -- ped the camera focuses on
    options = {
        { label = 'Tell me about yourself', menu = 'npc_about' },
        { label = 'Buy something', onSelect = function() print('shop') end },
        { label = 'Goodbye', event = 'my:npc:goodbye', args = { 1 } },
    },
})
```

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | string | yes | Unique id, passed to `ShowDialog` |
| `title` | string | yes | Character name in header |
| `subtitle` | string | no | Small text under title |
| `text` | string | yes | Dialogue body, typewriter effect |
| `speed` | number | no | Typing speed, ms per character |
| `entity` | entity | yes | Ped for camera + mugshot. If invalid, no cam framing |
| `options` | table | yes | See [Branching](./branching.md) |

{% hint style="info" %}
Calling `RegisterDialog` twice with the same `id` overwrites it. Use this with `RefreshDialog` to update an open dialog in place.
{% endhint %}

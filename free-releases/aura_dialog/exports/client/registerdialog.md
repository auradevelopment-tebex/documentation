---
description: RegisterDialog export.
---

# RegisterDialog

Registers a dialog so it can be opened by id.

```lua
exports['aura_dialog']:RegisterDialog(data)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `data.id` | string | Unique dialog id, required |
| `data.title` | string | Header name |
| `data.subtitle` | string | Subtitle, optional |
| `data.text` | string | Body text |
| `data.speed` | number | Typing speed, optional |
| `data.entity` | entity | Ped for camera + mugshot |
| `data.options` | table | Option list, see Usage |

Example:

```lua
exports['aura_dialog']:RegisterDialog({
    id = 'npc_main',
    title = 'John Doe',
    subtitle = 'Paleto Bay',
    text = 'Hello there!',
    entity = entity,
    options = {
        { label = 'Goodbye', onSelect = function() print('bye') end },
    },
})
```

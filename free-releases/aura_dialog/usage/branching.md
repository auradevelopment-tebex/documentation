---
description: Branching dialogs with menu in aura_dialog.
---

# Branching

Set `menu` on an option to switch to another registered dialog without closing the UI. Camera stays put if `entity` is the same — this is how multi-page conversations work.

```lua
{ label = 'Tell me about yourself', menu = 'npc_about' }
```

Example with two pages:

```lua
exports['aura_dialog']:RegisterDialog({
    id = 'npc_main',
    title = 'John Doe',
    subtitle = 'Paleto Bay',
    text = 'Hello there. What can I do for you?',
    entity = entity,
    options = {
        { label = 'Tell me about yourself', menu = 'npc_about' },
        { label = 'Goodbye', onSelect = function() print('bye') end },
    }
})
```

If `menu` is set together with `event` / `serverEvent`, the events fire first, then the menu opens. `onSelect` is ignored on `menu` options unless `keepOpen` is used — see [Events & Callbacks](./events-and-callbacks.md).

---
description: How aura_dialog works - register, show, branch, close.
---

# Usage

aura_dialog is **client-side**. Pattern is always the same:

1. `RegisterDialog` after your ped exists
2. `ShowDialog(id)` on interact (`E`, target, etc.)
3. Player picks an option — `menu` switches page, `event` / `serverEvent` / `onSelect` run logic
4. `CloseDialog` or `RefreshDialog` to finish or update in place

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
    },
})

exports['aura_dialog']:ShowDialog('npc_main')
```

Next: [Registering Dialogs](./registering-dialogs.md)

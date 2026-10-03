---
description: Branching dialogs with menu in aura_dialog.
---

# Branching

Set `menu` on an option to switch to another registered dialog without closing the UI. Camera stays put if `entity` is the same — this is how the Trevor tree works.

```lua
{ label = 'Who are you, exactly?', menu = 'trevor_backstory' }
```

Full flow from the bundled example:

* `trevor_main` → `trevor_backstory` / `trevor_early_life` / `trevor_michael` / `trevor_business` / `trevor_goodbye`
* `trevor_backstory` → `trevor_early_life` / `trevor_blaine` / back to `trevor_main`
* `trevor_business` → `trevor_oneils` / `trevor_crew` / back

```lua
exports['aura_dialog']:RegisterDialog({
    id = 'trevor_main',
    title = 'Trevor Philips',
    subtitle = 'Sandy Shores, Blaine County',
    text = "Oh great, another person walkin' up to me...",
    entity = trevorPed,
    options = {
        { label = 'Who are you, exactly?', menu = 'trevor_backstory' },
        { label = 'Never mind. Goodbye.', menu = 'trevor_goodbye' },
    }
})
```

If `menu` is set together with `event` / `serverEvent`, the events fire first, then the menu opens. `onSelect` is ignored on `menu` options unless `keepOpen` is used — see [Events & Callbacks](./events-and-callbacks.md).

---
description: Frequently asked questions for aura_dialog.
---

# FAQ

### How do I disable the Trevor example?

In `config.lua`:

```lua
Config.TrevorExample = false
```

Restart the resource. No ped spawns and no dialogs register.

### Dialog won't open - `No dialog registered with id`?

You called `ShowDialog` before `RegisterDialog`, or with a typo. Register after your ped exists, then open on interact.

### Mugshot is missing / black?

`MugShotBase64` failed or is not started. Make sure it starts before `aura_dialog`. Dialog still works, just without portrait. Or call `ShowDialog(id, false)` to skip it intentionally.

### Can I update text without closing?

Yes. Use `keepOpen = true` on the option, re-`RegisterDialog` with the same `id`, then `RefreshDialog(id)`.

### Does it need a framework?

No. Standalone — only `ox_lib` + `MugShotBase64` are required.

### Where is the UI?

The UI is served from `web/build/index.html`.

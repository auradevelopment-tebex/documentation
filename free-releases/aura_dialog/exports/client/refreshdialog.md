---
description: RefreshDialog export.
---

# RefreshDialog

Updates the currently open dialog in place — new text/options without closing, camera and focus are untouched.

```lua
exports['aura_dialog']:RefreshDialog(id)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `id` | string | Must match the currently open dialog, otherwise does nothing |

Use with `keepOpen` options: run async work in `onSelect`, re-`RegisterDialog` the same `id`, then call this.

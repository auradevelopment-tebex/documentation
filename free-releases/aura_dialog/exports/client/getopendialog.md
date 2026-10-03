---
description: GetOpenDialog export.
---

# GetOpenDialog

Returns the id of the currently open dialog, or `nil`.

```lua
local id = exports['aura_dialog']:GetOpenDialog()
```

Use to guard double-opens or to check state before refreshing.

---
description: Client exports for aura_dialog.
---

# Exports

All functions are client exports on `aura_dialog`:

| Export | Description |
| --- | --- |
| [RegisterDialog](./client/registerdialog.md) | Register a dialog by id |
| [ShowDialog](./client/showdialog.md) | Open a registered dialog |
| [RefreshDialog](./client/refreshdialog.md) | Update open dialog in place |
| [CloseDialog](./client/closedialog.md) | Close current dialog |
| [GetOpenDialog](./client/getopendialog.md) | Get current dialog id or nil |

```lua
exports['aura_dialog']:RegisterDialog(data)
exports['aura_dialog']:ShowDialog(id)
exports['aura_dialog']:RefreshDialog(id)
exports['aura_dialog']:CloseDialog()
local id = exports['aura_dialog']:GetOpenDialog()
```

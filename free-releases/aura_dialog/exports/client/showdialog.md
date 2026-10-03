---
description: ShowDialog export.
---

# ShowDialog

Opens the dialog with the given id. Frames the camera on the dialog's `entity`, enables NUI focus and sends data to the UI.

```lua
exports['aura_dialog']:ShowDialog(id)
exports['aura_dialog']:ShowDialog(id, useMugshot)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `id` | string | Id of a registered dialog |
| `useMugshot` | boolean | Optional, `false` = skip mugshot. Default `true` |

{% hint style="warning" %}
Errors with `No dialog registered with id: <id>` if you call it before `RegisterDialog`. Register after your ped exists.
{% endhint %}

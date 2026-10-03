---
description: Events and callbacks for dialog options.
---

# Events & Callbacks

Each option supports one or more behaviors:

| Field | Type | Description |
| --- | --- | --- |
| `label` | string | Button text |
| `disabled` | boolean | Optional, renders button disabled |
| `menu` | string | Optional, id of another dialog to open |
| `onSelect` | function | Optional, `onSelect(args)` run on select |
| `event` | string | Optional, client event fired with `args` |
| `serverEvent` | string | Optional, server event fired with `args` |
| `args` | any | Optional, payload for `onSelect` / events |
| `keepOpen` | boolean | Optional, run handler without closing |

### Rules

* With `menu`: fires `serverEvent` / `event`, then opens `menu`. `onSelect` does not run.
* With `keepOpen=true`: runs `onSelect` only, dialog stays open. Re-`RegisterDialog` the same `id` + `RefreshDialog(id)` to update text in place — camera and focus are untouched.
* Without `menu` / `keepOpen`: closes first, then runs `onSelect` / `event` / `serverEvent`.

```lua
-- Buy, closes dialog
{ label = 'Buy', serverEvent = 'shop:buy', args = { item = 'bread', price = 5 } }

-- Async update, stays open
{
    label = 'Check stock',
    keepOpen = true,
    onSelect = function()
        -- fetch stock, then:
        -- exports['aura_dialog']:RegisterDialog({ id = 'shop_main', ... new text ... })
        -- exports['aura_dialog']:RefreshDialog('shop_main')
    end
}
```

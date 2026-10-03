---
description: >-
  A FiveM resource for creating and managing map blips in-game. Blips are fully
  configurable and persist across server restarts via KVP storage. Includes a
  developer API for use from other resources.
---

# aura\_blips



***

### Requirements

* [ox\_lib](https://github.com/overextended/ox_lib)

***

### Installation

1. Drop the `aura_blips` folder into your server `resources` directory.
2. Add the following to your `server.cfg`:

```cfg
ensure ox_lib
ensure aura_blips

# Grant access to a specific ACE group
add_ace group.admin aura_blips.use allow

# Assign a player to that group (replace with your license)
add_principal identifier.license:YOUR_LICENSE_HERE group.admin
```

3. Start or restart the resource.

***

### Configuration

`config.lua` contains two values:

```lua
Config.Command      = 'blipscreator'   -- Command used to open the UI
Config.AcePermission = 'aura_blips.use' -- ACE permission required to use the command
```

***

### Usage

Open the UI in-game with:

```
/blipscreator
```

***

### Features

#### Create Tab

* Set a label, coordinates, sprite, color, scale, display mode, flashing, and short range
* Click the clipboard icon to auto-fill your current in-game coordinates
* Assign a blip to a category
* 86 GTA V blip colors available via color selector
* Display mode options: Both, Map Only, Minimap Only

#### Active Blips Tab

* View all created blips in a searchable list
* Edit any blip's properties live
* Teleport directly to a blip's location
* Delete blips

#### Categories Tab

* Create named categories to group blips
* Delete categories (blips assigned to them become uncategorized)

#### General

* Blips and categories persist across restarts via KVP
* Dark and light theme support
* ACE-based authorization, no framework dependency

***

### Developer API

All exports are client-side.

***

#### `CreateBlip(data)`

Creates a new blip.

```lua
---@param data BlipData
---@return number? idx Index of the created blip, nil on failure
exports['aura_blips']:CreateBlip({
    label       = 'Police Station',
    coords      = vector3(441.3, -982.6, 30.7),  -- or coords = { x, y, z }
    sprite      = 60,
    color       = 3,
    scale       = 0.9,
    display     = 4,         -- 0 = hidden, 2 = map only, 3 = minimap only, 4 = both
    flashing    = 'none',    -- 'none' | 'normal' | 'fast'
    shortRange  = true,
    categoryId  = nil,       -- optional: number ID of a category
})
```

***

#### `RemoveBlip(idx)`

Removes a blip by its index.

```lua
---@param idx number
---@return boolean success
exports['aura_blips']:RemoveBlip(1)
```

***

#### `EditBlip(idx, data)`

Edits an existing blip. Only the fields you provide will be updated.

```lua
---@param idx number
---@param data BlipData
---@return boolean success
exports['aura_blips']:EditBlip(1, {
    label = 'Updated Label',
    color = 5,
})
```

***

#### `GetBlipCount()`

Returns the total number of active blips.

```lua
---@return number count
local count = exports['aura_blips']:GetBlipCount()
```

***

#### `GetBlip(idx)`

Returns the data table for a single blip by index.

```lua
---@param idx number
---@return table? blip
local blip = exports['aura_blips']:GetBlip(1)
if blip then
    print(blip.label, blip.coords.x, blip.coords.y)
end
```

***

### BlipData Fields

| Field            | Type    | Required | Description                                        |
| ---------------- | ------- | -------- | -------------------------------------------------- |
| `label`          | string  | Yes      | Display name shown on map                          |
| `coords`         | vector3 | Yes      | World coordinates `{ x, y, z }`                    |
| `sprite`         | number  | No       | GTA V blip sprite ID (default: `1`)                |
| `color`          | number  | No       | GTA V blip color ID `0-85` (default: `0`)          |
| `scale`          | number  | No       | Size multiplier (default: `1.0`)                   |
| `display`        | number  | No       | Display mode `0/2/3/4` (default: `4`)              |
| `flashing`       | string  | No       | `'none'`, `'normal'`, `'fast'` (default: `'none'`) |
| `shortRange`     | boolean | No       | Only visible when nearby (default: `true`)         |
| `categoryId`     | number  | No       | ID of a category to assign this blip to            |
| `secondaryColor` | number  | No       | Secondary blip color override                      |

***

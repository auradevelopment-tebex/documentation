# aura\_dialog

aura\_dialog is a free, lightweight NPC dialog system for FiveM. It renders a clean, typewriter-styled conversation panel with selectable options. Perfect for NPC conversations, quests, shops, or any scripted dialogue.

### Features

* **Exports-driven:** register dialogs from any resource and open them on demand
* **Typewriter text** with configurable typing speed
* **3D panel styling** with adjustable tilt, perspective, and shadow
* **Keyboard + mouse controls:** pick an option or press ESC to close
* **Multi-screen dialogs:** chain dialogs together with `menu` options
* **Actions on select:** client/server events, callbacks, or simple args
* **Example NPC** to showcase how it works that can be disabled in config
* **Framework agnostic:** works with any server, no framework dependency at all!



### Preview

![3D effect enabled](https://uplaods.auradevelopment.xyz/images/Screenshot%202026-08-29%20213017.png)

![3D effect disabled](https://uplaods.auradevelopment.xyz/images/Screenshot%202026-08-29%20213058.png)

![Config example](https://uplaods.auradevelopment.xyz/images/Screenshot%202026-08-29%20213216.png)

{% embed url="https://youtu.be/KiOJcIMjvpg" %}

### Requirements

* [ox\_lib](https://github.com/overextended/ox_lib) (required)

### Quick start

```lua
exports['aura_dialog']:RegisterDialog({
    id = 'npc_main',
    title = 'John Doe',
    subtitle = 'Paleto Bay',
    text = 'Hello there. What can I do for you?',
    entity = entity, -- the NPC the camera focuses on
    options = {
        { label = 'Tell me about yourself', menu = 'npc_about' },
        { label = 'Goodbye', onSelect = function() print('bye') end },
    },
})

exports['aura_dialog']:ShowDialog('npc_main')
```

***

### Installation

1. Download the `aura_dialog` folder from the release.
2. Drop it into your `resources` (or `resources/[standalone]`) folder.
3. Make sure [ox\_lib](https://github.com/overextended/ox_lib) is installed and starts **before** aura\_dialog.
4. Add the resource to your `server.cfg`:

```cfg
ensure ox_lib
ensure aura_dialog
```

5. Restart your server (or `refresh` + `ensure aura_dialog`).

The release comes pre-built with `web/build` , so the UI works out of the box.

#### Building the UI (optional)

Only needed if you modify the React/Tailwind source under `web/src`.

```bash
cd web
npm install
npm run build
```

The build output goes to `web/build`, which is what the resource serves.

#### Verifying it works

With the default config the example NPC (Trevor) spawns near Davis impound. Walk up to him and press **E** to open the dialog. You can disable the example in `config.lua`:

```lua
Config.TrevorExample = false
```

***

### Configuration

All configuration lives in `config.lua` at the resource root.

#### UI styling

```lua
Config.Ui = {
    ThreeDEffect = true,  -- Enables the 3D panel tilt
    Perspective = 800,    -- 3D perspective strength; lower is more pronounced
    TiltX = 4.0,          -- Vertical tilt in degrees
    TiltY = -14.0,        -- Horizontal tilt in degrees; negative tilts left
    Shadow = true,        -- Enables the panel drop shadow
}
```

| Setting        | Type    | Default | Description                                  |
| -------------- | ------- | ------- | -------------------------------------------- |
| `ThreeDEffect` | boolean | `true`  | Set to `false` to render a flat panel        |
| `Perspective`  | number  | `800`   | Perspective strength; lower = more depth     |
| `TiltX`        | number  | `4.0`   | Vertical tilt of the panel in degrees        |
| `TiltY`        | number  | `-14.0` | Horizontal tilt in degrees (negative = left) |
| `Shadow`       | boolean | `true`  | Enables the drop shadow on the panel         |

#### Example NPC

```lua
Config.TrevorExample = true
```

Set to `false` to disable the bundled Trevor NPC example entirely. You should disable it once you integrate the resource into your own scripts. This is just a showcase to show you how it could work.

***

### Usage

aura\_dialog is a **client-side** resource. Register dialogs from any resource (for example a shop script) and open them when a player interacts.

#### Registering a dialog

```lua
exports['aura_dialog']:RegisterDialog({
    id = 'npc_main',          -- unique id, used to open the dialog
    title = 'John Doe',       -- character name shown in the header
    subtitle = 'Paleto Bay',  -- subtitle under the name
    text = 'Hello there!',    -- the typewriter dialogue text
    speed = 35,               -- (optional) typing speed in ms per character
    entity = entity,          -- NPC entity the camera focuses on
    options = {
        { label = 'Tell me about yourself', menu = 'npc_about' },
        { label = 'Buy something', onSelect = function() print('shop') end },
        { label = 'Goodbye', event = 'my:npc:goodbye', args = { 1 } },
    },
})
```

> Register dialogs **after** the NPC entity exists. The example script does this right after spawning the ped.

#### Opening and closing

```lua
-- Open a dialog by id
exports['aura_dialog']:ShowDialog('npc_main')

-- Close the currently open dialog (client-side, anywhere)
exports['aura_dialog']:CloseDialog()

-- Check if a dialog is currently open
local isOpen = exports['aura_dialog']:GetOpenDialog()
```

#### Options

Each option supports one or more behaviors:

| Field         | Type     | Description                                          |
| ------------- | -------- | ---------------------------------------------------- |
| `label`       | string   | Text shown on the button                             |
| `disabled`    | boolean  | (optional) Renders the button disabled               |
| `menu`        | string   | (optional) id of another dialog to switch to instead |
| `onSelect`    | function | (optional) callback run after the dialog closes      |
| `event`       | string   | (optional) client event to trigger with `args`       |
| `serverEvent` | string   | (optional) server event to trigger with `args`       |
| `args`        | any      | (optional) payload passed to `onSelect` / events     |

**Chaining dialogs**

Set `menu` on an option to navigate to another registered dialog without closing the UI:

```lua
{ label = 'Tell me about yourself', menu = 'npc_about' }
```

**Triggering events**

```lua
{ label = 'Buy', serverEvent = 'shop:buy', args = { item = 'bread', price = 5 } }
```

#### Controls

* Click an option (or press its number) to select it.
* Press **ESC** to close the dialog.

***

### API Reference

All functions are exported as `exports['aura_dialog']`.

#### RegisterDialog

```lua
exports['aura_dialog']:RegisterDialog(data)
```

Registers a dialog so it can be opened by id. See Usage for the data structure.

| Parameter | Type   | Description                 |
| --------- | ------ | --------------------------- |
| `data.id` | string | Unique dialog id (required) |

#### ShowDialog

```lua
exports['aura_dialog']:ShowDialog(id)
```

Opens the dialog with the given id. Frames the camera on the dialog's `entity`, enables NUI focus, and sends the data to the UI.

| Parameter | Type   | Description               |
| --------- | ------ | ------------------------- |
| `id`      | string | Id of a registered dialog |

#### CloseDialog

```lua
exports['aura_dialog']:CloseDialog()
```

Closes the currently open dialog, releases NUI focus, and restores the camera.

#### GetOpenDialog

```lua
local id = exports['aura_dialog']:GetOpenDialog()
```

Returns the id of the currently open dialog, or `nil` .

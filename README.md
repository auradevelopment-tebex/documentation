---
description: A modern loading screen for FiveM, inspired by Lucid City.
---

# aura\_loadingscreen

Aura Loadingscreen displays a background slideshow, music player, and keybind guide while players connect to your server. It is standalone and works without any framework.

***

### Purchase

| Step        | Details                                                                                                           |
| ----------- | ----------------------------------------------------------------------------------------------------------------- |
| 1. Purchase | [**store.auradevelopment.xyz**](https://store.auradevelopment.xyz)                                                |
| 2. Download | CFX Portal granted assets: [**portal.cfx.re/assets/granted-assets**](https://portal.cfx.re/assets/granted-assets) |
| 3. Updates  | Delivered through the CFX Portal                                                                                  |

{% hint style="info" %}
Only one loading screen resource can be active at a time. Disable or remove any other loading screen before using this one.
{% endhint %}

***

### Installation

1. Download the latest version from your [CFX Portal granted assets](https://portal.cfx.re/assets/granted-assets)
2. Extract `aura_loadingscreen` into your server `resources` folder, for example `resources/[standalone]/aura_loadingscreen`
3. Add to your `server.cfg`:

```cfg
ensure aura_loadingscreen
```

4. Restart your server
5. Join the server to see the loading screen during connection

{% hint style="success" %}
Make sure to place `ensure aura_loadingscreen` in your config and restart the server after any config changes.
{% endhint %}

***

### Configuration

All settings are in one file:

**`shared/config.lua`**

Edit the file, save, and restart the server.

Default configuration:

```lua
local Config <const> = {
    Debug = false,

    Color = '327F61',

    Background = {
        type = 'video', -- 'images' for slideshow, 'video' for video background
        images = {
            './images/backgrounds/1.png',
            './images/backgrounds/2.png',
            './images/backgrounds/3.png',
            './images/backgrounds/4.png',
            './images/backgrounds/5.png'
        }, -- fallback slideshow if the video can't load
        video = './videos/video.mp4', -- local file, DIRECT .mp4/.webm link, or Streamable/Vimeo link
        -- allowedHosts is only needed for remote videos, not local files:
        allowedHosts = { 'streamable.com', 'vimeo.com', 'player.vimeo.com' },
    },

    Keybinds = {
        ['CTRL']  = 'Crouch',
        ['ALT']   = 'Interact',
        ['Caps']  = 'Talk Over Radio',
        ['Tab']   = 'Open Frikin Menu',
        ['Esc']   = 'Open Map',
        ['1']     = 'Use 1st Inventory Item',
        ['2']     = 'Use 2nd Inventory Item',
        ['3']     = 'Use 3rd Inventory Item',
        ['4']     = 'Use 4th Inventory Item',
        ['5']     = 'Use 5th Inventory Item',
        ['M']     = 'Open Phone',
        ['X']     = 'Put Your Hands Up',
        ['G']     = 'Toggle Engine',
        ['U']     = 'Ragdoll',
        ['T']     = 'Open Chat',
        ['B']     = 'Toggle Seatbelt',
        ['L']     = 'Lock/Unlock Vehicle',
        ['F']     = 'Enter/Exit Vehicle',
        ['J']     = 'Toggle ID Display',
        ['V']     = 'Toggle Voice Chat',
        ['Shift'] = 'Sprint',
        ['H']     = 'Cross Arms'
    },

    Playlist = {
        {
            author = 'Witchitaw Slim',
            songName = 'I cant complain',
            file = './audios/1.mp3',
            logo = './images/logo.png'
        },
        {
            author = 'Baha Bank$',
            songName = 'Wanna Have Fund$',
            file = './audios/2.mp3',
            logo = './images/logo.png'
        },
        -- more tracks ...
    },

    Socials = {
        discord = 'https://discord.gg/yourserver',
        website = 'https://yourwebsite.com',
        youtube = 'https://youtube.com/@yourchannel',
        x = 'https://x.com/yourhandle',
    },
}

_G.Config = Config
```

#### Debug

```lua
Debug = false
```

Set to `true` to show additional logs in the server console. Keep it `false` during normal use.

#### Color

```lua
Color = '327F61'
```

The main theme color for the loading screen. It is used for the progress bar, keyboard highlights, and music player accents.

Need a hex code? Pick one at [htmlcolorcodes.com](https://htmlcolorcodes.com/).

You can use with or without `#`:

{% tabs %}
{% tab title="Default" %}
```lua
Color = '327F61'
```
{% endtab %}

{% tab title="With Hash" %}
```lua
Color = '#8B5CF6'
```
{% endtab %}

{% tab title="Red" %}
```lua
Color = '#E63946'
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Use a 6-character hex color (for example `327F61` or `#327F61`).
{% endhint %}

#### Background

```lua
Background = {
    type = 'video', -- 'images' for slideshow, 'video' for video background
    images = {
        './images/backgrounds/1.png',
        './images/backgrounds/2.png',
        './images/backgrounds/3.png',
        './images/backgrounds/4.png',
        './images/backgrounds/5.png'
    }, -- fallback slideshow if the video can't load
    video = './videos/video.mp4', -- local file, DIRECT .mp4/.webm link, or Streamable/Vimeo link (auto-embedded muted - YouTube is not supported)
    -- allowedHosts is only needed for remote videos, not local files:
    allowedHosts = { 'streamable.com', 'vimeo.com', 'player.vimeo.com' },
}
```

Set `type = 'images'` for a rotating slideshow, or `type = 'video'` for a looping video background. If the video can't load, the `images` slideshow is shown instead.

Paths are relative to `web/dist` and must start with `./`.

To customize:

* **Replace an image:** Overwrite a file in `web/dist/images/backgrounds/` and keep the same path
* **Add an image:** Put a new file in `web/dist/images/backgrounds/` (for example `6.png`) and add its path to the list: `'./images/backgrounds/6.png'`
* **Remove an image:** Remove its line from the list
* **Use only one image:** Leave a single entry in the list and it will be shown statically
* **Use your own video host:** Add it to `allowedHosts` and set `video` to the file link, for example `allowedHosts = { 'streamable.com', 'vimeo.com', 'player.vimeo.com', 'yourdomain.com' }` with `video = 'https://yourdomain.com/background.mp4'`

{% hint style="warning" %}
Keep images optimized and under 2MB each for fast loading. Large files will slow down the loading screen itself.
{% endhint %}

#### Keybinds

```lua
Keybinds = {
    ['CTRL'] = 'Crouch',
    ['ALT']  = 'Interact',
    ['Shift'] = 'Sprint',
}
```

Each entry is `['Key Label'] = 'Description'`.

The key label must match the label shown on the virtual keyboard. Common labels include: `Esc`, `1` to `0`, `-`, `=`, `Tab`, `Q` to `P`, `[`, `]`, `\`, `Caps`, `A` to `L`, `;`, `'`, `Enter`, `Shift`, `Z` to `M`, `<`, `>`, `/`, `CTRL`, `Win`, `ALT`, `Space`.

Only keys that are in this list will appear highlighted and clickable on the keyboard. When a player clicks a key, it shows `Press To - Description`.

<details>

<summary>Full keyboard layout</summary>

```
Row 1: Esc, 1, 2, 3, 4, 5, 6, 7, 8, 9, 0, -, =, Backspace
Row 2: Tab, Q, W, E, R, T, Y, U, I, O, P, [, ], \
Row 3: Caps, A, S, D, F, G, H, J, K, L, ;, ', Enter
Row 4: Shift, Z, X, C, V, B, N, M, <, >, /, Shift
Row 5: CTRL, Win, ALT, Space, Alt, CTRL + Arrow keys
```

Labels are case sensitive. Use `CTRL`, `ALT`, `Caps`, `Shift`, `Tab`, `Esc` exactly as shown.

</details>

To add or remove a keybind, simply add or remove a line from the table.

#### Playlist

```lua
Playlist = {
    {
        author = 'Witchitaw Slim',
        songName = 'I cant complain',
        file = './audios/1.mp3',
        logo = './images/logo.png'
    },
    {
        author = 'Baha Bank$',
        songName = 'Wanna Have Fund$',
        file = './audios/2.mp3',
        logo = './images/logo.png'
    },
}
```

Each track needs:

* `author` - Artist name
* `songName` - Song title
* `file` - Audio file: a local path relative to `web/dist` (for example `'./audios/1.mp3'`), or a direct remote link (for example `'https://yourdomain.com/song.mp3'`)
* `logo` - Artwork for the track (usually `'./images/logo.png'`)

The player supports play/pause, previous/next track, volume control, progress bar, and pressing `Space` to play or pause. Tracks are shuffled on load.

To add a new song:

1. Put the audio file in `web/dist/audios/` (for example `13.mp3`), or host it remotely as a direct link
2. Add a new entry to `Playlist` with `file = './audios/13.mp3'`
3. Remote audio links must come from a host listed in `allowedHosts`
4. Restart the server

Supported formats are `.mp3` and `.ogg`. `.mp3` is recommended.

#### Socials

```lua
Socials = {
    discord = 'https://discord.gg/yourserver',
    website = 'https://yourwebsite.com',
    youtube = 'https://youtube.com/@yourchannel',
    x = 'https://x.com/yourhandle',
}
```

A vertical rail of translucent icons on the right side of the screen: Discord, website (globe), YouTube and X. Clicking an icon opens the link in the player's browser.

* Replace each value with your own link
* Set any entry to `''` to hide its icon (for example `discord = ''`)
* Restart the server after changing links

***

### Customization Tips

**Changing the logo**

Replace `web/dist/images/logo.png` with your own logo and keep the same filename, or change the `logo` path in any playlist entry.

**Adding more songs**

Add entries to `Playlist` for each song. Local files go in `web/dist/audios/`, or use a remote link (see below).

**Using fewer backgrounds**

If you only want one background, leave one entry in `Background`. If you want many, add more paths. The slideshow adapts automatically.

***

### Troubleshooting

{% tabs %}
{% tab title="Loading screen not showing" %}
* Make sure only one loading screen resource is running. Stop any other loading screen and keep only `aura_loadingscreen`.
* Make sure `aura_loadingscreen` is ensured in `server.cfg`.
* Restart the server and reconnect, do not just respawn.
{% endtab %}

{% tab title="Stuck on loading screen" %}
* The loading screen closes automatically when your character spawns. If your framework changes how spawning works, make sure the spawn event still fires.
* As a temporary fix, another resource can close it for a player: `TriggerClientEvent('aura_loadingscreen:client:forceClose', playerId)`
{% endtab %}

{% tab title="Music not playing" %}
* Check that each `file` path in `Playlist` is correct and that the file actually exists in `web/dist/audios/`.
* Remote audio links must be direct file links from a host listed in `allowedHosts`.
* Click play or press `Space` to start playback.
{% endtab %}

{% tab title="Backgrounds not showing" %}
* Check that each path in `Background` starts with `./` and matches a real file in `web/dist/images/backgrounds/`.
* Make sure images are valid `png` or `jpg` files and not too large.
* Remote image links must come from a host listed in `allowedHosts`.
* After changing the config, restart the server.
{% endtab %}

{% tab title="Video background not playing" %}
* The video can be a local file in `web/dist/videos/`, a direct `.mp4`/`.webm` link, or a Streamable/Vimeo link. Streamable/Vimeo watch links are converted to muted autoplay embeds automatically. Watch pages from other hosts (YouTube etc.) are not supported in loading screens and fall back to the slideshow.
* Remote videos only load from hosts listed in `allowedHosts`. Add your host there, for example `allowedHosts = { 'streamable.com', 'vimeo.com', 'player.vimeo.com', 'yourdomain.com' }`.
* Embeds require the host to allow embedding.
{% endtab %}

{% tab title="Keybinds not highlighting" %}
* Only keys that are in `Keybinds` will be highlighted. The label must match exactly, for example `CTRL` not `Ctrl`.
{% endtab %}

{% tab title="Color not changing" %}
* Make sure the hex code is 6 characters, with or without `#`, for example `327F61` or `#327F61`.
* Save the file and restart the server.
{% endtab %}
{% endtabs %}

***

### Support

If you need help, join our [Discord](https://discord.gg/pPzbpY6SKW) and create a resource support ticket with your `shared/config.lua` and a description of the issue. For the latest version, always download from [portal.cfx.re/assets/granted-assets](https://portal.cfx.re/assets/granted-assets).

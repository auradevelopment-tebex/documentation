---
description: Common issues with fixes for aura_foodtruck.
---

# Common Issues

Fixes for the most common setup mistakes.

### No target options on the truck

The bridge resolves `ox_target` first, then `qb-target`. If neither is started, no options appear.

Fix: start one of them before `aura_foodtruck`. `interact` / `sleepless_interact` are not supported.

### `framework returned empty job data` in console

Your framework (`qbx_core` / `qb-core` / `es_extended`) is missing or starts after `aura_foodtruck`.

Fix: `ensure` the framework before `aura_foodtruck` in `server.cfg`.

### Tray / storage won't open

On `qb-inventory` and friends the stash opens through the inventory's own stash API. If nothing happens, check the server console for inventory errors and confirm the stash id isn't already open elsewhere (most inventories lock a stash to one viewer).

Fix: close any duplicate stash views, restart `aura_foodtruck` to re-register stashes.

### Cooking gives items without ingredients / bills do nothing

You have a modified client or an old `web/dist`. The server re-validates every cook and payment — a manipulated client only gets itself an error.

Fix: rebuild the UI (`npm run build` in `web/`) if you edited it, and make sure `web/dist/index.html` exists (the release workflow validates this).

### NPC customers never arrive

`/sellfoodtruck` needs the truck's job, and customers spawn 13–19 m away — make sure there's walkable ground around the truck and you stay within `sales.maxDistance` (20 m).

Fix: check job, move the truck somewhere open, watch for the "Started selling" notify.

### Tablet opens but shows no logs / stats

Logging is probably disabled. `logging.enabled = false` (or individual `logging.types`) turns off the events the dashboard is computed from.

Fix: re-enable the log types you want stats for. Old logs are pruned after `logs.retentionDays` (default 90).

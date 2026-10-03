---
description: Common issues with fixes for aura_dialog.
---

# Common Issues

Fixes for the most common setup mistakes.

### `lib.points` nil / error on start

`ox_lib` is missing or starts after `aura_dialog`.

Fix: `ensure ox_lib` before `ensure aura_dialog`, add `@ox_lib/init.lua` is already in `fxmanifest` — do not remove it.

### No `[E]` prompt / Trevor never spawns

`Config.TrevorExample = false`, or model `player_two` failed to load.

Fix: set it to `true` for testing, restart, check server console for model load errors. Interact distance is `3.0m` at `346.31, -1696.43, 47.3`.

### Camera stuck after close

Another script forced NUI focus or died mid-dialog.

Fix: call `exports['aura_dialog']:CloseDialog()` once (e.g. on resource stop / player death) to release focus and destroy the cam.

### Options do nothing

You used `menu` pointing to an unregistered id, or forgot `args`.

Fix: register every `menu` target first, check spelling (`npc_main` vs `npc_Main` matters).

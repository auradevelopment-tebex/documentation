---
description: Controls and camera behavior for aura_dialog.
---

# Controls

* Click an option (or press its number key) to select it
* Press **ESC** to close

Opening a dialog sets NUI focus (`SetNuiFocus(true, true)`) and creates a scripted camera:

* Offset `0, 1.5, 0.3` from `entity` + `0.2z`, facing `heading + 180`, FOV `40`, 500ms blend
* Re-opening for the **same entity** (menu navigation) keeps the camera where it is
* Closing releases focus and blends back with a race-safe destroy

Mugshots are taken once per entity per session via `MugShotBase64` and reused. Pass `false` as second arg to `ShowDialog(id, false)` to skip the mugshot.

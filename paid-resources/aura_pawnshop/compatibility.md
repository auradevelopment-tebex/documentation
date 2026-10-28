---
description: Frameworks, inventories, banking and other resources aura_pawnshop works with.
---

# Compatibility

The resource detects the resources below by itself when it starts. You don't select them anywhere: start the one you use **before** `aura_pawnshop`. No external bridge resource is needed; all integrations live in the resource's own `bridge/` folder.

### Framework

| Resource | Supported | Notes |
| --- | --- | --- |
| `qbx_core` | Yes | Checked first |
| `qb-core` | Yes | |
| `es_extended` | Yes | The top grade must be named `boss` (or be the highest grade) |

### Inventory

The resource needs an inventory that can create stashes and put items into them from the server: that is how storage, counter sales and walk-in sales work.

| Resource | Supported | Notes |
| --- | --- | --- |
| `ox_inventory` | Yes | **Recommended** |
| `qb-inventory` | Yes | Version **2.x** only. With 1.x the resource prints an error and disables storage, counter sales and walk-in sales |
| `qs-inventory` | Yes | |
| `origen_inventory` | Yes | |
| `tgiann-inventory` | Yes | |
| `jpr-inventory` | Yes | |
| `core_inventory` | Yes | |
| `ps-inventory` | Partly | Storage opens, but the resource can't put items into it: players can't sell at the counter and staff can't buy from walk-in sellers |
| `codem-inventory` | Partly | Same as `ps-inventory`. Its stashes also skip the resource's own range and rank checks |
| ESX built-in | No | No stashes. Use `ox_inventory` with ESX |

### Target

| Resource | Supported |
| --- | --- |
| `ox_target` | Yes, checked first |
| `qb-target` | Yes |

Other target resources need a change in `bridge/target/client.lua`.

### Banking (shop money)

The shop's money lives in a society/business account named by `Society.account` (`pawn` by default).

| Resource | Supported |
| --- | --- |
| `Renewed-Banking` | Yes |
| `okokBanking` | Yes |
| `fd_banking` | Yes |
| `kartik-banking` | Yes |
| `wasabi_banking` | Yes |
| `tgg-banking` | Yes |
| `tgiann-bank` | Yes |
| `qb-banking` | Yes |
| `esx_addonaccount` (ESX society) | Yes, account `society_pawn` |
| None of the above | The resource keeps the shop's money in its own database table (`StandaloneBank`) |

### Other resources

All optional. When none is running, the resource uses ox_lib or GTA defaults.

| System | Detected resources |
| --- | --- |
| Notifications | `okokNotify`, `lation_ui`, `wasabi_notify`, `brutal_notify`, `t-notify`, `mythic_notify` (else ox_lib) |
| Progress bars | `lation_ui`, `progressbar` (else ox_lib) |
| Vehicle keys (delivery van) | `wasabi_carlock`, `mk_vehiclekeys`, `Renewed-Vehiclekeys`, `qs-vehiclekeys`, `cd_garage`, `okokGarage` (else the QBCore `vehiclekeys` event) |
| Fuel (delivery van) | `LegacyFuel`, `cdn-fuel`, `ps-fuel`, `lc_fuel`, `qb-fuel`, `okokGasStation`, `x-fuel`, `ti_fuel`, `qs-fuelstations`; `ox_fuel` and others reading the `fuel` state bag |
| Clothing (staff wardrobe) | `rcore_clothing`, `crm-appearance`, `illenium-appearance`, `fivem-appearance`, `qb-clothing`, `skinchanger` |
| Walk-in conversations | [`aura_dialog`](../../free-releases/aura_dialog/README.md) (required for walk-ins) |
| Customer photos | `MugShotBase64` |

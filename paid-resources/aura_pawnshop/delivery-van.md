---
description: The aurapawnvan delivery van included with aura_pawnshop, and how to use another vehicle.
---

# Delivery Van

aura_pawnshop includes **`aurapawnvan`**, a branded van with an Aura Pawnshop livery. Employees drive it to deliver marketplace orders.

### Installing the van

There is nothing to install. The van is part of the resource:

* `stream/` holds the model and textures.
* `data/aurapawnvan/` holds `vehicles.meta` and `carvariations.meta`, loaded by `fxmanifest.lua`.

Starting `aura_pawnshop` streams the van to every player. Do not move these files into another resource, and do not add the van to a separate vehicle pack, or it is loaded twice.

{% hint style="info" %}
The van is a delivery vehicle, not a car players own. It spawns at `Delivery.pickup` when an employee accepts an order and is removed when the run ends. You don't need to add it to your garage or vehicle shop.
{% endhint %}

### Look of the van

In `configs/shared/main.lua`:

```lua
Delivery = {
    truckModel = `aurapawnvan`,
    truckLook = {
        livery = 0,
        primary = vec3(16, 16, 19),
        secondary = vec3(16, 16, 19),
    },
    platePrefix = 'PAWN',
    fuelLevel = 65.0,
    ...
}
```

* `livery = 0` is the Aura Pawnshop livery.
* `primary` / `secondary` are the paint colours as red, green, blue (0 to 255).
* Remove the whole `truckLook` block to keep the model's own colours.
* `platePrefix` sets the plate text. 4 random digits are added after it, for example `PAWN4821`.

### Using a different vehicle

Set `truckModel` to any vehicle model, for example the plain GTA van:

```lua
truckModel = `speedo`,
```

Remove `truckLook` (or at least `livery`) when you swap models, because other vehicles don't have the pawnshop livery.

### Keys and fuel

When the van spawns, the shop gives the driver its keys and sets its fuel to `fuelLevel`. It works with the key and fuel resources listed in [Compatibility](./compatibility.md#other-resources). If your key resource is not listed, drivers may not be able to start the van: add it in `bridge/vehiclekey/client.lua`.

### What happens if the van is lost

* **Destroyed or gone before delivery:** the run ends and the order goes back on the board, so another employee can take it.
* **Lost after the delivery:** the payout is already banked, nothing is lost.
* **Driver cancels, disconnects or the timer runs out:** the order goes back on the board.

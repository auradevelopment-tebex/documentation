---
description: The custom-made delivery van included with aura_pawnshop, and how to use another vehicle.
---

# Delivery Van

aura_pawnshop includes a **custom-made delivery van** with an Aura Pawnshop livery. Employees drive it to deliver marketplace orders.

### Installing the van

There is nothing to install. The van ships inside the resource and is loaded automatically when `aura_pawnshop` starts, for every player.

Do not copy the van into another resource or a vehicle pack, or it is loaded twice.

{% hint style="info" %}
The van is a delivery vehicle, not a car players own. It spawns at the pick-up point behind the shop when an employee accepts an order and is removed when the run ends. You don't need to add it to your garage or vehicle shop.
{% endhint %}

### Look of the van

In `configs/shared/main.lua`, under `Delivery`:

```lua
truckLook = {
    livery = 0,
    primary = vec3(16, 16, 19),
    secondary = vec3(16, 16, 19),
},
platePrefix = 'PAWN',
fuelLevel = 65.0,
```

* `livery = 0` is the Aura Pawnshop livery.
* `primary` / `secondary` are the paint colours as red, green, blue (0 to 255).
* Remove the whole `truckLook` block to keep the van's own colours.
* `platePrefix` sets the plate text. 4 random digits are added after it, for example `PAWN4821`.

### Using a different vehicle

`truckModel` in the same `Delivery` block is set to the included van. To use another vehicle, replace its value with that vehicle's model, for example the plain GTA van:

```lua
truckModel = `speedo`,
```

Remove `truckLook` (or at least `livery`) when you swap, because other vehicles don't have the pawnshop livery. To go back to the included van, put the original `truckModel` line from the downloaded config back.

### Keys and fuel

When the van spawns, the resource gives the driver its keys and sets its fuel to `fuelLevel`. It works with the key and fuel resources listed in [Compatibility](./compatibility.md#other-resources).

If none of the listed key resources is running, the van is left unlocked so the employee can drive it without a key.

### What happens if the van is lost

* **Destroyed or gone before delivery:** the run ends and the order goes back on the board, so another employee can take it.
* **Lost after the delivery:** the payout is already banked, nothing is lost.
* **Driver cancels, disconnects or the timer runs out:** the order goes back on the board.

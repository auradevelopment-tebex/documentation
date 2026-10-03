---
hidden: true
---

# aura\_dailyrewards

#### **Daily login rewards & a lucky wheel your players will actually log in for**

[![Store](https://img.shields.io/badge/%F0%9F%9B%92_Store-store.auradevelopment.xyz-6C5CE7?style=for-the-badge)](https://store.auradevelopment.xyz) [![Discord](https://img.shields.io/badge/%F0%9F%92%AC_Discord-join-5865F2?style=for-the-badge)](https://discord.gg/auradevelopment)

***

### What is Aura DailyRewards?

Aura DailyRewards gives your players a full month of daily rewards in one clean panel. Every day a player logs in, a new reward becomes claimable — cash, items, weapons or bank money. Missed a day? No problem: any reward for a day the player played stays claimable for the rest of the month.

On top of the calendar sits a fully animated **lucky wheel** — a real prop in the world that players spin for free once a day, with bonus spins earned simply by playing..

Everything is handled server-side, so players can't cheat their way into extra rewards.

{% hint style="success" %}
**One script, any server.** Aura DailyRewards runs on ESX, QBCore and QBox out of the box through aura\_bridge — it auto-detects your framework and inventory. No code edits needed.
{% endhint %}

***

### Features

* **Monthly reward calendar:** lockable/unlockable/redeemed states, full month visible at a glance
* **Redeem All:** one click claims every available reward
* **Physical lucky wheel:** real prop, smooth spin animation, 20 prize sectors, sound fx
* **Weighted prize chances** — configure how rare each wheel prize is in seconds
* **4 reward types** — items, weapons, cash and bank money
* **Playtime spins** — players earn bonus spins for time played (fully configurable)
* **Player welcome card** — live mugshot, character name and playtime
* **Live countdown** — players always know when the next daily reward resets
* **Automatic resets** — daily and monthly resets run themselves

***

### Requirements

| Dependency                                                   | Purpose                             |
| ------------------------------------------------------------ | ----------------------------------- |
| [ox\_lib](https://github.com/overextended/ox_lib)            | Core utilities                      |
| [oxmysql](https://github.com/overextended/oxmysql)           | Saving player progress              |
| aura\_bridge                                                 | Framework & inventory compatibility |
| [MugShotBase64](https://github.com/BaziForYou/MugShotBase64) | Player mugshot in the welcome card  |

***

### Installation

1. Drop `aura_dailyrewards` into your resources folder
2. Add the following to your `server.cfg`, in this order:

```fxserver
ensure ox_lib
ensure oxmysql
ensure aura_bridge
ensure MugShotBase64
ensure aura_dailyrewards
```

3. Restart the server — database tables are created automatically
4. In-game, type **`/dailyrewards`**&#x20;

***

### Configuration

Everything you need lives in `configs/` — no need to touch any script code.

#### Wheel & general settings

{% code title="configs/shared/main.lua" lineNumbers="true" %}
```lua
Config = {
    enable = true,                  -- enable/disable the lucky wheel
    timeToSpin = 10.0,              -- spin animation duration (seconds)
    sounds = { ... },               -- spin & win sounds
    spinZone = { ... },             -- where players interact with the wheel
    wheelPosition = vec3(...),      -- where the wheel prop spawns
    initialWheelRotation = vec3(...),
    prizes = { ... },               -- one entry per wheel sector
}
```
{% endcode %}

#### Monthly rewards

One file per month: `configs/server/months/month_1.lua` → `month_12.lua`. Each day of the month is one reward:

{% code title="configs/server/months/month_8.lua" lineNumbers="true" %}
```lua
MonthlyRewards[8] = {
    [1]  = { rewardType = "cash",   rewardName = "",                rewardAmount = 20000 },
    [4]  = { rewardType = "item",   rewardName = "bandage",         rewardAmount = 5 },
    [10] = { rewardType = "weapon", rewardName = "weapon_appistol", rewardAmount = 1 },
    [12] = { rewardType = "bank",   rewardName = "",                rewardAmount = 5000 },
}
```
{% endcode %}

{% hint style="info" %}
All 12 month files are pre-filled with sensible rewards that you can freely rename to fit your server's items.
{% endhint %}

#### Lucky wheel prizes

{% code title="configs/server/spins.lua" lineNumbers="true" %}
```lua
SpinConfig = {
    playtimeMinutesPerSpin = 120,        -- minutes played per bonus spin
    resetPlaytimeSpinsMonthly = true,    -- wipe playtime spins on the 1st of each month
    prizes = {
        [5] = {                          -- wheel sector this prize belongs to
            prizeIndex = 5,
            chance = 5.44,               -- higher = more common
            callback = function(playerId, playerSource)
                Framework.AddAccountBalance(playerSource, 'cash', 100000)
            end
        },
    }
}
```
{% endcode %}

***

### Reward Types

| Type     | What it does                    | Example                |
| -------- | ------------------------------- | ---------------------- |
| `item`   | Gives an inventory item         | `"bandage"` x5         |
| `weapon` | Gives a weapon                  | `"weapon_appistol"` x1 |
| `cash`   | Adds money to the player's cash | `$20,000`              |
| `bank`   | Adds money to the player's bank | `$5,000`               |

***

### The Lucky Wheel

The wheel spawns as a real prop at the position you configure, with an indicator above it so players can see exactly what they land on. Players walk up, spin the wheel, and watch it slow down onto their prize — complete with spin and win sound fx.

* **Daily spin** — one free spin per player per day
* **Playtime spins** — bonus spins for every `playtimeMinutesPerSpin` minutes played
* **Prizes** — fully up to you: cash, items, weapons, anything your server can give

{% hint style="warning" %}
The wheel's `chance` values are relative weights, not percentages — a prize with chance `10` is twice as likely as one with chance `5`.
{% endhint %}

***

### Exports

#### Server

{% code lineNumbers="true" %}
```lua
-- Grant bonus playtime spins to a player
exports['aura_dailyrewards']:AddPlaytimeSpinsToPlayer(identifier, amount)
```
{% endcode %}

#### Client

{% code lineNumbers="true" %}
```lua
-- Open the daily rewards panel
exports['aura_dailyrewards']:toggleUI()
```
{% endcode %}

***

### FAQ

<details>

<summary>Can players claim a reward from a day they missed?</summary>

Yes — any day the player was online stays claimable for the rest of the month.

</details>

<details>

<summary>Do playtime spins carry over to the next month?</summary>

Your choice — control it with `resetPlaytimeSpinsMonthly` in `configs/server/spins.lua`.

</details>

<details>

<summary>Can I add more wheel prizes?</summary>

Yes — add a prize entry for any wheel sector in `configs/server/spins.lua` and label it in the shared config.

</details>

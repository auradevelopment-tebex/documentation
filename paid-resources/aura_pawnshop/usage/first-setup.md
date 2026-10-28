---
description: What the owner does on the first day to get aura_pawnshop running for players.
---

# First Setup

Do this once, in game, as the owner (`pawn` job, top grade). It takes about five minutes.

{% stepper %}
{% step %}

### Become the owner

An admin gives the owner the job at the top grade:

```
/setjob <id> pawn 4
```

From now on the owner hires everyone else in game. Nobody else needs `/setjob`.
{% endstep %}

{% step %}

### Put money in the shop account

Go to the **Management terminal** and open **Treasury**. Deposit some of your cash.

The shop pays players from this account when they sell at the counter, and pays drivers their commission. With `$0` in the account, the pawnbroker refuses every sale with *"The shop can not cover that buy-in right now."*
{% endstep %}

{% step %}

### Choose the shop mode

In **Settings**, pick how the counter works:

* **NPC mode** (default): the pawnbroker NPC stands behind the counter and buys from players automatically, even when no staff are online.
* **Player mode:** the NPC leaves. Staff deal with customers themselves, using the display tray.

Marketplace, deliveries and walk-ins work in both modes.
{% endstep %}

{% step %}

### Check the buy list

Open **Buy List**. It shows every item the counter buys and what it pays. Turn items off, lower prices, or set a cap on how many the shop buys.
{% endstep %}

{% step %}

### Hire staff

The new employee must be in the shop (within 25 m of the **Management terminal**). Open **Employees**, choose **Hire** and pick them from the nearby players list. They get a job offer on their screen and must accept it.

New hires start at the lowest grade. Promote them in **Employees**. Managers can only promote, demote and fire people below their own grade.
{% endstep %}

{% step %}

### Adjust ranks (optional)

Open **Ranks** to change what each grade may do, for example letting grade `2` see transactions. The defaults are listed in [Configuration](../configuration.md#staff-permissions-permissions).
{% endstep %}
{% endstepper %}

The shop is ready. Customers can sell at the counter, and staff can start [listing items](./marketplace-and-deliveries.md).

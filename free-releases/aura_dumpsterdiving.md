# aura\_dumpsterdiving

Aura Dumpster Diving is a comprehensive QBCore resource that allows players to search through garbage containers throughout the city for valuable items.\
This immersive script enhances roleplay by providing a realistic scavenging experience with multiple gameplay mechanics.

### Installation

#### **Step 1: Add the "gloves" item**

Go to qb-core/shared/items.lua and paste the following:

```lua
gloves = {
    name = 'gloves',
    label = 'Clean Gloves',
    weight = 0,
    type = 'item',
    image = 'gloves.png',
    unique = true,
    useable = true,
    shouldClose = false,
    combinable = nil,
    description = 'Some clean gloves for yo filthy ahh...'
},
```

#### Step 2: Add the resource

Drag and drop the resource anywhere in your server files and ensure it is added in `server.cfg`.

#### Step 3: Add the gloves image

Navigate to `qb-inventory/html/images` and place the `gloves.png` file inside.

#### Step 4: Restart your server

Restart your server to apply the changes.

***

### &#x20;Key Features

* **Extensive Prop Support**: Search over **100+ garbage props** throughout the map
* **Realistic Animations**: Character walks to the garbage and performs searching animations
* **Cooldown System**: Prevents repeated searches of the same container with **server-side validation**
* **Required Items**: Players need specific items (like **gloves**) to search through garbage
* **Anti-Exploit Measures**: Server-side validation prevents common exploit methods

***

### &#x20;Performance Optimized

* Efficient resource usage with minimal performance impact
* Smart cooldown cleanup to prevent memory leaks
* Optimized prop detection and interaction
* **0.00 resmon** active and idle

***

### &#x20;Usage

Players can approach any garbage container in the city and use the **target system** to interact with it.\
If they have the required items, they'll attempt to search through the garbage.

* A **skill-based minigame** determines success
* Animated search process follows
* Successful searches yield **random items** based on the configured probability table
* Chance of attracting unwanted attention from **stray dogs** 🐕

***

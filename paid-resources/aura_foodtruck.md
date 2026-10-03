# aura\_foodtruck

**aura\_foodtruck** is a complete FiveM resource that turns any vehicle into a fully functional food truck business. Employees cook menu items from real ingredients, serve walk-up NPC customers, ring up player orders at the register, and manage the entire operation from an in-game business tablet with upgrades, banking, and activity logs.

{% hint style="info" %}
This guide covers every supported setup — pick your inventory (**qb-inventory**, **ox\_inventory**, or any other inventory on **ESX**) during installation. All item lists include `foodtruck_tablet`, the inventory item version of the business tablet.
{% endhint %}

### Features

* **Recipe-based cooking** — Craft menu items from ingredient requirements, with per-item cook timers, a live crafting queue, animations, and smoke particle effects.
* **Cash register** — Send bills to nearby players who pay through a clean payment prompt UI. Every payment is validated server-side and logged.
* **Walk-up NPC customers** — Toggle selling mode and random NPC customers wander up to your truck and place orders. They have patience; take too long and they leave.
* **Business tablet** — Dashboard with profile image, live stats, activity logs, upgrade shop, and deposit/withdraw banking.
* **Upgrades shop** — Six purchasable upgrades (marketing, signage, service flow, premium ingredients, express prep, customer comfort) with escalating costs per level.
* **Job interaction points** — Tray, storage stash, cooking station, register, and handoff points via target, restricted by job where configured.
* **Consumables** — Eating/drinking crafted food restores hunger/thirst with proper animations & props, including alcohol support, all values configurable per item.
* **8 pre-configured branded trucks** — Snr Buns, Wig Wam, Bean Machine, Burger Shot, Cluckin' Bell, Greasy Joe's, Pizza This and Taco Farmer, each with its own recipes and UI theme.
* **Activity logging** — Configurable per-event database logging of crafted items, payments, NPC orders, upgrades, and bank transactions.
* **Auto version checking** — Checks for updates so you stay updated!

### Installation

#### Prerequisites

Required dependencies:

* **aura\_bridge** — Latest version
* **ox\_lib** — v3.30.6 or higher

#### Step-by-Step Installation

**1. Download and Install Dependencies**

```lua
-- Ensure you have aura_bridge installed
-- Ensure you have ox_lib installed
```

**2. Download the Resource**

```lua
-- Place the aura_foodtruck folder in your server's resources directory
-- Example: resources/[aura]/aura_foodtruck/
```

**3. Add to server.cfg**

```cfg
ensure ox_lib
ensure aura_bridge
ensure aura_foodtruck
```

**4. Framework additions**

Pick the tab that matches your inventory. Every item list includes `foodtruck_tablet` — using it opens the business tablet (`tablet.openMode` in `config.lua` controls whether it opens via item, command, or both).

Using any other supported inventory, open a ticket and we'll map it out for you!

{% tabs %}
{% tab title="QBCore (qb-inventory)" %}
Add the following jobs to your `qb-core/shared/jobs.lua`:

```lua
wigwam = {
    label = 'Wig Wam Food Truck',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 50 },
        ['1'] = { name = 'Cook', payment = 75 },
        ['2'] = { name = 'Chef', payment = 100 },
        ['3'] = { name = 'Head Chef', payment = 125 },
        ['4'] = { name = 'Owner', isboss = true, payment = 150 },
    },
},
beanmachine = {
    label = 'Bean Machine',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee Barista', payment = 50 },
        ['1'] = { name = 'Barista', payment = 75 },
        ['2'] = { name = 'Senior Barista', payment = 100 },
        ['3'] = { name = 'Shift Supervisor', payment = 125 },
        ['4'] = { name = 'Manager', isboss = true, payment = 150 },
    },
},
burgershot = {
    label = 'Burgershot',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 50 },
        ['1'] = { name = 'Cook', payment = 75 },
        ['2'] = { name = 'Grill Master', payment = 100 },
        ['3'] = { name = 'Shift Manager', payment = 125 },
        ['4'] = { name = 'Owner', isboss = true, payment = 150 },
    },
},
cluckinbell = {
    label = 'Cluckin\' Bell',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 50 },
        ['1'] = { name = 'Cook', payment = 75 },
        ['2'] = { name = 'Fryer Master', payment = 100 },
        ['3'] = { name = 'Shift Manager', payment = 125 },
        ['4'] = { name = 'Owner', isboss = true, payment = 150 },
    },
},
greasyjoes = {
    label = 'Greasy Joes',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 50 },
        ['1'] = { name = 'Cook', payment = 75 },
        ['2'] = { name = 'Grill Master', payment = 100 },
        ['3'] = { name = 'Shift Manager', payment = 125 },
        ['4'] = { name = 'Owner', isboss = true, payment = 150 },
    },
},
pizzeria = {
    label = 'Pizzeria',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 50 },
        ['1'] = { name = 'Pizza Maker', payment = 75 },
        ['2'] = { name = 'Head Pizza Chef', payment = 100 },
        ['3'] = { name = 'Shift Manager', payment = 125 },
        ['4'] = { name = 'Owner', isboss = true, payment = 150 },
    },
},
tacofarmer = {
    label = 'Taco Farmer',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 50 },
        ['1'] = { name = 'Taco Maker', payment = 75 },
        ['2'] = { name = 'Head Taco Chef', payment = 100 },
        ['3'] = { name = 'Shift Manager', payment = 125 },
        ['4'] = { name = 'Owner', isboss = true, payment = 150 },
    },
},
snrbuns = {
    label = 'Snr Buns',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 50 },
        ['1'] = { name = 'Bun Maker', payment = 75 },
        ['2'] = { name = 'Head Bun Chef', payment = 100 },
        ['3'] = { name = 'Shift Manager', payment = 125 },
        ['4'] = { name = 'Owner', isboss = true, payment = 150 },
    },
}
```

If you are using qb-inventory, add the following items to your `qb-core/shared/items.lua`:

```lua
-- Food Truck - Ingredients
burgerpatty = { name = 'burgerpatty', label = 'Beef Patty', weight = 200, type = 'item', image = 'burgerpatty.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Premium beef patty for gourmet burgers' },
nori_sheets = { name = 'nori_sheets', label = 'Nori Seaweed Sheets', weight = 50, type = 'item', image = 'nori_sheets.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Dried seaweed sheets for Asian fusion dishes' },
rice = { name = 'rice', label = 'Rice', weight = 100, type = 'item', image = 'rice.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Clean Japanese rice' },
hot_sauce = { name = 'hot_sauce', label = 'Hot Sauce', weight = 100, type = 'item', image = 'hot_sauce.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Sweet and savory Japanese sauce' },
pickles = { name = 'pickles', label = 'Pickles', weight = 50, type = 'item', image = 'pickles.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Sweet and tangy pickle slices' },
chicken_wings_raw = { name = 'chicken_wings_raw', label = 'Raw Chicken Wings', weight = 300, type = 'item', image = 'chicken_wings_raw.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Fresh chicken wings ready to cook' },
salt = { name = 'salt', label = 'Salt', weight = 10, type = 'item', image = 'salt.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Coarse salt for seasoning' },
matcha = { name = 'matcha', label = 'Matcha Powder', weight = 50, type = 'item', image = 'matcha.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Premium Japanese green tea powder' },
lettuce = { name = 'lettuce', label = 'Lettuce', weight = 50, type = 'item', image = 'lettuce.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Fresh lettuce leaves' },
raw_sushi = { name = 'raw_sushi', label = 'Raw Sushi', weight = 200, type = 'item', image = 'raw_sushi.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Fresh sushi ingredients' },
dough = { name = 'dough', label = 'Dough', weight = 400, type = 'item', image = 'dough.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Clean dough ready for baking!' },
cooking_chocolate = { name = 'cooking_chocolate', label = 'Cooking Chocolate', weight = 400, type = 'item', image = 'cooking_chocolate.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Chocolate filling for pastries' },
coffee_bean = { name = 'coffee_bean', label = 'Coffee Bean', weight = 400, type = 'item', image = 'coffee_bean.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Fresh coffee beans for brewing' },
chickenbreast = { name = 'chickenbreast', label = 'Chicken Breast', weight = 250, type = 'item', image = 'chickenbreast.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Fresh chicken breast for cooking' },
burger_onion = { name = 'burger_onion', label = 'Onion', weight = 100, type = 'item', image = 'burger_onion.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Fresh onion for burgers' },
burger_icecream_empty = { name = 'burger_icecream_empty', label = 'Empty Cup', weight = 50, type = 'item', image = 'burger_icecream_empty.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Empty cup for drinks and desserts' },
frozennuggets = { name = 'frozennuggets', label = 'Frozen Nuggets', weight = 200, type = 'item', image = 'frozennuggets.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Frozen chicken nuggets ready to fry' },
sirloin_steak = { name = 'sirloin_steak', label = 'Raw Sirloin Steak', weight = 300, type = 'item', image = 'sirloin_steak.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Premium raw sirloin steak' },
slicedpotato = { name = 'slicedpotato', label = 'Sliced Potato', weight = 150, type = 'item', image = 'slicedpotato.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Freshly sliced potatoes ready to cook' },
tomato = { name = 'tomato', label = 'Tomato', weight = 500, type = 'item', image = 'tomato.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A fresh tomato, great for salads and sauces.' },
pepperoni = { name = 'pepperoni', label = 'Pepperoni', weight = 100, type = 'item', image = 'pepperoni.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Sliced pepperoni for pizzas' },
fish = { name = 'fish', label = 'Fish', weight = 1000, type = 'item', image = 'fish.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Freshly caught fish.' },
beef = { name = 'beef', label = 'Beef', weight = 1000, type = 'item', image = 'beef.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Raw beef, great for cooking.' },
taco_shell = { name = 'taco_shell', label = 'Taco Shell', weight = 50, type = 'item', image = 'taco_shell.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Crispy taco shells ready to fill' },
rawhotdog = { name = 'rawhotdog', label = 'Raw Hot Dog', weight = 150, type = 'item', image = 'rawhotdog.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Raw hot dog sausage ready to cook' },
blueberry = { name = 'blueberry', label = 'Blueberry', weight = 50, type = 'item', image = 'blueberry.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'Fresh blueberries, perfect for baking or snacking.' },
milk = { name = 'milk', label = 'Milk', weight = 1000, type = 'item', image = 'milk.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Fresh dairy product.' },

-- Wig Wam Food Truck - Finished Foods
ramen = { name = 'ramen', label = 'Tonkotsu Ramen', weight = 500, type = 'item', image = 'ramen.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Delicious tonkotsu ramen with wagyu and special toppings' },
teriyaki_wings = { name = 'teriyaki_wings', label = 'Teriyaki Glazed Wings', weight = 350, type = 'item', image = 'teriyaki_wings.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crispy chicken wings glazed with teriyaki sauce' },
matcha_milkshake = { name = 'matcha_milkshake', label = 'Matcha Milkshake', weight = 400, type = 'item', image = 'matcha_milkshake.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Creamy matcha and vanilla ice cream shake' },
tokyo_fusion_burger = { name = 'tokyo_fusion_burger', label = 'Tokyo Fusion Burger', weight = 550, type = 'item', image = 'tokyo_fusion_burger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Double wagyu patty with nori and special sauce' },
doublechicken_burger = { name = 'doublechicken_burger', label = 'Double Chicken Burger', weight = 500, type = 'item', image = 'doublechicken_burger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Double chicken patty burger with fresh toppings' },
sushi = { name = 'sushi', label = 'Assorted Sushi Platter', weight = 400, type = 'item', image = 'sushi.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Fresh assorted sushi rolls and nigiri'},

-- Bean Machine Food Truck - Finished Foods
muffin = { name = 'muffin', label = 'Chocolate Muffin', weight = 250, type = 'item', image = 'muffin.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Freshly baked chocolate chip muffin' },
croissant = { name = 'croissant', label = 'Butter Croissant', weight = 200, type = 'item', image = 'croissant.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Flaky buttery croissant with chocolate filling' },
bean_coffee2 = { name = 'bean_coffee2', label = 'Classic Bean Coffee', weight = 350, type = 'item', image = 'bean_coffee2.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Rich and smooth coffee made from premium beans' },
bean_carmalcoffee = { name = 'bean_carmalcoffee', label = 'Caramel Coffee', weight = 400, type = 'item', image = 'bean_carmalcoffee.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Sweet caramel-flavored coffee with a chocolate twist' },

-- Burgershot Food Truck - Finished Foods
burger_shotrings = { name = 'burger_shotrings', label = 'Shot Rings', weight = 200, type = 'item', image = 'burger_shotrings.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crispy onion rings' },
burger_icecream = { name = 'burger_icecream', label = 'Ice Cream', weight = 300, type = 'item', image = 'burger_icecream.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Delicious ice cream' },
burger_heartstopper = { name = 'burger_heartstopper', label = 'Heart Stopper', weight = 700, type = 'item', image = 'burger_heartstopper.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Massive triple patty burger with all the fixings' },
burger_chickenwrap = { name = 'burger_chickenwrap', label = 'Chicken Wrap', weight = 400, type = 'item', image = 'burger_chickenwrap.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Grilled chicken wrap with fresh veggies' },
burger_bleeder = { name = 'burger_bleeder', label = 'Bleeder Burger', weight = 500, type = 'item', image = 'burger_bleeder.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Juicy double burger with cheese and toppings' },
burger_softdrink = { name = 'burger_softdrink', label = 'Soft Drink', weight = 350, type = 'item', image = 'burger_softdrink.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Refreshing soft drink' },
burger_rimjob = { name = 'burger_rimjob', label = 'Rim Job', weight = 500, type = 'item', image = 'burger_rimjob.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Special donut with unique toppings' },
burger_shotnuggets = { name = 'burger_shotnuggets', label = 'Shot Nuggets', weight = 250, type = 'item', image = 'burger_shotnuggets.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crispy nuggets' },
cone_chocolate = { name = 'cone_chocolate', label = 'Chocolate Ice Cream Cone', weight = 150, type = 'item', image = 'cone_chocolate.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Delicious chocolate ice cream in a cone' },
cone_blueberry = { name = 'cone_blueberry', label = 'Blueberry Ice Cream Cone', weight = 150, type = 'item', image = 'cone_blueberry.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Sweet blueberry ice cream in a cone' },
chickenburger = { name = 'chickenburger', label = 'Chicken Burger', weight = 450, type = 'item', image = 'chickenburger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Juicy chicken patty burger' },
chicken_breastsandwich = { name = 'chicken_breastsandwich', label = 'Chicken Breast Sandwich', weight = 400, type = 'item', image = 'chicken_breastsandwich.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Grilled chicken breast sandwich' },
cheeseburger = { name = 'cheeseburger', label = 'Cheeseburger', weight = 450, type = 'item', image = 'cheeseburger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Classic cheeseburger with all toppings' },
bltsandwich = { name = 'bltsandwich', label = 'BLT Sandwich', weight = 350, type = 'item', image = 'bltsandwich.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Bacon, lettuce, and tomato sandwich' },

-- Cluckin' Bell Food Truck - Finished Foods
nuggets = { name = 'nuggets', label = 'Chicken Nuggets', weight = 250, type = 'item', image = 'nuggets.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crispy golden chicken nuggets' },
pickleburger = { name = 'pickleburger', label = 'Pickle Burger', weight = 450, type = 'item', image = 'pickleburger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Burger with extra pickles and special sauce' },
burger_chickenmelt = { name = 'burger_chickenmelt', label = 'Chicken Melt', weight = 400, type = 'item', image = 'burger_chickenmelt.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Melted cheese chicken sandwich' },
wings = { name = 'wings', label = 'Chicken Wings', weight = 350, type = 'item', image = 'wings.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crispy chicken wings' },

-- Greasy Joes Food Truck - Finished Foods
bellini = { name = 'bellini', label = 'Bellini Cocktail', weight = 300, type = 'item', image = 'bellini.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Classic Italian sparkling cocktail' },
beerglass3 = { name = 'beerglass3', label = 'Cold Beer', weight = 350, type = 'item', image = 'beerglass3.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Ice cold beer in a glass' },
bacon_cheeseburger = { name = 'bacon_cheeseburger', label = 'Bacon Cheeseburger', weight = 550, type = 'item', image = 'bacon_cheeseburger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Juicy burger with bacon and cheese' },
steak_potato = { name = 'steak_potato', label = 'Steak & Potato', weight = 650, type = 'item', image = 'steak_potato.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Grilled sirloin steak with roasted potatoes' },
sirloinsteak = { name = 'sirloinsteak', label = 'Sirloin Steak', weight = 500, type = 'item', image = 'sirloinsteak.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Perfectly grilled sirloin steak' },
steakburger = { name = 'steakburger', label = 'Steak Burger', weight = 600, type = 'item', image = 'steakburger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Premium steak burger with toppings' },

-- Pizzeria Food Truck - Finished Foods
basket_fries = { name = 'basket_fries', label = 'Basket of Fries', weight = 300, type = 'item', image = 'basket_fries.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crispy golden fries in a basket' },
ppizza = { name = 'ppizza', label = 'Pepperoni Pizza', weight = 800, type = 'item', image = 'ppizza.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Classic pepperoni pizza with melted cheese' },
pmushroomspizza = { name = 'pmushroomspizza', label = 'Mushroom Pizza', weight = 800, type = 'item', image = 'pmushroomspizza.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Delicious mushroom pizza with fresh toppings' },
ppizzaslice = { name = 'ppizzaslice', label = 'Pizza Slice', weight = 150, type = 'item', image = 'ppizzaslice.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A single slice of pizza' },
pvegpizza = { name = 'pvegpizza', label = 'Vegetarian Pizza', weight = 800, type = 'item', image = 'pvegpizza.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Fresh vegetarian pizza with corn, tomato, and mushrooms' },
wine_barbera = { name = 'wine_barbera', label = 'Barbera Wine', weight = 400, type = 'item', image = 'wine_barbera.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Italian Barbera red wine' },
wine_dolcetto = { name = 'wine_dolcetto', label = 'Dolcetto Wine', weight = 400, type = 'item', image = 'wine_dolcetto.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Italian Dolcetto red wine' },

-- Taco Farmer Food Truck - Finished Foods
burrito = { name = 'burrito', label = 'Burrito', weight = 500, type = 'item', image = 'burrito.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Large burrito filled with meat and vegetables' },
gin_and_tonic = { name = 'gin_and_tonic', label = 'Gin and Tonic', weight = 350, type = 'item', image = 'gin_and_tonic.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Classic gin and tonic cocktail' },
hotdog_taco = { name = 'hotdog_taco', label = 'Hot Dog Taco', weight = 300, type = 'item', image = 'hotdog_taco.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Hot dog served in a taco shell' },
sprite = { name = 'sprite', label = 'Sprite', weight = 350, type = 'item', image = 'sprite.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Refreshing lemon-lime soda' },
sprunk = { name = 'sprunk', label = 'Sprunk', weight = 350, type = 'item', image = 'sprunk.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Classic Sprunk soda' },
sprunklight = { name = 'sprunklight', label = 'Sprunk Light', weight = 350, type = 'item', image = 'sprunklight.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Light version of Sprunk soda' },
taco_beef = { name = 'taco_beef', label = 'Beef Taco', weight = 250, type = 'item', image = 'taco_beef.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crunchy taco with seasoned beef' },
taco_chicken = { name = 'taco_chicken', label = 'Chicken Taco', weight = 250, type = 'item', image = 'taco_chicken.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crunchy taco with grilled chicken' },
taco_fish = { name = 'taco_fish', label = 'Fish Taco', weight = 250, type = 'item', image = 'taco_fish.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crunchy taco with fried fish' },

-- Snr Buns Food Truck - Finished Foods
cheese_fries = { name = 'cheese_fries', label = 'Cheese Fries', weight = 300, type = 'item', image = 'cheese_fries.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Crispy fries topped with melted cheese.' },
cheese_burger_fries = { name = 'cheese_burger_fries', label = 'Cheeseburger & Fries Combo', weight = 700, type = 'item', image = 'cheese_burger_fries.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Cheeseburger served with a side of fries.' },
tripleburger = { name = 'tripleburger', label = 'Triple Burger', weight = 800, type = 'item', image = 'tripleburger.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Triple patty cheeseburger with all the fixings.' },

-- Bean Machine Additions
cheesecake = { name = 'cheesecake', label = 'Cheesecake', weight = 400, type = 'item', image = 'cheesecake.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A rich and creamy cheesecake dessert.' },
cb_donut = { name = 'cb_donut', label = 'Chocolate Donut', weight = 150, type = 'item', image = 'cb_donut.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A white milk donut topped with chocolate.' },
cremecaramel = { name = 'cremecaramel', label = 'Crème Caramel', weight = 350, type = 'item', image = 'cremecaramel.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A smooth and creamy caramel custard dessert.' },
cake_chocolate = { name = 'cake_chocolate', label = 'Chocolate Cake', weight = 500, type = 'item', image = 'cake_chocolate.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A moist and decadent chocolate cake.' },
cakepop = { name = 'cakepop', label = 'Cake Pop', weight = 100, type = 'item', image = 'cakepop.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A sweet cake pop treat on a stick.' },
blueberry_pie = { name = 'blueberry_pie', label = 'Blueberry Pie', weight = 450, type = 'item', image = 'blueberry_pie.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A delicious pie filled with fresh blueberries.' },
brownies = { name = 'brownies', label = 'Brownies', weight = 300, type = 'item', image = 'brownies.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Fudgy chocolate brownies.' },
baquette = { name = 'baquette', label = 'Baguette', weight = 250, type = 'item', image = 'baquette.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A classic French baguette.' },

-- Business Tablet
foodtruck_tablet = {
    name = 'foodtruck_tablet',
    label = 'Food Truck Tablet',
    weight = 700,
    type = 'item',
    image = 'foodtruck_tablet.png',
    unique = true,
    useable = true,
    shouldClose = true,
    description = 'A business tablet for managing food truck orders, logs, upgrades, and bank activity.',
},
```
{% endtab %}

{% tab title="ESX (other inventories)" %}
If using the ESX framework, run the following SQL in your database manager.

Jobs:

```sql
INSERT INTO `jobs` (`name`, `label`) VALUES
('wigwam', 'Wig Wam Food Truck'),
('beanmachine', 'Bean Machine'),
('burgershot', 'Burgershot'),
('cluckinbell', 'Cluckin\' Bell'),
('greasyjoes', 'Greasy Joes'),
('pizzeria', 'Pizzeria'),
('tacofarmer', 'Taco Farmer'),
('snrbuns', 'Snr Buns');

INSERT INTO `job_grades` (`job_name`, `grade`, `name`, `label`, `salary`, `skin_male`, `skin_female`) VALUES
-- Wig Wam Food Truck
('wigwam', 0, 'trainee', 'Trainee', 50, '{}', '{}'),
('wigwam', 1, 'cook', 'Cook', 75, '{}', '{}'),
('wigwam', 2, 'chef', 'Chef', 100, '{}', '{}'),
('wigwam', 3, 'headchef', 'Head Chef', 125, '{}', '{}'),
('wigwam', 4, 'owner', 'Owner', 150, '{}', '{}'),

-- Bean Machine Food Truck
('beanmachine', 0, 'trainee', 'Trainee Barista', 50, '{}', '{}'),
('beanmachine', 1, 'barista', 'Barista', 75, '{}', '{}'),
('beanmachine', 2, 'seniorbarista', 'Senior Barista', 100, '{}', '{}'),
('beanmachine', 3, 'shiftsupervisor', 'Shift Supervisor', 125, '{}', '{}'),
('beanmachine', 4, 'manager', 'Manager', 150, '{}', '{}'),

-- Burger Shot Food Truck
('burgershot', 0, 'trainee', 'Trainee', 50, '{}', '{}'),
('burgershot', 1, 'cook', 'Cook', 75, '{}', '{}'),
('burgershot', 2, 'grillmaster', 'Grill Master', 100, '{}', '{}'),
('burgershot', 3, 'shiftmanager', 'Shift Manager', 125, '{}', '{}'),
('burgershot', 4, 'owner', 'Owner', 150, '{}', '{}'),

-- Cluckin' Bell Food Truck
('cluckinbell', 0, 'trainee', 'Trainee', 50, '{}', '{}'),
('cluckinbell', 1, 'cook', 'Cook', 75, '{}', '{}'),
('cluckinbell', 2, 'fryermaster', 'Fryer Master', 100, '{}', '{}'),
('cluckinbell', 3, 'shiftmanager', 'Shift Manager', 125, '{}', '{}'),
('cluckinbell', 4, 'owner', 'Owner', 150, '{}', '{}'),

-- Greasy Joes Food Truck
('greasyjoes', 0, 'trainee', 'Trainee', 50, '{}', '{}'),
('greasyjoes', 1, 'cook', 'Cook', 75, '{}', '{}'),
('greasyjoes', 2, 'grillmaster', 'Grill Master', 100, '{}', '{}'),
('greasyjoes', 3, 'shiftmanager', 'Shift Manager', 125, '{}', '{}'),
('greasyjoes', 4, 'owner', 'Owner', 150, '{}', '{}'),

-- Pizzeria Food Truck
('pizzeria', 0, 'trainee', 'Trainee', 50, '{}', '{}'),
('pizzeria', 1, 'pizzamaker', 'Pizza Maker', 75, '{}', '{}'),
('pizzeria', 2, 'headpizzachef', 'Head Pizza Chef', 100, '{}', '{}'),
('pizzeria', 3, 'shiftmanager', 'Shift Manager', 125, '{}', '{}'),
('pizzeria', 4, 'owner', 'Owner', 150, '{}', '{}'),

-- Taco Farmer Food Truck
('tacofarmer', 0, 'trainee', 'Trainee', 50, '{}', '{}'),
('tacofarmer', 1, 'tacomaker', 'Taco Maker', 75, '{}', '{}'),
('tacofarmer', 2, 'headtacochef', 'Head Taco Chef', 100, '{}', '{}'),
('tacofarmer', 3, 'shiftmanager', 'Shift Manager', 125, '{}', '{}'),
('tacofarmer', 4, 'owner', 'Owner', 150, '{}', '{}'),

-- Snr Buns Food Truck
('snrbuns', 0, 'trainee', 'Trainee', 50, '{}', '{}'),
('snrbuns', 1, 'bunmaker', 'Bun Maker', 75, '{}', '{}'),
('snrbuns', 2, 'headbunchef', 'Head Bun Chef', 100, '{}', '{}'),
('snrbuns', 3, 'shiftmanager', 'Shift Manager', 125, '{}', '{}'),
('snrbuns', 4, 'owner', 'Owner', 150, '{}', '{}');
```

If you are using any other inventory with ESX, add the items with the following SQL:

```sql
INSERT IGNORE INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`) VALUES
('burgerpatty', 'Beef Patty', 200, 0, 1),
('nori_sheets', 'Nori Seaweed Sheets', 50, 0, 1),
('rice', 'Rice', 100, 0, 1),
('hot_sauce', 'Hot Sauce', 100, 0, 1),
('pickles', 'Pickles', 50, 0, 1),
('chicken_wings_raw', 'Raw Chicken Wings', 300, 0, 1),
('salt', 'Salt', 10, 0, 1),
('matcha', 'Matcha Powder', 50, 0, 1),
('lettuce', 'Lettuce', 50, 0, 1),
('raw_sushi', 'Raw Sushi', 200, 0, 1),
('dough', 'Dough', 400, 0, 1),
('cooking_chocolate', 'Cooking Chocolate', 400, 0, 1),
('coffee_bean', 'Coffee Bean', 400, 0, 1),
('chickenbreast', 'Chicken Breast', 250, 0, 1),
('burger_onion', 'Onion', 100, 0, 1),
('burger_icecream_empty', 'Empty Cup', 50, 0, 1),
('frozennuggets', 'Frozen Nuggets', 200, 0, 1),
('sirloin_steak', 'Raw Sirloin Steak', 300, 0, 1),
('slicedpotato', 'Sliced Potato', 150, 0, 1),
('tomato', 'Tomato', 500, 0, 1),
('pepperoni', 'Pepperoni', 100, 0, 1),
('fish', 'Fish', 1000, 0, 1),
('beef', 'Beef', 1000, 0, 1),
('taco_shell', 'Taco Shell', 50, 0, 1),
('rawhotdog', 'Raw Hot Dog', 150, 0, 1),
('blueberry', 'Blueberry', 50, 0, 1),
('milk', 'Milk', 500, 0, 1),

('ramen', 'Tonkotsu Ramen', 500, 0, 1),
('teriyaki_wings', 'Teriyaki Glazed Wings', 350, 0, 1),
('matcha_milkshake', 'Matcha Milkshake', 400, 0, 1),
('tokyo_fusion_burger', 'Tokyo Fusion Burger', 550, 0, 1),
('doublechicken_burger', 'Double Chicken Burger', 500, 0, 1),
('sushi', 'Assorted Sushi Platter', 400, 0, 1),

('muffin', 'Chocolate Muffin', 250, 0, 1),
('croissant', 'Butter Croissant', 200, 0, 1),
('bean_coffee2', 'Classic Bean Coffee', 350, 0, 1),
('bean_carmalcoffee', 'Caramel Coffee', 400, 0, 1),

('burger_shotrings', 'Shot Rings', 200, 0, 1),
('burger_icecream', 'Ice Cream', 300, 0, 1),
('burger_heartstopper', 'Heart Stopper', 700, 0, 1),
('burger_chickenwrap', 'Chicken Wrap', 400, 0, 1),
('burger_bleeder', 'Bleeder Burger', 500, 0, 1),
('burger_softdrink', 'Soft Drink', 350, 0, 1),
('burger_rimjob', 'Rim Job', 500, 0, 1),
('burger_shotnuggets', 'Shot Nuggets', 250, 0, 1),
('cone_chocolate', 'Chocolate Ice Cream Cone', 150, 0, 1),
('cone_blueberry', 'Blueberry Ice Cream Cone', 150, 0, 1),
('chickenburger', 'Chicken Burger', 450, 0, 1),
('chicken_breastsandwich', 'Chicken Breast Sandwich', 400, 0, 1),
('cheeseburger', 'Cheeseburger', 450, 0, 1),
('bltsandwich', 'BLT Sandwich', 350, 0, 1),

('nuggets', 'Chicken Nuggets', 250, 0, 1),
('pickleburger', 'Pickle Burger', 450, 0, 1),
('burger_chickenmelt', 'Chicken Melt', 400, 0, 1),
('wings', 'Chicken Wings', 350, 0, 1),

('bellini', 'Bellini Cocktail', 300, 0, 1),
('beerglass3', 'Cold Beer', 350, 0, 1),
('bacon_cheeseburger', 'Bacon Cheeseburger', 550, 0, 1),
('steak_potato', 'Steak & Potato', 650, 0, 1),
('sirloinsteak', 'Sirloin Steak', 500, 0, 1),
('steakburger', 'Steak Burger', 600, 0, 1),

('basket_fries', 'Basket of Fries', 300, 0, 1),
('ppizza', 'Pepperoni Pizza', 800, 0, 1),
('pmushroomspizza', 'Mushroom Pizza', 800, 0, 1),
('ppizzaslice', 'Pizza Slice', 150, 0, 1),
('pvegpizza', 'Vegetarian Pizza', 800, 0, 1),
('wine_barbera', 'Barbera Wine', 400, 0, 1),
('wine_dolcetto', 'Dolcetto Wine', 400, 0, 1),

('burrito', 'Burrito', 500, 0, 1),
('gin_and_tonic', 'Gin and Tonic', 350, 0, 1),
('hotdog_taco', 'Hot Dog Taco', 300, 0, 1),
('sprite', 'Sprite', 350, 0, 1),
('sprunk', 'Sprunk', 350, 0, 1),
('sprunklight', 'Sprunk Light', 350, 0, 1),
('taco_beef', 'Beef Taco', 250, 0, 1),
('taco_chicken', 'Chicken Taco', 250, 0, 1),
('taco_fish', 'Fish Taco', 250, 0, 1),

('cheese_fries', 'Cheese Fries', 300, 0, 1),
('cheese_burger_fries', 'Cheeseburger & Fries Combo', 700, 0, 1),
('tripleburger', 'Triple Burger', 800, 0, 1),

('cheesecake', 'Cheesecake', 400, 0, 1),
('cb_donut', 'Chocolate Donut', 150, 0, 1),
('cremecaramel', 'Crème Caramel', 350, 0, 1),
('cake_chocolate', 'Chocolate Cake', 500, 0, 1),
('cakepop', 'Cake Pop', 100, 0, 1),
('blueberry_pie', 'Blueberry Pie', 450, 0, 1),
('brownies', 'Brownies', 300, 0, 1),
('baquette', 'Baguette', 250, 0, 1),

('foodtruck_tablet', 'Food Truck Tablet', 700);
```
{% endtab %}

{% tab title="ox_inventory" %}
If you are using ox\_inventory, skip the QBCore item list and the ESX items SQL and add all of the food truck items below to your `ox_inventory/data/items.lua` instead. The resource registers every usable item (the tablet and all consumables) with your framework and handles eating/drinking removal itself, so keep the definitions exactly in this form, don't add `consume`, `client`, or `server` tables.

```lua
-- Food Truck - Ingredients
['burgerpatty'] = { label = 'Beef Patty', weight = 200, description = 'Premium beef patty for gourmet burgers' },
['nori_sheets'] = { label = 'Nori Seaweed Sheets', weight = 50, description = 'Dried seaweed sheets for Asian fusion dishes' },
['rice'] = { label = 'Rice', weight = 100, description = 'Clean Japanese rice' },
['hot_sauce'] = { label = 'Hot Sauce', weight = 100, description = 'Sweet and savory Japanese sauce' },
['pickles'] = { label = 'Pickles', weight = 50, description = 'Sweet and tangy pickle slices' },
['chicken_wings_raw'] = { label = 'Raw Chicken Wings', weight = 300, description = 'Fresh chicken wings ready to cook' },
['salt'] = { label = 'Salt', weight = 10, description = 'Coarse salt for seasoning' },
['matcha'] = { label = 'Matcha Powder', weight = 50, description = 'Premium Japanese green tea powder' },
['lettuce'] = { label = 'Lettuce', weight = 50, description = 'Fresh lettuce leaves' },
['raw_sushi'] = { label = 'Raw Sushi', weight = 200, description = 'Fresh sushi ingredients' },
['dough'] = { label = 'Dough', weight = 400, description = 'Clean dough ready for baking!' },
['cooking_chocolate'] = { label = 'Cooking Chocolate', weight = 400, description = 'Chocolate filling for pastries' },
['coffee_bean'] = { label = 'Coffee Bean', weight = 400, description = 'Fresh coffee beans for brewing' },
['chickenbreast'] = { label = 'Chicken Breast', weight = 250, description = 'Fresh chicken breast for cooking' },
['burger_onion'] = { label = 'Onion', weight = 100, description = 'Fresh onion for burgers' },
['burger_icecream_empty'] = { label = 'Empty Cup', weight = 50, description = 'Empty cup for drinks and desserts' },
['frozennuggets'] = { label = 'Frozen Nuggets', weight = 200, description = 'Frozen chicken nuggets ready to fry' },
['sirloin_steak'] = { label = 'Raw Sirloin Steak', weight = 300, description = 'Premium raw sirloin steak' },
['slicedpotato'] = { label = 'Sliced Potato', weight = 150, description = 'Freshly sliced potatoes ready to cook' },
['tomato'] = { label = 'Tomato', weight = 500, description = 'A fresh tomato, great for salads and sauces.' },
['pepperoni'] = { label = 'Pepperoni', weight = 100, description = 'Sliced pepperoni for pizzas' },
['fish'] = { label = 'Fish', weight = 1000, description = 'Freshly caught fish.' },
['beef'] = { label = 'Beef', weight = 1000, description = 'Raw beef, great for cooking.' },
['taco_shell'] = { label = 'Taco Shell', weight = 50, description = 'Crispy taco shells ready to fill' },
['rawhotdog'] = { label = 'Raw Hot Dog', weight = 150, description = 'Raw hot dog sausage ready to cook' },
['blueberry'] = { label = 'Blueberry', weight = 50, description = 'Fresh blueberries, perfect for baking or snacking.' },
['milk'] = { label = 'Milk', weight = 1000, description = 'Fresh dairy product.' },

-- Wig Wam Food Truck - Finished Foods
['ramen'] = { label = 'Tonkotsu Ramen', weight = 500, description = 'Delicious tonkotsu ramen with wagyu and special toppings' },
['teriyaki_wings'] = { label = 'Teriyaki Glazed Wings', weight = 350, description = 'Crispy chicken wings glazed with teriyaki sauce' },
['matcha_milkshake'] = { label = 'Matcha Milkshake', weight = 400, description = 'Creamy matcha and vanilla ice cream shake' },
['tokyo_fusion_burger'] = { label = 'Tokyo Fusion Burger', weight = 550, description = 'Double wagyu patty with nori and special sauce' },
['doublechicken_burger'] = { label = 'Double Chicken Burger', weight = 500, description = 'Double chicken patty burger with fresh toppings' },
['sushi'] = { label = 'Assorted Sushi Platter', weight = 400, description = 'Fresh assorted sushi rolls and nigiri' },

-- Bean Machine Food Truck - Finished Foods
['muffin'] = { label = 'Chocolate Muffin', weight = 250, description = 'Freshly baked chocolate chip muffin' },
['croissant'] = { label = 'Butter Croissant', weight = 200, description = 'Flaky buttery croissant with chocolate filling' },
['bean_coffee2'] = { label = 'Classic Bean Coffee', weight = 350, description = 'Rich and smooth coffee made from premium beans' },
['bean_carmalcoffee'] = { label = 'Caramel Coffee', weight = 400, description = 'Sweet caramel-flavored coffee with a chocolate twist' },

-- Burgershot Food Truck - Finished Foods
['burger_shotrings'] = { label = 'Shot Rings', weight = 200, description = 'Crispy onion rings' },
['burger_icecream'] = { label = 'Ice Cream', weight = 300, description = 'Delicious ice cream' },
['burger_heartstopper'] = { label = 'Heart Stopper', weight = 700, description = 'Massive triple patty burger with all the fixings' },
['burger_chickenwrap'] = { label = 'Chicken Wrap', weight = 400, description = 'Grilled chicken wrap with fresh veggies' },
['burger_bleeder'] = { label = 'Bleeder Burger', weight = 500, description = 'Juicy double burger with cheese and toppings' },
['burger_softdrink'] = { label = 'Soft Drink', weight = 350, description = 'Refreshing soft drink' },
['burger_rimjob'] = { label = 'Rim Job', weight = 500, description = 'Special donut with unique toppings' },
['burger_shotnuggets'] = { label = 'Shot Nuggets', weight = 250, description = 'Crispy nuggets' },
['cone_chocolate'] = { label = 'Chocolate Ice Cream Cone', weight = 150, description = 'Delicious chocolate ice cream in a cone' },
['cone_blueberry'] = { label = 'Blueberry Ice Cream Cone', weight = 150, description = 'Sweet blueberry ice cream in a cone' },
['chickenburger'] = { label = 'Chicken Burger', weight = 450, description = 'Juicy chicken patty burger' },
['chicken_breastsandwich'] = { label = 'Chicken Breast Sandwich', weight = 400, description = 'Grilled chicken breast sandwich' },
['cheeseburger'] = { label = 'Cheeseburger', weight = 450, description = 'Classic cheeseburger with all toppings' },
['bltsandwich'] = { label = 'BLT Sandwich', weight = 350, description = 'Bacon, lettuce, and tomato sandwich' },

-- Cluckin' Bell Food Truck - Finished Foods
['nuggets'] = { label = 'Chicken Nuggets', weight = 250, description = 'Crispy golden chicken nuggets' },
['pickleburger'] = { label = 'Pickle Burger', weight = 450, description = 'Burger with extra pickles and special sauce' },
['burger_chickenmelt'] = { label = 'Chicken Melt', weight = 400, description = 'Melted cheese chicken sandwich' },
['wings'] = { label = 'Chicken Wings', weight = 350, description = 'Crispy chicken wings' },

-- Greasy Joes Food Truck - Finished Foods
['bellini'] = { label = 'Bellini Cocktail', weight = 300, description = 'Classic Italian sparkling cocktail' },
['beerglass3'] = { label = 'Cold Beer', weight = 350, description = 'Ice cold beer in a glass' },
['bacon_cheeseburger'] = { label = 'Bacon Cheeseburger', weight = 550, description = 'Juicy burger with bacon and cheese' },
['steak_potato'] = { label = 'Steak & Potato', weight = 650, description = 'Grilled sirloin steak with roasted potatoes' },
['sirloinsteak'] = { label = 'Sirloin Steak', weight = 500, description = 'Perfectly grilled sirloin steak' },
['steakburger'] = { label = 'Steak Burger', weight = 600, description = 'Premium steak burger with toppings' },

-- Pizzeria Food Truck - Finished Foods
['basket_fries'] = { label = 'Basket of Fries', weight = 300, description = 'Crispy golden fries in a basket' },
['ppizza'] = { label = 'Pepperoni Pizza', weight = 800, description = 'Classic pepperoni pizza with melted cheese' },
['pmushroomspizza'] = { label = 'Mushroom Pizza', weight = 800, description = 'Delicious mushroom pizza with fresh toppings' },
['ppizzaslice'] = { label = 'Pizza Slice', weight = 150, description = 'A single slice of pizza' },
['pvegpizza'] = { label = 'Vegetarian Pizza', weight = 800, description = 'Fresh vegetarian pizza with corn, tomato, and mushrooms' },
['wine_barbera'] = { label = 'Barbera Wine', weight = 400, description = 'Italian Barbera red wine' },
['wine_dolcetto'] = { label = 'Dolcetto Wine', weight = 400, description = 'Italian Dolcetto red wine' },

-- Taco Farmer Food Truck - Finished Foods
['burrito'] = { label = 'Burrito', weight = 500, description = 'Large burrito filled with meat and vegetables' },
['gin_and_tonic'] = { label = 'Gin and Tonic', weight = 350, description = 'Classic gin and tonic cocktail' },
['hotdog_taco'] = { label = 'Hot Dog Taco', weight = 300, description = 'Hot dog served in a taco shell' },
['sprite'] = { label = 'Sprite', weight = 350, description = 'Refreshing lemon-lime soda' },
['sprunk'] = { label = 'Sprunk', weight = 350, description = 'Classic Sprunk soda' },
['sprunklight'] = { label = 'Sprunk Light', weight = 350, description = 'Light version of Sprunk soda' },
['taco_beef'] = { label = 'Beef Taco', weight = 250, description = 'Crunchy taco with seasoned beef' },
['taco_chicken'] = { label = 'Chicken Taco', weight = 250, description = 'Crunchy taco with grilled chicken' },
['taco_fish'] = { label = 'Fish Taco', weight = 250, description = 'Crunchy taco with fried fish' },

-- Snr Buns Food Truck - Finished Foods
['cheese_fries'] = { label = 'Cheese Fries', weight = 300, description = 'Crispy fries topped with melted cheese.' },
['cheese_burger_fries'] = { label = 'Cheeseburger & Fries Combo', weight = 700, description = 'Cheeseburger served with a side of fries.' },
['tripleburger'] = { label = 'Triple Burger', weight = 800, description = 'Triple patty cheeseburger with all the fixings.' },

-- Bean Machine Additions
['cheesecake'] = { label = 'Cheesecake', weight = 400, description = 'A rich and creamy cheesecake dessert.' },
['cb_donut'] = { label = 'Chocolate Donut', weight = 150, description = 'A white milk donut topped with chocolate.' },
['cremecaramel'] = { label = 'Crème Caramel', weight = 350, description = 'A smooth and creamy caramel custard dessert.' },
['cake_chocolate'] = { label = 'Chocolate Cake', weight = 500, description = 'A moist and decadent chocolate cake.' },
['cakepop'] = { label = 'Cake Pop', weight = 100, description = 'A sweet cake pop treat on a stick.' },
['blueberry_pie'] = { label = 'Blueberry Pie', weight = 450, description = 'A delicious pie filled with fresh blueberries.' },
['brownies'] = { label = 'Brownies', weight = 300, description = 'Fudgy chocolate brownies.' },
['baquette'] = { label = 'Baguette', weight = 250, description = 'A classic French baguette.' },

-- Business Tablet
['foodtruck_tablet'] = { label = 'Food Truck Tablet', weight = 700, stack = false, close = true, description = 'A business tablet for managing food truck orders, logs, upgrades, and bank activity.' },
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Using the `foodtruck_tablet` item opens the same UI as the `/foodtrucktablet` command.
{% endhint %}

**5. Restart Server**

Restart your FiveM server to load the resource.

**6. Add Inventory Images**

Copy the item images from the resource's `_install/inv images` folder to your inventory's image directory:

```
# qb-inventory / other inventories
aura_foodtruck/_install/inv images/*  ->  <your_inventory>/images/

# ox_inventory
aura_foodtruck/_install/inv images/*  ->  ox_inventory/web/images/
```

### Configuration

All options live in `config.lua`. Every option and its shipped default is documented below.

**General**

| Option           | Default | Description                                                                    |
| ---------------- | ------- | ------------------------------------------------------------------------------ |
| `debug`          | `false` | Prints debug messages to the server/client consoles. Turn off on live servers. |
| `useConsumables` | `true`  | If true, eating/drinking crafted items restores hunger/thirst.                 |

**Interaction Points (`target`)**

| Option                            | Default                       | Description                                                                       |
| --------------------------------- | ----------------------------- | --------------------------------------------------------------------------------- |
| `target.offsetRadius`             | `0.75`                        | How close (in meters) the player must stand to a point before its option appears. |
| `target.interactDistance`         | `2.0`                         | How far away (in meters) the player can be to see the option at all.              |
| `target.customerInteractDistance` | `2.3`                         | How close the player must be to a waiting NPC customer to hand over an order.     |
| `target.offsets.storage`          | `vector3(0.41, -3.20, 0.59)`  | Storage attachment offset, relative to the truck model.                           |
| `target.offsets.register`         | `vector3(-1.00, -1.57, 0.89)` | Register attachment offset, relative to the truck model.                          |
| `target.offsets.tray`             | `vector3(-1.10, -0.61, 0.80)` | Tray attachment offset, relative to the truck model.                              |
| `target.offsets.cooking`          | `vector3(0.66, 1.43, 0.82)`   | Cooking station attachment offset, relative to the truck model.                   |
| `target.offsets.handoff`          | `vector3(-1.60, -0.92, 0.55)` | Order handoff attachment offset, relative to the truck model.                     |

Use `/foodtruckoffset` in-game to find and print new offsets for custom truck models.

**Business Tablet (`tablet`)**

| Option                       | Default                           | Description                                                                                                                                 |
| ---------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `tablet.item`                | `'foodtruck_tablet'`              | Inventory item that opens the business tablet. Registered as a usable item — using it from your inventory opens the same UI as the command. |
| `tablet.command`             | `'foodtrucktablet'`               | Chat command that opens the business tablet.                                                                                                |
| `tablet.openMode`            | `'both'`                          | How the tablet can be opened: `'item'`, `'command'`, or `'both'`.                                                                           |
| `tablet.defaultProfileImage` | `'./svg/exampleProfileImage.png'` | Avatar used until the owner sets one.                                                                                                       |
| `tablet.maxLogs`             | `80`                              | How many recent activity logs the tablet shows.                                                                                             |
| `tablet.ownerGrades`         | `{ 3, 4 }`                        | Job grades allowed to open the tablet (empty table = everyone in the job).                                                                  |
| `tablet.useCharacterNames`   | `true`                            | `true` = firstname lastname, `false` = FiveM/Steam name.                                                                                    |

Job aliases — maps your server's actual job names to the food truck jobs (`['your_server_job_name'] = 'foodtruck_job_name'`):

| Server job    | Food truck job |
| ------------- | -------------- |
| `burger`      | `burgershot`   |
| `burger_shot` | `burgershot`   |
| `pizza`       | `pizzeria`     |
| `pizzathis`   | `pizzeria`     |
| `taco`        | `tacofarmer`   |

**Activity Logging (`logging`)**

| Option                                 | Default | Description                                            |
| -------------------------------------- | ------- | ------------------------------------------------------ |
| `logging.enabled`                      | `true`  | Master switch — set to `false` to disable ALL logging. |
| `logging.types.crafted`                | `true`  | A player finished cooking an item.                     |
| `logging.types.order_paid`             | `true`  | A player paid a register bill.                         |
| `logging.types.player_order_completed` | `true`  | A register order was marked as served.                 |
| `logging.types.npc_order_created`      | `true`  | A walk-up NPC placed an order.                         |
| `logging.types.npc_order_served`       | `true`  | A walk-up NPC order was handed over.                   |
| `logging.types.npc_order_expired`      | `true`  | A walk-up NPC left because the order took too long.    |
| `logging.types.upgrade_purchased`      | `true`  | A business upgrade was bought.                         |
| `logging.types.bank_deposit`           | `true`  | Money deposited into the business bank.                |
| `logging.types.bank_withdraw`          | `true`  | Money withdrawn from the business bank.                |

**Cooking (`cooking`)**

| Option                      | Default                   | Description                                              |
| --------------------------- | ------------------------- | -------------------------------------------------------- |
| `cooking.maxQuantity`       | `10`                      | Max items a player can cook at once.                     |
| `cooking.mechanicAnim.dict` | `'mini@repair'`           | Animation dictionary played while cooking.               |
| `cooking.mechanicAnim.name` | `'fixing_a_ped'`          | Animation name played while cooking.                     |
| `cooking.mechanicAnim.flag` | `49`                      | Animation flag.                                          |
| `cooking.smoke.dict`        | `'core'`                  | Particle dictionary for the cooking smoke effect.        |
| `cooking.smoke.ptfx`        | `'exp_grd_grenade_smoke'` | Particle effect that puffs from the truck while cooking. |
| `cooking.smoke.scale`       | `0.58`                    | Smoke particle scale.                                    |
| `cooking.smoke.duration`    | `6500`                    | How long one puff lasts (milliseconds).                  |
| `cooking.smoke.color`       | `vector3(1.0, 1.0, 1.0)`  | RGB tint (0.0–1.0 per channel).                          |

**Orders (`orders`)**

| Option                | Default | Description                                                                      |
| --------------------- | ------- | -------------------------------------------------------------------------------- |
| `orders.completedTtl` | `60`    | How long a served order stays in the orders list before being removed (seconds). |

**NPC Sales (`sales`)**

| Option                     | Default           | Description                                                                                                                                                                                                                                                                                      |
| -------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `sales.enabled`            | `true`            | Enables walk-up NPC customers (the `/sellfoodtruck` system).                                                                                                                                                                                                                                     |
| `sales.command`            | `'sellfoodtruck'` | Chat command to start/stop selling.                                                                                                                                                                                                                                                              |
| `sales.account`            | `'society'`       | Where sale money goes. `'society'` = the owning job's society/business bank account (via your banking resource), `'cash'` or `'bank'` = paid directly to the employee. When `'society'` is set, register bills are taken from the customer's cash and upgrades/deposits use the employee's cash. |
| `sales.defaultPrice`       | `35`              | Fallback price when neither the recipe nor `sales.prices` sets one.                                                                                                                                                                                                                              |
| `sales.orderDelay`         | `25000`           | Milliseconds between NPC customers spawning.                                                                                                                                                                                                                                                     |
| `sales.maxActiveCustomers` | `1`               | Max NPC customers waiting at the same time (before upgrades).                                                                                                                                                                                                                                    |
| `sales.spawnDistance.min`  | `13.0`            | Minimum distance from the truck NPCs spawn (meters).                                                                                                                                                                                                                                             |
| `sales.spawnDistance.max`  | `19.0`            | Maximum distance from the truck NPCs spawn (meters).                                                                                                                                                                                                                                             |
| `sales.handoffDistance`    | `3.5`             | How close to the truck NPCs stop and wait for their order (meters).                                                                                                                                                                                                                              |
| `sales.maxDistance`        | `20.0`            | Safety limit — if you get this far from the truck, or the truck is deleted, NPC sales stop automatically and waiting customers are sent away (meters).                                                                                                                                           |

Customer ped models (`sales.peds` — picked at random):

| # | Model               |
| - | ------------------- |
| 1 | `a_m_y_business_01` |
| 2 | `a_f_y_business_02` |
| 3 | `a_m_m_eastsa_02`   |
| 4 | `a_f_m_bevhills_01` |
| 5 | `a_m_y_hipster_01`  |

Per-item price overrides (`sales.prices` — item result name = price; anything not listed falls back to `sales.defaultPrice`):

| Item           | Price |
| -------------- | ----- |
| `bean_coffee2` | `$15` |
| `brownies`     | `$14` |
| `cheesecake`   | `$20` |

**Sales Upgrades (`sales.upgrades`)**

Each level costs `baseCost * (currentLevel + 1)` — e.g. the first level costs `baseCost`, the next costs `baseCost * 2`, and so on.

| Upgrade              | Label               | Icon                        | Description                                                              | Max Level | Base Cost | Effect per Level                               |
| -------------------- | ------------------- | --------------------------- | ------------------------------------------------------------------------ | --------- | --------- | ---------------------------------------------- |
| `marketing`          | Street Marketing    | `fa-solid fa-bullhorn`      | Reduces customer delay and increases the chance of back-to-back walkups. | 3         | `$500`    | Removes 5000 ms from `orderDelay`              |
| `signage`            | Menu Signage        | `fa-solid fa-sign-hanging`  | Adds one extra item per NPC order at higher levels.                      | 2         | `$750`    | NPC orders get 2 items instead of 1 at level 2 |
| `service`            | Service Flow        | `fa-solid fa-people-arrows` | Allows more active customer orders around the truck.                     | 2         | `$1000`   | +1 waiting customer                            |
| `premiumIngredients` | Premium Ingredients | `fa-solid fa-seedling`      | Improves sale margins for every player and NPC order.                    | 3         | `$1250`   | +8% payout bonus                               |
| `expressPrep`        | Express Prep        | `fa-solid fa-stopwatch`     | Speeds up kitchen craft timers for busy rushes.                          | 3         | `$1500`   | Cooking is 8% faster                           |
| `customerComfort`    | Customer Comfort    | `fa-solid fa-couch`         | Makes walk-up customers wait longer before leaving.                      | 2         | `$900`    | NPCs wait 20 extra seconds                     |

**Consumables**

What happens when a player eats/drinks a crafted item — amount of hunger/thirst restored (0–100).

<details>

<summary>Eat — hunger restored (<code>consumables.eat</code>)</summary>

| Item                     | Hunger |
| ------------------------ | ------ |
| `ramen`                  | 40     |
| `tokyo_fusion_burger`    | 50     |
| `teriyaki_wings`         | 35     |
| `sushi`                  | 45     |
| `doublechicken_burger`   | 55     |
| `muffin`                 | 25     |
| `croissant`              | 30     |
| `cb_donut`               | 20     |
| `baquette`               | 35     |
| `cheesecake`             | 40     |
| `cremecaramel`           | 40     |
| `cake_chocolate`         | 45     |
| `cakepop`                | 25     |
| `blueberry_pie`          | 40     |
| `brownies`               | 35     |
| `burger_heartstopper`    | 60     |
| `burger_bleeder`         | 50     |
| `burger_chickenwrap`     | 40     |
| `burger_shotrings`       | 30     |
| `burger_icecream`        | 25     |
| `burger_rimjob`          | 55     |
| `burger_shotnuggets`     | 35     |
| `nuggets`                | 35     |
| `pickleburger`           | 45     |
| `burger_chickenmelt`     | 50     |
| `wings`                  | 40     |
| `sirloinsteak`           | 55     |
| `steak_potato`           | 65     |
| `steakburger`            | 50     |
| `bacon_cheeseburger`     | 55     |
| `ppizza`                 | 60     |
| `pmushroomspizza`        | 60     |
| `pvegpizza`              | 55     |
| `ppizzaslice`            | 30     |
| `basket_fries`           | 35     |
| `taco_beef`              | 40     |
| `taco_chicken`           | 40     |
| `taco_fish`              | 35     |
| `burrito`                | 55     |
| `hotdog_taco`            | 35     |
| `cheese_fries`           | 35     |
| `cheese_burger_fries`    | 45     |
| `tripleburger`           | 60     |
| `cone_chocolate`         | 20     |
| `cone_blueberry`         | 20     |
| `chickenburger`          | 50     |
| `chicken_breastsandwich` | 45     |
| `cheeseburger`           | 50     |
| `bltsandwich`            | 40     |

</details>

<details>

<summary>Drink — thirst restored (<code>consumables.drink</code>)</summary>

| Item                | Thirst |
| ------------------- | ------ |
| `matcha_milkshake`  | 40     |
| `bean_coffee2`      | 35     |
| `bean_carmalcoffee` | 40     |
| `burger_softdrink`  | 35     |
| `sprite`            | 30     |
| `sprunk`            | 30     |
| `sprunklight`       | 30     |
| `gin_and_tonic`     | 35     |

</details>

<details>

<summary>Alcohol — thirst restored (<code>consumables.alcohol</code>)</summary>

| Item            | Thirst |
| --------------- | ------ |
| `beerglass3`    | 30     |
| `bellini`       | 35     |
| `wine_barbera`  | 35     |
| `wine_dolcetto` | 35     |

</details>

**Food Trucks (`foodTrucks`)**

One entry per vehicle model. Each truck defines its owning `job`, UI `theme`, and `recipes`.

Every truck defines these shared interaction points in its `targets` table:

| Point           | Inventory Type                 | Slots | Weight   | Job Restricted | Interact Distance |
| --------------- | ------------------------------ | ----- | -------- | -------------- | ----------------- |
| Tray            | `tray` (separate from storage) | 25    | 50000 g  | No             | 1.45 m            |
| Cooking station | — (recipe menu)                | —     | —        | Yes\*          | 1.35 m            |
| Storage         | `stash`                        | 100   | 200000 g | Yes            | 1.25 m            |
| Register        | — (billing)                    | —     | —        | Yes            | 1.30 m            |

\* Bean Machine's cooking station is open to everyone (`jobRestricted = false`); all other trucks restrict it to employees.

| Truck Model | Brand         | Job           | Theme       |
| ----------- | ------------- | ------------- | ----------- |
| `sbsb`      | Snr Buns      | `snrbuns`     | snrbuns     |
| `sbww`      | Wig Wam       | `wigwam`      | wigwam      |
| `sbbm`      | Bean Machine  | `beanmachine` | beanmachine |
| `sbbs`      | Burger Shot   | `burgershot`  | burgershot  |
| `sbcb`      | Cluckin' Bell | `cluckinbell` | cluckinbell |
| `sbgj`      | Greasy Joe's  | `greasyjoes`  | greasyjoes  |
| `sbpz`      | Pizza This... | `pizzeria`    | pizzathis   |
| `sbtf`      | Taco Farmer   | `tacofarmer`  | tacofarmer  |

Sale prices below are the effective price after `sales.prices` overrides / `sales.defaultPrice` fallback are applied at runtime.

<details>

<summary>Snr Buns (<code>sbsb</code>)</summary>

| Category       | Result                   | Label                    | Cook Time | Sale Price | Ingredients                                             |
| -------------- | ------------------------ | ------------------------ | --------- | ---------- | ------------------------------------------------------- |
| Buns & Burgers | `tripleburger`           | Triple Burger            | 35 s      | $35        | burgerpatty ×3, cheese ×2, lettuce ×1, burger\_onion ×1 |
| Buns & Burgers | `cheese_burger_fries`    | Cheese Burger Fries      | 20 s      | $35        | burgerpatty ×1, cheese ×2, slicedpotato ×2              |
| Buns & Burgers | `chickenburger`          | Chicken Burger           | 25 s      | $35        | chickenbreast ×1, burgerpatty ×1, cheese ×1, lettuce ×1 |
| Buns & Burgers | `cheeseburger`           | Cheeseburger             | 20 s      | $35        | burgerpatty ×1, cheese ×2, lettuce ×1, burger\_onion ×1 |
| Sides          | `cheese_fries`           | Cheese Fries             | 15 s      | $35        | slicedpotato ×3, cheese ×1                              |
| Sides          | `cone_chocolate`         | Chocolate Ice Cream Cone | 10 s      | $35        | burger\_icecream\_empty ×1, cooking\_chocolate ×1       |
| Sides          | `cone_blueberry`         | Blueberry Ice Cream Cone | 10 s      | $35        | burger\_icecream\_empty ×1, blueberry ×1                |
| Sides          | `chicken_breastsandwich` | Chicken Breast Sandwich  | 20 s      | $35        | chickenbreast ×2, cheese ×1, lettuce ×1                 |
| Sides          | `bltsandwich`            | BLT Sandwich             | 15 s      | $35        | bacon ×2, lettuce ×2, burger\_onion ×1                  |

</details>

<details>

<summary>Wig Wam (<code>sbww</code>)</summary>

| Category          | Result                 | Label                  | Cook Time | Sale Price | Ingredients                                               |
| ----------------- | ---------------------- | ---------------------- | --------- | ---------- | --------------------------------------------------------- |
| Burgers           | `tokyo_fusion_burger`  | Tokyo Fusion Burger    | 30 s      | $35        | burgerpatty ×2, nori\_sheets ×2, rice ×1, lettuce ×2      |
| Burgers           | `doublechicken_burger` | Double Chicken Burger  | 25 s      | $35        | chickenbreast ×2, cheese ×1, lettuce ×1, burger\_onion ×1 |
| Sides             | `teriyaki_wings`       | Teriyaki Glazed Wings  | 20 s      | $35        | chicken\_wings\_raw ×6, hot\_sauce ×2, salt ×1            |
| Drinks & Desserts | `matcha_milkshake`     | Matcha Milkshake       | 10 s      | $35        | matcha ×1, milk ×1                                        |
| Japanese Specials | `ramen`                | Tonkotsu Ramen         | 25 s      | $35        | burgerpatty ×2, nori\_sheets ×3, rice ×2, hot\_sauce ×1   |
| Japanese Specials | `sushi`                | Assorted Sushi Platter | 30 s      | $35        | raw\_sushi ×3, nori\_sheets ×2, rice ×2, pickles ×1       |

</details>

<details>

<summary>Bean Machine (<code>sbbm</code>)</summary>

| Category      | Result              | Label               | Cook Time | Sale Price | Ingredients                                |
| ------------- | ------------------- | ------------------- | --------- | ---------- | ------------------------------------------ |
| Pastries      | `muffin`            | Chocolate Muffin    | 20 s      | $35        | dough ×1, cooking\_chocolate ×2            |
| Pastries      | `croissant`         | Butter Croissant    | 25 s      | $35        | dough ×2, cooking\_chocolate ×1            |
| Pastries      | `cb_donut`          | Chocolate Donut     | 15 s      | $35        | dough ×1, cooking\_chocolate ×1, milk ×1   |
| Pastries      | `baquette`          | Baguette            | 30 s      | $35        | dough ×3, butter ×1                        |
| Coffee Drinks | `bean_coffee2`      | Classic Bean Coffee | 10 s      | $15        | coffee\_bean ×3                            |
| Coffee Drinks | `bean_carmalcoffee` | Caramel Coffee      | 15 s      | $35        | coffee\_bean ×3, cooking\_chocolate ×1     |
| Desserts      | `cheesecake`        | Cheesecake          | 40 s      | $20        | cheese ×2, sugar ×1, dough ×1              |
| Desserts      | `cremecaramel`      | Crème Caramel       | 35 s      | $35        | milk ×2, sugar ×2, egg ×2                  |
| Desserts      | `cake_chocolate`    | Chocolate Cake      | 45 s      | $35        | dough ×2, cooking\_chocolate ×3, milk ×1   |
| Desserts      | `cakepop`           | Cake Pop            | 20 s      | $35        | dough ×1, cooking\_chocolate ×2            |
| Desserts      | `blueberry_pie`     | Blueberry Pie       | 40 s      | $35        | dough ×2, blueberry ×5, sugar ×1           |
| Desserts      | `brownies`          | Brownies            | 30 s      | $14        | cooking\_chocolate ×3, butter ×1, sugar ×1 |

</details>

<details>

<summary>Burger Shot (<code>sbbs</code>)</summary>

| Category          | Result                | Label          | Cook Time | Sale Price | Ingredients                                             |
| ----------------- | --------------------- | -------------- | --------- | ---------- | ------------------------------------------------------- |
| Burgers           | `burger_heartstopper` | Heart Stopper  | 30 s      | $35        | burgerpatty ×3, cheese ×3, lettuce ×2, burger\_onion ×1 |
| Burgers           | `burger_bleeder`      | Bleeder Burger | 25 s      | $35        | burgerpatty ×2, cheese ×2, lettuce ×1, burger\_onion ×1 |
| Burgers           | `burger_chickenwrap`  | Chicken Wrap   | 20 s      | $35        | chickenbreast ×2, lettuce ×2, cheese ×1                 |
| Sides             | `burger_shotrings`    | Shot Rings     | 15 s      | $35        | burger\_onion ×3                                        |
| Sides             | `burger_shotnuggets`  | Shot Nuggets   | 15 s      | $35        | frozennuggets ×1                                        |
| Sides             | `burger_rimjob`       | Rim Job Donut  | 15 s      | $35        | dough ×1, cooking\_chocolate ×1, milk ×1                |
| Drinks & Desserts | `burger_softdrink`    | Soft Drink     | 5 s       | $35        | —                                                       |
| Drinks & Desserts | `burger_icecream`     | Ice Cream      | 10 s      | $35        | burger\_icecream\_empty ×1                              |

</details>

<details>

<summary>Cluckin' Bell (<code>sbcb</code>)</summary>

| Category      | Result               | Label           | Cook Time | Sale Price | Ingredients                                              |
| ------------- | -------------------- | --------------- | --------- | ---------- | -------------------------------------------------------- |
| Chicken Items | `nuggets`            | Chicken Nuggets | 15 s      | $35        | frozennuggets ×1                                         |
| Chicken Items | `wings`              | Chicken Wings   | 20 s      | $35        | chickenbreast ×2                                         |
| Chicken Items | `burger_chickenmelt` | Chicken Melt    | 25 s      | $35        | chickenbreast ×2, cheese ×2, lettuce ×1                  |
| Burgers       | `pickleburger`       | Pickle Burger   | 25 s      | $35        | burgerpatty ×1, pickles ×3, lettuce ×1, burger\_onion ×1 |
| Deserts       | `burger_icecream`    | Ice Cream       | 5 s       | $35        | burger\_icecream\_empty ×1                               |

</details>

<details>

<summary>Greasy Joe's (<code>sbgj</code>)</summary>

| Category | Result               | Label              | Cook Time | Sale Price | Ingredients                                                |
| -------- | -------------------- | ------------------ | --------- | ---------- | ---------------------------------------------------------- |
| Steaks   | `sirloinsteak`       | Sirloin Steak      | 30 s      | $35        | sirloin\_steak ×1                                          |
| Steaks   | `steak_potato`       | Steak & Potato     | 35 s      | $35        | sirloin\_steak ×1, slicedpotato ×2                         |
| Burgers  | `steakburger`        | Steak Burger       | 30 s      | $35        | sirloin\_steak ×1, cheese ×2, lettuce ×1, burger\_onion ×1 |
| Burgers  | `bacon_cheeseburger` | Bacon Cheeseburger | 25 s      | $35        | burgerpatty ×2, bacon ×3, cheese ×2, lettuce ×1            |
| Drinks   | `beerglass3`         | Cold Beer          | 5 s       | $35        | —                                                          |
| Drinks   | `bellini`            | Bellini Cocktail   | 10 s      | $35        | —                                                          |

</details>

<details>

<summary>Pizza This... (<code>sbpz</code>)</summary>

| Category | Result            | Label            | Cook Time | Sale Price | Ingredients                                          |
| -------- | ----------------- | ---------------- | --------- | ---------- | ---------------------------------------------------- |
| Pizzas   | `ppizza`          | Pepperoni Pizza  | 40 s      | $35        | dough ×1, tomato ×2, cheese ×2, pepperoni ×3         |
| Pizzas   | `pmushroomspizza` | Mushroom Pizza   | 40 s      | $35        | dough ×1, tomato ×2, cheese ×2, mushroom ×3          |
| Pizzas   | `pvegpizza`       | Vegetarian Pizza | 40 s      | $35        | dough ×1, tomato ×2, cheese ×2, mushroom ×1, corn ×1 |
| Pizzas   | `ppizzaslice`     | Pizza Slice      | 10 s      | $35        | dough ×1, tomato ×1, cheese ×1                       |
| Sides    | `basket_fries`    | Basket of Fries  | 15 s      | $35        | slicedpotato ×3                                      |
| Drinks   | `wine_barbera`    | Barbera Wine     | 5 s       | $35        | —                                                    |
| Drinks   | `wine_dolcetto`   | Dolcetto Wine    | 5 s       | $35        | —                                                    |

</details>

<details>

<summary>Taco Farmer (<code>sbtf</code>)</summary>

| Category            | Result          | Label        | Cook Time | Sale Price | Ingredients                                                   |
| ------------------- | --------------- | ------------ | --------- | ---------- | ------------------------------------------------------------- |
| Tacos               | `taco_beef`     | Beef Taco    | 20 s      | $35        | taco\_shell ×1, beef ×2, lettuce ×1, cheese ×1                |
| Tacos               | `taco_chicken`  | Chicken Taco | 20 s      | $35        | taco\_shell ×1, chicken\_wings\_raw ×2, lettuce ×1, cheese ×1 |
| Tacos               | `taco_fish`     | Fish Taco    | 20 s      | $35        | taco\_shell ×1, fish ×2, lettuce ×1                           |
| Burritos & Specials | `burrito`       | Burrito      | 30 s      | $35        | beef ×2, chicken\_wings\_raw ×1, lettuce ×2, cheese ×2        |
| Burritos & Specials | `hotdog_taco`   | Hotdog Taco  | 15 s      | $35        | taco\_shell ×1, rawhotdog ×1, burger\_onion ×1                |
| Drinks              | `sprite`        | Sprite       | 5 s       | $35        | —                                                             |
| Drinks              | `sprunk`        | Sprunk       | 5 s       | $35        | —                                                             |
| Drinks              | `sprunklight`   | Sprunk Light | 5 s       | $35        | —                                                             |
| Drinks              | `gin_and_tonic` | Gin & Tonic  | 10 s      | $35        | —                                                             |

</details>

### Dependencies

* **aura\_bridge**
* **ox\_lib**
* **oxmysql**

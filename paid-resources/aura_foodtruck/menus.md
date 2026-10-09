---
description: Trucks, recipes, prices and consumables in aura_foodtruck.
---

# Menus

| Truck Model | Brand | Job | Theme |
| --- | --- | --- | --- |
| `sbsb` | Snr Buns | `snrbuns` | snrbuns |
| `sbww` | Wig Wam | `wigwam` | wigwam |
| `sbbm` | Bean Machine | `beanmachine` | beanmachine |
| `sbbs` | Burger Shot | `burgershot` | burgershot |
| `sbcb` | Cluckin' Bell | `cluckinbell` | cluckinbell |
| `sbgj` | Greasy Joe's | `greasyjoes` | greasyjoes |
| `sbpz` | Pizza This | `pizzeria` | pizzathis |
| `sbtf` | Taco Farmer | `tacofarmer` | tacofarmer |

Every truck has the same four interaction points:

| Point | Inventory | Slots | Weight | Job restricted | Distance |
| --- | --- | --- | --- | --- | --- |
| Tray | tray (separate from storage) | 25 | 50000 g | No | 1.45 m |
| Cooking station | recipe menu | — | — | Yes* | 1.35 m |
| Storage | stash | 100 | 200000 g | Yes | 1.25 m |
| Register | billing | — | — | Yes | 1.30 m |

Sale prices below are the effective price after `sales.prices` overrides / `sales.defaultPrice` fallback are applied at runtime.

<details>

<summary>Snr Buns (<code>sbsb</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Buns & Burgers | `tripleburger` | Triple Burger | 35 s | $35 | burgerpatty ×3, cheese ×2, lettuce ×1, burger_onion ×1 |
| Buns & Burgers | `cheese_burger_fries` | Cheese Burger Fries | 20 s | $35 | burgerpatty ×1, cheese ×2, slicedpotato ×2 |
| Buns & Burgers | `chickenburger` | Chicken Burger | 25 s | $35 | chickenbreast ×1, burgerpatty ×1, cheese ×1, lettuce ×1 |
| Buns & Burgers | `cheeseburger` | Cheeseburger | 20 s | $35 | burgerpatty ×1, cheese ×2, lettuce ×1, burger_onion ×1 |
| Sides | `cheese_fries` | Cheese Fries | 15 s | $35 | slicedpotato ×3, cheese ×1 |
| Sides | `cone_chocolate` | Chocolate Ice Cream Cone | 10 s | $35 | burger_icecream_empty ×1, cooking_chocolate ×1 |
| Sides | `cone_blueberry` | Blueberry Ice Cream Cone | 10 s | $35 | burger_icecream_empty ×1, blueberry ×1 |
| Sides | `chicken_breastsandwich` | Chicken Breast Sandwich | 20 s | $35 | chickenbreast ×2, cheese ×1, lettuce ×1 |
| Sides | `bltsandwich` | BLT Sandwich | 15 s | $35 | bacon ×2, lettuce ×2, burger_onion ×1 |

</details>

<details>

<summary>Wig Wam (<code>sbww</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Burgers | `tokyo_fusion_burger` | Tokyo Fusion Burger | 30 s | $35 | burgerpatty ×2, nori_sheets ×2, rice ×1, lettuce ×2 |
| Burgers | `doublechicken_burger` | Double Chicken Burger | 25 s | $35 | chickenbreast ×2, cheese ×1, lettuce ×1, burger_onion ×1 |
| Sides | `teriyaki_wings` | Teriyaki Glazed Wings | 20 s | $35 | chicken_wings_raw ×6, hot_sauce ×2, salt ×1 |
| Drinks & Desserts | `matcha_milkshake` | Matcha Milkshake | 10 s | $35 | matcha ×1, milk ×1 |
| Japanese Specials | `ramen` | Tonkotsu Ramen | 25 s | $35 | burgerpatty ×2, nori_sheets ×3, rice ×2, hot_sauce ×1 |
| Japanese Specials | `sushi` | Assorted Sushi Platter | 30 s | $35 | raw_sushi ×3, nori_sheets ×2, rice ×2, pickles ×1 |

</details>

<details>

<summary>Bean Machine (<code>sbbm</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Pastries | `muffin` | Chocolate Muffin | 20 s | $35 | dough ×1, cooking_chocolate ×2 |
| Pastries | `croissant` | Butter Croissant | 25 s | $35 | dough ×2, cooking_chocolate ×1 |
| Pastries | `cb_donut` | Chocolate Donut | 15 s | $35 | dough ×1, cooking_chocolate ×1, milk ×1 |
| Pastries | `baquette` | Baguette | 30 s | $35 | dough ×3, butter ×1 |
| Coffee Drinks | `bean_coffee2` | Classic Bean Coffee | 10 s | $15 | coffee_bean ×3 |
| Coffee Drinks | `bean_carmalcoffee` | Caramel Coffee | 15 s | $35 | coffee_bean ×3, cooking_chocolate ×1 |
| Desserts | `cheesecake` | Cheesecake | 40 s | $20 | cheese ×2, sugar ×1, dough ×1 |
| Desserts | `cremecaramel` | Crème Caramel | 35 s | $35 | milk ×2, sugar ×2, egg ×2 |
| Desserts | `cake_chocolate` | Chocolate Cake | 45 s | $35 | dough ×2, cooking_chocolate ×3, milk ×1 |
| Desserts | `cakepop` | Cake Pop | 20 s | $35 | dough ×1, cooking_chocolate ×2 |
| Desserts | `blueberry_pie` | Blueberry Pie | 40 s | $35 | dough ×2, blueberry ×5, sugar ×1 |
| Desserts | `brownies` | Brownies | 30 s | $14 | cooking_chocolate ×3, butter ×1, sugar ×1 |

</details>

<details>

<summary>Burger Shot (<code>sbbs</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Burgers | `burger_heartstopper` | Heart Stopper | 30 s | $35 | burgerpatty ×3, cheese ×3, lettuce ×2, burger_onion ×1 |
| Burgers | `burger_bleeder` | Bleeder Burger | 25 s | $35 | burgerpatty ×2, cheese ×2, lettuce ×1, burger_onion ×1 |
| Burgers | `burger_chickenwrap` | Chicken Wrap | 20 s | $35 | chickenbreast ×2, lettuce ×2, cheese ×1 |
| Sides | `burger_shotrings` | Shot Rings | 15 s | $35 | burger_onion ×3 |
| Sides | `burger_shotnuggets` | Shot Nuggets | 15 s | $35 | frozennuggets ×1 |
| Sides | `burger_rimjob` | Rim Job Donut | 15 s | $35 | dough ×1, cooking_chocolate ×1, milk ×1 |
| Drinks & Desserts | `burger_softdrink` | Soft Drink | 5 s | $35 | — |
| Drinks & Desserts | `burger_icecream` | Ice Cream | 10 s | $35 | burger_icecream_empty ×1 |

</details>

<details>

<summary>Cluckin' Bell (<code>sbcb</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Chicken Items | `nuggets` | Chicken Nuggets | 15 s | $35 | frozennuggets ×1 |
| Chicken Items | `wings` | Chicken Wings | 20 s | $35 | chickenbreast ×2 |
| Chicken Items | `burger_chickenmelt` | Chicken Melt | 25 s | $35 | chickenbreast ×2, cheese ×2, lettuce ×1 |
| Burgers | `pickleburger` | Pickle Burger | 25 s | $35 | burgerpatty ×1, pickles ×3, lettuce ×1, burger_onion ×1 |
| Deserts | `burger_icecream` | Ice Cream | 5 s | $35 | burger_icecream_empty ×1 |

</details>

<details>

<summary>Greasy Joe's (<code>sbgj</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Steaks | `sirloinsteak` | Sirloin Steak | 30 s | $35 | sirloin_steak ×1 |
| Steaks | `steak_potato` | Steak & Potato | 35 s | $35 | sirloin_steak ×1, slicedpotato ×2 |
| Burgers | `steakburger` | Steak Burger | 30 s | $35 | sirloin_steak ×1, cheese ×2, lettuce ×1, burger_onion ×1 |
| Burgers | `bacon_cheeseburger` | Bacon Cheeseburger | 25 s | $35 | burgerpatty ×2, bacon ×3, cheese ×2, lettuce ×1 |
| Drinks | `beerglass3` | Cold Beer | 5 s | $35 | — |
| Drinks | `bellini` | Bellini Cocktail | 10 s | $35 | — |

</details>

<details>

<summary>Pizza This (<code>sbpz</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Pizzas | `ppizza` | Pepperoni Pizza | 40 s | $35 | dough ×1, tomato ×2, cheese ×2, pepperoni ×3 |
| Pizzas | `pmushroomspizza` | Mushroom Pizza | 40 s | $35 | dough ×1, tomato ×2, cheese ×2, mushroom ×3 |
| Pizzas | `pvegpizza` | Vegetarian Pizza | 40 s | $35 | dough ×1, tomato ×2, cheese ×2, mushroom ×1, corn ×1 |
| Pizzas | `ppizzaslice` | Pizza Slice | 10 s | $35 | dough ×1, tomato ×1, cheese ×1 |
| Sides | `basket_fries` | Basket of Fries | 15 s | $35 | slicedpotato ×3 |
| Drinks | `wine_barbera` | Barbera Wine | 5 s | $35 | — |
| Drinks | `wine_dolcetto` | Dolcetto Wine | 5 s | $35 | — |

</details>

<details>

<summary>Taco Farmer (<code>sbtf</code>)</summary>

| Category | Result | Label | Cook Time | Sale Price | Ingredients |
| --- | --- | --- | --- | --- | --- |
| Tacos | `taco_beef` | Beef Taco | 20 s | $35 | taco_shell ×1, beef ×2, lettuce ×1, cheese ×1 |
| Tacos | `taco_chicken` | Chicken Taco | 20 s | $35 | chicken_wings_raw ×2, lettuce ×1, cheese ×1 |
| Tacos | `taco_fish` | Fish Taco | 20 s | $35 | taco_shell ×1, fish ×2, lettuce ×1 |
| Burritos & Specials | `burrito` | Burrito | 30 s | $35 | beef ×2, chicken_wings_raw ×1, lettuce ×2, cheese ×2 |
| Burritos & Specials | `hotdog_taco` | Hotdog Taco | 15 s | $35 | taco_shell ×1, rawhotdog ×1, burger_onion ×1 |
| Drinks | `sprite` | Sprite | 5 s | $35 | — |
| Drinks | `sprunk` | Sprunk | 5 s | $35 | — |
| Drinks | `sprunklight` | Sprunk Light | 5 s | $35 | — |
| Drinks | `gin_and_tonic` | Gin & Tonic | 10 s | $35 | — |

</details>

### Consumables

Amount of hunger/thirst restored (0–100) per item when used from the inventory.

<details>

<summary>Eat — hunger (<code>consumables.eat</code>)</summary>

| Item | Hunger |
| --- | --- |
| `ramen` | 40 |
| `tokyo_fusion_burger` | 50 |
| `teriyaki_wings` | 35 |
| `sushi` | 45 |
| `doublechicken_burger` | 55 |
| `muffin` | 25 |
| `croissant` | 30 |
| `cb_donut` | 20 |
| `baquette` | 35 |
| `cheesecake` | 40 |
| `cremecaramel` | 40 |
| `cake_chocolate` | 45 |
| `cakepop` | 25 |
| `blueberry_pie` | 40 |
| `brownies` | 35 |
| `burger_heartstopper` | 60 |
| `burger_bleeder` | 50 |
| `burger_chickenwrap` | 40 |
| `burger_shotrings` | 30 |
| `burger_icecream` | 25 |
| `burger_rimjob` | 55 |
| `burger_shotnuggets` | 35 |
| `nuggets` | 35 |
| `pickleburger` | 45 |
| `burger_chickenmelt` | 50 |
| `wings` | 40 |
| `sirloinsteak` | 55 |
| `steak_potato` | 65 |
| `steakburger` | 50 |
| `bacon_cheeseburger` | 55 |
| `ppizza` | 60 |
| `pmushroomspizza` | 60 |
| `pvegpizza` | 55 |
| `ppizzaslice` | 30 |
| `basket_fries` | 35 |
| `taco_beef` | 40 |
| `taco_chicken` | 40 |
| `taco_fish` | 35 |
| `burrito` | 55 |
| `hotdog_taco` | 35 |
| `cheese_fries` | 35 |
| `cheese_burger_fries` | 45 |
| `tripleburger` | 60 |
| `cone_chocolate` | 20 |
| `cone_blueberry` | 20 |
| `chickenburger` | 50 |
| `chicken_breastsandwich` | 45 |
| `cheeseburger` | 50 |
| `bltsandwich` | 40 |

</details>

<details>

<summary>Drink — thirst (<code>consumables.drink</code>)</summary>

| Item | Thirst |
| --- | --- |
| `matcha_milkshake` | 40 |
| `bean_coffee2` | 35 |
| `bean_carmalcoffee` | 40 |
| `burger_softdrink` | 35 |
| `sprite` | 30 |
| `sprunk` | 30 |
| `sprunklight` | 30 |
| `gin_and_tonic` | 35 |

</details>

<details>

<summary>Alcohol — thirst (<code>consumables.alcohol</code>)</summary>

| Item | Thirst |
| --- | --- |
| `beerglass3` | 30 |
| `bellini` | 35 |
| `wine_barbera` | 35 |
| `wine_dolcetto` | 35 |

</details>

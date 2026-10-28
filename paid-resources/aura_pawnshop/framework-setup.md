---
description: Framework setup for aura_pawnshop - the pawn job, the 66 items and their images.
---

# Framework Setup

The shop needs two things from your server: the `pawn` **job** and the 66 **items** it buys and sells. Do both, then restart the server.

### 1. The job

The shop runs on one job, `pawn`, with 5 grades:

| Grade | Name | Can do |
| --- | --- | --- |
| `0` | Pawn Clerk | Storage, marketplace tablet, deliveries, walk-ins |
| `1` | Appraiser | Same as grade 0 |
| `2` | Sales Associate | Same as grade 0 |
| `3` | Store Manager | Also the boss menu, manager storage, hiring, buy list |
| `4` | Owner (boss) | Everything: withdrawals, permissions, policies, upgrades |

These are the defaults. The owner can change what each grade may do in game ([Boss Menu](./usage/boss-menu.md)).

{% tabs %}
{% tab title="QBCore" %}
Add to `qb-core/shared/jobs.lua`:

```lua
pawn = {
    label = 'Pawn Shop',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Pawn Clerk', payment = 50 },
        ['1'] = { name = 'Appraiser', payment = 100 },
        ['2'] = { name = 'Sales Associate', payment = 150 },
        ['3'] = { name = 'Store Manager', payment = 200 },
        ['4'] = { name = 'Owner', isboss = true, payment = 300 },
    },
},
```
{% endtab %}

{% tab title="QBOX" %}
Add to `qbx_core/shared/jobs.lua`:

```lua
['pawn'] = {
    label = 'Pawn Shop',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        [0] = { name = 'Pawn Clerk', payment = 50 },
        [1] = { name = 'Appraiser', payment = 100 },
        [2] = { name = 'Sales Associate', payment = 150 },
        [3] = { name = 'Store Manager', payment = 200 },
        [4] = { name = 'Owner', isboss = true, payment = 300 },
    },
},
```
{% endtab %}

{% tab title="ESX" %}
Run this once in your database (HeidiSQL, phpMyAdmin or txAdmin), then restart the server. ESX only reads jobs at startup.

```sql
-- whitelisted = 1 keeps the job out of the job centre: staff must be hired in the shop
INSERT INTO jobs (name, label, whitelisted) VALUES ('pawn', 'Pawn Shop', 1);

-- the highest grade must be named 'boss': that is how ESX and the shop recognise the owner
INSERT INTO job_grades (job_name, grade, name, label, salary, skin_male, skin_female) VALUES
('pawn', 0, 'pawn_clerk', 'Pawn Clerk', 50, '{}', '{}'),
('pawn', 1, 'appraiser', 'Appraiser', 100, '{}', '{}'),
('pawn', 2, 'sales_associate', 'Sales Associate', 150, '{}', '{}'),
('pawn', 3, 'store_manager', 'Store Manager', 200, '{}', '{}'),
('pawn', 4, 'boss', 'Owner', 300, '{}', '{}');

-- the shop's bank account (esx_addonaccount / esx_society); the shop also creates it if it is missing
INSERT IGNORE INTO addon_account (name, label, shared) VALUES ('society_pawn', 'Pawn Shop', 1);
INSERT INTO addon_account_data (account_name, money, owner)
SELECT 'society_pawn', 0, NULL FROM DUAL
WHERE NOT EXISTS (SELECT 1 FROM addon_account_data WHERE account_name = 'society_pawn');
```

Already have a `pawn` job? Make it whitelisted and make sure its top grade is named `boss`:

```sql
UPDATE jobs SET whitelisted = 1 WHERE name = 'pawn';
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Different job name or number of grades? Change `JOB_NAME`, `MANAGER_GRADE` and `MAX_GRADE` at the very top of `configs/shared/main.lua`. The job name must match your framework exactly.
{% endhint %}

### 2. The items

Pick the tab for **your inventory**, not your framework. ESX with `ox_inventory` uses the ox_inventory tab.

{% tabs %}
{% tab title="ox_inventory" %}
Add to `ox_inventory/data/items.lua`, inside the returned table:

```lua
['antique_vase'] = {
    label = 'Antique Vase',
    weight = 1500,
    stack = false,
    close = true,
    description = 'A delicate antique vase.',
},
['antiqueartifact'] = {
    label = 'Antique Artifact',
    weight = 2000,
    stack = false,
    close = true,
    description = 'A mysterious antique artifact.',
},
['bear'] = {
    label = 'Bear Plushie',
    weight = 500,
    stack = true,
    close = true,
    description = 'A cuddly bear plushie.',
},
['beatbox'] = {
    label = 'Beatbox',
    weight = 2500,
    stack = false,
    close = true,
    description = 'A portable beatbox speaker.',
},
['black_classic_watch'] = {
    label = 'Black Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with a black finish.',
},
['black_digital_watch'] = {
    label = 'Black Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'A black digital watch.',
},
['blue_classic_watch'] = {
    label = 'Blue Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with a blue finish.',
},
['blue_digital_watch'] = {
    label = 'Blue Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'A blue digital watch.',
},
['blue_gameboy'] = {
    label = 'Blue Gameboy',
    weight = 400,
    stack = false,
    close = true,
    description = 'A blue handheld gameboy.',
},
['cheap_necklace'] = {
    label = 'Cheap Necklace',
    weight = 100,
    stack = true,
    close = true,
    description = 'A cheap necklace, barely worth the clasp.',
},
['colle_alien'] = {
    label = 'Alien Figurine',
    weight = 700,
    stack = false,
    close = true,
    description = 'A collectible alien figurine.',
},
['colle_beast'] = {
    label = 'Beast Figurine',
    weight = 800,
    stack = false,
    close = true,
    description = 'A collectible beast figurine.',
},
['colle_bigfoot'] = {
    label = 'Bigfoot Figurine',
    weight = 900,
    stack = false,
    close = true,
    description = 'A collectible bigfoot figurine.',
},
['colle_imporage'] = {
    label = 'Imporage Figurine',
    weight = 800,
    stack = false,
    close = true,
    description = 'A collectible imporage figurine.',
},
['colle_pogo'] = {
    label = 'Pogo Figurine',
    weight = 600,
    stack = false,
    close = true,
    description = 'A collectible pogo figurine.',
},
['colle_prbubble'] = {
    label = 'Prbubble Figurine',
    weight = 700,
    stack = false,
    close = true,
    description = 'A collectible prbubble figurine.',
},
['colle_rsrcomm'] = {
    label = 'Rsr Comm Figurine',
    weight = 750,
    stack = false,
    close = true,
    description = 'A collectible rsr comm figurine.',
},
['colle_rsrgeneric'] = {
    label = 'Rsr Generic Figurine',
    weight = 750,
    stack = false,
    close = true,
    description = 'A collectible rsr generic figurine.',
},
['console_cjd500'] = {
    label = 'CJD-500 Console',
    weight = 800,
    stack = false,
    close = true,
    description = 'A CJD-500 game console.',
},
['diamond'] = {
    label = 'Diamond',
    weight = 1000,
    stack = true,
    close = true,
    description = 'A diamond seems like the jackpot to me!',
},
['diamond_ring'] = {
    label = 'Diamond Ring',
    weight = 1500,
    stack = true,
    close = true,
    description = 'A diamond ring seems like the jackpot to me!',
},
['electronickit'] = {
    label = 'Electronic Kit',
    weight = 100,
    stack = true,
    close = true,
    description = 'If you\'ve always wanted to build a robot you can maybe start here. Maybe you\'ll be the new Elon Musk?',
},
['gameboy'] = {
    label = 'Yellow Gameboy',
    weight = 400,
    stack = false,
    close = true,
    description = 'A yellow handheld gameboy.',
},
['gold_bracelet'] = {
    label = 'Gold Bracelet',
    weight = 200,
    stack = false,
    close = true,
    description = 'A gold bracelet.',
},
['gold_chain'] = {
    label = 'Gold Chain',
    weight = 200,
    stack = false,
    close = true,
    description = 'A gold chain.',
},
['indigo_classic_watch'] = {
    label = 'Indigo Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with an indigo finish.',
},
['indigo_digital_watch'] = {
    label = 'Indigo Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'An indigo digital watch.',
},
['limited_jewelry'] = {
    label = 'Limited Jewelry',
    weight = 300,
    stack = false,
    close = true,
    description = 'A limited edition jewelry piece.',
},
['old_watch'] = {
    label = 'Old Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'An old worn watch, still ticking.',
},
['orange_classic_watch'] = {
    label = 'Orange Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with an orange finish.',
},
['orange_digital_watch'] = {
    label = 'Orange Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'An orange digital watch.',
},
['perle_high'] = {
    label = 'Perle High',
    weight = 150,
    stack = false,
    close = true,
    description = 'A high-grade perle gemstone.',
},
['perle_mid'] = {
    label = 'Perle Mid',
    weight = 150,
    stack = false,
    close = true,
    description = 'A mid-grade perle gemstone.',
},
['perle_rare'] = {
    label = 'Perle Rare',
    weight = 150,
    stack = false,
    close = true,
    description = 'A rare perle gemstone.',
},
['pink_classic_watch'] = {
    label = 'Pink Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with a pink finish.',
},
['pink_digital_watch'] = {
    label = 'Pink Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'A pink digital watch.',
},
['plush_01a'] = {
    label = 'Pink Plushie',
    weight = 400,
    stack = true,
    close = true,
    description = 'A soft pink plushie.',
},
['plush_02a'] = {
    label = 'Green Plushie',
    weight = 400,
    stack = true,
    close = true,
    description = 'A soft green plushie.',
},
['plush_03a'] = {
    label = 'Blue Plushie',
    weight = 400,
    stack = true,
    close = true,
    description = 'A soft blue plushie.',
},
['plush_05a'] = {
    label = 'Mexican Plushie',
    weight = 450,
    stack = true,
    close = true,
    description = 'A yellow mexican plushie.',
},
['plush_06a'] = {
    label = 'Red Plushie',
    weight = 400,
    stack = true,
    close = true,
    description = 'A soft red plushie.',
},
['plush_07a'] = {
    label = 'Anime Plushie',
    weight = 400,
    stack = true,
    close = true,
    description = 'An anime girl plushie.',
},
['plush_08a'] = {
    label = 'Anime Plushie',
    weight = 400,
    stack = true,
    close = true,
    description = 'An anime girl plushie.',
},
['plush_09a'] = {
    label = 'Old Master Plushie',
    weight = 450,
    stack = true,
    close = true,
    description = 'An old master plushie.',
},
['red_classic_watch'] = {
    label = 'Red Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with a red finish.',
},
['red_digital_watch'] = {
    label = 'Red Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'A red digital watch.',
},
['rolex'] = {
    label = 'Golden Watch',
    weight = 1500,
    stack = true,
    close = true,
    description = 'A golden watch seems like the jackpot to me!',
},
['ruby_ring'] = {
    label = 'Ruby Ring',
    weight = 150,
    stack = false,
    close = true,
    description = 'A ring set with a ruby.',
},
['sapphire_earring'] = {
    label = 'Sapphire Earring',
    weight = 100,
    stack = false,
    close = true,
    description = 'An earring set with a sapphire.',
},
['sapphire_ring'] = {
    label = 'Sapphire Ring',
    weight = 150,
    stack = false,
    close = true,
    description = 'A ring set with a sapphire.',
},
['saxo'] = {
    label = 'Saxophone',
    weight = 3000,
    stack = false,
    close = true,
    description = 'A brass saxophone.',
},
['silver_bracelet'] = {
    label = 'Silver Bracelet',
    weight = 200,
    stack = false,
    close = true,
    description = 'A silver bracelet.',
},
['silver_chain'] = {
    label = 'Silver Chain',
    weight = 200,
    stack = false,
    close = true,
    description = 'A silver chain.',
},
['silver_watch'] = {
    label = 'Silver Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A silver watch.',
},
['skull_alien'] = {
    label = 'Alien Skull',
    weight = 800,
    stack = false,
    close = true,
    description = 'A strange alien skull.',
},
['statue1_men'] = {
    label = '',
    weight = 6000,
    stack = false,
    close = true,
    description = 'A heavy statue of a man.',
},
['statue1_panther'] = {
    label = 'Panther Statue',
    weight = 8000,
    stack = false,
    close = true,
    description = 'A heavy panther statue.',
},
['statue1_women'] = {
    label = '',
    weight = 6000,
    stack = false,
    close = true,
    description = 'A heavy statue of a woman.',
},
['toothgold'] = {
    label = 'Gold Tooth',
    weight = 100,
    stack = true,
    close = true,
    description = 'A gold tooth.',
},
['vase_modern'] = {
    label = 'Modern Vase',
    weight = 1200,
    stack = false,
    close = true,
    description = 'A sleek modern vase.',
},
['violet_classic_watch'] = {
    label = 'Violet Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with a violet finish.',
},
['violet_digital_watch'] = {
    label = 'Violet Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'A violet digital watch.',
},
['white_classic_watch'] = {
    label = 'White Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with a white finish.',
},
['white_digital_watch'] = {
    label = 'White Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'A white digital watch.',
},
['yellow_classic_watch'] = {
    label = 'Yellow Classic Watch',
    weight = 250,
    stack = false,
    close = true,
    description = 'A classic watch with a yellow finish.',
},
['yellow_digital_watch'] = {
    label = 'Yellow Digital Watch',
    weight = 200,
    stack = false,
    close = true,
    description = 'A yellow digital watch.',
},
```
{% endtab %}

{% tab title="qb-inventory and qb-based" %}
`qb-inventory`, `ps-inventory`, `qs-inventory`, `codem-inventory`, `origen_inventory`, `tgiann-inventory`, `jpr-inventory` and `core_inventory` read items from `qb-core/shared/items.lua`.

`rolex`, `diamond`, `diamond_ring` and `electronickit` already ship with QBCore, so they are not in this block. If you removed them from your server, add them back. Add:

```lua
antique_vase = { name = 'antique_vase', label = 'Antique Vase', weight = 1500, type = 'item', image = 'antique_vase.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A delicate antique vase.' },
antiqueartifact = { name = 'antiqueartifact', label = 'Antique Artifact', weight = 2000, type = 'item', image = 'antiqueartifact.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A mysterious antique artifact.' },
bear = { name = 'bear', label = 'Bear Plushie', weight = 500, type = 'item', image = 'bear.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A cuddly bear plushie.' },
beatbox = { name = 'beatbox', label = 'Beatbox', weight = 2500, type = 'item', image = 'beatbox.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A portable beatbox speaker.' },
black_classic_watch = { name = 'black_classic_watch', label = 'Black Classic Watch', weight = 250, type = 'item', image = 'black_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with a black finish.' },
black_digital_watch = { name = 'black_digital_watch', label = 'Black Digital Watch', weight = 200, type = 'item', image = 'black_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A black digital watch.' },
blue_classic_watch = { name = 'blue_classic_watch', label = 'Blue Classic Watch', weight = 250, type = 'item', image = 'blue_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with a blue finish.' },
blue_digital_watch = { name = 'blue_digital_watch', label = 'Blue Digital Watch', weight = 200, type = 'item', image = 'blue_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A blue digital watch.' },
blue_gameboy = { name = 'blue_gameboy', label = 'Blue Gameboy', weight = 400, type = 'item', image = 'blue_gameboy.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A blue handheld gameboy.' },
cheap_necklace = { name = 'cheap_necklace', label = 'Cheap Necklace', weight = 100, type = 'item', image = 'cheap_necklace.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A cheap necklace, barely worth the clasp.' },
colle_alien = { name = 'colle_alien', label = 'Alien Figurine', weight = 700, type = 'item', image = 'colle_alien.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible alien figurine.' },
colle_beast = { name = 'colle_beast', label = 'Beast Figurine', weight = 800, type = 'item', image = 'colle_beast.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible beast figurine.' },
colle_bigfoot = { name = 'colle_bigfoot', label = 'Bigfoot Figurine', weight = 900, type = 'item', image = 'colle_bigfoot.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible bigfoot figurine.' },
colle_imporage = { name = 'colle_imporage', label = 'Imporage Figurine', weight = 800, type = 'item', image = 'colle_imporage.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible imporage figurine.' },
colle_pogo = { name = 'colle_pogo', label = 'Pogo Figurine', weight = 600, type = 'item', image = 'colle_pogo.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible pogo figurine.' },
colle_prbubble = { name = 'colle_prbubble', label = 'Prbubble Figurine', weight = 700, type = 'item', image = 'colle_prbubble.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible prbubble figurine.' },
colle_rsrcomm = { name = 'colle_rsrcomm', label = 'Rsr Comm Figurine', weight = 750, type = 'item', image = 'colle_rsrcomm.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible rsr comm figurine.' },
colle_rsrgeneric = { name = 'colle_rsrgeneric', label = 'Rsr Generic Figurine', weight = 750, type = 'item', image = 'colle_rsrgeneric.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A collectible rsr generic figurine.' },
console_cjd500 = { name = 'console_cjd500', label = 'CJD-500 Console', weight = 800, type = 'item', image = 'console_cjd500.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A CJD-500 game console.' },
diamond                      = { name = 'diamond', label = 'Diamond', weight = 1000, type = 'item', image = 'diamond.png', unique = false, useable = false, shouldClose = true, description = 'A diamond seems like the jackpot to me!' },
diamond_ring                 = { name = 'diamond_ring', label = 'Diamond Ring', weight = 1500, type = 'item', image = 'diamond_ring.png', unique = false, useable = false, shouldClose = true, description = 'A diamond ring seems like the jackpot to me!' },
electronickit                = { name = 'electronickit', label = 'Electronic Kit', weight = 100, type = 'item', image = 'electronickit.png', unique = false, useable = true, shouldClose = true, description = 'If you\'ve always wanted to build a robot you can maybe start here. Maybe you\'ll be the new Elon Musk?' },
gameboy = { name = 'gameboy', label = 'Yellow Gameboy', weight = 400, type = 'item', image = 'gameboy.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A yellow handheld gameboy.' },
gold_bracelet = { name = 'gold_bracelet', label = 'Gold Bracelet', weight = 200, type = 'item', image = 'gold_bracelet.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A gold bracelet.' },
gold_chain = { name = 'gold_chain', label = 'Gold Chain', weight = 200, type = 'item', image = 'gold_chain.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A gold chain.' },
indigo_classic_watch = { name = 'indigo_classic_watch', label = 'Indigo Classic Watch', weight = 250, type = 'item', image = 'indigo_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with an indigo finish.' },
indigo_digital_watch = { name = 'indigo_digital_watch', label = 'Indigo Digital Watch', weight = 200, type = 'item', image = 'indigo_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'An indigo digital watch.' },
limited_jewelry = { name = 'limited_jewelry', label = 'Limited Jewelry', weight = 300, type = 'item', image = 'limited_jewelry.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A limited edition jewelry piece.' },
old_watch = { name = 'old_watch', label = 'Old Watch', weight = 250, type = 'item', image = 'old_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'An old worn watch, still ticking.' },
orange_classic_watch = { name = 'orange_classic_watch', label = 'Orange Classic Watch', weight = 250, type = 'item', image = 'orange_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with an orange finish.' },
orange_digital_watch = { name = 'orange_digital_watch', label = 'Orange Digital Watch', weight = 200, type = 'item', image = 'orange_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'An orange digital watch.' },
perle_high = { name = 'perle_high', label = 'Perle High', weight = 150, type = 'item', image = 'perle_high.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A high-grade perle gemstone.' },
perle_mid = { name = 'perle_mid', label = 'Perle Mid', weight = 150, type = 'item', image = 'perle_mid.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A mid-grade perle gemstone.' },
perle_rare = { name = 'perle_rare', label = 'Perle Rare', weight = 150, type = 'item', image = 'perle_rare.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A rare perle gemstone.' },
pink_classic_watch = { name = 'pink_classic_watch', label = 'Pink Classic Watch', weight = 250, type = 'item', image = 'pink_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with a pink finish.' },
pink_digital_watch = { name = 'pink_digital_watch', label = 'Pink Digital Watch', weight = 200, type = 'item', image = 'pink_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A pink digital watch.' },
plush_01a = { name = 'plush_01a', label = 'Pink Plushie', weight = 400, type = 'item', image = 'plush_01a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A soft pink plushie.' },
plush_02a = { name = 'plush_02a', label = 'Green Plushie', weight = 400, type = 'item', image = 'plush_02a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A soft green plushie.' },
plush_03a = { name = 'plush_03a', label = 'Blue Plushie', weight = 400, type = 'item', image = 'plush_03a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A soft blue plushie.' },
plush_05a = { name = 'plush_05a', label = 'Mexican Plushie', weight = 450, type = 'item', image = 'plush_05a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A yellow mexican plushie.' },
plush_06a = { name = 'plush_06a', label = 'Red Plushie', weight = 400, type = 'item', image = 'plush_06a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A soft red plushie.' },
plush_07a = { name = 'plush_07a', label = 'Anime Plushie', weight = 400, type = 'item', image = 'plush_07a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'An anime girl plushie.' },
plush_08a = { name = 'plush_08a', label = 'Anime Plushie', weight = 400, type = 'item', image = 'plush_08a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'An anime girl plushie.' },
plush_09a = { name = 'plush_09a', label = 'Old Master Plushie', weight = 450, type = 'item', image = 'plush_09a.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'An old master plushie.' },
red_classic_watch = { name = 'red_classic_watch', label = 'Red Classic Watch', weight = 250, type = 'item', image = 'red_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with a red finish.' },
red_digital_watch = { name = 'red_digital_watch', label = 'Red Digital Watch', weight = 200, type = 'item', image = 'red_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A red digital watch.' },
rolex                        = { name = 'rolex', label = 'Golden Watch', weight = 1500, type = 'item', image = 'rolex.png', unique = false, useable = false, shouldClose = true, description = 'A golden watch seems like the jackpot to me!' },
ruby_ring = { name = 'ruby_ring', label = 'Ruby Ring', weight = 150, type = 'item', image = 'ruby_ring.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A ring set with a ruby.' },
sapphire_earring = { name = 'sapphire_earring', label = 'Sapphire Earring', weight = 100, type = 'item', image = 'sapphire_earring.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'An earring set with a sapphire.' },
sapphire_ring = { name = 'sapphire_ring', label = 'Sapphire Ring', weight = 150, type = 'item', image = 'sapphire_ring.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A ring set with a sapphire.' },
saxo = { name = 'saxo', label = 'Saxophone', weight = 3000, type = 'item', image = 'saxo.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A brass saxophone.' },
silver_bracelet = { name = 'silver_bracelet', label = 'Silver Bracelet', weight = 200, type = 'item', image = 'silver_bracelet.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A silver bracelet.' },
silver_chain = { name = 'silver_chain', label = 'Silver Chain', weight = 200, type = 'item', image = 'silver_chain.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A silver chain.' },
silver_watch = { name = 'silver_watch', label = 'Silver Watch', weight = 250, type = 'item', image = 'silver_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A silver watch.' },
skull_alien = { name = 'skull_alien', label = 'Alien Skull', weight = 800, type = 'item', image = 'skull_alien.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A strange alien skull.' },
statue1_men = { name = 'statue1_men', label = "Men's Statue", weight = 6000, type = 'item', image = 'statue1_men.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A heavy statue of a man.' },
statue1_panther = { name = 'statue1_panther', label = 'Panther Statue', weight = 8000, type = 'item', image = 'statue1_panther.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A heavy panther statue.' },
statue1_women = { name = 'statue1_women', label = "Women's Statue", weight = 6000, type = 'item', image = 'statue1_women.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A heavy statue of a woman.' },
toothgold = { name = 'toothgold', label = 'Gold Tooth', weight = 100, type = 'item', image = 'toothgold.png', unique = false, useable = false, shouldClose = false, combinable = nil, description = 'A gold tooth.' },
vase_modern = { name = 'vase_modern', label = 'Modern Vase', weight = 1200, type = 'item', image = 'vase_modern.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A sleek modern vase.' },
violet_classic_watch = { name = 'violet_classic_watch', label = 'Violet Classic Watch', weight = 250, type = 'item', image = 'violet_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with a violet finish.' },
violet_digital_watch = { name = 'violet_digital_watch', label = 'Violet Digital Watch', weight = 200, type = 'item', image = 'violet_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A violet digital watch.' },
white_classic_watch = { name = 'white_classic_watch', label = 'White Classic Watch', weight = 250, type = 'item', image = 'white_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with a white finish.' },
white_digital_watch = { name = 'white_digital_watch', label = 'White Digital Watch', weight = 200, type = 'item', image = 'white_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A white digital watch.' },
yellow_classic_watch = { name = 'yellow_classic_watch', label = 'Yellow Classic Watch', weight = 250, type = 'item', image = 'yellow_classic_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A classic watch with a yellow finish.' },
yellow_digital_watch = { name = 'yellow_digital_watch', label = 'Yellow Digital Watch', weight = 200, type = 'item', image = 'yellow_digital_watch.png', unique = true, useable = false, shouldClose = false, combinable = nil, description = 'A yellow digital watch.' },
```
{% endtab %}

{% tab title="ESX built-in" %}
Only for the ESX built-in inventory. Run in your database:

```sql
INSERT INTO items (name, label, weight, rare, can_remove) VALUES
('antique_vase', 'Antique Vase', 1500, 0, 1),
('antiqueartifact', 'Antique Artifact', 2000, 0, 1),
('bear', 'Bear Plushie', 500, 0, 1),
('beatbox', 'Beatbox', 2500, 0, 1),
('black_classic_watch', 'Black Classic Watch', 250, 0, 1),
('black_digital_watch', 'Black Digital Watch', 200, 0, 1),
('blue_classic_watch', 'Blue Classic Watch', 250, 0, 1),
('blue_digital_watch', 'Blue Digital Watch', 200, 0, 1),
('blue_gameboy', 'Blue Gameboy', 400, 0, 1),
('cheap_necklace', 'Cheap Necklace', 100, 0, 1),
('colle_alien', 'Alien Figurine', 700, 0, 1),
('colle_beast', 'Beast Figurine', 800, 0, 1),
('colle_bigfoot', 'Bigfoot Figurine', 900, 0, 1),
('colle_imporage', 'Imporage Figurine', 800, 0, 1),
('colle_pogo', 'Pogo Figurine', 600, 0, 1),
('colle_prbubble', 'Prbubble Figurine', 700, 0, 1),
('colle_rsrcomm', 'Rsr Comm Figurine', 750, 0, 1),
('colle_rsrgeneric', 'Rsr Generic Figurine', 750, 0, 1),
('console_cjd500', 'CJD-500 Console', 800, 0, 1),
('diamond', 'Diamond', 1000, 0, 1),
('diamond_ring', 'Diamond Ring', 1500, 0, 1),
('electronickit', 'Electronic Kit', 100, 0, 1),
('gameboy', 'Yellow Gameboy', 400, 0, 1),
('gold_bracelet', 'Gold Bracelet', 200, 0, 1),
('gold_chain', 'Gold Chain', 200, 0, 1),
('indigo_classic_watch', 'Indigo Classic Watch', 250, 0, 1),
('indigo_digital_watch', 'Indigo Digital Watch', 200, 0, 1),
('limited_jewelry', 'Limited Jewelry', 300, 0, 1),
('old_watch', 'Old Watch', 250, 0, 1),
('orange_classic_watch', 'Orange Classic Watch', 250, 0, 1),
('orange_digital_watch', 'Orange Digital Watch', 200, 0, 1),
('perle_high', 'Perle High', 150, 0, 1),
('perle_mid', 'Perle Mid', 150, 0, 1),
('perle_rare', 'Perle Rare', 150, 0, 1),
('pink_classic_watch', 'Pink Classic Watch', 250, 0, 1),
('pink_digital_watch', 'Pink Digital Watch', 200, 0, 1),
('plush_01a', 'Pink Plushie', 400, 0, 1),
('plush_02a', 'Green Plushie', 400, 0, 1),
('plush_03a', 'Blue Plushie', 400, 0, 1),
('plush_05a', 'Mexican Plushie', 450, 0, 1),
('plush_06a', 'Red Plushie', 400, 0, 1),
('plush_07a', 'Anime Plushie', 400, 0, 1),
('plush_08a', 'Anime Plushie', 400, 0, 1),
('plush_09a', 'Old Master Plushie', 450, 0, 1),
('red_classic_watch', 'Red Classic Watch', 250, 0, 1),
('red_digital_watch', 'Red Digital Watch', 200, 0, 1),
('rolex', 'Golden Watch', 1500, 0, 1),
('ruby_ring', 'Ruby Ring', 150, 0, 1),
('sapphire_earring', 'Sapphire Earring', 100, 0, 1),
('sapphire_ring', 'Sapphire Ring', 150, 0, 1),
('saxo', 'Saxophone', 3000, 0, 1),
('silver_bracelet', 'Silver Bracelet', 200, 0, 1),
('silver_chain', 'Silver Chain', 200, 0, 1),
('silver_watch', 'Silver Watch', 250, 0, 1),
('skull_alien', 'Alien Skull', 800, 0, 1),
('statue1_men', 'Men''s Statue', 6000, 0, 1),
('statue1_panther', 'Panther Statue', 8000, 0, 1),
('statue1_women', 'Women''s Statue', 6000, 0, 1),
('toothgold', 'Gold Tooth', 100, 0, 1),
('vase_modern', 'Modern Vase', 1200, 0, 1),
('violet_classic_watch', 'Violet Classic Watch', 250, 0, 1),
('violet_digital_watch', 'Violet Digital Watch', 200, 0, 1),
('white_classic_watch', 'White Classic Watch', 250, 0, 1),
('white_digital_watch', 'White Digital Watch', 200, 0, 1),
('yellow_classic_watch', 'Yellow Classic Watch', 250, 0, 1),
('yellow_digital_watch', 'Yellow Digital Watch', 200, 0, 1);
```

{% hint style="danger" %}
The ESX built-in inventory has no stashes, so shop storage, counter sales and the warehouse do not work with it. Use `ox_inventory`.
{% endhint %}
{% endtab %}
{% endtabs %}

### 3. Item images

The shop's own menus find item images automatically: first in your inventory's image folder, then in the `_images/` folder that ships with the resource. You don't need to do anything for the shop menus.

Your **inventory** only shows images it has itself. Copy every `.png` from `aura_pawnshop/_images/` into your inventory's image folder:

| Inventory | Image folder |
| --- | --- |
| `ox_inventory` | `ox_inventory/web/images/` |
| `qb-inventory` | `qb-inventory/html/images/` |
| `ps-inventory` | `ps-inventory/html/images/` |
| `qs-inventory` | `qs-inventory/html/images/` |
| `codem-inventory` | `codem-inventory/html/itemimages/` |
| others | the folder your inventory documents |

{% hint style="warning" %}
Do not host images on imgur or Discord. Those links expire or get blocked, and the images stop showing for everyone.
{% endhint %}

### 4. Check it

Restart the server. Every missing item prints a red line in the server console:

```
[pawnshop] invalid item 'rolex' in Marketplace.basePrices — not in the items database, skipped
```

No red lines means every item was found. To check one item in game, run `/pawnitems rolex` as an admin and read the server console ([Commands](./commands.md)).

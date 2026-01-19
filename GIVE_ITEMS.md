# Giving Items to Players

This guide covers how to give players items (including enchanted ones) via rcon commands on the Minecraft server.

## Basic Commands

### Command Format via flyctl

All commands are executed through the Fly.io SSH console:

```bash
flyctl ssh console --app da-mines -C "rcon-cli <command>"
```

### Basic Give Syntax

```
/give <player> <item> [amount]
```

**Examples:**
```bash
# Give 64 diamonds
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond 64"

# Give 1 diamond sword
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_sword"

# Give 16 golden apples
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName golden_apple 16"

# Give enchanted golden apple (Notch apple)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName enchanted_golden_apple"
```

---

## Enchantments Reference

### Weapon Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Sharpness | `sharpness` | 5 | Sword, Axe |
| Smite | `smite` | 5 | Sword, Axe |
| Bane of Arthropods | `bane_of_arthropods` | 5 | Sword, Axe |
| Knockback | `knockback` | 2 | Sword |
| Fire Aspect | `fire_aspect` | 2 | Sword |
| Looting | `looting` | 3 | Sword |
| Sweeping Edge | `sweeping_edge` | 3 | Sword |
| Cleaving | `cleaving` | 3 | Axe (Combat) |

### Armor Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Protection | `protection` | 4 | All Armor |
| Fire Protection | `fire_protection` | 4 | All Armor |
| Blast Protection | `blast_protection` | 4 | All Armor |
| Projectile Protection | `projectile_protection` | 4 | All Armor |
| Thorns | `thorns` | 3 | All Armor |
| Respiration | `respiration` | 3 | Helmet |
| Aqua Affinity | `aqua_affinity` | 1 | Helmet |
| Feather Falling | `feather_falling` | 4 | Boots |
| Depth Strider | `depth_strider` | 3 | Boots |
| Frost Walker | `frost_walker` | 2 | Boots |
| Soul Speed | `soul_speed` | 3 | Boots |
| Swift Sneak | `swift_sneak` | 3 | Leggings |

### Tool Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Efficiency | `efficiency` | 5 | Pickaxe, Shovel, Axe, Hoe, Shears |
| Silk Touch | `silk_touch` | 1 | Pickaxe, Shovel, Axe, Hoe |
| Fortune | `fortune` | 3 | Pickaxe, Shovel, Axe, Hoe |

### Bow Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Power | `power` | 5 | Bow |
| Punch | `punch` | 2 | Bow |
| Flame | `flame` | 1 | Bow |
| Infinity | `infinity` | 1 | Bow |

### Crossbow Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Quick Charge | `quick_charge` | 3 | Crossbow |
| Multishot | `multishot` | 1 | Crossbow |
| Piercing | `piercing` | 4 | Crossbow |

### Trident Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Loyalty | `loyalty` | 3 | Trident |
| Impaling | `impaling` | 5 | Trident |
| Riptide | `riptide` | 3 | Trident |
| Channeling | `channeling` | 1 | Trident |

### Mace Enchantments (1.21+)

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Density | `density` | 5 | Mace |
| Breach | `breach` | 4 | Mace |
| Wind Burst | `wind_burst` | 3 | Mace |

### Universal Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Unbreaking | `unbreaking` | 3 | All Equipment |
| Mending | `mending` | 1 | All Equipment |
| Curse of Vanishing | `vanishing_curse` | 1 | All Equipment |
| Curse of Binding | `binding_curse` | 1 | All Armor |

### Fishing Rod Enchantments

| Enchantment | ID | Max Level | Applies To |
|-------------|-----|-----------|------------|
| Luck of the Sea | `luck_of_the_sea` | 3 | Fishing Rod |
| Lure | `lure` | 3 | Fishing Rod |

---

## Item Components (1.21+ Format)

Minecraft 1.21+ uses a new component-based system for item data. Components are added in square brackets after the item name.

### Enchantments Component

```
item[enchantments={enchant1:level,enchant2:level}]
```

**Example:**
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_sword[enchantments={sharpness:5,unbreaking:3,mending:1}]"
```

### Custom Name Component

```
item[custom_name='\"Display Name\"']
```

**Example:**
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_sword[custom_name='\"Excalibur\"']"
```

### Lore Component

```
item[lore=['\"Line 1\"','\"Line 2\"']]
```

**Example:**
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_sword[lore=['\"A legendary blade\"','\"Forged in dragon fire\"']]"
```

### Unbreakable Component

```
item[unbreakable={}]
```

**Example:**
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_pickaxe[unbreakable={}]"
```

### Damage Component (Durability)

```
item[damage=<value>]
```

The `damage` value represents how much durability has been used (0 = full durability).

**Example:**
```bash
# Give a diamond sword with half durability used (max is 1561)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_sword[damage=780]"
```

### Combining Components

Components can be combined with commas:

```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_sword[enchantments={sharpness:5,mending:1},custom_name='\"Excalibur\"',unbreakable={}]"
```

---

## Comprehensive Examples

### Weapons

#### Diamond Sword (Max Enchants)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_sword[enchantments={sharpness:5,knockback:2,fire_aspect:2,looting:3,sweeping_edge:3,unbreaking:3,mending:1}]"
```

#### Netherite Sword (Max Enchants)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_sword[enchantments={sharpness:5,knockback:2,fire_aspect:2,looting:3,sweeping_edge:3,unbreaking:3,mending:1}]"
```

#### Diamond Axe (Combat)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_axe[enchantments={sharpness:5,unbreaking:3,mending:1}]"
```

#### Smite Sword (Undead Slayer)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_sword[enchantments={smite:5,knockback:2,fire_aspect:2,looting:3,unbreaking:3,mending:1}]"
```

#### Mace (1.21+)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName mace[enchantments={density:5,breach:4,wind_burst:3,unbreaking:3,mending:1}]"
```

#### Trident (Loyalty)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName trident[enchantments={loyalty:3,impaling:5,unbreaking:3,mending:1}]"
```

#### Trident (Riptide)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName trident[enchantments={riptide:3,impaling:5,unbreaking:3,mending:1}]"
```

#### Trident (Channeling)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName trident[enchantments={channeling:1,loyalty:3,impaling:5,unbreaking:3,mending:1}]"
```

### Armor

#### Netherite Helmet (Max Protection)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_helmet[enchantments={protection:4,respiration:3,aqua_affinity:1,thorns:3,unbreaking:3,mending:1}]"
```

#### Netherite Chestplate (Max Protection)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_chestplate[enchantments={protection:4,thorns:3,unbreaking:3,mending:1}]"
```

#### Netherite Leggings (Max Protection)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_leggings[enchantments={protection:4,swift_sneak:3,thorns:3,unbreaking:3,mending:1}]"
```

#### Netherite Boots (Max Protection)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_boots[enchantments={protection:4,feather_falling:4,depth_strider:3,soul_speed:3,thorns:3,unbreaking:3,mending:1}]"
```

#### Fire Protection Set
```bash
# Helmet
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_helmet[enchantments={fire_protection:4,respiration:3,aqua_affinity:1,unbreaking:3,mending:1}]"

# Chestplate
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_chestplate[enchantments={fire_protection:4,unbreaking:3,mending:1}]"

# Leggings
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_leggings[enchantments={fire_protection:4,unbreaking:3,mending:1}]"

# Boots
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_boots[enchantments={fire_protection:4,feather_falling:4,unbreaking:3,mending:1}]"
```

#### Elytra (Max Enchants)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName elytra[enchantments={unbreaking:3,mending:1}]"
```

### Tools

#### Diamond Pickaxe (Fortune)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_pickaxe[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1}]"
```

#### Diamond Pickaxe (Silk Touch)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_pickaxe[enchantments={efficiency:5,silk_touch:1,unbreaking:3,mending:1}]"
```

#### Netherite Pickaxe (Fortune)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_pickaxe[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1}]"
```

#### Netherite Pickaxe (Silk Touch)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_pickaxe[enchantments={efficiency:5,silk_touch:1,unbreaking:3,mending:1}]"
```

#### Diamond Shovel
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_shovel[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1}]"
```

#### Diamond Hoe
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_hoe[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1}]"
```

#### Shears
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName shears[enchantments={efficiency:5,unbreaking:3,mending:1}]"
```

### Ranged Weapons

#### Bow (Power + Infinity)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName bow[enchantments={power:5,punch:2,flame:1,infinity:1,unbreaking:3}]"
```

#### Bow (Power + Mending)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName bow[enchantments={power:5,punch:2,flame:1,unbreaking:3,mending:1}]"
```

#### Crossbow (Multishot)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName crossbow[enchantments={quick_charge:3,multishot:1,unbreaking:3,mending:1}]"
```

#### Crossbow (Piercing)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName crossbow[enchantments={quick_charge:3,piercing:4,unbreaking:3,mending:1}]"
```

### Special Items

#### Fishing Rod (Max Enchants)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName fishing_rod[enchantments={luck_of_the_sea:3,lure:3,unbreaking:3,mending:1}]"
```

#### Flint and Steel
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName flint_and_steel[enchantments={unbreaking:3,mending:1}]"
```

#### Shield
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName shield[enchantments={unbreaking:3,mending:1}]"
```

#### Carrot on a Stick
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName carrot_on_a_stick[enchantments={unbreaking:3,mending:1}]"
```

#### Warped Fungus on a Stick
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName warped_fungus_on_a_stick[enchantments={unbreaking:3,mending:1}]"
```

### Named Items with Lore

#### Named Sword
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_sword[enchantments={sharpness:5,unbreaking:3,mending:1},custom_name='\"Blade of Legends\"']"
```

#### Sword with Lore
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_sword[enchantments={sharpness:5,mending:1},custom_name='\"Dragonslayer\"',lore=['\"Forged in the End\"','\"Fear the blade\"']]"
```

#### Unbreakable Named Pickaxe
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_pickaxe[enchantments={efficiency:5,fortune:3},custom_name='\"The Excavator\"',unbreakable={}]"
```

### Potions and Tipped Arrows

#### Potions
```bash
# Healing Potion
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName potion[potion_contents={potion:strong_healing}]"

# Strength Potion (Extended)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName potion[potion_contents={potion:long_strength}]"

# Night Vision (Extended)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName potion[potion_contents={potion:long_night_vision}]"

# Fire Resistance (Extended)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName potion[potion_contents={potion:long_fire_resistance}]"

# Invisibility (Extended)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName potion[potion_contents={potion:long_invisibility}]"

# Slow Falling (Extended)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName potion[potion_contents={potion:long_slow_falling}]"

# Water Breathing (Extended)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName potion[potion_contents={potion:long_water_breathing}]"
```

#### Splash Potions
```bash
# Splash Healing
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName splash_potion[potion_contents={potion:strong_healing}]"

# Splash Harming
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName splash_potion[potion_contents={potion:strong_harming}]"
```

#### Tipped Arrows
```bash
# Arrow of Harming (64)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName tipped_arrow[potion_contents={potion:strong_harming}] 64"

# Arrow of Poison (64)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName tipped_arrow[potion_contents={potion:strong_poison}] 64"

# Arrow of Slowness (64)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName tipped_arrow[potion_contents={potion:long_slowness}] 64"

# Arrow of Weakness (64)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName tipped_arrow[potion_contents={potion:long_weakness}] 64"

# Spectral Arrow (64)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName spectral_arrow 64"
```

---

## God Items (Maximum Enchantments)

### God Sword
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_sword[enchantments={sharpness:5,knockback:2,fire_aspect:2,looting:3,sweeping_edge:3,unbreaking:3,mending:1},custom_name='\"God Sword\"']"
```

### God Pickaxe (Fortune)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_pickaxe[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1},custom_name='\"God Pickaxe\"']"
```

### God Pickaxe (Silk Touch)
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_pickaxe[enchantments={efficiency:5,silk_touch:1,unbreaking:3,mending:1},custom_name='\"Silk Pickaxe\"']"
```

### God Axe
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_axe[enchantments={efficiency:5,sharpness:5,fortune:3,unbreaking:3,mending:1},custom_name='\"God Axe\"']"
```

### God Shovel
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_shovel[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1},custom_name='\"God Shovel\"']"
```

### God Hoe
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_hoe[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1},custom_name='\"God Hoe\"']"
```

### God Bow
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName bow[enchantments={power:5,punch:2,flame:1,infinity:1,unbreaking:3},custom_name='\"God Bow\"']"
```

### God Trident
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName trident[enchantments={loyalty:3,impaling:5,channeling:1,unbreaking:3,mending:1},custom_name='\"God Trident\"']"
```

### God Mace
```bash
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName mace[enchantments={density:5,breach:4,wind_burst:3,unbreaking:3,mending:1},custom_name='\"God Mace\"']"
```

---

## Bulk Commands / Kits

### Full God Armor Set

Copy and run each command:

```bash
# Helmet
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_helmet[enchantments={protection:4,respiration:3,aqua_affinity:1,thorns:3,unbreaking:3,mending:1}]"

# Chestplate
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_chestplate[enchantments={protection:4,thorns:3,unbreaking:3,mending:1}]"

# Leggings
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_leggings[enchantments={protection:4,swift_sneak:3,thorns:3,unbreaking:3,mending:1}]"

# Boots
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_boots[enchantments={protection:4,feather_falling:4,depth_strider:3,soul_speed:3,thorns:3,unbreaking:3,mending:1}]"
```

### Starter Kit

```bash
# Iron tools
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_pickaxe"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_axe"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_shovel"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_sword"

# Iron armor
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_helmet"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_chestplate"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_leggings"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName iron_boots"

# Food and basics
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName cooked_beef 64"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName torch 64"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName oak_planks 64"
```

### Mining Kit

```bash
# Fortune pickaxe
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_pickaxe[enchantments={efficiency:5,fortune:3,unbreaking:3,mending:1}]"

# Silk touch pickaxe
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_pickaxe[enchantments={efficiency:5,silk_touch:1,unbreaking:3,mending:1}]"

# Shovel
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName diamond_shovel[enchantments={efficiency:5,unbreaking:3,mending:1}]"

# Torches
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName torch 64"

# Food
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName golden_carrot 64"
```

### Combat Kit

```bash
# Sword
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName netherite_sword[enchantments={sharpness:5,knockback:2,fire_aspect:2,looting:3,sweeping_edge:3,unbreaking:3,mending:1}]"

# Bow
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName bow[enchantments={power:5,punch:2,flame:1,infinity:1,unbreaking:3}]"

# Arrow
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName arrow 64"

# Shield
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName shield[enchantments={unbreaking:3,mending:1}]"

# Golden apples
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName golden_apple 16"
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName enchanted_golden_apple 4"

# Totems
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName totem_of_undying 2"
```

### Elytra Travel Kit

```bash
# Elytra
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName elytra[enchantments={unbreaking:3,mending:1}]"

# Firework rockets (duration 3)
flyctl ssh console --app da-mines -C "rcon-cli give PlayerName firework_rocket[fireworks={flight_duration:3}] 64"
```

---

## Tips

1. **Replace `PlayerName`** with the actual player's username in all commands.

2. **Incompatible enchantments** cannot be combined:
   - Sharpness / Smite / Bane of Arthropods (choose one)
   - Protection / Fire Protection / Blast Protection / Projectile Protection (choose one)
   - Silk Touch / Fortune (choose one)
   - Infinity / Mending (choose one)
   - Loyalty / Riptide (choose one)
   - Channeling / Riptide (choose one)
   - Depth Strider / Frost Walker (choose one)
   - Multishot / Piercing (choose one)

3. **Quotes in custom names** - Use escaped quotes for names with spaces.

4. **Command length limits** - Very long commands may need to be split.

5. **Case sensitivity** - All item and enchantment IDs are lowercase with underscores.

6. **Testing** - Test commands on yourself first before giving items to other players.

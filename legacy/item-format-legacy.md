# Item format (Legacy)

## Vanilla Items (not include NBT)

* We use XItemStack item format, click [here](https://github.com/CryptoMorin/XSeries/wiki/XItemStack) to know more.
* **All option except material are optional.**&#x20;
* **Those options also can be used in hook items.**

If you don't understand this format by above link, let me give you an example here:

```yaml
display-item: 
# This is the key option which you use item format here.
  material: APPLE 
  # Minecraft material id. 
  # See all id here: https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html
  name: '&fAn apple a day keeps the doctor away!'
  # Item display name. Support color codes.
  lore: 
    - '&7This is really?'
    - '&7Wait, this is the second line?'
  # Item lore. Support color codes.
  amount: 1
  # Item amount.
  damage: 10
  # Item damage, which means durability.
  skull: 'eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvMzE4N2Q2ODY4NjgwOWFlZGEwOWE3ZmQwNmFmNzUwMzQzYjdmMTdhNDM2MDZkMmZlOTg4N2VlZTNmZjk4YTMwMSJ9fX0='
  # Skill texture, only support 'PLAYER_HEAD' material.
  unbreakable: true
  # Whether this item should unbreakable.
  custom-model-data: 100
  # Item custom model data, useful for ItemsAdder or Oraxen users.
  enchants:
    ARROW_FIRE: 2
    DURABILITY: 3
  # Item enchants, use Enchantment ID: Level as format.
  # https://hub.spigotmc.org/javadocs/spigot/org/bukkit/enchantments/Enchantment.html
  stored-enchants: 
    ARROW_FIRE: 3
  # Stored enchantment in the book are different than the enchantments applied to the item itself.
  # Only support material 'ENCHANTED_BOOK'
  flags: [HIDE_ATTRIBUTES, HIDE_POTION_EFFECTS]
  # Item flags.
  glow: true
  # Whether glow.
  attributes:
    GENERIC_ATTACK_DAMAGE: # https://hub.spigotmc.org/javadocs/spigot/org/bukkit/attribute/Attribute.html
      name: generic.attack_damage # https://minecraft.fandom.com/zh/wiki/%E5%B1%9E%E6%80%A7
      amount: 12
      operation: ADD_NUMBER # https://hub.spigotmc.org/javadocs/spigot/org/bukkit/attribute/AttributeModifier.Operation.html
      slot: HAND # HEAD or CHEST or LEGS or FEET or HAND or OFF_HAND
  spawner: ZOMBIE
  # Set spawner entity type.
  # https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html
```

This example is not 100% show the format, you need click the link above to see more.

## Saved Item

* Use `material` option, like: material: `superior_sword`. `superior_sword` is your saved item ID.

## Hook Item

* hook-plugin: What plugin you want this item hook into, for now, UltimateShop supports `EcoItems, EcoArmor, MMOItems, ItemsAdder, Oraxen, MythicMobs, eco, NeigeItems`. **Required.**
* hook-item: What item you want to in the hook plugin **Required.**:
* For `EcoItems, Oraxen, MythicMobs`, you should write item id.
* For `ItemsAdder, eco`, you should write `namespace:item id`. Eco's namespace id plugin name, like `talismans`.
* For `EcoArmor`, you should write `armor set id;;armor slot`. `armor slot` can be set to **BOOTS, CHESTPLATE, ELYTRA, HELMET, LEGGINGS**.
* For `MMOItems`, you should write `item type id;;item id`.

For example:

```yaml
display-item:
  hook-plugin: MMOItems
  hook-item: AXE;;TEST_AXE
  # Add more enchants for mmoitems item!
  enchants:
    ARROW_FIRE: 2
    DURABILITY: 3
    COIN_REPAIR: 2 # A EcoEnchants enchantment
```

## Extra option: plugin-enchants  - Premium version only

* Support `AdvancedEnchantments` only for now.
* Plugin like `EcoEnchants, ExcellentEnchants` are vanilla enchants like plugin, you just need to put their enchantment ID to enchants option (like above).

You can use plugin-enchants option to add plugin enchants for your item.

```yaml
display-item:
  hook-plugin: MMOItems
  hook-item: AXE;;EXECUTIONER_AXE
  # Add more enchants for mmoitems item!
  enchants:
    ARROW_FIRE: 2
    DURABILITY: 3
    COIN_REPAIR: 2 # A EcoEnchants enchantment
  plugin-enchants:
    PLANTER: 5 # A AdvancedEnchantments enchantment
```

## Extra option: content

* Can use this option to make brushable block has loot item.

```yaml
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    add-lore:
      - '&fBuy it for now: {buy-price}'
    products:
      1:
        material: suspicious_sand
        amount: 1
        name: '&fMagic Sand'
        lore:
          - '&fA sand that includes apple!'
        content:
          material: APPLE
```

## When used in buy price or sell price:

Support use those extra options:

* max-amount: Max amount, useful for dynamic prices. **Optional.**
* min-amount: Min amount, useful for dynamic prices.**Optional.**

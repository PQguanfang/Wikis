# Component Format

{% hint style="info" %}
This feature is only available for **1.21.5+** **Paper** server users.
{% endhint %}

## Custom Name

```yaml
component:
  name: '<blue>A good sword'
```

## Item Name

```yaml
component:
  item-name: '<yellow>Not Bad sword'
```

## Lore

```yaml
component:
  lore:
    - '<gray>This is really nice!'
```

## Custom Model Data

```yaml
component:
  custom-model-data:
    float: # Custom Model Data Type
      - '1'
    flag:
      - 'true'
    string:
      - 'Let me just test it!'
    color:
      - '255, 255, 0'
```

## Max Stack

```yaml
component:
  max-stack: 5
```

## Food

```yaml
component:
  food:
    can-always-eat: true
    nutrition: 5
    saturation: 5
```

## Tool

```yaml
component:
  tool:
    damage-per-block: 5
    mining-speed: 1.3
    destroy-blocks-in-creative: true
    rules:
      # blocks, speed, correctForDrops
      - 'stone, 1.4, true'
```

## Jukebox

```yaml
component:
  song: otherside
```

## Glow

```yaml
component:
  glow: true
```

## Unbreakable

```yaml
component:
  unbreakable: true
```

## Rarity

```yaml
component:
  rarity: COMMON
```

## Hide Tooltips

```yaml
component:
  hide-tooltip:
    - 'lore' # Data Type. For list of them, please view: https://jd.papermc.io/paper/1.21.5/io/papermc/paper/datacomponent/DataComponentTypes.html
```

## Enchants

```yaml
component:
  enchants:
    mending: 1 # Enchant ID: Level
```

## Attributes

```yaml
component:
  attributes:
    GENERIC_MAX_HEALTH: # Attribute ID
      name: 'UltiamteShop'
      amount: 5
      operation: ADD_NUMBER
      slot: ANY
```

# Rotate Product

You can create dynamic rotate product in shop by using our conditions system.

First, you need add conditions section at `products` config, if you have `display-item` section, you need use our [Display Item Format](../base/display-item-format.md).

Here is an example:

```yaml
items:
  A:
    price-mode: CLASSIC_ANY
    product-mode: CLASSIC_ANY
    display-item:
      # Condition ID
      1:
        material: APPLE
        amount: 12
        name: '&eApple'
        lore:
          - '&fToday product:'
          - '&7  - Apple'
          - '{random_rotate}'
      # Condition ID
      2:
        material: RED_WOOL
        amount: 12
        name: '&eRed Wool'
        lore:
          - '&fToday product:'
          - '&7  - Red Wool'
          - ''
      # Condition ID
      3:
        material: WHEAT
        amount: 12
        name: '&eWheat'
        lore:
          - '&fToday product:'
          - '&7  - Wheat'
          - ''
    display-item-conditions:
      1: 
        # Check conditions page for more info
        - 'placeholder: {random_rotate};;==;;A'
      2: 
        - 'placeholder: {random_rotate};;==;;B'
      3:
        - 'placeholder: {random_rotate};;==;;C'
    products:
      1:
        material: APPLE
        amount: 1
        conditions:
          - 'placeholder: {random_rotate};;==;;A'
      2:
        material: RED_WOOL
        amount: 1
        conditions:
          - 'placeholder: {random_rotate};;==;;B'   
      3:
        material: WHEAT
        amount: 1
        conditions:
          - 'placeholder: {random_rotate};;==;;C'  
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 2
        placeholder: '&6{amount} Coins'
        start-apply: 0  
    sell-prices:
      1:
        economy-plugin: Vault
        amount: 1
        placeholder: '&6{amount} Coins'
        start-apply: 0
    sell-limits:
      global: 640
      default: 128
      vip: 192
    sell-limits-conditions:
      vip:
        - 'permission: group.vip'
    sell-limits-reset-mode: 'TIMED'
    sell-limits-reset-time: '00:00:00'  
```

In this example, we used `{random_rotate}` placeholder in placeholder condition. You need register this random placeholder at `config.yml`.

```yaml
placeholder:
  # Premium version only.
  random:
    rotate:
      reset-mode: TIMED
      reset-time: '00:00:00'
      elements:
        - 'A'
        - 'B'
        - 'C'
```

In this example, we register a random placeholder called rotate. It will refresh every day at 0:00:00.

If this random placeholder picked **A** element, today's product is **Apple**, becuase only apple product and display item will meet the placeholder condition. Similar to B and C element.

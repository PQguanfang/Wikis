# 📂Shops

An example shop file is here:

```yaml
settings:
  menu: 'example-shop-menu'
  buy-more: true
  shop-name: 'Food Shop'
  hide-message: false
  
general-configs:
  # This means all products in this shop will use this price mode and product mode.
  # unless they have set other value.
  price-mode: CLASSIC_ANY
  product-mode: CLASSIC_ANY
  # Support all product options, like prices, products, limits and so on!
  fail-actions:
    1:
      type: sound
      sound: block.note_block.bass
    
items:
  A:
    display-name: "Apple"
    price-mode: ANY
    product-mode: ALL
    products:
      1:
        material: APPLE
        amount: 1
      2: 
        material: BREAD
        amount: 5
        conditions:
          1:
            type: permission: 
            permission: 'group.vip'
        give-actions:
          1:
            type: message
            message: 'Wow, seems that you are a VIP player, so we bonud give you 5 breads!'
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 200
        placeholder: '{amount} Coins'
        start-apply: 0
      2:
        economy-plugin: PlayerPoints
        amount: 10
        placeholder: '{amount} Points'
        start-apply: 5
    sell-prices:
      1:
        economy-plugin: Vault
        amount: 50
        placeholder: '{amount} Coins'
      2:
        economy-plugin: PlayerPoints
        amount: 1
        start-apply: 5
        placeholder: '{amount} Points'
        give-actions:
          1: 
            type: message: 
            message: 'Wow, seems that you have already sell 5 apples!'
    buy-actions:
      1:
        type: player_command
        command: 'say %player_name% purchased an Apple!'
      2:
        type: announcement
        message: '&7%player_name% purchased an Apple!'
  B:
    display-item:
      material: BREAD
      name: '&cSuper Bread'
    display-name: "Bread"
    add-lore:
      - '@a&ePurchase: {buy-price}'
      - '@b&eSell: {sell-price}'
    bedrock:
      hide: false
      icon: 'url;;https://raw.githubusercontent.com/Jens-Co/MinecraftItemImages/main/1.20/bread.png'
    buy-more: true
    buy-more-menu:
      menu: buy-more-2
      max-amount: 16
    price-mode: ANY
    product-mode: ALL
    products:
      1:
        material: BREAD
        amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 200
        placeholder: '{amount} Coins'
        start-apply: 0
      2:
        economy-plugin: PlayerPoints
        amount: 10
        placeholder: '{amount} Points'
        start-apply: 5
    sell-prices:
      1:
        economy-plugin: Vault
        amount: 50
        placeholder: '{amount} Coins'
      2:
        economy-plugin: PlayerPoints
        amount: 1
        start-apply: 5
        placeholder: '{amount} Points'
    buy-limits:
      global: 100
      default: 10
      test-condition: 20
    buy-limits-conditions:
      test-condition:
        1:
          type: permission
          permission: 'test.permission'
    buy-times-reset-mode: 'TIMED'
    buy-times-reset-time: '00:00:00'
  C:
    display-item: 
      material: DIAMOND
    as-sub-button: A
buttons:
  a:
    display-item:
      material: arrow
      name: '&cPrevious page'
      lore:
        - '&7Click to view previous page!'
    actions:
      - 'shop_menu: crops'    
```

## Settings

* menu: Shop menu name, which means menu file name.
* buy-more: Whether product in this shop can open buy more menu.
* shop-name: Shop display name, which used in `{shop-name}` placeholder.
* hide-message: Whether we hide the messages that will send after player buy or sell items in this shop.

## General Configs

The product configuration options set here will apply to all products. For `buy-action`, `sell-actions` and `fail-actions`, we will auto merge the value set here and in product configs.

## Items

Items is products, product can not only be real items, but also virtual items, like 100 gems economy.

For more info, please view [Products](products.md) page.

## Buttons

Shops can add buttons which has custom actions when player clicks it, view [Menus](../menus/general-menus.md) page for more info.

## Different from single thing's give-actions and item's buy-actions/sell-actions&#x20;

* `give-actions` only executed when the single thing is used and give to player. `buy-actions/sell-actions` will always executed when player successfully buy or sell the item.&#x20;
* `give-actions`'s `{amount}` placeholder will return the single price/product amount, `buy-actions/sell-actions` will return the amount player buy or sell the item in this time. For example, player sell 64x apple, and obtain 100 coins by this, `give-actions`'s `{amount}` placeholder will return 100, and `buy-actions/sell-actions` will return 64.

## Dynamic Value

You can set dynamic value in `buy-prices`, `sell-prices` section's `amount` option and `buy-limits`, `sell-limits` section's value in shop configs.

Also in `buy-prices` and `sell-prices` section, you can set new 2 options:

* max-amount: Price max amount, useful for dynamic prices. **Optional.**
* min-amount: Price min amount, useful for dynamic prices. **Optional.**

Please carefully note that if you want to use our PlaceholderAPI extansion's placeholder, you have to use our new format, for example:

```yaml
    buy-prices:
      1:
        economy-plugin: Vault
        amount: '15 - {sell-times-player} * 0.1 + %ultimateshop_farming_B_sell-times-player% * 0.1'
        # We use the new format without { and } symbol.
        placeholder: '{amount}$'
        start-apply: 0
```

Additionally, you need to set `menu.shop.click-update` to `true` if the related to product is also in the menu you opened. Otherwise this price won't auto update after you sell B product.

## Alternative Options

* `products.XXX.conditions` can be replaced by `products-conditions` section.
* `buy(sell)-prices.XXX.conditions` can be replaced by `buy(sell)-prices-conditions` section.

For example,

```yaml
    products:
      1:
        material: REDSTONE
        amount: 1
    products-conditions:
      1: 
        type: placeholder
        placeholder: '{random_daily-1}'
        rule: '=='
        value: 'A'
```

is same as:

```yaml
    products:
      1:
        material: REDSTONE
        amount: 1
        conditions:
          1:
            type: placeholder
            placeholder: '{random_daily-1}'
            rule: '=='
            value: 'A'
```

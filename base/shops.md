# Shops

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

### Items ID / Product ID

Product ID must be a single char, because we need use them in shop menu `layout` option.

* display-item: Product display item in shop menu, it can be different from the real item player will obtain after purchase. For virtual items, you must set `display-item` here, otherwise they can not be displayed in GUI. For real items, you must enable `auto-set-first-product` option under `display-item` section to let you remove this section, after enable, if `display-item` is not set, the first product real items will be used as display item. This section use [Item format](../legacy/item-format-legacy.md). **Optional (if not set, will use first products)**
  * display-item.modify-lore: Whether we will modify display item lore. **Optional (default to true)**
* display-name: Set product display name in {product} placeholder and buy more menu display item. **Optional.**
* add-lore: Set special [display item add lore](../advanced/display-item-add-lore.md) for this product, if not set, we will use default value set in config.yml. **Optional.**
* bedrock: View [this page](../advanced/bedrock-ui-premium.md).
* buy-more: Set whether this product can open buy more menu, **you must delete shop's buy-more option to make this option has effect! Optional.**
* buy-more-menu: Set up separate buy more menu settings for the product. **Optional. Require 2.2.10+ version.**
* price-mode: Support `ANY, ALL, CLASSIC_ANY, CLASSIC_ALL`. **Required.**
* product-mode: Same as above. **Required if you have products section.**

<table><thead><tr><th width="118">Mode</th><th width="179">ANY</th><th>ALL</th><th>CLASSIC_ANY</th><th>CLASSIC_ALL</th></tr></thead><tbody><tr><td>Product Give</td><td>Give random products that meet conditions.</td><td>Give all products.</td><td>Same as ANY.</td><td>Same as ALL.</td></tr><tr><td>Product /Price Take</td><td>First product/price that we found player meet condition and have enough amount.</td><td>Players must have all products/prices that meet conditions to sell.</td><td>Same as ANY.</td><td>Same as ALL.</td></tr><tr><td>Price Give (means sell)</td><td>First prices meet the condition requirements.</td><td>All prices will be given.</td><td>Same as ANY.</td><td>Same as ALL.</td></tr><tr><td>Price Support</td><td>Support dynamic price &#x26; <code>apply</code> option.</td><td>Same as ALL.</td><td>Price must be same at  everytime.</td><td>Same as CLASSIC_ALL.</td></tr><tr><td>Server  Performances</td><td>Maybe high when you have much buy/sell requests.</td><td>Same as ALL.</td><td>Low, just like other shop plugins doing!</td><td>Same as CLASSIC_ANY.</td></tr></tbody></table>

* products: Product items. Support [Item format](../legacy/item-format-legacy.md) and [Economy format](economy-format.md). You can also add [Custom Sell Match Method](../advanced/custom-item-match-method.md) here. **Optional. If not set, player won't get anything after buy/sell. Useful for command shop.**
  * products.conditions: Player must meet the condition to use this product. **For more info, please view** [**Single Things**](single-things.md) **page.**
  * products.give-actions: The action will run after this product is been give to player, see [Action](../legacy/actions-legacy.md) for more info. **Optional. For more info, please view** [**Single Things**](single-things.md) **page.**
  * products.give-item: Whether we will give this product item to player when he trying to buy.
* buy-prices: Product buy prices. Support [Item format](../legacy/item-format-legacy.md) and [Economy format](economy-format.md). You can also add [Custom Sell Match Method](../advanced/custom-item-match-method.md) here. **Optional. If not set, product can not be purchased.**
  * buy-prices.start-apply: Start which times this price will apply. Only supports `ANY` or `ALL` price type. **Optional. Default to 0.**
  * buy-prices.end-apply: Last times the price will apply. Only supports `ANY` or `ALL` price type. **Optional. Default to infinite.**
  * buy-prices.apply: Which times this price will apply, format: `[1,2,3,4]`. Only supports `ANY` or `ALL` price type. **Optional. Default use start-apply option value.**
  * buy-prices.placeholder: Price display name in {price} placeholder. **Optional. Default unknown language key.**
  * buy-prices.conditions: Player must meet the condition to use this price. **Optional. Default don't have any conditions. For more info, please view** [**Single Things**](single-things.md) **page.**
* sell-prices: Product sell prices. Support [Item format](../legacy/item-format-legacy.md) and [Economy format](economy-format.md). You can also add [Custom Sell Match Method](../advanced/custom-item-match-method.md) here. **Optional. If not set, product can not be selled.**
  * sell-prices also support all sub options like in `buy-prices`.
  * sell-prices.give-actions: The action will run after this sell price is been give to player, see [Action](../legacy/actions-legacy.md) for more info. **Optional. For more info, please view** [**Single Things**](single-things.md) **page.**
* buy-actions: The action will run after buy this product, see [Action](../legacy/actions-legacy.md) for more info. **Optional.**
* sell-actions: The action will run after sell this product, see [Action](../legacy/actions-legacy.md) for more info. **Optional.**
* fail-actions: The action will run if we fail to buy or sell this product, see [Action](../legacy/actions-legacy.md) for more info. **Optional. In example above we put this on general-configs and set it as a fail sound.**
* buy-conditions: The condition player need to meet to buy this product, see [Condition](../legacy/conditions-legacy.md) for more info. **Optional**.
* sell-conditions: The condition player need to meet to sell this product, see [Condition](../legacy/conditions-legacy.md) for more info. **Optional**.
* buy-limits: Set the maximum times of buy/sell times. **Optional. If not set, product can be purchased with unlimited times.**
  * buy-limits.global: Global limit. **Optional.**
  * buy-limits.default: If player don't meet any condition set below, they will use this limit. **Required if you have set buy-limits.**
* buy-limits.\<Condition ID>: Players who meet this condition will use this limit. Condition format can be found at [Conditions](../legacy/conditions-legacy.md). For example:

```yaml
buy-limits:
  default: 10
  vip: 20
buy-limits-conditions:
  vip: 
    - 'permission: test.permission'
```

* sell-limits: Same as buy-limits, but use for sell.
* buy-times-reset-mode/buy-times-reset-time/sell-times-reset-mode/sell-times-reset-time: Please view [this page](buy-sell-times-reset.md).

### Sub Buttons <mark style="color:red;">- Premium</mark>

Sometimes, you want to display same product in different menus, or you want to make 2 or more buttons for same product. Well, `as-sub-button` option can help you. Just set another product ID here, then this button will also be considered as the product you set here.

* display-item: Supports set different display item for sub buttons.
* as-sub-button: Type `Product ID` or `ShopID;;ProductID` here.

## Buttons

Shops can add buttons which has custom actions when player clicks it, view [Menus](menus.md) page for more info.

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

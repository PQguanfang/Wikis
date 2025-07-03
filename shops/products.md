# 🛒Products

Here is an example of 2 product configs:

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: STRING
        amount: 1
        give-actions:
          1:
            type: message
            message: 'You get a string!'
    buy-prices:
      1:
        match-placeholder: '%player_health%'
        amount: '1.65'
        placeholder: '{amount}$'
        start-apply: 0
    sell-prices:
      1:
        match-placeholder: '%player_health%'
        amount: '1.65'
        placeholder: '{amount}$'
        start-apply: 0
        give-actions:
          1:
            type: console_command
            command: 'eco give {player} {amount}'
  B:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: FEATHER
        amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: '0.55'
        placeholder: '{amount}$'
        start-apply: 0
    sell-prices:
      1:
        economy-plugin: Vault
        amount: '0.52'
        placeholder: '{amount}$'
        start-apply: 0
```

## Items ID / Product ID

Product ID must be a single char, because we need use them in shop menu `layout` option.

## General Options

* display-item: Product display item in shop menu, it can be different from the real item player will obtain after purchase. For virtual items, you must set `display-item` here, otherwise they can not be displayed in GUI. For real items, you must enable `auto-set-first-product` option under `display-item` section to let you remove this section, after enable, if `display-item` is not set, the first product real items will be used as display item. This section use [Item format](../format/itemformat-tm/). **Optional (if not set, will use first products)**
  * display-item.modify-lore: Whether we will modify display item lore. **Optional (default to true)**
* display-name: Set product display name in {product} placeholder and buy more menu display item. **Optional.**
* add-lore: Set special [display item add lore](../menus/display-item-add-lore.md) for this product, if not set, we will use default value set in config.yml. **Optional.**
* bedrock: View [this page](../menus/bedrock-menus-premium.md).
* buy-more: Set whether this product can open buy more menu, **you must delete shop's buy-more option to make this option has effect! Optional.**
* buy-more-menu: Set up separate buy more menu settings for the product. **Optional. Require 2.2.10+ version.**
* price-mode: Support `ANY, ALL, CLASSIC_ANY, CLASSIC_ALL`. **Required.**
* product-mode: Same as above. **Required if you have products section.**

<table><thead><tr><th width="118">Mode</th><th width="179">ANY</th><th>ALL</th><th>CLASSIC_ANY</th><th>CLASSIC_ALL</th></tr></thead><tbody><tr><td>Product Give</td><td>Give random products that meet conditions.</td><td>Give all products.</td><td>Same as ANY.</td><td>Same as ALL.</td></tr><tr><td>Product /Price Take</td><td>First product/price that we found player meet condition and have enough amount.</td><td>Players must have all products/prices that meet conditions to sell.</td><td>Same as ANY.</td><td>Same as ALL.</td></tr><tr><td>Price Give (means sell)</td><td>First prices meet the condition requirements.</td><td>All prices will be given.</td><td>Same as ANY.</td><td>Same as ALL.</td></tr><tr><td>Price Support</td><td>Support dynamic price &#x26; <code>apply</code> option.</td><td>Same as ALL.</td><td>Price must be same at  everytime.</td><td>Same as CLASSIC_ALL.</td></tr><tr><td>Server  Performances</td><td>Maybe high when you have much buy/sell requests.</td><td>Same as ALL.</td><td>Low, just like other shop plugins doing!</td><td>Same as CLASSIC_ANY.</td></tr></tbody></table>

* buy-actions: The action will run after buy this product, use [Action Forma](../format/action-format.md)t here. **Optional.**
* sell-actions: The action will run after sell this product,  use [Action Forma](../format/action-format.md)t here. **Optional.**
* fail-actions: The action will run if we fail to buy or sell this product,  use [Action Forma](../format/action-format.md)t here. **Optional. In example above we put this on general-configs and set it as a fail sound.**
* buy-conditions: The condition player need to meet to buy this product, use [Condition Format](../format/condition-format.md) here. **Optional**.
* sell-conditions: The condition player need to meet to sell this product, use [Condition Format](../format/condition-format.md) here. **Optional**.
* buy-limits: Set the maximum times of buy/sell times. **Optional. If not set, product can be purchased with unlimited times.**
  * buy-limits.global: Global limit. **Optional.**
  * buy-limits.default: If player don't meet any condition set below, they will use this limit. **Required if you have set buy-limits.**
* buy-limits.\<Condition ID>: Players who meet this condition will use this limit. Condition format can be found at [Conditions](../format/condition-format.md). For example:

```yaml
buy-limits:
  default: 10
  vip: 20
buy-limits-conditions:
  vip: 
    1:
      type: permission
      permission: 'test.permission'
```

* sell-limits: Same as buy-limits, but use for sell.

## Single Thing Options

This section of the configuration includes the following options:

* buy-prices
* sell-prices
* products

The introduction of these options is on a separate page, please [click here](products-config-single-thing.md) to view.

## Buy/Sell Times Reset Options

This section of the configuration includes the following options:

* buy-times-reset-mode
* buy-times-reset-time
* buy-times-reset-time-format
* sell-times-reset-mode
* sell-times-reset-time
* sell-times-reset-time-format

The introduction of these options is on a separate page, please [click here](product-config-buy-sell-times-reset.md) to view.

## Dynamic Value

You can set placeholders (including PlaceholderAPI) and [Math Calculate Format](../format/math-calculate-format.md) in `buy-prices`, `sell-prices` section's `amount` option and `buy-limits`, `sell-limits` section's value in shop configs.

Available built-in placeholder, for more info about them, please view [Built-In Placeholders](../placeholders/built-in-placeholder.md) page.

* {buy-times-player}
* {buy-times-server}
* {buy-total-player} <mark style="color:red;">**- PREMIUM, 3.8.3+**</mark>
* {buy-total-server} <mark style="color:red;">**- PREMIUM, 3.8.3+**</mark>
* {sell-times-player}
* {sell-times-server}
* {sell-total-player} <mark style="color:red;">**- PREMIUM, 3.8.3+**</mark>
* {sell-total-server} <mark style="color:red;">**- PREMIUM, 3.8.3+**</mark>
* {last-buy-player} <mark style="color:red;">**- PREMIUM**</mark>
* {last-buy-server} <mark style="color:red;">**- PREMIUM**</mark>
* {last-sell-player} <mark style="color:red;">**- PREMIUM**</mark>
* {last-sell-server} <mark style="color:red;">**- PREMIUM**</mark>
* {last-buy-reset-player} <mark style="color:red;">**- PREMIUM**</mark>
* {last-buy-reset-server} <mark style="color:red;">**- PREMIUM**</mark>
* {last-sell-reset-player} <mark style="color:red;">**- PREMIUM**</mark>
* {last-sell-reset-server} <mark style="color:red;">**- PREMIUM**</mark>

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

## Sub Buttons <mark style="color:red;">- Premium</mark>

Sometimes, you want to display same product in different menus, or you want to make 2 or more buttons for same product. Well, `as-sub-button` option can help you. Just set another product ID here, then this button will also be considered as the product you set here.

* display-item: Supports set different display item for sub buttons.
* as-sub-button: Type `Product ID` or `ShopID;;ProductID` here.

The example of **Sub Buttons** can be found at [Shops](shops.md) page, please check out the `C` section under `items` in the head example.

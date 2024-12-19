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

Each single product or price in one product we called **single thing**. So, each product have those thing type:

* Buy Prices: The buy price of this product, player need pay the buy price to obtain this product, if this thing type do not exist (which means `buy-prices` section does not exist in the config), this product can not be purcahsed.
* Sell Prices: The sell price of this product, player need sell the products to shop, then he will get the sell price you set here, if this thing type do not exist (which means `sell-prices` section does not exist in the config), this product can not be sold.
* Products: The products of this  product, player will get the products you set here after buy, and need give his products to shop when selling.

## Items ID / Product ID

Product ID must be a single char, because we need use them in shop menu `layout` option.

## General Options

* display-item: Product display item in shop menu, it can be different from the real item player will obtain after purchase. For virtual items, you must set `display-item` here, otherwise they can not be displayed in GUI. For real items, you must enable `auto-set-first-product` option under `display-item` section to let you remove this section, after enable, if `display-item` is not set, the first product real items will be used as display item. This section use [Item format](broken-reference). **Optional (if not set, will use first products)**
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
    - 'permission: test.permission'
```

* sell-limits: Same as buy-limits, but use for sell.

## Single Thing Options

Each thing type can set unlimited related to single things, like set 5 buy prices, 100 sell prices and even 1k products!

Each single thing have those types:

* Vanilla Item: Use [ItemFormat](../format/itemformat-tm.md) to tell us what Minecraft item you want to sell in shop or you want to player pay. **(Buy/Sell/Products)**
* Hook Item: Use [Supported Plugins](../info/compatibility.md)'s item to tell us what custom item you want to sell in shop or you want to player pay. This type still use [ItemFormat](../format/itemformat-tm.md).**(Buy/Sell/Products)**
* Match Item: Use [Custom Item Match Method](../features/custom-item-match-method.md) to tell us which items you want to match. **(Buy/Products)**
* Vanilla Economy/Hook Economy: Use [EconomyFormat](../format/economyformat-tm.md) to tell us how much money you want to player pay or give to player. **(Buy/Sell/Products)**
* Custom: If those types do not meet your need, you can make a custom single thing! You need add `match-placeholder` option at single thing config to make plugin know what the now amount player have of this custom product/price, and then we will compare the now amount you set here and the required amount. In the example above, we will compare player's health. **If your economy plugins do not supported, just place it's player balance placeholder here and all is solved! (Sell/Products)&#x20;**<mark style="color:red;">**(Premium)**</mark>
* Free: Single thing do not include ItemFormat, EconomyFormat, match-item section and match-placeholder section will be consider as free.

In product configurations, we set the corresponding type of single thing through several options. And according to the type you want, fill in the corresponding config format in these options. There may be additional options to fill in for different single things, as follows:

* products: Product items. Support [Item format](../format/itemformat-tm.md) and [Economy format](../format/economyformat-tm.md). You can also add [Custom Sell Match Method](../features/custom-item-match-method.md) or other things depend on single thing type here. **Optional. If not set, player won't get anything after buy/sell. Useful for command shop.**
  * products.conditions: Player must meet the condition to use this product. **For more info, please view** [**Single Things**](common-examples.md) **page.**
  * products.give-actions: The action will run after this product is been give to player, see [Action](broken-reference) for more info. **Optional. For more info, please view** [**Single Things**](common-examples.md) **page.**
  * products.give-item: Whether we will give this product item to player when he trying to buy.
* buy-prices: Product buy prices. Support Item format and [Economy format](../format/economyformat-tm.md). You can also add [Custom Sell Match Method](../features/custom-item-match-method.md) or other things depend on single thing type here. **Optional. If not set, product can not be purchased.**
  * buy-prices.start-apply: Start which times this price will apply. Only supports `ANY` or `ALL` price type. **Optional. Default to 0.**
  * buy-prices.end-apply: Last times the price will apply. Only supports `ANY` or `ALL` price type. **Optional. Default to infinite.**
  * buy-prices.apply: Which times this price will apply, format: `[1,2,3,4]`. Only supports `ANY` or `ALL` price type. **Optional. Default use start-apply option value.**
  * buy-prices.placeholder: Price display name in {price} placeholder. **Optional. Default unknown language key.**
  * buy-prices.conditions: Player must meet the condition to use this price. **Optional. Default don't have any conditions.**&#x20;
* sell-prices: Product sell prices. Support [Item format](../format/itemformat-tm.md) and [Economy format](../format/economyformat-tm.md). You can also add [Custom Sell Match Method](../features/custom-item-match-method.md) here. **Optional. If not set, product can not be selled.**
  * sell-prices also support all sub options like in `buy-prices`.
  * sell-prices.give-actions: The action will run after this sell price is been give to player, see [Action](../format/action-format.md) for more info. **Optional.**

You may note: you can set action will run when the single thing is been give to player, and set the conditions that player need meet to use the single thing. This is very useful you want to play sound, excute command after player buy or sell.

* Actions: Add `give-actions` section in single thing config. Very useful for command shop, permission shop, enchant shop. Also, **if your economy plugins/item plugins do not supported in UltimateShop, just put the command of give money/item here to solve the problem!** (`{player}` means player name, `{amount}` means the price/product amount) If you want to make the product be actions only, don't forget add `give-item: false` in the single thing option!
* Conditions: Add `conditions` section in single thing config.&#x20;

## Buy/Sell Times Reset Options

### Option Types

Buy times have those options:

* buy-times-reset-mode (before 3.3.0 is buy-limits-reset-mode, but they are same)
* buy-times-reset-time (before 3.3.0 is buy-limits-reset-time, but they are same)
* buy-times-reset-format

Sell times have those options:

* sell-times-reset-mode (before 3.3.0 is sell-limits-reset-mode, but they are same)
* sell-times-reset-time (before 3.3.0 is sell-limits-reset-time, but they are same)
* sell-times-reset-format

If you want to enable buy times and sell times reset for all products, you can simply modify it at `config.yml` file.

```yaml
use-times:
  default-reset-mode: 'NEVER'
  default-reset-time: '00:00:00'
  # This only works for CUSTOM type of reset mode.
  default-reset-time-format: 'yyyy-MM-dd HH:mm:ss'
```

No matter what methods you set it up in, we can see that this feature consists of three option types:

* reset mode
* reset time
* reset time format (only required for CUSTOM type)

### Reset Mode

Support those modes:

* NEVER:&#x20;
* TIMER: It will reset after the time you specify, for example, after 5 hours.
* TIMED: It will be reset at the corresponding time, such as 8:15 pm.
* COOLDOWN\_TIMER (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* COOLDOWN\_TIMED (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* RANDOM\_PLACEHOLDER: Synchronize with the reset time of the specified random placeholder. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* CUSTOM: Directly enter the reset time in reset time, and the plugin will not perform any calculations. Recommend obtain reset time through the Placeholder API results. You need set time format at `reset-time-format` type option to helps us know how does your PlaceholderAPI results be like. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>

### Difference between COOLDOWN\_TIMED (or COOLDOWN\_TIMER) and TIMED (or TIMER)

`TIMED` and `TIMER` will start generating reset time after each buy or sell until the player reaches the limit, while `COOLDOWN_TIMED` and `COOLDOWN_TIMER` will start generating reset time after the first buy or sell and will never update the reset time until the reset time reached.

For this reason, when using `COOLDOWN_TIMED` or `COOLDOWN_TIMER` mode, the reset time will not automatically adjust due to server restarts, configuration modifications, or other reasons. This means that if you mistakenly set the product to refresh after 1 year, the reset time will not automatically change due to your correction, but `TIMED` or `TIMER` rules can do this.

### Reset Time

Different reset modes require different values to be filled in here. Supports placeholders, <mark style="color:red;">**the placeholder used here must be on the server side, which means that all players receive the same value.**</mark>

#### NEVER

Don't need anything here.

#### TIMER/COOLDOWN\_TIMER

You can enter 3 to 5 numbers here, separated by a `:` symbol between each number. For example: `15:00:00`.

Each number from **right** to **left** represents:

* Seconds
* Minutes
* Hours
* Days <mark style="color:red;">**- Premium**</mark>
* Months <mark style="color:red;">**- Premium**</mark>

In this example, represents 15 hours later. Which means: **if now time is 2023-09-04 12:00:00. Will reset after 15 hours, which means 2023-09-05 03:00:00.**

#### TIMED/COOLDOWN\_TIMED

The composition of TIMED and TIMER is almost identical, but the first three digits from the right-hand side represent the time of day. Let's also take 15:00:00 as an example:

If now time is 2023-09-04 12:00:00, will reset at 2023-09-04 15:00:00.

This is the result obtained with days set to 0. If you set it to 1, we will add another day, and that's it.

It is worth noting that if you want to do a daily store, days should be set to 0, and if you want to do a weekly store, days should be set to 6. Because you need to reset the number of times on the last day, not on the second day after the last day, right?

#### CUSTOM <mark style="color:red;">**- Premium**</mark>

You only need to enter a Placeholder API placeholder here, and the result of the placeholder must include the complete year, month, day, hour, minute, and second. You also need to enter their format in the reset time format option, because different types of placeholders return different time formats, making it difficult for plugins to achieve uniformity.&#x20;

#### RANDOM\_PLACEHOLDER <mark style="color:red;">**- Premium**</mark>

Enter a valid random placeholder ID here.

### Dynamic Reset Time <mark style="color:red;">**- Premium**</mark>

This example uses a random placeholder to randomly refresh products after 3, 4, or 5 hours, instead of a fixed time refresh.

Created a random placeholder like:

```yaml
  # Premium version only.
  random:
    reset:
      reset-mode: ONCE
      elements:
        - '03:00:00'
        - '04:00:00'
        - '05:00:00'
```

Use this placeholder at `buy-times-reset-time` option.

```yaml
  B:
    price-mode: ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: GOLD_INGOT
        amount: 1
    buy-prices:
      # 
    sell-prices:
      #
    buy-limits:
      default: '2'
    buy-times-reset-mode: 'TIMED'
    buy-times-reset-time: '{random_reset}' # <--- Used here, sell-times also works!
```

### Reset Time do not correct?

* The product must have been purchased or selled once before the next reset time can be stored. Otherwise, we can only display the possible reset time calculated based on the current time after the transaction is completed.

## Sub Buttons <mark style="color:red;">- Premium</mark>

Sometimes, you want to display same product in different menus, or you want to make 2 or more buttons for same product. Well, `as-sub-button` option can help you. Just set another product ID here, then this button will also be considered as the product you set here.

* display-item: Supports set different display item for sub buttons.
* as-sub-button: Type `Product ID` or `ShopID;;ProductID` here.

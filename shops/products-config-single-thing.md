# 💰Products Config: Single Thing

Each single product or price in one product we called **single thing**. So, each product have those thing type:

* Buy Prices: The buy price of this product, player need pay the buy price to obtain this product, if this thing type do not exist (which means `buy-prices` section does not exist in the config), this product can not be purcahsed.
* Sell Prices: The sell price of this product, player need sell the products to shop, then he will get the sell price you set here, if this thing type do not exist (which means `sell-prices` section does not exist in the config), this product can not be sold.
* Products: The products of this  product, player will get the products you set here after buy, and need give his products to shop when selling.

## Single Thing Types

Each thing type can set unlimited related to single things, like set 5 buy prices, 100 sell prices and even 1k products!

Each single thing have those types:

* Vanilla Item: Use [ItemFormat](../format/itemformat-tm/) to tell us what Minecraft item you want to sell in shop or you want to player pay. **(Buy/Sell/Products)**
* Hook Item: Use [Supported Plugins](../info/compatibility.md)'s item to tell us what custom item you want to sell in shop or you want to player pay. This type still use [ItemFormat](../format/itemformat-tm/).**(Buy/Sell/Products)**
* Match Item: Use [Custom Item Match Method](../features/custom-item-match-method.md) to tell us which items you want to match. **(Buy/Products)**
* Vanilla Economy/Hook Economy: Use [EconomyFormat](../format/economyformat-tm.md) to tell us how much money you want to player pay or give to player. **(Buy/Sell/Products)**
* Custom: If those types do not meet your need, you can make a custom single thing! You need add `match-placeholder` option at single thing config to make plugin know what the now amount player have of this custom product/price, and then we will compare the now amount you set here and the required amount. In the example above, we will compare player's health. **If your economy plugins do not supported, just place it's player balance placeholder here and all is solved! (Sell/Products)&#x20;**<mark style="color:red;">**(Premium)**</mark>
* Free: Single thing do not include ItemFormat, EconomyFormat, match-item section and match-placeholder section will be consider as free.

## Options

```yaml
  A:
    price-mode: ALL
    product-mode: CLASSIC_ANY
    products:
      1:
        material: emerald
      2:
        material: diamond
    buy-prices:
      1:
        economy-plugin: Vault
        amount: '55+({buy-times-server}-{sell-times-server})*0.1'
        max-amount: 5500
        min-amount: 325
        placeholder: '{amount}$'
        start-apply: 0
      2:
        economy-plugin: PlayerPoints
        amount: '2'
        placeholder: '{amount}$'
        start-apply: 5
        end-apply: 15
    sell-prices:
      1:
        economy-plugin: Vault
        amount: '15'
        max-amount: 455
        min-amount: 1
        placeholder: '{amount}$'
        start-apply: 0 
  B:
    products:
      1:
        # The product
        material: APPLE
        amount: 64
        give-actions:
          1:
            multi-once: true
            type: message
            message: 'eco give {player} {amount}'
    buy-prices:
      1:
        # Buy Match Placeholder
        match-placeholder: '%player_health%'
        placeholder: '{amount}$'
        amount: 5
        take-actions:
          1:
            multi-once: true
            type: console_command
            command: 'eco take {player} {amount}'
    sell-prices:
      1:
        # Sell Give Command
        give-actions:
          1:
            type: 'message'
            message: 'eco give {player} {amount} 1'
        amount: 500
        placeholder: '{amount}$'
    
```

In product configurations, we set the corresponding type of single thing through several options. And according to the type you want, fill in the corresponding config format in these options. There may be additional options to fill in for different single things, as follows:

* products: Product items. Support [Item format](../format/itemformat-tm/) and [Economy format](../format/economyformat-tm.md). You can also add [Custom Sell Match Method](../features/custom-item-match-method.md) or other things depend on single thing type here. **Optional. If not set, player won't get anything after buy/sell. Useful for command shop.**
  * products.conditions: Player must meet the condition to use this product. Use [Condition Format](../format/condition-format.md)  here.
  * products.give-actions: The action will run after this product is been give to player. Use [Action Format](../format/action-format.md) here.&#x20;
  * products.take-actions: The action will run after this product is been taken from player. Use [Action Format](../format/action-format.md) here.&#x20;
  * products.give-item: Whether we will give this product item to player when he trying to buy.
* buy-prices: Product buy prices. Support Item format and [Economy format](../format/economyformat-tm.md). You can also add [Custom Sell Match Method](../features/custom-item-match-method.md) or other things depend on single thing type here. **Optional. If not set, product can not be purchased.**
  * buy-prices.start-apply: Start which times this price will apply. Only supports `ANY` or `ALL` price type. **Optional. Default to 0.**
  * buy-prices.end-apply: Last times the price will apply. Only supports `ANY` or `ALL` price type. **Optional. Default to infinite.**
  * buy-prices.apply: Which times this price will apply, format: `[1,2,3,4]`. Only supports `ANY` or `ALL` price type. **Optional. Default use start-apply option value.**
  * buy-prices.placeholder: Price display name in `{price}` placeholder. **Optional. Default unknown language key.**
  * buy-prices.conditions: Player must meet the condition to use this price. Use [Condition Format](../format/condition-format.md)  here. **Optional. Default don't have any conditions.**&#x20;
  * buy-prices.take-actions: The action will run after this buy price is been taken from player. Use [Action Format](../format/action-format.md) here.&#x20;
* sell-prices: Product sell prices. Support [Item format](../format/itemformat-tm/) and [Economy format](../format/economyformat-tm.md). You can also add [Custom Sell Match Method](../features/custom-item-match-method.md) here. **Optional. If not set, product can not be selled.**
  * sell-prices also support all sub options like in `buy-prices`.
  * sell-prices.give-actions: The action will run after this sell price is been give to player, see [Action](../format/action-format.md) for more info. **Optional.**

## Actions and Conditions for Single Thing

You may note: you can set action will run when the single thing is been give to player, and set the conditions that player need meet to use the single thing. This is very useful you want to play sound, excute command after player buy or sell.

* Actions: Add `give-actions` section in single thing config. Very useful for command shop, permission shop, enchant shop. Also, **if your economy plugins/item plugins do not supported in UltimateShop, just put the command of give money/item here to solve the problem!** (`{player}` means player name, `{amount}` means the price/product amount)\
  **If you want to make the product be actions only, don't forget add `give-item: false` in the single thing option!**
* Conditions: Add `conditions` section in single thing config.&#x20;

### Different from single thing's `give-actions` and item's `buy-actions/sell-actions`:

* `give-actions` only executed when the single thing is used and give to player. `buy-actions/sell-actions` will always executed when player successfully buy or sell the item.&#x20;
* `give-actions`'s `{amount}` placeholder will return the single price/product amount, `buy-actions/sell-actions` will return the amount player buy or sell the item in this time. For example, player sell 64x apple, and obtain 100 coins by this, `give-actions`'s `{amount}` placeholder will return 100, and `buy-actions/sell-actions` will return 64.

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

Start from 3.4.3, you can customize the **keys** for conditions of **single things**. If you confirm that your products, buy prices, and sell prices are using same conditions at a time, you can set their keys to the same value, so that you don't have to configure their conditions separately for each single thing. You can find the settings at `config.yml` file like below:

```yaml
conditions:
  products-key: 'conditions'
  buy-prices-key: 'conditions'
  sell-prices-key: 'conditions'
  display-item-key: 'conditions'
```

This example make all `conditions` key be same, so the shop config should be also like:

```yaml
items:
  A:
    price-mode: CLASSIC_ANY
    product-mode: CLASSIC_ANY
    products:
      one:
        material: REDSTONE
        amount: 1
        give-actions:
          1:
            type: message
            message: 'Hello!'
      two:
        material: IRON_INGOT
        amount: 1
    sell-prices:
      one:
        economy-plugin: Vault
        amount: 1
        placeholder: '&6{amount} Coins'
        start-apply: 0
      two:
        economy-plugin: Vault
        amount: 3
        placeholder: '&6{amount} Coins'
        start-apply: 0
    conditions:
      one: # Condition ID
        1: # Means first condition
          type: placeholder
          placeholder: '{random_daily}'
          rule: '=='
          value: 'A'
      two:
        1:
          type: placeholder
          placeholder: '{random_daily}'
          rule: '=='
          value: 'B'
```

In this example, if condition **one** is meet, we will also use the product with ID **one** and sell price wth ID **one**.

For actions, it is recommended you use give-actions in each single thing instead of buy-actions or sell-actions, because their conditions are separate and cannot be synchronized with the conditions of a single thing, configuring them will be more complicated.

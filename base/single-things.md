# Single Things

Each single product or price in one product we called single thing.

## Things

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

Each product have those thing type:

* Buy Prices: The buy price of this product, player need pay the buy price to obtain this product, if this thing type do not exist (which means `buy-prices` section does not exist in the config), this product can not be purcahsed.
* Sell Prices: The sell price of this product, player need sell the products to shop, then he will get the sell price you set here, if this thing type do not exist (which means `sell-prices` section does not exist in the config), this product can not be sold.
* Products: The products of this  product, player will get the products you set here after buy, and need give his products to shop when selling.

## Single Thing

Each thing type can set unlimited related to single things, like set 5 buy prices, 100 sell prices and even 1k products!

Each single thing have those types:

* Vanilla Item: Use [ItemFormat](item-format.md) to tell us what Minecraft item you want to sell in shop or you want to player pay. **(Buy/Sell/Products)**
* Hook Item: Use [Supported Plugins](directly-supported-plugins.md)'s item to tell us what custom item you want to sell in shop or you want to player pay. This type still use [ItemFormat](item-format.md).**(Buy/Sell/Products)**
* Match Item: Use [Custom Item Match Method](../advanced/custom-item-match-method.md) to tell us which items you want to match. **(Buy/Products)**
* Vanilla Economy/Hook Economy: Use [EconomyFormat](economy-format.md) to tell us how much money you want to player pay or give to player. **(Buy/Sell/Products)**
* Custom: If those types do not meet your need, you can make a custom single thing! You need add `match-placeholder` option at single thing config to make plugin know what the now amount player have of this custom product/price, and then we will compare the now amount you set here and the required amount. In the example above, we will compare player's health. **If your economy plugins do not supported, just place it's player balance placeholder here and all is solved! (Sell/Products)&#x20;**<mark style="color:red;">**(Premium)**</mark>
* <mark style="color:blue;">Free: Single thing do not include ItemFormat, EconomyFormat, match-item section and match-placeholder section will be consider as free.</mark>

## Actions and Conditions

You can set action will run when the single thing is been give to player, and set the conditions that player need meet to use the single thing. This is very useful you want to play sound, excute command after player buy or sell.

* Actions: Add `give-actions` section in single thing config. For more info, please view [Shops](shops.md) page. Very useful for command shop, permission shop, enchant shop. Also, **if your economy plugins/item plugins do not supported in UltimateShop, just put the command of give money/item here to solve the problem!** (`{player}` means player name, `{amount}` means the price/product amount) If you want to make the product be actions only, don't forget add `give-item: false` in the single thing option!
* Conditions: Add `conditions` section in single thing config. For more info, please view [Shops](shops.md) page.

## Example of use actions in single thing config (Spanwer Shop/Commmand Shop)

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    display-item:
      name: 'Chicken Spawner'
      material: PLAYER_HEAD
      skull: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvNjQ3ZTJlNWQ1NWI2ZDA0OTQzNTE5YmVkMjU1N2M2MzI5ZTMzYjYwYjkwOWRlZTg5MjNjZDg4YjExNTIxMCJ9fX0=
      amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 350000
        placeholder: '{amount}⛂'
    buy-actions:
      1:
        type: console_command
        command: "ws give %player_name% spawner chicken 1"
```

## Example: Seasonal Price

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: potato
        amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 2
        placeholder: '&6{amount} Coins'
        conditions:
          1: 
            type: placeholder
            placeholder: '%rs_season%'
            rule: '=='
            value: 'Spring'
      2:
        economy-plugin: Vault
        amount: 1.8
        placeholder: '&6{amount} Coins'
        conditions:
          1: 
            type: placeholder
            placeholder: '%rs_season%'
            rule: '=='
            value: 'Summber'
      3:
        economy-plugin: Vault
        amount: 3.2
        placeholder: '&6{amount} Coins'
        conditions:
          1: 
            type: placeholder
            placeholder: '%rs_season%'
            rule: '=='
            value: 'Fall'
      4:
        economy-plugin: Vault
        amount: 8.8
        placeholder: '&6{amount} Coins'
        conditions:
          1: 
            type: placeholder
            placeholder: '%rs_season%'
            rule: '=='
            value: 'Winter'     
```

## Example: Use for not supported item plugins as products

```yaml
    display-item:
      material: APPLE
      # You can hold the item and type command /shop generateitemformat to get the ItemFormat here.
    products:
      1:
        # Sell Match
        match-item:
          contains-lore:
            - 'test1'
        # Buy Give Command
        give-actions:
          1:
            type: console_command
            command: 'items give {player} {amount}'
          2:
            type: message
            message: 'test message'
        amount: 64
```

## Example: Use for not supported economy plugins as prices.

```yaml
    products:
      1:
        # The product
        material: APPLE
        # Buy Give Command
        give-actions:
          1:
            type: console_command
            command: 'eco take {player} {amount}'
        amount: 64
    buy-prices:
      1:
        # Buy Match Placeholder
        match-placeholder: '%economy_now_balance_placeholder%'
        amount: 500
    sell-prices:
      1:
        # Sell Give Command
        give-actions:
          1:
            type: 'console_command'
            command: 'eco give {player} {amount}'
        amount: 500
```

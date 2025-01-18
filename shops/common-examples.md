# 📚Common Examples

## Common Example

This example has sell limits, which means player can only sell this product X times every day.

* Sell limits can help your server has "economy balance", even player has 10000 rotten flesh, he still can only sell 64x in this example.
* In this example, VIP players will have 50% more sell limits, which can help your server has more supporter.
* In this example, sell limits will reset at local time '0:00:00', which means midnight.
* In this example, we set price and product mode has `CLASSIC_` prefix, this will save server performance, you should use this when you didn't set `start-apply` option to other value in `prices` section.

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: rotten_flesh
        amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 10
        placeholder: '&6{amount} Coins'
        start-apply: 0
    sell-prices:
      1:
        economy-plugin: Vault
        amount: 0.8
        placeholder: '&6{amount} Coins'
        start-apply: 0
    sell-limits:
      global: 1280
      default: 64
      vip: 192
    sell-limits-conditions:
      vip:
        1:
          type: permission
          permission: 'group.vip'
    sell-limits-reset-mode: 'TIMED'
    sell-limits-reset-time: '00:00:00'  
```

## Economy Exchange Example

In this example, we make some changes that different from Common Product Example:

* We added `display-item` section, because there is no real item products in this example.
* We set price and product mode without `CLASSIC_` prefix because we set start-apply option to other value.

```yaml
items:
  A:
    display-item:
      material: GOLDEN_BLOCK
    price-mode: ALL
    product-mode: ANY
    products:
      1:
        economy-plugin: PlayerPoints
        amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 10
        placeholder: '&6{amount} Coins'
        apply: [1,2,3,4,5]
      1:
        economy-plugin: Vault
        amount: 20
        placeholder: '&6{amount} Coins'
        start-apply: 6
    buy-limits:
      global: 1000
      default: 10
      vip: 20
    buy-limits-conditions:
      vip:
        1:
          type: permission
          permission 'group.vip'
    buy-limits-reset-mode: 'TIMED'
    buy-limits-reset-time: '00:00:00'
```

## MMOItems Example

<pre class="language-yaml"><code class="lang-yaml"><strong>items:
</strong>  E:
    products:
      1:
        hook-plugin: MMOItems
        hook-item: AXE;;EXECUTIONER_AXE
        amount: 1
    price-mode: ANY
    product-mode: ALL
    buy-prices:
      1:
        economy-type: exp
        amount: 1
        start-apply: 0
        placeholder: '1 Exp'
    sell-prices:
      1:
        economy-type: exp
        amount: 1
        start-apply: 0
        placeholder: '1 Exp'
</code></pre>

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


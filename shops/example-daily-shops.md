# 📅Example: Daily Shops

{% hint style="info" %}
This example will only work for <mark style="color:red;">**PREMIUM**</mark> version of **UltimateShop**!
{% endhint %}

## Create random placeholder

We need to create a random placeholders. This placeholder can be used in conjunction with the [condition](../format/condition-format.md) system to achieve different products appearing at this shop every day, thereby achieving the same effect as the daily shop plugin.

In this example, we created a new random placeholder config called `daily.yml` at `random_placeholder` folder. And it's options represents:

* `reset-mode` and `reset-time`: This placeholder refreshed every day.
* `element-amount`: This placeholder will randomly pick 5 elements when it refresh, this is same as the amount of slots in this daily shop.
* `elements`: The result determines what product will appear in this slot by the condition system. So the quantity of elements should be equal to the quantity of all possible products in the daily shop.

In this example, this daily shop will has 5 slots and 7 possible products, so each day, it will has 2 products be hidden, and 5 products randomly picked to display in shop.

Please view [Random Placeholder](../placeholders/random-placeholder-premium.md) page for more info about random placeholder.

```yaml
reset-mode: TIMED
reset-time: '00:00:00'
element-amount: 5
elements:
  - 'A'
  - 'B'
  - 'C'
  - 'D'
  - 'E'
  - 'F'
  - 'G'
```

## Configure Shop

The various options used in this example are detailed on the [Shops](shops.md) page. If you are unsure of the purpose of each option, please refer to that article.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

```yaml
settings:
  menu: 'example-shop-menu'
  buy-more: true
  shop-name: 'Daily Shop'
  hide-message: false

general-configs:
  price-mode: CLASSIC_ANY
  product-mode: CLASSIC_ANY
  display-item:
    1:
      material: REDSTONE
      amount: 1
      name: '&eRedstone'
      lore:
        - '&fToday Product:'
        - '&7  - Redstone'
    2:
      material: IRON_INGOT
      amount: 1
      name: '&eIron Ingot'
      lore:
        - '&fToday Product:'
        - '&7  - Iron Ingot'
    3:
      material: GOLD_INGOT
      amount: 1
      name: '&eGold Ingot'
      lore:
        - '&fToday Product:'
        - '&7  - Gold Ingot'
    4:
      material: COPPER_INGOT
      amount: 1
      name: '&eCopper Ingot'
      lore:
        - '&fToday Product:'
        - '&7  - Copper Ingot'
    5:
      material: DIAMOND
      amount: 1
      name: '&eDiamond'
      lore:
        - '&fToday Product:'
        - '&7  - Diamond'
    6:
      material: LAPIS_LAZULI
      amount: 1
      name: '&eLapis lazuli'
      lore:
        - '&fToday Product:'
        - '&7  - Diamond'
    7:
      material: EMERALD
      amount: 1
      name: '&eEmerald'
      lore:
        - '&fToday Product:'
        - '&7  - Emerald'
  products:
    1:
      material: REDSTONE
      amount: 1
    2:
      material: IRON_INGOT
      amount: 1
    3:
      material: GOLD_INGOT
      amount: 1
    4:
      material: COPPER_INGOT
      amount: 1
    5:
      material: DIAMOND
      amount: 1
    6:
      material: LAPIS_LAZULI
      amount: 1
    7:
      material: EMERALD
      amount: 1
  sell-prices:
    1:
      economy-plugin: Vault
      amount: 1
      placeholder: '&6{amount} Coins'
      start-apply: 0
  sell-limits:
    global: 640
    default: 18
    vip: 256
  sell-limits-conditions:
    vip:
      1: 
        type: permission
        permission: 'group.vip'
  sell-limits-reset-mode: 'TIMED'
  sell-limits-reset-time: '00:00:00'

items:
  A:
    sell-prices:
      1:
        economy-plugin: Vault
        amount: 1
        placeholder: '&6{amount} Coins'
        start-apply: 0
    display-item-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'G'
    products-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;1}'
          rule: '=='
          value: 'G'
  B:
    display-item-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'G'
    products-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;2}'
          rule: '=='
          value: 'G'
  C:
    display-item-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'G'
    products-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;3}'
          rule: '=='
          value: 'G'
  D:
    display-item-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'G'
    products-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;4}'
          rule: '=='
          value: 'G'
  E:
    display-item-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'G'
    products-conditions:
      1: 
        1: 
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'A'
      2: 
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'B'
      3:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'C'
      4:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'D'
      5:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'E'
      6:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'F'
      7:
        1:
          type: placeholder
          placeholder: '{random_daily;;5}'
          rule: '=='
          value: 'G'
```

## FAQ: Too complex?

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
      one:
        1:
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

## FAQ: Price are same for all products?

This is because you only created one unconditional price here, which results in all products using this price. If you don't want this, you can learn to do it like `display-item` and `products`.

For example:

<pre class="language-yaml"><code class="lang-yaml"><strong>general-configs:
</strong><strong>  # Configs...
</strong><strong>
</strong><strong>items:
</strong><strong>  sell-prices:
</strong>    1:
      economy-plugin: Vault
      amount: 1
      placeholder: '&#x26;6{amount} Coins'
      start-apply: 0
  sell-prices-conditions:
    1:
      # Conditions...
</code></pre>

The reason why options like `products` are separated from their corresponding conditional options is that the products in your shop are fixed, so each slot has the same `products` option. However, the randomly selected product in each slot are not consistent, so the `conditions` option needs to be separated separately.

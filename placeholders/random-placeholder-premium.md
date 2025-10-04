# 🔀Random Placeholder - Premium

We added `{random}` built-in placeholder in premium version.

## Config

All random placeholder configs are stored in `random_placeholders` folder. The file name is it's ID, for example: `rotate.yml` means it's ID is `rotate`. An example of it's config is like below:

```yaml
reset-mode: TIMED
reset-time: '00:00:00'
per-player-element: true
element-sort: true
element-amount: 5
elements:
  A:
    rate: 1
    conditions:
      1:
        type: permission
        permission: 'test.permission'
  B:
    rate: 5
  C:
    rate: 2
  D:
    rate: 5
  E:
    rate: 2
  F:
    rate: 15
  G:
    rate: 7
```

* per-player-element: If set to `false`, all players will use the same value output by random placeholder. For example, player 1 will get **A**, and player 2 will get the same value, even if the player reaches 100 million, the value will be the same. If set to `true`, the values output by each player will be different from each other, and conditions can be set for elements. If an element does not meet the conditions, the player will never be able to extract it.

{% hint style="info" %}
This option is <mark style="color:red;">**NOT**</mark> recommended to be changed after enabling this random placeholder, as it may cause the plugin to detect errors (such as a per player random placeholder appearing in the global database) and output a prompt in the console that cannot be blocked.\
The random placeholder of per player cannot be applied to global server scenarios, and vice versa. Random placeholders without per player enabled cannot be applied to per player scenarios. For example, when using the `resetrandomplaceholder` command, the per player's random placeholder must enter the player name in the command parameters, while the per player's random placeholder cannot enter the player name in the command parameters, otherwise the plugin will prompt an error.
{% endhint %}

* element-sort: If set to `false`, the result of the random placeholder will be out of order. For example, if you set `elements` to `A, B, C, D, E` and the randomly generated result is `B, D`, the result of the random placeholder may be `B, D`, or `D, B`. However, if set to `true`, the result will be output strictly in the order of elements, and the output result can only be `B, D`. **(Added in 3.12.2)**&#x20;
* reset-mode/reset-time: Please view below to know.
* element-amount: The amount of the element will picked in this placeholder. **(Added in 3.1.0)**
* elements: The random element what placeholder will picked.&#x20;

There are two ways to express `elements`.&#x20;

The first is to write all elements in the form of a list, where the rate of each element is equal and without any conditions. **Support use \~ symbol means pick random number, for example, 5\~100 means pick one random number from 5 to 100.**

```yaml
elements:
  - 'A'
  - 'B'
  - 'C'
```

```yaml
elements:
# Random number from 5 to 100.
  - '5~100'
```

The second is to use the form of subsections, where each element has options for `rate` and `conditions` to fill in. The `conditions` option is not required and only support when `per-player-elemen`t being set to true. **(Added in 3.12.0)**

```yaml
elements:
  A:
    rate: 1
    conditions:
      1:
        type: permission
        permission: 'test.permission'
  B:
    rate: 5
  C:
    rate: 2
```

## Use Placeholder

Use `{random_<ID>;;<Number>}` placeholder to display it's value, like `{random_daily;;2}` will query `daily` random placeholder's **second** element picked. For more info, please view [Placeholders](built-in-placeholder.md) page. For example of this placeholder usage, please view [Daily Shop](../shops/example-daily-shops.md) page.

## Reset Placeholder

You can reset placeholder by setting `reset-mode` and `reset-time` option.&#x20;

Supports below reset mode:

* ONCE: Each time it is used, it will reset and is not applicable to the price, as the price seen by the player opening the store and the actual transaction result are calculated twice, so you cannot achieve price synchronization.
* TIMER/TIMED/NEVER: Please view [this page](../shops/products.md#buy-sell-times-reset-options) to know more. We will generate reset time after random placeholder be used once. The reset time will not automatically adjust based on configuration updates. If you set the reset time incorrectly, you will need to delete the corresponding data.

For more info, please view [this page](../shops/product-config-buy-sell-times-reset.md).

## Example: Random Price

### Create new random placeholder

In this example, we create a new random placeholder config called `price.yml` at `random_placeholder` folder.

```yaml
reset-mode: TIMED
reset-time: '00:00:00'
elements:
# Random number from 5 to 100.
  - '5~100'
```

### Set dynamic value in your product configs

Use `{random_price}` placeholder at any product's price config. Like I add this placeholder in this product:

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: coal
        amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: '{random_price}' # <--- Changed line
        placeholder: '&6{amount} Coins'
        start-apply: 0
```

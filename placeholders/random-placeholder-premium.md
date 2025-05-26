# 🔀Random Placeholder - Premium

We added `{random}` built-in placeholder in premium version.

## Config

All random placeholder configs are stored in `random_placeholders` folder. The file name is it's ID, for example: `rotate.yml` means it's ID is `rotate`. An example of it's config is like below:

```yaml
reset-mode: TIMED
reset-time: '00:00:00'
elements:
  - 'A'
  - 'B'
  - 'C'
```

* reset-mode/reset-time: Please view below to know.
* element-amount: The amount of the element will picked. **(Added in 3.1.0)**
* elements: The random element what placeholder will picked.&#x20;
  * **Support use \~ symbol means pick random number, for example, 5\~100 means pick one random number from 5 to 100.**&#x20;

```yaml
reset-mode: TIMED
reset-time: '00:00:00'
element-amount: 2
elements:
  - 'A'
  - 'B'
  - 'C'
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

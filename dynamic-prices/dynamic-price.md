# 🔄Dynamic Price

## Enable Math Feature

Change your `config.yml` file:

* Change

```yaml
math:
  # Enabled base math calculate?
  # Will support + - * / only.
  enabled: false
```

to

```yaml
math:
  # Enabled base math calculate?
  # Will support + - * / only.
  enabled: true
```

* Change&#x20;

```yaml
placeholder:
  data:
    can-used-in-amount: false
```

to

```yaml
placeholder:
  data:
    can-used-in-amount: true
```

## Set dynamic value for your product configs

Open one of your shop configs, find the product you want to enable dynamic price.

Like I want to enable for this product:

```yaml
  A:
    display-name: 'Custom Name!'
    price-mode: ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: sea_lantern
    buy-prices:
      1:
        economy-type: exp
        amount: '5+({buy-times-server}-{sell-times-server})*0.2'
        max-amount: 15
        min-amount: 1
        start-apply: 0
        placeholder: '{amount} Exp'
    sell-prices:
      1:
        economy-type: exp
        amount: '5+({buy-times-server}-{sell-times-server})*0.2'
        max-amount: 15
        min-amount: 1
        start-apply: 0
        placeholder: '{amount} Exp'
```

First, you need set `price-mode` to `ALL` or `ANY`.

Set amount option to the value you want here, like put a common dynamic formula here, if your math is not good, let me explain it:

* 5 is base price, which means the start price.
* 0.2 is each time one player buy or sell one this product, then the price will up or down.
* We also added `max-amount` and `min-amount` option, to avoid price is too high or too low.

<figure><img src="../.gitbook/assets/屏幕截图 2023-10-08 201124.png" alt=""><figcaption></figcaption></figure>

The formula you set here is not limited, but you need carefully check whether player can earn money by purchase them then just sell them without do anything. Because of this, the `max-amount` and `min-amount` option is very important. For example, you set:

* Buy Price Formula: `2.8+{buy-times-server}*0.1-{sell-times-server}*0.06`
* Sell Price Formula: `2.38+{buy-times-server}*0.1-{sell-times-server}*0.06`

In this way, your `max-amount` option should be lower than the price at the <mark style="color:red;">**n**</mark>(th) purchase or sellling time.

How to get the number called <mark style="color:red;">**n**</mark>? This number must meet:

\[(**Buy Price Base Price** - **Sell Price Base Price**)/(**Buy Up Price** - **Sell Down Price**)] >= Accumulation from 1 to n.

In this example: `(2.8-2.38)/(0.1-0.06) >= 1+2+3+4` (if up to 5, the formula will not meet), so <mark style="color:red;">n</mark> max number is 4 in this example.

Remerber: <mark style="color:red;">Your different formulas require reasonable setting of different values in max-amount and min-amount. The safest approach is to set the price of each purchase or sellling change to the same value.</mark>

Another common dynamic price formula is price changed based on the percentage, like: `100 * (1.5 ^ ({buy-times-server}-{sell-times-server}))`. In this example:

* **100** is base price.
* **1.5** is the multiplier of the price after each purchase or sellling.&#x20;
* In this example, first time buy with no sell is **100**, then is **150 (+50%)**, then is **225 (150 + 150 \* 50%)**.
* Don't forget set `min-amount` option to a number near **100** to avoid the price become too low!

## Available Placeholders

* {buy-times-player}
* {buy-times-server}
* {sell-times-player}
* {sell-times-server}
* {last-buy-player}
* {last-buy-server}
* {last-sell-player}
* {last-sell-server}

For more info about those placeholders, please view [this page](../placeholders/built-in-placeholder.md).

## Dynamic Price per player

As long as you can ensure that the placeholder used in the formula is per player, the calculated price result will naturally be per player. In the above example, we used global placeholders such as `{buy-times-server}`, and you only need to replace the `server` with the `player` to display the player's own buy times value. The relevant content is explained in detail in the [Placeholders](../placeholders/built-in-placeholder.md) page.

## Set buy / sell limits for your products

Please view [Products](../shops/products.md) page for info and example.

## Reset dynamic price

Many people ask this question, and I feel that the person asking this question simply does not understand the essence of UltimateShop. The dynamic price is determined by a formula, so you cannot reset the price directly. To reset the price, the variables used in your formula must be reset. If you use variables such as `{buy-times-server}` exactly as described in this section, they can be reset.

You can reset the buy times or sell times by our auto reset feature, you can find more info at [Buy/Sell Times Reset](../shops/product-config-buy-sell-times-reset.md) page.

# 🌱Example: Stock (like in life)

{% hint style="info" %}
This means real life stock, for set limit of buy/sell times, please view [Products](products.md) page.
{% endhint %}

## Set dynamic value for your product configs

The plugin itself does not store inventory data, but we can cleverly solve this problem by setting buy limits. Read [dynamic prices](../dynamic-prices/dynamic-price.md) before read this page. Similar to Dynamic Prices, if you want to make stock system, do it in `buy-limits` option and put `{server-times-server}` placeholder in it, for example:

```yaml
  A:
    price-mode: ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: echo_shard
        amount: 1
    buy-prices:
      1:
        economy-plugin: EcoBits
        economy-type: quest_points
        amount: 5
        placeholder: '&b{amount} Quest Points'
        start-apply: 0
    sell-prices:
      1:
        economy-plugin: EcoBits
        economy-type: quest_points
        amount: 5
        placeholder: '&b{amount} Quest Points'
        start-apply: 0
    buy-limits:
      global: '{sell-times-server}' 
    buy-times-reset-mode: 'NEVER'
    buy-times-reset-time: '00:00:00' 
```

We changed:

* `price-mode` option to `ANY` or `ALL`.
* `buy-limits` option to `{sell-times-server}` . For sell limits, you need write `{buy-times-server}` here. Replace the placeholder to `{buy-times-player}` and `{sell-times-player}` to make the stock be per player.
* `buy-limits-reset-mode` option to `'NEVER'`

In this way, we can ensure that players can only purchase items in the same quantity as the sell times (means restocking by other players sell it)

## FAQ: Restock

The person who asked this question didn't understand this plugin at all. Your stock is achieved by setting a buy limit for the product. To restock, it is essentially resetting the buy times. This content is introduced on [this page](product-config-buy-sell-times-reset.md).

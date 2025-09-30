# 🌱Example: Stock (like in life)

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
    buy-times-max-value: 640 # Max Stock
```

We changed:

* `price-mode` option to `ANY` or `ALL`.
* `buy-limits` option to `{sell-times-server}` . For sell limits, you need write `{buy-times-server}` here. Replace the placeholder to `{buy-times-player}` and `{sell-times-player}` to make the stock be per player.
* `buy-limits-reset-mode` option to `'NEVER'`
* You can set max stock by setting `buy-times-max-value` option.
* &#x20;  &#x20;

## FAQ: Restock

The person who asked this question didn't understand this plugin at all. Your stock is achieved by setting a buy limit for the product. To restock, it is essentially resetting the buy times. This content is introduced on [this page](product-config-buy-sell-times-reset.md).

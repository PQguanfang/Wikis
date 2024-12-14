# Stock (like in life)

## Set dynamic value for your product configs

Read [dynamic prices](../advanced/dynamic-price.md) before read this page. Similar to Dynamic Prices, if you want to make stock system, do it in `buy-limits` option, for example:

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
    buy-limits-reset-mode: 'NEVER'
    buy-limits-reset-time: '00:00:00' 
```

We changed:

* `price-mode` option to `ANY` or `ALL`.
* `buy-limits` option to `{sell-times-server}` . For sell limits, you need write `{buy-times-server}` here. Replace the placeholder to `{buy-times-player}` and `{sell-times-player}` to make the stock be per player.
* `buy-limits-reset-mode` option to `'NEVER'`

## Clear your data every month!

It is recommended to use the `setbuytimes` or `setselltimes` command every month to clean up the buy and sell data of products, with an upper limit of `2147483647`. If this value is exceeded, the plugin will not function properly.

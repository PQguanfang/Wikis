# Common Shop

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
        - 'permission: group.vip'
    sell-limits-reset-mode: 'TIMED'
    sell-limits-reset-time: '00:00:00'  
```

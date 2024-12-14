# Economy Exchange

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
        - 'permission: group.vip'
    buy-limits-reset-mode: 'TIMED'
    buy-limits-reset-time: '00:00:00'
```

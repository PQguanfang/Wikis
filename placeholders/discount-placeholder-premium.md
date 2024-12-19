# 🔖Discount Placeholder - Premium

We added `{discount}` built-in placeholder in plugin.

## Configure

* Open `config.yml`, find those contents:

```yaml
placeholder:
  # Premium version only.
  discount:
    buy:
      mode: MIN
      default: 1
      vip: 0.5
      mvp: 0.3
    sell:
      mode: MAX
      default: 1
      vip: 1.5
      mvp: 2
  discount-conditions:
    vip:
      type: permission
      permission: 'group.vip'
    mvp:
      type: permission
      permission: 'group.mvp'
```

Change the value you would like.

* mode: You can create unlimited discount placeholder and have 2 type: MIN and MAX, min means buy, which player pay lower price for products, max means sell, which player get more money form sell items.
* default: Default value, there is no reason you change this value other than 1.
* vip/mvp: Condition ID value, players meet the conditions will use those value.

For conditions, view [Conditions](broken-reference).

## Use Placeholder

Use `{discount_<ID>}` placeholder to display it's value. For more info, please view [Placeholders](built-in-placeholder.md) page.

Like:&#x20;

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: sea_lantern
        lore: 
          - '%player_health%'
    buy-prices:
      1:
        economy-plugin: Vault
        amount: '{discount_buy} * 5' # <--- Changed line
        start-apply: 0
        placeholder: '{amount} Coins'
```

* 5 is base price, then use {discount\_buy} before it.

## Auto Apply Discount Placeholder

* Start from 2.3.2, you can auto apply discount discount placeholder to all prices! Just configure it in `config.yml` file.

```yaml
placeholder:
  auto-settings:
    # If enabled, we will auto add discount placeholder at all price amount.
    # This can avoid the need to add the discount option in the amount options for each price.
    add-discount-in-all-price-amount:
      enabled: false
      buy-placeholder: buy
      sell-placeholder: sell
      black-dynamic-price: true
      black-shops:
        - 'example'
```

* It is recommend you disable this feature for dynamic price, if you want to enable it for dynamic price too, just change `black-dynamic-price` option to false here!
* If you want to disable this feature for specified shops, use `black-shops` option.

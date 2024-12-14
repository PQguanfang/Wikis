# Discount (In free version)

There are 2 ways to do it in free version.

Premium version built-in a feature called Random Placeholder which is more easy to use, check [this page](../advanced/discount-premium.md) to know more.

## Method 1

Open one of your shop configs, find the product you want to make discount for specified players.

Like I want to enable for this product:

```yaml
  A:
    display-name: 'Custom Name!'
    price-mode: CLASSIC_ANY
    product-mode: CLASSIC_ALL
    products:
      1:
        material: sea_lantern
    buy-prices:
      1:
        economy-type: exp
        amount: '15'
        start-apply: 0
        placeholder: '{amount} Exp'
        conditions:
          - 'permission: group.vip'
      2:
        economy-type: exp
        amount: '30'
        start-apply: 0
        placeholder: '{amount} Exp' 
    sell-prices:
      1:
        economy-type: exp
        amount: '6'
        start-apply: 0
        placeholder: '{amount} Exp'
        conditions:
          - 'permission: group.vip'
      2:
        economy-type: exp
        amount: '3'
        start-apply: 0
        placeholder: '{amount} Exp' 
```

We have set:

* Make price-mode to `CLASSIC_ANY` or `ANY`. If you want to use `ALL` mode, see method 2.
* Added second price both in `buy-prices` and `sell-prices` section.

The first section is for VIP players, player has `group.vip` permission can use this price, otherwise they have to use second one, which is more experience for buy, and cheaper for sell.

## Method 2

This method require other plugin which has custom placeholder feature. If you don't know anyone, I recommend you use Auxiolor's libreforge.

### How to get libreforge?

* Are you using his plugin? Like EcoEnchants, and so on. If sure, that is built-in those plugins.
* If you don't have anyone of it, download Action free version here: [https://www.spigotmc.org/resources/actions-free-%E2%AD%95-customize-your-server-%E2%9C%85-create-scripts-perks-automations-%E2%9C%A8-50-plugin-hooks.109738/](https://www.spigotmc.org/resources/actions-free-%E2%AD%95-customize-your-server-%E2%9C%85-create-scripts-perks-automations-%E2%9C%A8-50-plugin-hooks.109738/)
* Since libreforge is also a Spigot plugin, if you are PRO server owner, you can try build jar file of it by yourself. I am not owner of librefroge, so I can not share it here. [https://github.com/Auxilor/libreforge](https://github.com/Auxilor/libreforge)

### Add condition placeholder

Open your server after install those plugins, then you will found `plugins/libreforge/config.yml` file.

Open it, and add below contents at `placeholders` section.

```yaml
placeholders:
- id: shop_discount
  default: '1'
  values:
  - conditions:
    - id: has_permission
      args:
        permission: 'group.mvp'
    value: '0.2'
  - conditions:
    - id: has_permission
      args:
        permission: 'group.vip'
    value: '0.5'
```

This means if player don't have `group.vip` and `group.mvp` permission, it will return 1.

If player has `group.mvp` permission, it will return 0.2.

If player has `group.vip` permission, it will return 0.5.

You should carefully the order, like this example, if player both has group.vip and group.mvp permission, you should make sure placeholder will reuturn lower value, so I made group.mvp in first location.

### Use this placeholder at amount option

Set price section amount option to %libreforge\_shop\_product%\*\<productAmount>.

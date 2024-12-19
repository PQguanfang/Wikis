# 🏆Example: Rewards

Rewards is very similar to Shops, but rewards don't have any price, and usually, it needs to be coordinated with the menu system.

## Example for Daily Rewards

Create new shop config at `/shops/` folder, then create new product like this:&#x20;

```yaml
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: DIAMOND
        amount: 16
      2:
        material: IRON_INGOT
        amount: 64
      3:
        economy-plugin: Vault
        amount: 1500
    buy-prices:
      1:
        economy-type: exp
        amount: 0
        placeholder: 'Free'
    buy-limits:
      default: '1'
    buy-limits-reset-mode: 'TIMED'
    buy-limits-reset-time: '00:00:00' 
```

In this example, players can purchase this "product" once each day, and because the price is free, so we can consider it as "reward".

If you want to make VIP players have bonus 64x bread, then just use our conditions system, like this:

```yaml
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: DIAMOND
        amount: 16
      2:
        material: IRON_INGOT
        amount: 64
      3:
        economy-plugin: Vault
        amount: 1500
      4:
        material: BREAD
        amount: 64
        conditions:
          1:
            type: permission
            permission: 'group.vip'
    buy-prices:
      1:
        economy-type: exp
        amount: 0
        placeholder: 'Free'
    buy-limits:
      default: '1'
    buy-limits-reset-mode: 'TIMED'
    buy-limits-reset-time: '00:00:00' 
```

If you also want to VIP players have **50%** chance to get bonus 1x diamond sword, then we need create a new random placeholder at `config.yml`:

```yaml
  random:
    chance:
      reset-mode: ONCE
      reset-time: '00:00:00'
      elements:
        - '1~100'
```

Then also use condition system:

```yaml
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: DIAMOND
        amount: 16
      2:
        material: IRON_INGOT
        amount: 64
      3:
        economy-plugin: Vault
        amount: 1500
      4:
        material: BREAD
        amount: 64
        conditions:
          1:
            type: permission
            permission: 'group.vip'
      5:
        material: BREAD
        amount: 64
        conditions:
          1:
            type: permission
            permission: 'group.vip'
          2:
            type: placeholder: 
            placeholder: '{random_chance}'
            rule: '>'
            value: '50'
    buy-prices:
      1:
        economy-type: exp
        amount: 0
        placeholder: 'Free'
    buy-limits:
      default: '1'
    buy-limits-reset-mode: 'TIMED'
    buy-limits-reset-time: '00:00:00' 
```

## Example for Streak Rewards

Please download this example pack then carefully read [Display Item Format](../format/display-item-format.md), [Shops](shops.md) and [Conditions](broken-reference) page to understand it.&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

**How to use this resource?**&#x20;

Copy and drag the UltimateShop folder to your server's plugins folder. UltimateShop 1.7.7+ version is **REQUIRED**.

**Where to change rewards?**&#x20;

Open `UltimateShop/shops/streak.yml`, edit the `buy-actions`.&#x20;

```yaml
buy-actions:
  1:
    type: console_command
    command: test'
    apply: [1] 
```

**How to make streak be cycle?**&#x20;

Add below contents at `buy-actions` option:

```yaml
  1:
    type: console_command
    command: 'shop setbuytimes streak A %player_name% 0-31'
```

Replace A to B if you are trying add it at the second stread rewards.

DO NOT USE IT FOR NOW, IT DOES NOT SUPPORT V3 VERSION.

{% file src="../.gitbook/assets/UltimateShop_Streak_Rewards.zip" %}

# Display Item Add Lore

## General Setting

You can set it at `config.yml` file.

Default example:

```yaml
  add-lore:
    - '@n '
    - '@a&ePurchase: {buy-price}'
    - '@b&eSell: {sell-price}'
    - '@c&#FF7777Player Buy Stock: {buy-times-player}/{buy-limit-player}'
    - '@d&#FF7777Server Buy Stock: {buy-times-server}/{buy-limit-server}'
    - '@e&#FF7777Player Sell Limit: {sell-times-player}/{sell-limit-player}'
    - '@f&#FF7777Server Sell Limit: {sell-times-server}/{sell-limit-server}'
    - '@g '
    - '@g&#ff3300cCan not buy more!'
    - '@g&8Refresh Time: {buy-refresh-player}'
    - '@i '
    - '@i&#ff3300Sold Out!'
    - '@i&8Refresh Time: {buy-refresh-server}'
    - '@h '
    - '@h&#ff3300Can not sell more!'
    - '@h&8Refresh Time: {sell-refresh-player}'
    - '@j'
    - '@j&#ff3300Can not sell more for server!'
    - '@j&8Refresh Time: {sell-refresh-server}'
    - '@n '
    - '@a{buy-click}'
    - '@b{sell-click}'
    - '@k&#FFFACDRight-Shift click to pick amount!'
    - '@b&#FFFACDDrop (Q key) to sell all!'
```

## Per Product Setting

You can set different add lore format for different product, add the `add-lore` arg in the product config. Check [shops](../base/shops.md) page product B to find the example.

## Prefix - Conditional Symbol

Each line start with '@+lower case' will be consider as conditional line. We will only display this line when this condition is meet.

@a - This product has buy price. (Means has buy-prices section)

@b - This product has sell price. (Means has sell-prices section)

@c - This product has player buy limit. (Means has buy-limits.player option)

@d - This product has server buy limit. (Means has buy-limits.global option)

@e - Similar to @c, but it's sell.

@f - Similar to @d, but it's sell.

@g - This product has reached player buy limit.

@h - This product has reached player sell limit.

@i - This product has reached server buy limit.

@j - This product has reached server sell limit.

@k - Player is **not** opening buy more menu and this product has enabled buy more feature.

@l - This product is in buying cooldown.

@m - This product is in selling cooldown.

@n - Buy/sell price (corresponding to the Click type) is valid. For example, buy click type require buy price is valid.

## Suffix

-b - This line will only display for Java players.

-m - This line will only display in buy more menu.

-i - The condition symbol in this line will work as negation.

If you want to use multi suffix, you need follow those order: `-i-m-b`.

## New Line Symbol

Use `;;` symbol if you want to start a new line, this is very useful for some people want to display price in multi lines.

```yaml
placeholder:
  price:
    split-symbol-any: ';;' # <--- Changed this in config.yml
    split-symbol-all: ';;' # <--- Changed this in config.yml
    unknown: "Unknown"
```

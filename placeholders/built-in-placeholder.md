# 🔧Built-in Placeholder

## Built-in Placeholders List

<table><thead><tr><th width="147">Placeholder</th><th>Display Info</th><th>Where can use</th></tr></thead><tbody><tr><td>{shop}</td><td>Display Shop ID (filename).</td><td>Message File<br>Actions</td></tr><tr><td>{shop-name}</td><td>Display Shop Display Name.</td><td>Shop Menu<br>Actions</td></tr><tr><td>{shop-menu}</td><td>Display Shop Menu ID.</td><td>Actions</td></tr><tr><td>{product}</td><td>Display Product ID.</td><td>Message File</td></tr><tr><td>{amount}</td><td>Display shop or sell amount.</td><td>Message File<br>Actions<br>Price <code>placeholder</code> option</td></tr><tr><td>{status}</td><td>Show whether now price is greatter or less than base price. Only use for dynamic price.</td><td>Price <code>placeholder</code> option</td></tr><tr><td>{item}</td><td>Display Purchased Items Name.</td><td>Message File</td></tr><tr><td>{menu}</td><td>Display Menu ID.</td><td>Message File</td></tr><tr><td>{price}</td><td>Display Buy/Sell price.</td><td>Message File</td></tr><tr><td>{limit}</td><td>Display Buy/Sell limits.</td><td>Message File</td></tr><tr><td>{times}</td><td>Display Buy/Sell times.</td><td>Message File</td></tr><tr><td>{refresh}</td><td>Display Product Reset Refresh Time or Cooldown Refresh Time.</td><td>Message File</td></tr><tr><td>{buy-price}</td><td>See above.</td><td>Display Item Add Lore<br>PlaceholderAPI Support</td></tr><tr><td>{sell-price}</td><td>See above.</td><td>Display Item Add Lore<br>PlaceholderAPI Support</td></tr><tr><td>{buy-times-player}</td><td>See above.</td><td>Display Item Add Lore<br>PlaceholderAPI Support<br><code>amount</code> option</td></tr><tr><td>{buy-limit-player}</td><td>See above.</td><td>Display Item Add Lore<br>PlaceholderAPI Support</td></tr><tr><td>{buy-refresh-player}</td><td>See above.</td><td>Display Item Add Lore<br>PlaceholderAPI Support</td></tr><tr><td>{buy-cooldown-player}</td><td>See above.</td><td>Display Item Add Lore<br>PlaceholderAPI Support</td></tr><tr><td>{sell-xxx}</td><td>See above.<br>xxx is same as buy, like {sell-limit-playe}</td><td>See above.</td></tr><tr><td>{xxx-server}</td><td>See above.<br>xxx is same as player, like {buy-limit-server}</td><td>See above.</td></tr><tr><td>{buy-click}</td><td>View Buy Price Status</td><td>Display Item Add Lore</td></tr><tr><td>{sell-click}</td><td>View Sell Price Status</td><td>Display Item Add Lore</td></tr><tr><td>{item-name}</td><td>Display product display name</td><td>Display Item Add Lore<br>PlaceholderAPI Support</td></tr><tr><td>{random_&#x3C;ID>}</td><td>Query random placeholder's first picked element.<br>For more info about random placeholder, please view <a href="random-placeholder-premium.md">Random</a> page.</td><td>Anywhere in plugin<br><mark style="color:red;"><strong>PREMIUM</strong></mark></td></tr><tr><td>{random_&#x3C;ID>;;&#x3C;Number>}</td><td>Quert random placeholder specife number of picked element, if this number of picked element does not exist, we will quert the last picked element. You can set max amount of picked element by <code>element-amount</code> option in random placeholder.</td><td>Anywhere in plugin<br><mark style="color:red;"><strong>PREMIUM</strong></mark></td></tr><tr><td>{random-times_&#x3C;ID>}</td><td>View random placeholder refresh time.</td><td>Anywhere in plugin<br><mark style="color:red;"><strong>PREMIUM</strong></mark></td></tr><tr><td>{discount_&#x3C;ID>}</td><td>Use discount placeholder.<br>For more info, please view <a href="discount-placeholder-premium.md">Discount</a> page.</td><td>Anywhere in plugin<br><mark style="color:red;"><strong>PREMIUM</strong></mark></td></tr><tr><td>{compare_&#x3C;number1>_&#x3C;number2}</td><td>Compare 2 numbers. Result format can be changed in <code>config.yml</code> file.</td><td>Anywhere in plugin<br><mark style="color:red;"><strong>PREMIUM</strong></mark></td></tr><tr><td>{math_&#x3C;mathStr>}</td><td>Calculate the math string you put. Like <code>{math_10+50}</code> will print 60.<br>Require you enable <code>math.enabled</code> option in config.yml file.<br>You can set result scale at <code>placeholder.math.scale</code> option.</td><td>Anywhere in plugin</td></tr></tbody></table>

## PlaceholderAPI Support

All built-in placeholders above that has PlaceholderAPI Support tag can be used in PlaceholderAPI expansion:

Use `%ultimateshop_<shopID>_<productID>_<builtInPlaceholder>%` to display built-in placeholder outsite of the plugin!

For example:

`%ultimateshop_example_A_{buy-limit-player}%`

**Start from 2.5.6 version, you don't need put {} symbol into builtInPlaceholder arg, new format example, if you want to use this placeholderapi in our plugin, you have to use this new format becuase we will auto parse built-in placeholder into the value, this new format can avoid this:**

`%ultimateshop_example_A_buy-limit-player%`

For random and discount placeholder, you don't need specife the shop and the product, just put the placeholder after `ultimateshop`. For example:

`%ultimateshop_{random-times_rotate}%`

This don't support remove {} symbol.

## New Line Symbol

Use `;;` symbol if you want to start a new line, this is very useful for some people want to display price in multi lines.

```yaml
placeholder:
  price:
    split-symbol-any: ';;' # <--- Changed this in config.yml
    split-symbol-all: ';;' # <--- Changed this in config.yml
    unknown: "Unknown"
```


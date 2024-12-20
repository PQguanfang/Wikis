# ⌨️Commands

## /shop menu \<menuID>/\<shopID>

Open common menu or shop menu.&#x20;

Require `ultimateshop.menu` permission.

For console, should extra add `<player>` arg at the end of command, like `/shop menu test Player1`.

Support add `-b` at the end of the command to bypass menu open condition check. <mark style="color:red;">**(Premium version only)**</mark>

## /shop quickbuy \<shopID> \<productID> \[amount]

Quick purchase item.

Require `ultimateshop.quickbuy` permission.

For console, should extra add `<player>` arg at the end of command, like `/shop quickbuy test A Player1`.

## /shop quicksell \<shopID> \<productID> \[amount]

Same as quickbuy, just replace quickbuy to quicksell.

`amount` arg can be replaced to `*` symbol, then plugin will auto sell all the items you can sell. <mark style="color:red;">**(Premium version only)**</mark>

## /shop reload

Reload the plugin, some configs need you restart server.

Require `ultimateshop.reload` permission.

## /shop givesellstick \<itemID> \<playerID> \[amount] <mark style="color:red;">**(Premium version only)**</mark>

Give specifeid player specified amount (if not set, default to 1) sell stick.&#x20;

Require `ultimateshop.givesellstick` permission.

## /shop setbuytimes/setselltimes \<shopID> \<productID> \<player>/global \[times]

Set player's specified product buy times to specified value.

Require `ultimateshop.setbuytimes` permission.

If didn't set `times` arg, we will think you are trying to reset the buy/sell times.

`productID` arg can be replaced to `*` symbol, then plugin will auto pick up all product in specified shop. <mark style="color:red;">**(Premium version only)**</mark>

`setselltimes` is similar to setbuytimes here.

{% hint style="info" %}
The global arg means set buy/sell times for `{buy-times-server}` or `{sell-times-server}` placeholer, not means set buy/sell times for all players.&#x20;

It is **impossible** to set all player data at once through commands in UltimateShop. Because assuming your server has hundreds of thousands of player data, without excellent performance optimization code, the server will immediately crash. You may see very few economy plugins or item plugins providing this feature, but they are selling it as a selling point. We have not declared ourselves providing this feature on any occasion, and this feature will not be added in the future because it is very time-consuming and not very meaningful. You can achieve similar functions through the **auto reset** function, and relevant information can be viewed on [this page](../shops/product-config-buy-sell-times-reset.md).
{% endhint %}

## /shop addbuytimes/addselltimes \<shopID> \<productID> \<player>/global \<times>

Add specified value to player's specified product buy times.

Require `ultimateshop.addtbuytimes` permission.

`productID` arg can be replaced to `*` symbol, then plugin will auto pick up all product in specified shop. <mark style="color:red;">**(Premium version only)**</mark>

`addselltimes` is similar to setbuytimes here.

## /shop sellall

Open sellall menu.

Require `ultimateshop.sellall` permission.

## /shop saveitem \<itemID> <a href="#mc-saveitem-less-than-itemid-greater-than" id="mc-saveitem-less-than-itemid-greater-than"></a>

Save your hold items.

Require `ultimateshop.saveitem` permission.

## /shop generateitemformat

Generate hold item into Item Format at `plugins/UltimateShop` folder.

Require `ultimateshop.generateitemformat` permission.

## /shop getplaceholdervalue \<text> <mark style="color:red;">**(Premium version only)**</mark>

Parse input text to get placeholder value in it.

Require `ultimateshop.getplaceholdervalue` permission.

## /shop resetrandomplaceholder \<placeholderID> <mark style="color:red;">**(Premium version only)**</mark>

Reset random placeholder value.

Require `ultimateshop.resetrandomplaceholder` permission.

## /shop setrandomplaceholder \<placeholderID> \[element] <mark style="color:red;">**(Premium version only)**</mark>

Set random placeholder value.&#x20;

Different from resetrandomplaceholder, setrandomplaceholder won't reset refresh time and allow users pick specifeid element.

Support add `-b` at the end of the command to bypass element exist check, which means you can set the custom element you'd like. For example, my random placeholder only have `A,B,C` total 3 elements, if I type **D** as element here, plugin will print error message, if you add `-b` suffix, then the placeholder value will be set to **D** and plugin never print error message, but it is not recommended.

Require `ultimateshop.setrandomplaceholder` permission.

## /shop editor <mark style="color:red;">**(Premium version only)**</mark>

Open shop editor.

Require **UltimateShopEditor** addon plugin, download it at SpigotMC.

Require `ultimateshop.editor` permission.

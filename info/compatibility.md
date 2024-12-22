# 🔗Compatibility

The compatibility of plugins mainly includes hooks for **item plugins** and **economy plugins**. Unlike other plugins of the same type, we can support them regardless of their appearance. There are two methods to support them: **direct compatibility** and **indirect compatibility**.

## **Direct compatibility**

Direct compatibility refers to the use of item plugins or the economy of economic plugins directly in **ItemFormat** or **EconomyFormat**. This compatibility method is the simplest and officially supported.

### <mark style="color:red;">Directly</mark> supported item plugins list

* ItemsAdder
* Oraxen
* EcoItems
* EcoArmor
* MMOItems
* MythicMobs
* eco
* NeigeItems
* ExecutableItems
* Nexo

### <mark style="color:red;">Directly</mark> supported economy plugins list

* PlayerPoints
* CoinsEngine
* UltraEconomy
* EcoBits
* PEconomy
* RedisEconomy
* RoyaleEconomy
* VotingPlugin

The following provides an example of directly obtaining items from the **ItemsAdder** plugin through the direct compatibility feature in **ItemFormat** and using economy from **Vault** plugin in **EconomyFormat**:

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1: 
        hook-plugin: ItemsAdder # Item Format
        hook-item: fishing_pack:common_fishing_bait # Item Forma
    buy-prices:
      1:
        economy-plugin: Vault # Economy Format
        amount: 5
        start-apply: 0
        placeholder: '&65 Coins'
```

## **Indirect compatibility**

Indirect compatibility refers to the flexible use of various features of plugins to enable them to associate with these plugins.

* Save Item: We telled you a command called `/shop saveitem` at [Commands](commands.md) page, we also telled you can set `material` option in [Item Format](../format/itemformat-tm.md)  to the save item ID you was set to use them.
* Buy Actions: We telled you a option called `buy-actions` in shop configs at [Shops](../shops/shops.md) page. In [Actions](../format/action-format.md) page, we also telled you we support use command in actions, so just use the give item command here, all is done.
* Give Actions: We telled you this feature at [Single Things](../shops/common-examples.md) page which is very similar to Buy Actions. What's more, we even give you an example at that page.

### Example: Use for not supported item plugins as products

In this example, we first fill in the **ItemFormat** through the display item option to describe the item from an incompatible plugin, so that players can see what the item looks like in the menu.

In the `products` option, we use the [Custom Sell Match](../features/custom-item-match-method.md) feature, which allows us to flexibly set the rules for selling matches for this item, such as contains lore, etc. Then, we use `give-actions` format to execute the item give command, so that player can obtain this item after buy.

```yaml
    display-item:
      material: APPLE
      # You can hold the item and type command /shop generateitemformat to get the ItemFormat here.
    products:
      1:
        # Sell Match
        match-item:
          contains-lore:
            - 'test1'
        # Buy Give Command
        give-actions:
          1:
            type: console_command
            command: 'items give {player} {amount}'
          2:
            type: message
            message: 'test message'
        amount: 64
```

If you use the Paper server and the item is fixed (the items generated each time are identical), you can use the Save item function: you only need to use the `/shop saveitem` command, then use the `material` option in **ItemFormat**, and fill in the ID of the save item in this option.

### Example: Use for not supported economy plugins as prices.

In this example, we mainly flexibly implemented different types of single thing and `give-actions` options, whose functions can be found on the [Products](../shops/products.md) page. Specifically, assuming the player purchases this product, the `match-placeholder` in buy options is used to determine if the player has enough economy. If it meets the requirement, the player will receive an apple. As a result, the `give-actions` will be executed and the player's economy will be taked. Similarly, during selling, as the player obtains the sell price, the `give-actions` in the sell price will be executed, and therefore the player will receive economy.

```yaml
    products:
      1:
        # The product
        material: APPLE
        # Buy Give Command
        give-actions:
          1:
            type: console_command
            command: 'eco take {player} {amount}'
        amount: 64
    buy-prices:
      1:
        # Buy Match Placeholder
        match-placeholder: '%economy_now_balance_placeholder%'
        amount: 500
    sell-prices:
      1:
        # Sell Give Command
        give-actions:
          1:
            type: 'console_command'
            command: 'eco give {player} {amount}'
        amount: 500
```

## NeigeItems: Item Name Translation Hook

Through this hook, the localized names of vanilla items can be automatically displayed in the language set in NeigeItems.

Download NeigeItems here: [https://github.com/ankhorg/NeigeItems-Kotlin/releases](https://github.com/ankhorg/NeigeItems-Kotlin/releases)

You should download NeigeItems-xxx.jar (not NeigeItems-api), the file lager than 10MB.

Install it in your server.

All is done! Now plugin will auto display localized item name for now.

## MythicChanger: Extra Item Format option

Through this hook, based on the [ItemFormat](../format/itemformat-tm.md), items can be further modified to their desired appearance.

This feature require your server must install **MythicChanger** plugin, please get it here:

**FREE:** [Click to download](https://www.spigotmc.org/resources/mythicchanger-match-and-modify-all-your-items-without-trouble-1-14-1-21.98523/)

**PREMIUM:** [Click to download](https://www.spigotmc.org/resources/mythicchanger-premium-match-and-modify-all-your-items-without-trouble-1-14-1-21.115913/)

For how to configure the `change-item` section, please read MythicChanger's wiki, [click here](https://app.gitbook.com/o/1ZYzpAAIW7ljevWhGq0R/s/L4peJBqYHI4WQpPthtO4/) to visit. Please note that some of the change rules require <mark style="color:red;">**PREMIUM version of MythicChanger, not PREMIUM version of UltimateShop**</mark><mark style="color:red;">!</mark>

{% hint style="info" %}
If you are using **premium version of MythicChanger**, it will allow you use custom NBT tag by adding nbt-xxx rule here. You can also use `/mc viewnbt` command to view the hold item NBT info.
{% endhint %}

```yaml
change-item:
  set-name: '&fGood Diamond Sword'
```

## AdvancedEnchantments: Extra Item Format option <mark style="color:red;">- Premium</mark>

Through this hook, based on the [ItemFormat](../format/itemformat-tm.md), items can have custom enchantments from AdvancedmentEnchantments.

Plugin like `EcoEnchants, ExcellentEnchants` are vanilla enchants like plugin, you just need to put their enchantment ID to enchants option (like above).

You can use plugin-enchants option to add plugin enchants for your item.

```yaml
plugin-enchants:
  PLANTER: 5 # A AdvancedEnchantments enchantment
```

## MythicChanger: Custom Item Match

[Custom Item Match Method](../features/custom-item-match-method.md) feature requires MythicChanger.

# FAQ

## Q: Does the /shop command have permission?

A: Use `/shop` can directly open a menu called `main`. This is a feature called **Auto Open**, and you can disable it at config.yml file with `menu.auto-open.enabled` option. If you only want some players to be exposed to this command, you can set `conditions` for the menu so that only players who meet the specified conditions can open the menu. For more info, please view [Menus](menus.md) page.

## Q: How do I sell item from UltimateShop not directly supported item plugins?

A: If you really read this Wiki carefully, you wouldn't ask such simple questions. Wiki has telled you solutions everywhere.

* Save Item: We telled you a command called `/shop saveitem` at [Commands](commands.md) page, we also telled you can set `material` option in [Item Format](item-format.md)  to the save item ID you was set to use them.
* Buy Actions: We telled you a option called `buy-actions` in shop configs at [Shops](shops.md) page. In [Actions](actions.md) page, we also telled you we support use command in actions, so just use the give item command here, all is done.
* Give Actions: We telled you this feature at [Single Things](single-things.md) page which is very similar to Buy Actions. What's more, we even give you an example at that page.

## **Q: Why can I only sell 64x items at once?**

**A:** The person asking this question may never know a truth: before using the plugin, you should be familiar with the `config.yml` file. In `config.yml`, there is an option called sell. max amount, and I want you to know its purpose by looking at its name.

## Q: How to change the max amount limit of buy more menu?

A: There is a option called `menu.buy-more.<buy more menu name>.max-amount` option in `config.yml` file, or `buy-more-menu.max-amount` option in your product configs if you are setting up a separate buy more menu for a certain product.

## **Q: How can I sell ItemsAdder item?**

A:

```yaml
items:
  A:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        hook-plugin: ItemsAdder
        hook-item: fishing_pack:common_fishing_bait
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 5
        start-apply: 0
        placeholder: '&65 Coins'
```

## **Q: What does start-apply mean?**

A: This means which times this price will apply. If you set it to 5, price will apply after player buy or sell this product 5 times.

This option will only work for `ANY` or `ALL` price-mode.

## Q: What is different from full (free) version and premium version?

A: Check [Welcome](../) page for more info.

## Q: Can I set different add lore for each product?

A: Yes, in [Shop](shops.md) page we have telled you that `add-lore` also works in each product configs!

## Q: Shop menu can not open after use once!

A: Make sure your `config.yml` is latest format, if not, update it. Or, you are using menu cooldown system, disable it may fix.

## Q: How can I translate item name in buy more menu and plugin message?

A: View [Localized Item Name](../advanced/localized-item-name.md) page.&#x20;

## Q: UltimateShop print Error:XXX message in console.

A: What I want to tell you is already put in the error message itself, like:

#### Error: Can not get prices section in your shop config!!

If there are no issues with the shop, there is no need to pay attention to it. The error message reported by the plugin is a prompt, and the plugin will automatically attempt to fix it once it detects this error.

## Q: How to reset dynamic price?

A: View [Dynamic Price](../advanced/dynamic-price.md) page.

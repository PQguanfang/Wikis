# 🔲General Menus

All menu files are saved in `/menus/` folder.

## Types

There are 3 types of menus.

* Common Menus: Just like other menu plugins doing. You can use them open other shop menus.
* Shop Menus: Shop menus will display products in specified shop in it. Each shop config has a `menu` option to set their corresponding shop menu. The shop menu has all features of a common menu. Multiple shops can share the same shop menu, so when you open these stores, the layout of the menu will be the same.
* Buy More Menus: Can select amount of you will buy or sell. This type of menus have more settings, please view [Buy More Menus](buy-more-menus.md) page to know more. **Buy more menu can only open from shop menus with selecting a product, it can not be directly opened**.

## Configs

* title: Menu title, for shop menu type, support `{shop-name}` to display shop displayname which set in it's config.
* size: Menu size, only support one of the number: **9,18,27,36,45,54**.
* layout: Button layout, this is a list option, list row must equals `size/9`, each line lengh must equals 9. Each character here corresponds to one slot in Minecraft, and 54 characters correspond to 54 slots.
* buttons: Button configs, button ID must be a single char, and use it in `layout` option to set where this button display in menu.
* conditions: Only players who meet the conditions can open this menu, use [Condition Format](../format/condition-format.md) here.
* open-actions: Do action when open this menu, use [Action Format](../format/action-format.md) here.
* close-actions: Do action when close this menu, use [Action Format](../format/action-format.md) here. <mark style="color:red;">**Please carefully note that when you have already opened a menu, if you open other menus through actions or other means, it will also trigger close actions**</mark>**.**&#x20;
* bedrock: Please view [Bedrock M](bedrock-menus-premium.md)[enu](bedrock-menus-premium.md) page to know about it.
* custom-command: Custom Command settings for common menu, if you want to set custom command for shop menu, please add them at [Shops](../shops/shops.md) config.

Example:

```yaml
title: 'Shop'

size: 54

bedrock:
  enabled: true
  content: '&fWelcome to shop.'
  
custom-command:
  name: 'mineral'
  description: 'Custom Words'

conditions: []
  
open-actions:
  1:
    type: sound
    sound: 'ui.button.click' 

close-actions:
  1:
    type: sound
    sound: 'ui.button.click' 

layout:
  - '000000000'
  - '000000000'
  - '0000A0000'
  - '000000000'
  - '000000000'
  - '000000000'

buttons:
  A:
    display-item:
      material: BREAD
      name: '&dFoods'
      lore:
        - '&7Click to open food shop!'
    actions:
      1:
        type: shop_menu
        menu: 'example'
```

For each button, we have those options:

* display-item: The display item of this button, should use [Display Item Format](../format/display-item-format.md).
* actions: The action will executed after we click this button. Use [Action Forma](../format/action-format.md)[t](../format/action-format.md) here.
* fail-actions: The action will executed if we don't meet the condition of this button. Use [Action Forma](../format/action-format.md)[t](../format/action-format.md) here.
* conditions: The condition of this button, if player don't meet this condition, then we will execute the `fail-action`. Use [Condition Format](../format/condition-format.md) here.

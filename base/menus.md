# Menus

All menu files are saved in `/menus/` folder.

## Types

There are 3 types of menus.

* Common Menus, just like other menu plugins doing. You can use them open other shop menus.
* Shop Menus, will display products in specified shop in it.
* Buy More Menus, can select amount of you will buy or sell. This type of menus have more settings, please view [Buy More Menus](menus.md) page to know more.

## Configs

* title: Menu title, for shop menu type, support `{shop-name}` to display shop displayname which set in it's config.
* size: Menu size, only support one of the number: 9,18,27,36,45,54.
* layout: Button layout, this is a list option, list row must equals `size/9`, each line lengh must equals 9.
* buttons: Button configs, button ID must be a single char, and use it in `layout` option to set where this button display in menu.
* conditions: Only players who meet the conditions can open this menu, see [Conditions](../legacy/conditions-legacy.md) for more info.
* open-actions: Do action when open this menu, see [Actions](../legacy/actions-legacy.md) for more info.
* close-actions: Do action when close this menu, see [Actions](../legacy/actions-legacy.md) for more info. <mark style="color:red;">**Please carefully note that when you have already opened a menu, if you open other menus through actions or other means, it will also trigger close actions**</mark>**.**&#x20;
* bedrock: Please view [Bedrock UI](../advanced/bedrock-ui-premium.md) page to know about it.

Example:

```yaml
title: 'Shop'

size: 54

bedrock:
  enabled: true
  content: '&fWelcome to shop.'

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

* display-item: The display item of this button, should use [Display Item Format](display-item-format.md).
* actions: The action will executed after we click this button.
* fail-actions: The action will executed if we don't meet the condition of this button, see [Actions](../legacy/actions-legacy.md) for more info.&#x20;
* conditions: The condition of this button, if player don't meet this condition, then we will execute the `fail-action`.

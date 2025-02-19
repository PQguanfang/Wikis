# 🪄Sell Stick - Premium

All sell stick configs are stored in `sell_sticks` folder. The file name is it's ID, for example: `A.yml` means it's ID is `A`. An example of it's config is like below:

```yaml
display-item:
  material: STICK
  name: '&dSell Stick &7(5 times)'
  lore:
    - '&fRight click a chest to use this item!'
    - ''
    - '&cLeft usages: {times}'

usage-times: 5

multiplier: 1.2

actions:
  1:
    type: sound
    sound: 'block.note_block.pling'

conditions: []
```

* display-item: The display item of sell stick. Should use [Item Format](../format/itemformat-tm.md).
* useage-times: Maxium usage times of this item. If this option value is less than 0 or does not exist, we will make this sell stick is infinite.
* multiplier: The multiplier of sell stick. It only supports economy type of price.
* actions: The action will execute after use this sell stick. Should use [Action format](../format/action-format.md).
* conditions: The condition player need meet to use this sell stick. Should use [Condition Format](../format/condition-format.md).

# Sell Stick - Premium

Open `config.yml` and find below contents:

```yaml
# Premium version only
sell-stick-items:
  A:
    material: STICK
    name: '&dSell stick &7(5 times)'
    lore:
      - '&fClick a chest to use this item!'
      - ''
      - '&cLeft usages: {times}'
    usage-times: 5
  B:
    material: STICK
    name: '&dAdvanced Sell stick &7(50 times)'
    lore:
      - '&fClick a chest to use this item!'
      - ''
      - '&cLeft usages: {times}'
    usage-times: 50
  C:
    material: STICK
    name: '&5Epic Sell Stick'
    lore:
      - '&fClick a chest to use this item!'
      - ''
      - '&cLeft usages: {times}'
    usage-times: -1
```

A and B is ItemID, below it's their config section.

Should use [Item Format](broken-reference).

* useage-times: Maxium usage times of this item. If this option value is less than 0 or does not exist, we will make this sell stick is infinite.

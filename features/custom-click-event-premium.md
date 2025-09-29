# 🎮Custom Click Event - Premium

* Start from version 2.5.1, you can set custom click event for products in shop GUI.
* Find those contents at `config.yml` file.

```yaml
  # Support value: https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.htm
  # Support use ;; symbol to make multi click type.
  click-event:
    buy: 'SHIFT_LEFT'
    sell: 'RIGHT'
    buy-or-sell: 'LEFT'
    # If you want to disable select-amount feature, set this to NEVER.
    select-amount: 'SHIFT_RIGHT'
    sell-all: 'DROP'
    buy-one-stack: 'SWAP_OFFHAND'
  # Custom click actions for shop menu.
  # Premium version only.
  click-event-actions:
    buy-one-stack:
      display-name: 'Buy One Stack'
      buy-only: true
      1:
        type: buy
        shop: '{shop}'
        item: '{item}'
        amount: 64
    sell-one-stack:
      display-name: 'Sell One Stack'
      sell-only: true
      1:
        type: sell
        shop: '{shop}'
        item: '{item}'
        amount: 64
```

* Here we create a new custom click event called `buy-one-stack`, in this custom event, we will execute a action which can buy this product x64 amount.
* After reload the server, if you press **F** key on a product, we will execute the action you set in `click-event-actions` section, like here we will buy x64 this item.

## Options

Each action in `click-event-actions` support those options, like example above:

* display-name: The friendly name displayed.
* buy-only: This click event button will only display when this product can be purchased (means has buy price).
* sell-only: This click event button will only display when this product can be sold (means has sell price).

Those options only work in bedrock form UI or Java Dialog UI.

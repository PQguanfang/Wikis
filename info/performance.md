# 🚀Performance

UltimateShop is just a shop plugin that usually does not have too much impact on the server. It is usually a performance issue caused by your unreasonable settings or other plugins, such as:

## Do not use ANY, ALL price/product mode unless necessary.

Different from `CLASSIC_ANY, CLASSIC_ALL` mode, `ANY` and `ALL` mode, the calculation for each buy or sell is independent. Only use the 2 mode when you set dynamic price or limit.

## MMOItems/MythicMobs Item generation performance.

Both plugins are spend much server resource to generate item than vanilla items.&#x20;

## Set placeholder.click.enabled option to false.

This maybe save server performance.

```yaml
  click:
    # If enabled, {buy-click} and {sell-stick} will display different value according to product status.
    # But, it will maybe make server lag if you are running big server and have many products in your shop.
    enabled: false
```

## Set cooldown for menu system.

Recommend use when you are running big server, it will make player no longer quickly click and reopen shop menu to make sure UltimateShop not lag your server.

```yaml
  # Recommend use when you are running big server, it will make player no longer quickly click
  # and reopen shop menu to make sure UltimateShop not lag your server.
  # In ticks.
  cooldown:
    click: 6 # Default value is -1, set value greater than 5 is recommended.
    reopen: 20 # Default value is -1, set value greater than 5 is recommended.
```

## Do not enable auto update GUI feature.

Enabling these options will significantly increase server performance consumption, but buttons within the GUI will be able to automatically update.

```yaml
  shop:
    # Whether shop menu will refresh every 1 second.
    # This will refresh placeholder that displayed in display item lore.
    # But maybe lead to server lag if you have much online players, and they are all opening shop GUI.
    update: false
    # Whether shop menu will refresh every click in it.
    # This will refresh placeholder that displayed in display item lore.
    # But maybe lead to server lag if you have much online players, and they are all opening shop GUI.
    click-update: false
```

In most cases, you just want the GUI to update and display the latest data when we reset buy times or sell times, so you can achieve this idea through `use-times.auto-reset-mode` option.

```yaml
  auto-reset-mode: true
```

If you pursue ultimate plugin performance, it's best not to turn on this option either.

```yaml
  auto-reset-mode: false
```

## Use BUKKIT item give method.

This item give method has the best performance, but the cost is that there may be some issues with stacking items, and when the player's inventory is full, we can only throw the excess items on the ground instead of preventing the player from further trading.

```yaml
give-item:
  # Support value: BUKKIT, SMART
  # SMART will cost more server performance but will follow the vanilla max stack to give player item, also support check full.
  give-method: BUKKIT
  # Only support SMART give method.
  check-full: false
```

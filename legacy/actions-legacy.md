# Actions (Legacy)

## Prefix Format

* All action support add prefix.
* `@Click Type@` means this action only executed when player use this click type to active this action. Won't work for `open-actions`, `close-action` in menu configs and `buy-actions`, `sell-actions` in product configs. For example:

```yaml
  N:
    display-item:
      material: RAIL
      name: '&a&lTRANSPORTS'
      lore:
        - '&7Some things related to'
        - '&7transport like rails.'
    actions:
      - '@LEFT@shop_menu: transport'
```

Then this button can only open shop menu by left click. **Please note that bedrock players can only left click in their client!**

## Suffix Format

* All action support add suffix.
* `-o` means this action will run only once when player try buy/sell this product. For example, player buy 50x APPLE, without this suffix, action will run 50 times, with this suffix, action will run only once.
* `-<number>` means this action will run only when player have buy/sell spcified times product, like -1 means action will run only when player first buy/sell this product.
* `-b` means when multiple products are about to be sold, adding this suffix means that only the first product's action will be executed.
* When using multiple suffixes, fill in the following order: `-b-<number>-o`.

## Available Placeholders

* {world}
* {amount}
* {player\_x}
* {player\_y}
* {player\_z}
* {player\_pitch}
* {player\_yaw}
* {player}
* {item} - Product ID
* {item-name} - Product Display Name
* {shop} - Shop ID
* {shop-name} - Shop Display Name
* {shop-menu} - Shop's Menu ID

## None

Will do nothing.

```yaml
- 'none'
```

## Sound

Send sound to player.

<pre class="language-yaml"><code class="lang-yaml"><strong>- 'sound: ui.button.click;;1;;1' 
</strong># "sound: SOUND;;volume;;pitch"
</code></pre>

Sound is recommend to use both `-b` and `-o` suffix, otherwise when use sell all or sell multi quantity items when play this sound multi times.

Example:

<pre class="language-yaml"><code class="lang-yaml"><strong>- 'sound: ui.button.click;;1;;1-b-o' 
</strong></code></pre>

## Message

Send a message to the player, support color code.

```yaml
- 'message: Hello!'
```

## Announcement

Send a message to all online players, support color code.&#x20;

```yaml
- 'announcement: Hello!'
```

## Effect

Give players potion effect.

```yaml
- 'effect: BLINDNESS;;1;;60'
```

**BLINDNESS** is SpigotAPI effect ID, its different form minecraft effect namespace, you can find them here: [https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/potion/PotionEffectType.html](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/potion/PotionEffectType.html).

**1** is effect level.

**60** is effect duration.

## Teleport

Teleport player to specified location.

```yaml
- 'teleport: LobbyWorld;;0;;128;;10'
```

**LobbyWorld** is world name.

**0** is X pos.

**128** is Y pos.

**10** is Z pos.

You can also add yaw and pitch at the end of action string, like:

```yaml
- 'teleport: DungeonWorld;;100;;30;;300;;90;;0'
```

## Player Command

Make the player excutes a command.

```yaml
- 'player_command: tell i am a boy!'
```

## Op Command

Make the player excutes a command as OP.

```yaml
- 'op_command: tell i am a boy!'
```

## Console Command

Make the console excutes a command.

```yaml
- 'console_command: op {player}'
```

## Spawn vanilla mobs

Spawn vanilla mobs, mob ID follow this page:

[https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/package-summary.html](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/package-summary.html)

```yaml
- 'entity_spawn: ZOMBIE'
```

## MythicMobs spawn

### MythicMobs Spawn at block location

Require MythicMobs.

```yaml
- 'mythicmobs_spawn: test;;1'
```

`test` is **Mob ID**, `1` is the **level**. Mob ID and level use `;;` spite.

Level can remove, this means you can set:

```yaml
- 'mythicmobs_spawn: test'
```

### MythicMobs Spawn at remote location

Require MythicMobs.

Simailr to MythicMobs Spawn at block location, but you need add `;;world name;;x;;y;;z` at the end of action string, for example:

```yaml
- 'mythicmobs_spawn: testMonster;;LobbyWorld;;11;;64;;12'
```

## Open Common Menu

Open specified common menus.

```yaml
- 'open_menu: main' # Open Java UI for Jave players 
# and open bedrock UI for bedrock players.
```

## Open Shop Menu

```yaml
- 'shop_menu: food_shop' # Open Java UI for Jave players 
# This is shop file name, not menu file name!
```

## Buy Product

```yaml
- 'buy: food;;A;;5' 
# Shop ID;;Product ID;;Amount
```

## Sell Product

```yaml
- 'sell: food;;A;;5' 
# Shop ID;;Product ID;;Amount
```

## Sell All

```yaml
- 'sellall: food;;A' 
```

## Close

Close the inventory.

```yaml
- 'close'
```

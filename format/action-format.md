# 🎬Action Format

The action format will consist of several options.

{% hint style="info" %}
The `actions` in the **Action Format** **example** only represent **Action Format** start from here. Please refer to the page description of the corresponding function for specific option names, such as `buy-actions`.
{% endhint %}

## General Options

#### Apply Times

This action will run only when player have buy/sell spcified times product.&#x20;

* start-apply: Start which times this action will apply. **Optional. Default to 0.**
* end-apply: Last times the action will apply. **Optional. Default to infinite.**
* apply: Which times this action will apply, format: `[1,2,3,4]`. **Optional. Default use start-apply option value.**

```yaml
    actions:
      1:
        apply: [1,2,3,4,5]
        start-apply: 1
        end-apply: 5
```

#### Sell All Once / Multi Once

When multiple products are about to be sold, adding this option means that only the first product's action will be executed. Very useful for sounds action, if you didn't add this, all product's sound action will execute.

```yaml
    actions:
      1:
        sell-all-once: true # In sell all
        multi-once: true # In buy more menu
```

#### Open Once

Only work for menu's open-actions option, if enabled, only the menu opened by the player for the first time will trigger this action, which means that if the opened menu was opened through another menu, this action cannot be triggered.

```yaml
    actions:
      1:
        open-once: true
```

#### Click Type

This action only executed when player use this click type to active this action. Won't work for `open-actions`, `close-action` in menu configs and `buy-actions`, `sell-actions` in product configs.

```yaml
    actions:
      1:
        click-type: LEFT
```

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

## Sound

Send sound to player.

```yaml
    actions:
      1:
        type: sound
        sound: 'ui.button.click'
        volume: 1
        pitch: 1
```

## Message

Send a message to the player, support color code.

```yaml
    actions:
      1:
        type: message
        message: 'Hello!'
```

## Title

Send title to the player, support the color code.

```yaml
    actions:
      1:
        type: title
        main-title: 'Good day'
        sub-title: 'Not bad'
        fade-in: 10
        stay: 70
        fade-out: 30
```

## Particle

```yaml
    actions:
      1: 
        type: particle
        particle: HEART
        count: 20
        offset-x: 0.3
        offset-y: 1.0
        offset-z: 0.3
        speed: 0.01
```

## Announcement

Send a message to all online players, support color code.&#x20;

```yaml
    actions:
      1:
        type: announcement
        message: 'Hello!'
```

## Effect

Give players potion effect.

```yaml
    actions:
      1:
        type: effect
        potion: BLINDNESS
        duration: 60
        level: 1
        ambient: true # Optional
        particles: true # Optional
        icon: true # Optional
```

## Teleport

Teleport player to specified location.

```yaml
    actions:
      1:
        type: teleport
        world: LobbyWorld
        x: 100
        y: 30
        z: 300
        pitch: 90 # Optional
        yaw: 0 # Optional
```

## Player Command

Make the player excutes a command.

```yaml
    actions:
      1:
        type: player_command
        command: 'tell Hello!'
```

## Op Command

Make the player excutes a command as OP.

```yaml
    actions:
      1:
        type: op_command
        command: 'tell Hello!'
```

## Console Command

Make the console excutes a command.

```yaml
    actions:
      1:
        type: console_command
        command: 'op {player}'
```

## Spawn vanilla mobs

Spawn vanilla mobs.

```yaml
    actions:
      1:
        type: entity_spawn
        entity: ZOMBIE
        world: LOBBY # Optional
        x: 100.0 # Optional
        y: 2.0 # Optional
        z: -100.0 # Optional
```

## MythicMobs spawn

Require MythicMobs.

```yaml
    actions:
      1:
        type: mythicmobs_spawn
        entity: Super_Skeleton
        level: 1 # Optional
        world: LOBBY # Optional
        x: 100.0 # Optional
        y: 2.0 # Optional
        z: -100.0 # Optional
```

## Open Common Menu

Open specified common menus.

```yaml
    actions:
      1:
        type: open_menu
        menu: main
```

## Open Shop Menu

```yaml
    actions:
      1:
        type: shop_menu
        shop: farming
```

## Open Buy More Menu

```yaml
    actions:
      1:
        type: buy_more_menu
        shop: farming
        item: A
```

## Open Buy More Menu with Custom Buy More Menu settings <mark style="color:red;">- Premium</mark>

```yaml
    actions:
      1:
        type: buy_more_menu
        shop: farming
        item: A
        buy-more-menu:
          menu: buy-more-buy
          max-amount: 128
```

## Open Sell All Menu

```yaml
    actions:
      1:
        type: sell_all_menu
```

## Buy Product

```yaml
    actions:
      1:
        type: buy
        shop: food
        item: A
        amount: 5 # Optional
```

## Sell Product

```yaml
    actions:
      1:
        type: sell
        shop: food
        item: A
        amount: 5 # Optional
        sell-all: true # Optional
```

## Close

Close the inventory.

```yaml
    actions:
      1:
        type: close
```

## Delay <mark style="color:red;">- Premium</mark>

Make the action run after X ticks.

```yaml
    actions:
      1:
        type: delay
        time: 50
        wait-for-player: true
        actions:
          1:
            type: entity_spawn
            entity: ZOMBIE
```

## Chance <mark style="color:red;">- Premium</mark>

Set the chance the action will be excuted, up to 100. 50 means this action has 50% chance to excute.

```yaml
    actions:
      1:
        type: chance
        rate: 50
        actions:
          1:
            type: entity_spawn
            entity: ZOMBIE
```

## Any <mark style="color:red;">- Premium</mark>

Randomly choose specified amount of actions to execute.

```yaml
    actions:
      1:
        type: any
        amount: 2
        actions:
          1:
            type: entity_spawn
            entity: ZOMBIE
          2:
            type: entity_spawn
            entity: SKELETON
          3:
            type: entity_spawn
            entity: WITHER
```

## Conditional <mark style="color:red;">- Premium</mark>

Only players meet the conditions you set here will be able to execute the action.

```yaml
    actions:
      1:
        type: conditional
        conditions:
          1: 
            type: world
            world: lobby
        actions:
          1:
            type: entity_spawn
            entity: ZOMBIE
```

## Connect <mark style="color:red;">- Premium</mark>

Require enable `bungeecord-sync.enabled` option in config.yml and correctly set the BungeeCord settings. For more info, please view [Multi Server Sync](../features/multi-server-sync-premium.md) page.

```yaml
    actions:
      1:
        type: connect
        server: 'lobby'
```

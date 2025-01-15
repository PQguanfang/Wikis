# ⚖️Condition Format

The condition format will consist of several options.

{% hint style="info" %}
The `conditions` in the **Condition Format example** only represent **Condition Format** from now on. Please refer to the page description of the corresponding function for specific option names, such as `buy-conditions`.
{% endhint %}

## General Options

#### Apply Times

This condition will only check when player have buy/sell spcified times product.&#x20;

* start-apply: Start which times this condition will apply. **Optional. Default to 0.**
* end-apply: Last times the condition will apply. **Optional. Default to infinite.**
* apply: Which times this condition will apply, format: `[1,2,3,4]`. **Optional. Default use start-apply option value.**

```yaml
    conditions:
      1:
        apply: [1,2,3,4,5]
        start-apply: 1
        end-apply: 5
```

#### Click Type

This condition only checked when player use this click type to use the button.&#x20;

```yaml
    conditions:
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

## World

Player must be in the world.

<pre class="language-yaml"><code class="lang-yaml"><strong>  conditions:
</strong>    1:
      type: world
      world: lobby
</code></pre>

## Biome

Player must be in the biome.

```yaml
  conditions:
    1:
      type: biome
      biome: oraxen
```

## Permission

Player must has the permission.

**Remember that OP players will always have all permissions unless plugin set it not by default, so if you want to test this condition, you have to deop yourself.**

```yaml
  conditions:
    1:
      type: permission
      permission: 'group.vip'
```

## Placeholder

Player must be meet the placeholder condition.

Rule can be set to:

* \>=
* <=
* \>
* <
* \== (String)
* \= (Number)
* != (Number or string)
* !\*= (Number or string) Not contains.
* \*= (String) Contains, for example, str \*= string is true, but example \*= ple is false.

```yaml
  conditions:
    1:
      type: placeholder
      placeholder: '%player_health%'
      rule: '<='
      value: 5
```

## Any <mark style="color:red;">- Premium</mark>

```yaml
  conditions:
    1:
      type: any
      conditions:
        1:
          type: placeholder
          placeholder: '%eco_balance%'
          rule: '>='
          value: 200
        2:
          type: placeholder
          placeholder: '%player_points%'
          rule: '>='
          value: 400
```

## Not <mark style="color:red;">- Premium</mark>

```yaml
  conditions:
    1:
      type: not
      conditions:
        1:
          type: placeholder
          placeholder: '%eco_balance%'
          rule: '>='
          value: 200
```

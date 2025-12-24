# ♻️Product Config: Buy/Sell Times Reset

## FAQ: Why this feature do not crash my server since it also reset all players buy/sell times?

This feature will not clear all players' buy/sell times at once. We will store **different timestamp data** based on the **reset mode**. When our estimated reset time has been reached, we will start resetting the data.&#x20;

* If the player is on the server, the buy/sell times will only be reset after the player opens the shop. (Before they open the shop, the buy/sell times didn't be reset)
* If the player is not on the server, the buy/sell times will only be reset after they join the server.

These measures are aimed at optimizing the performance of plugins when resetting data, and we will not change these behaviors. If you are surprised by these behaviors and do not want to do so, then replacing with other plugins is a better choice.

## Reset

We will only attempt to reset under the following circumstances:

* Before the player performs a purchase/sell operation
* When the player opens the shop GUI
* Auto reset (require enable `use-times.auto-reset-mode` option in `config.yml` file, will cost more server performance, player must online, otherwise we will try auto reset when he rejoin the server)

{% hint style="info" %}
This option solves the problem that the buy times and sell times cannot be reset in a timely manner when the reset time has arrived. If the product has never been purchased or sold, then there is no reset time and it will naturally not be reset
{% endhint %}

## Option Types

Buy times have those options:

* buy-times-reset-mode (before 3.3.0 is buy-limits-reset-mode, but they are same)
* buy-times-reset-time (before 3.3.0 is buy-limits-reset-time, but they are same)
* buy-times-reset-time-format
* buy-times-reset-value
* buy-times-max-value

Sell times have those options:

* sell-times-reset-mode (before 3.3.0 is sell-limits-reset-mode, but they are same)
* sell-times-reset-time (before 3.3.0 is sell-limits-reset-time, but they are same)
* sell-times-reset-time-format
* sell-times-reset-value
* sell-times-max-value

If you want to enable buy times and sell times reset for all products, you can simply modify it at `config.yml` file.

```yaml
use-times:
  default-reset-mode: 'NEVER'
  default-reset-time: '00:00:00'
  # This only works for CUSTOM type of reset mode.
  default-reset-time-format: 'yyyy-MM-dd HH:mm:ss'
  default-reset-value: 0
  # Set -1 to disable.
  default-max-value: -1
  # If set to true, product default buy / sell times will be set to reset value set in product configs or default value above.
  set-reset-value-by-default: true
  # If set to true, max value set in product configs or default value set above will only work for total placeholder.
  max-value-for-total-only: true
```

No matter what methods you set it up in, we can see that this feature consists of 5 option types:

* reset mode
* reset time
* reset time format (only required for `CUSTOM` type)
* reset value
* max value

## Reset Mode

Support those modes:

* NEVER:&#x20;
* TIMER: It will reset after the time you specify, for example, after 5 hours.
* TIMED: It will be reset at the corresponding time, such as 8:15 pm.
* COOLDOWN\_TIMER (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* COOLDOWN\_TIMED (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* COOLDOWN\_CUSTOM (Added in 3.9.1) <mark style="color:red;">**- Premium**</mark>
* RANDOM\_PLACEHOLDER: Synchronize with the reset time of the specified random placeholder. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* CUSTOM: Directly enter the reset time in reset time, and the plugin will not perform any calculations. Recommend obtain reset time through the Placeholder API results. You need set time format at `reset-time-format` type option to helps us know how does your PlaceholderAPI results be like. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>

{% hint style="info" %}
For random placeholder reset mode: supports `TIMER`, `TIMED`, `CUSTOM`. The reset time of the random placeholder will be saved to the server, so its usage effect is the same as `COOLDOWN_TIMER`, `COOLDOWN_TIMED` and `COOLDOWN_CUSTOM`.
{% endhint %}

### Difference between COOLDOWN\_TIMED (or COOLDOWN\_TIMER) and TIMED (or TIMER)

`TIMED` and `TIMER` will start generating reset time after each buy or sell until the player reaches the limit and not save the generated reset time, while `COOLDOWN_TIMED` and `COOLDOWN_TIMER` will immediately start generating the next reset time after the last reset and save the generated time. It will not reset again unless the rest time is reached.

{% hint style="info" %}
We will only attempt to reset and generate new reset time for `COOLDOWN_TIMED` and `COOLDOWN_TIMER`  reset mode under the following circumstances:

* Before the player performs a purchase/sell operation
* When the player opens the shop GUI
* Auto reset (require enable `use-times.auto-reset-mode` option in `config.yml` file, will cost more server performance, player must online, otherwise we will try auto reset when he rejoin the server)
{% endhint %}

For this reason, when using `COOLDOWN_TIMED` or `COOLDOWN_TIMER` mode, the reset time will not automatically adjust due to server restarts, configuration modifications, or other reasons. This means that if you mistakenly set the product to refresh after 1 year, the reset time will not automatically change due to your correction, but `TIMED` or `TIMER` rules can do this.

Also, when use last reset placeholder, `COOLDOWN_TIMED` or `COOLDOWN_TIMER` mode will return actual reset time, `TIMED` or `TIMER` mode will return the time that first buy or sell after reset.

## Reset Time

Different reset modes require different values to be filled in here. Supports placeholders, <mark style="color:red;">**the placeholder used here must be on the server side, which means that all players receive the same value.**</mark>

#### NEVER

Don't need anything here.

#### TIMER/COOLDOWN\_TIMER

You can enter 3 to 5 numbers here, separated by a `:` symbol between each number. For example: `15:00:00`.

Each number from **right** to **left** represents:

* Seconds
* Minutes
* Hours
* Days <mark style="color:red;">**- Premium**</mark>
* Months <mark style="color:red;">**- Premium**</mark>

In this example, represents 15 hours later. Which means: **if now time is 2023-09-04 12:00:00. Will reset after 15 hours, which means 2023-09-05 03:00:00.**

#### TIMED/COOLDOWN\_TIMED

The composition of TIMED and TIMER is almost identical, but the first three digits from the right-hand side represent the time of day. Let's also take 15:00:00 as an example:

If now time is 2023-09-04 12:00:00, will reset at 2023-09-04 15:00:00.

This is the result obtained with days set to 0. If you set it to 1, we will add another day, and that's it.

It is worth noting that if you want to do a daily store, days should be set to 0, and if you want to do a weekly store, days should be set to 6. Because you need to reset the number of times on the last day, not on the second day after the last day, right?

This type of reset mode also supports set multi reset time, each reset time use `;;` to splite, we will pick up the earliest reset time. For example: <mark style="color:red;">(Premium only)</mark>

```yaml
    sell-times-reset-mode: 'TIMED'
    sell-times-reset-time: '20:00:00;;19:00:00'
```

In this example, this product will reset reset at 19:00 and 20:00 every day.

#### CUSTOM/COOLDOWN\_CUSTOM <mark style="color:red;">**- Premium**</mark>

You only need to enter a Placeholder API placeholder here, and the result of the placeholder must include the complete year, month, day, hour, minute, and second. You also need to enter their format in the reset time format option, because different types of placeholders return different time formats, making it difficult for plugins to achieve uniformity.&#x20;

#### RANDOM\_PLACEHOLDER <mark style="color:red;">**- Premium**</mark>

Enter a valid random placeholder ID here.

## Reset Value <mark style="color:red;">**- Premium**</mark>

By default, the reset value is 0, but, if you want to make some difference, this is allowed. Also this option supports placeholders, If combined with a random placeholder, it can achieve different reset values for players after each reset.

The reset value is apply for each reset, if player never buy or sell the product, you need consider set default value before using reset value. For more info, please view below "Default Value" section.

<mark style="color:red;">This option is very dangerous, you must set it carefully</mark>. You <mark style="color:red;">**MUST**</mark> ensure that **the value of buy/sell limits is always greater than the value of buy/sell reset**. This means that once reset, players must be able to repurchase/sell items again, otherwise you will see a situation where this item can never be purchased/sell again, and this situation is irreversible **UNLESS** you remove the buy/sell limits for this product or use commands to set the buy/sell times manually, <mark style="color:red;">**REMEMBER THIS**</mark>!

## Default Value <mark style="color:red;">**- Premium**</mark>

The reset value will only be used after the buy times or sell times have been reset. Sometimes, if you not only want to do this, but also want to set it as the default value, you can enable the `use-times.set-reset-value-by-default` option in `config.yml` to do so. If you want a feature like default stock, it would be very useful.

## Max Value <mark style="color:red;">**- Premium**</mark>

You can set maximum values for buy times and sell times, and when the maximum value is reached, the plugin will no longer accumulate buy times and sell times.

Please note:

* After reaching the limit, players can still continue to purchase or sell products, but the plugin will not accumulate more times. If you want players to no longer purchase or sell products, then you should use the `buy-limits` option or `sell-limits` option in [Products](products.md) config instead of this feature.
* Due to the setting of an upper limit that no longer accumulates, if the set upper limit is greater than the limit value, buy limits and sell limits will no longer be useful. Other features not mentioned may also be affected.
* You can modify the `use-times.max-value-for-total-only` option in `config.yml` to ensure that the times placeholder accumulates normally even after reaching its maximum value, but the total placeholder does not continue to accumulate after reaching its maximum value. For information about these two placeholders, please refer to [this page](../placeholders/built-in-placeholders.md).

## Dynamic Reset Time <mark style="color:red;">**- Premium**</mark>

This example uses a random placeholder to randomly refresh products after 3, 4, or 5 hours, instead of a fixed time refresh.

Created a random placeholder like this in `random_placeholder` folder:

```yaml
reset-mode: ONCE
elements:
  - '03:00:00'
  - '04:00:00'
  - '05:00:00'
```

Use this placeholder at `buy-times-reset-time` option in any product configs.

```yaml
  B:
    price-mode: ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: GOLD_INGOT
        amount: 1
    buy-prices:
      # 
    sell-prices:
      #
    buy-limits:
      default: '2'
    buy-times-reset-mode: 'COOLDOWN_TIMED'
    buy-times-reset-time: '{random_reset}' # <--- Used here, sell-times also works!
```

## Dynamic Reset Value <mark style="color:red;">**- Premium**</mark>

By default, each reset will lead to player's buy times or sell times to 0, but you can also change it to different value, and even the random value!

Created a random placeholder like this in `random_placeholder` folder:

```yaml
reset-mode: ONCE
elements:
  - '0~20' # A random number from 0 to 20
  - '40' # A fixed number
```

Use this placeholder at `buy-times-reset-valuvalue` option in any product configs.

```yaml
  B:
    price-mode: ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: GOLD_INGOT
        amount: 1
    buy-prices:
      # 
    sell-prices:
      #
    buy-limits:
      default: '2'
    buy-times-reset-mode: 'TIMED'
    buy-times-reset-time: '19:00:00;;20:00:00' # <--- TIMED mode supports multi reset time!
    buy-times-reset-value: '{random_resetvalue}' # <--- Used random placeholder
```

## Cron Reset <mark style="color:red;">- Premium</mark>

You can use Cron format in reset time.&#x20;

* Set reset mode to `COOLDOWN_CUSTOM` (for random placeholder, set it to `CUSTOM`).
* Use `{cron_"<Cron Expression"}` built-in placeholder in reset time. Don't miss out the `"` symbol.

For example:

```yaml
    sell-times-reset-mode: 'COOLDOWN_CUSTOM'
    sell-times-reset-time: '{cron_"0 0 0 ? * 5"}'
    # sell-times-reset-time-format: 'yyyy-MM-dd HH:mm:ss' 
    # You do not need set a time format here, this just help you know there is a option that you can set custom time format.
```

You can obtain the Cron expression you want by asking ChatGPT. For example, the Cron expression in this example means to reset at 0:00 every Thursday. We do not provide any help related to how to write Cron expression.

Should use **Quartz** format.

{% hint style="info" %}
You **MUST** make sure that time format of the result of Cron placeholder (set it in `config.yml` file) and the time format you set here is same. By default, they are same.
{% endhint %}

## Reset Time does not correct?

* The product must have been purchased or sold (for `TIMED/TIMER`) OR been viewed (for `COOLDOWN_TIMED/COOLDOWN_TIMER`) once before the next reset time can be stored. Otherwise, we can only display the possible reset time calculated based on the current time after the transaction is completed.
* We will only reset the player's data when they are online. If the player is not online but has reached the reset time, we will reset it when they join the server again. The new reset time will be based on the current time, not the ideal reset time (because the player is not online at this time). The server data does not have this problem (because the server is always online), so it is very normal to use different reset times for the server and player. (Usually happens in `COOLDOWN_TIMER` reset mode)

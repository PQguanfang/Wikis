# ♻️Product Config: Buy/Sell Times Reset

## FAQ: Why this feature do not crash my server since it also reset all players buy/sell times?

This feature will not clear all players' buy/sell times at once. We will store **different timestamp data** based on the **reset mode**. When our estimated reset time has been reached, we will start resetting the data.&#x20;

* If the player is on the server, the buy/sell times will only be reset after the player opens the shop. (Before they open the shop, the buy/sell times didn't be reset)
* &#x20;If the player is not on the server, the buy/sell times will only be reset after they join the server.

These measures are aimed at optimizing the performance of plugins when resetting data, and we will not change these behaviors. If you are surprised by these behaviors and do not want to do so, then replacing with other plugins is a better choice.

## Option Types

Buy times have those options:

* buy-times-reset-mode (before 3.3.0 is buy-limits-reset-mode, but they are same)
* buy-times-reset-time (before 3.3.0 is buy-limits-reset-time, but they are same)
* buy-times-reset-time-format
* buy-times-reset-value

Sell times have those options:

* sell-times-reset-mode (before 3.3.0 is sell-limits-reset-mode, but they are same)
* sell-times-reset-time (before 3.3.0 is sell-limits-reset-time, but they are same)
* sell-times-reset-time-format
* sell-times-reset-value

If you want to enable buy times and sell times reset for all products, you can simply modify it at `config.yml` file.

```yaml
use-times:
  default-reset-mode: 'NEVER'
  default-reset-time: '00:00:00'
  # This only works for CUSTOM type of reset mode.
  default-reset-time-format: 'yyyy-MM-dd HH:mm:ss'
  default-reset-value: 0
```

No matter what methods you set it up in, we can see that this feature consists of three option types:

* reset mode
* reset time
* reset time format (only required for `CUSTOM` type)
* reset value

## Reset Mode

Support those modes:

* NEVER:&#x20;
* TIMER: It will reset after the time you specify, for example, after 5 hours.
* TIMED: It will be reset at the corresponding time, such as 8:15 pm.
* COOLDOWN\_TIMER (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* COOLDOWN\_TIMED (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* RANDOM\_PLACEHOLDER: Synchronize with the reset time of the specified random placeholder. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* CUSTOM: Directly enter the reset time in reset time, and the plugin will not perform any calculations. Recommend obtain reset time through the Placeholder API results. You need set time format at `reset-time-format` type option to helps us know how does your PlaceholderAPI results be like. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>

### Difference between COOLDOWN\_TIMED (or COOLDOWN\_TIMER) and TIMED (or TIMER)

`TIMED` and `TIMER` will start generating reset time after each buy or sell until the player reaches the limit, while `COOLDOWN_TIMED` and `COOLDOWN_TIMER` will start generating reset time after the first buy or sell and will never update the reset time until the reset time reached.

For this reason, when using `COOLDOWN_TIMED` or `COOLDOWN_TIMER` mode, the reset time will not automatically adjust due to server restarts, configuration modifications, or other reasons. This means that if you mistakenly set the product to refresh after 1 year, the reset time will not automatically change due to your correction, but `TIMED` or `TIMER` rules can do this.

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

#### CUSTOM <mark style="color:red;">**- Premium**</mark>

You only need to enter a Placeholder API placeholder here, and the result of the placeholder must include the complete year, month, day, hour, minute, and second. You also need to enter their format in the reset time format option, because different types of placeholders return different time formats, making it difficult for plugins to achieve uniformity.&#x20;

#### RANDOM\_PLACEHOLDER <mark style="color:red;">**- Premium**</mark>

Enter a valid random placeholder ID here.

## Reset Value <mark style="color:red;">**- Premium**</mark>

By default, the reset value is 0, but, if you want to make some difference, this is allowed. Also this option supports placeholders, If combined with a random placeholder, it can achieve different reset values for players after each reset.

## Dynamic Reset Time <mark style="color:red;">**- Premium**</mark>

This example uses a random placeholder to randomly refresh products after 3, 4, or 5 hours, instead of a fixed time refresh.

Created a random placeholder like this in `config.yml` file:

```yaml
  # Premium version only.
  random:
    reset:
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
    buy-times-reset-mode: 'TIMED'
    buy-times-reset-time: '{random_reset}' # <--- Used here, sell-times also works!
```

## Dynamic Reset Value <mark style="color:red;">**- Premium**</mark>

By default, each reset will lead to player's buy times or sell times to 0, but you can also change it to different value, and even the random value!

Created a random placeholder like this in `config.yml` file:

```yaml
  # Premium version only.
  random:
    reset:
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

## Reset Time do not correct?

* The product must have been purchased or selled once before the next reset time can be stored. Otherwise, we can only display the possible reset time calculated based on the current time after the transaction is completed.

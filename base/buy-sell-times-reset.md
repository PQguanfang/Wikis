# Buy/Sell Times Reset

You can set buy or sell times reset at each item's configs.

## Option Types

Buy times have those options:

* buy-times-reset-mode (before 3.3.0 is buy-limits-reset-mode, but they are same)
* buy-times-reset-time (before 3.3.0 is buy-limits-reset-time, but they are same)
* buy-times-reset-format

Sell times have those options:

* sell-times-reset-mode (before 3.3.0 is sell-limits-reset-mode, but they are same)
* sell-times-reset-time (before 3.3.0 is sell-limits-reset-time, but they are same)
* sell-times-reset-format

If you want to enable buy times and sell times reset for all products, you can simply modify it at `config.yml` file.

```yaml
use-times:
  default-reset-mode: 'NEVER'
  default-reset-time: '00:00:00'
  # This only works for CUSTOM type of reset mode.
  default-reset-time-format: 'yyyy-MM-dd HH:mm:ss'
```

No matter what methods you set it up in, we can see that this feature consists of three option types:

* reset mode
* reset time
* reset time format (only required for CUSTOM type)

## Reset Mode

Support those modes:

* NEVER:&#x20;
* TIMER: It will reset after the time you specify, for example, after 5 hours.
* TIMED: It will be reset at the corresponding time, such as 8:15 pm.
* COOLDOWN\_TIMER (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* COOLDOWN\_TIMED (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* RANDOM\_PLACEHOLDER: Synchronize with the reset time of the specified random placeholder. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>
* CUSTOM: Directly enter the reset time in reset time, and the plugin will not perform any calculations. Recommend obtain reset time through the Placeholder API results. You need set time format at `reset-time-format` type option to helps us know how does your PlaceholderAPI results be like. (Added in 3.3.0) <mark style="color:red;">**- Premium**</mark>

## Difference between COOLDOWN\_TIMED (or COOLDOWN\_TIMER) and TIMED (or TIMER)

`TIMED` and `TIMER` will start generating reset time after each buy or sell until the player reaches the limit, while `COOLDOWN_TIMED` and `COOLDOWN_TIMER` will start generating reset time after the first buy or sell and will never update the reset time until the reset time reached.

For this reason, when using `COOLDOWN_TIMED` or `COOLDOWN_TIMER` mode, the reset time will not automatically adjust due to server restarts, configuration modifications, or other reasons. This means that if you mistakenly set the product to refresh after 1 year, the reset time will not automatically change due to your correction, but `TIMED` or `TIMER` rules can do this.

## Reset Time

Different reset modes require different values to be filled in here. Supports placeholders, <mark style="color:red;">**the placeholder used here must be on the server side, which means that all players receive the same value.**</mark>

### NEVER

Don't need anything here.

### TIMER/COOLDOWN\_TIMER

You can enter 3 to 5 numbers here, separated by a `:` symbol between each number. For example: `15:00:00`.

Each number from **right** to **left** represents:

* Seconds
* Minutes
* Hours
* Days <mark style="color:red;">**- Premium**</mark>
* Months <mark style="color:red;">**- Premium**</mark>

In this example, represents 15 hours later. Which means: **if now time is 2023-09-04 12:00:00. Will reset after 15 hours, which means 2023-09-05 03:00:00.**

### TIMED/COOLDOWN\_TIMED

The composition of TIMED and TIMER is almost identical, but the first three digits from the right-hand side represent the time of day. Let's also take 15:00:00 as an example:

If now time is 2023-09-04 12:00:00, will reset at 2023-09-04 15:00:00.

This is the result obtained with days set to 0. If you set it to 1, we will add another day, and that's it.

It is worth noting that if you want to do a daily store, days should be set to 0, and if you want to do a weekly store, days should be set to 6. Because you need to reset the number of times on the last day, not on the second day after the last day, right?

### CUSTOM <mark style="color:red;">**- Premium**</mark>

You only need to enter a Placeholder API placeholder here, and the result of the placeholder must include the complete year, month, day, hour, minute, and second. You also need to enter their format in the reset time format option, because different types of placeholders return different time formats, making it difficult for plugins to achieve uniformity.&#x20;

### RANDOM\_PLACEHOLDER <mark style="color:red;">**- Premium**</mark>

Enter a valid random placeholder ID here.

## Dynamic Reset Time <mark style="color:red;">**- Premium**</mark>

This example uses a random placeholder to randomly refresh products after 3, 4, or 5 hours, instead of a fixed time refresh.

Created a random placeholder like:

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

Use this placeholder at `buy-times-reset-time` option.

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

## Reset Time do not correct?

* The product must have been purchased or selled once before the next reset time can be stored. Otherwise, we can only display the possible reset time calculated based on the current time after the transaction is completed.

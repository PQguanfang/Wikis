# ⛓️Conditional Placeholder - Premium

We added `{conditional}` built-in placeholder in plugin.

## Config

All random placeholder configs are stored in `conditional_placeholders` folder. The file name is it's ID, for example: `buy.yml` means it's ID is `buy`. An example of it's config is like below:

```yaml
mode: MAX

value:
  default: 1
  vip: 1.5
  mvp: 2

conditions:
  vip:
    1:
      type: permission
      permission: 'group.vip'
  mvp:
    1:
      type: permission
      permission: 'group.mvp'
```

* mode: The type of conditional placeholder.
  * DEFAULT: The basic mode checks whether the player meets the corresponding conditions from top to bottom, and if they do, the corresponding value will be immediately returned.
  * MAX: Require all values of the placeholder to be numbers, and the maximum value that meets the condition will be returned.
  * MIN: Similar to MAX, but min value will be returned.
* conditions: The condition of each value. Each condition id section should use [Condition Format](../format/condition-format.md).
* value: The value of each condition. A option called `default` is the value returned that if no condition meet.

## Use Placeholder

Use `{conditional_<ID>}` placeholder to display it's value. For more info, please view [Placeholders](built-in-placeholder.md) page. For example: `{conditional_buy}`

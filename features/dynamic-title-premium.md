# 🌈Dynamic Title - Premium

## Requirements

* Require packetevents plugin installed in your server.
* Only Paper and it's fork supported.
* Only test on 1.21.8 version, other version may supported.

## Click Update

Set `menu.title-update.enabled` option value to `true` in `config.yml` file. After enable, after each click button in menu, the title will be updated, very useful for display placeholder in title and then auto update value fater each click.

```yaml
  # PREMIUM version only
  title-update:
    enabled: true # <--- Set to true
    black-dynamic-title: true
    resend-items-pack: false
```

## Item Flashing

The Minecraft client itself does not support changing the title of a container after opening it, so you will see items flashing and quickly reappearing, which cannot be solved. You can try enable `menu.title-update.resend-items-pack` value to `true` in `config.yml` file. This will only slightly alleviate the situation.

## Animation&#x20;

You can set animation by setting dynamic title in menu configs, support Java menu only.

```yaml
title: 'Items Shop %localtime_time%' #<--- Old
dynamic-title: # <--- New dynamic title
  enabled: true
  titles:
    - "§aUltimateShop §7| §f欢迎来到 §e服务器商店§f!"
    - "§bUltimateShop §7| §f欢迎来到 §e服务器商店§f!"
    - "§dUltimateShop §7| §f欢迎来到 §e服务器商店§f!"
  interval: 45
```

All menu configs support add this section, before use this, you need set `menu.title-update.enabled` option value to `true` in `config.yml` file. If necessary, please set the value of the `menu.title-update.black-dynamic-title` option to `true` in `config.yml` file. This feature may also cause items flashing. By increasing the interval slightly and using the resend items pack, the situation may be slightly better.

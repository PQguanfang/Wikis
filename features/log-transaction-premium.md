# 💳Log Transaction - Premium

Open `config.yml` and find below contents:

```yaml
log-transaction:
  enabled: true
  # If set to empty value, we will just print the log into console.
  file: ''
  format: '{player} | {shop} | {buy-or-sell} | {item-name}x{amount} | {price}'
```

* If you set `file` option to empty, we will just print the log into console. Otherwise, we will log into the file you put here. The file must be a txt file.

## Format available placeholders:

* {player}
* {player-uuid}
* {item} - Product ID
* {item-name} - Product Display Name
* {shop} - Shop ID
* {shop-name} - Shop Display Name
* {buy-or-sell}
* {price}
* {time} - Display the log time

## Showcase

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

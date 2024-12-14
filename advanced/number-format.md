# Number Format

* Download PlaceholderAPI and **Formatter** expansion with command `/papi ecloud download Formatter`. Click [here](https://github.com/PlaceholderAPI/PlaceholderAPI/wiki/Placeholders#formatter) to know more.
* Edit product price placeholder option with this placeholder: `%formatter_number_format_{amount}%`.

Example:

```yaml
  C:
    price-mode: CLASSIC_ALL
    product-mode: CLASSIC_ALL
    products:
      1:
        material: potato
        amount: 1
    buy-prices:
      1:
        economy-plugin: Vault
        amount: 20000000
        placeholder: '&6%formatter_number_format_{amount}% Coins'
        start-apply: 0  
```

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

* Start from **2.3.2**, you can just use those options in config.yml to let plugin help you change `{amount}` placeholder instead of you change it manually!

```yaml
placeholder:
  auto-settings:
    # If enabled, we will try change {amount} in price placeholder option to the value you set here.
    change-amount-in-all-price-placeholder:
      enabled: true # <--- Change this to true
      replace-value: '%formatter_number_format_{amount}%' # <--- Change to same as here
```

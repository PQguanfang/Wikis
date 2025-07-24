# ⚡Course 1

The menu and store feature in the plugin are separate, and their configurations are stored in the menus folder and shops folder respectively.

* To know more info about menu feature, please read the **Menus** chapter.
* To know more info about menu feature, please read the **Shops** chapter.
* To know more info about the effect of other folder, please read the [Configuration files](../info/configuration-files.md) page.

The following is a sample configuration file for a shop:

```yaml
settings:
  menu: 'example-shop-menu'
  buy-more: true
  shop-name: 'Blocks Shop'
  hide-message: false

items:
  A:
    # ...
  B:
    # ...
  C:
    # ...
```

In there you’ll find the `settings.menu` option, which is crucial because it’s the central hub that connects your shop and menu. In this example, we set it to `example-shop-menu`.

You should be find the menu file at the `menus` folder, it will called `example-shop-menu.yml`.

<pre class="language-yaml"><code class="lang-yaml">title: '{shop-name}'
size: 54

layout:
  - '000000000'
  - '0ABCDEFG0'
  - '0HIJKLMN0'
  - '0OPQRSTU0'
  - '000000000'
  - 'a0003000b'

buttons:
<strong>  # ...
</strong></code></pre>

Among them, the `layout` option is crucial, as it determines where your products or buttons will be displayed. You will find that it consists of **6x9** characters, with each character corresponding to a slot in the Minecraft chest inventory. The characters entered in the corresponding position represent the items or buttons with the corresponding ID that we will display.

In this example:

* Actually, since there is no product or button with an ID of `0`, nothing will be displayed in the slot with a character of 0.
* If the shop using this menu has products with IDs A, B, C, D, etc., the corresponding products will be displayed in the corresponding slots.
* The same goes for buttons. I forgot to tell you that you can set custom buttons not only in the menu configuration file, but also in the shop configuration file.
* If you change the value of the `size` option, don't forget to remove the extra lines in the `layout` option. For example, if you set the value of the size option to 36, then the character composition of the layout option is 4x9.

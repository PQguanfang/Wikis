# ✅Requirements

## Java Version

* Basic Requirement: **Java9+**
* **Java 17+** is <mark style="color:red;">recommended</mark>. Java17 and above versions are recommended, but plugins are compiled using **Java9**, so theoretically, you only need Java9 or higher versions.

## Server Software

* **Paper** and its downstream forks are <mark style="color:red;">recommended</mark>. When the plugin detects that your server software is Paper, it will enable some features that are only available in Paper, some of which can provide subtle performance improvements. Meanwhile, you can also choose whether to use these Paper only features in the `paper-api` section of the `config.yml` file. The Spigot server can theoretically also be used.
* **Folia** server also supported. Please note: Folia's support is in the <mark style="color:red;">early testing stage</mark> and may be released in official versions or removed in the future. This support is not a guarantee.

## Server Version

* The plugin theoretically supports any version between **1.14** and **1.21.5**.
* Obviously, supporting so many versions is not an easy task. It is impossible for the author to test all versions between 1.14 and 1.21.5 every time the plugin is updated. If you encounter errors while using a certain version, <mark style="color:red;">please join our Discord feedback</mark>.

## An economy plugin if you want to use custom currency

* **UltimateShop** is just a shop plugin and does not provide custom economy functionality. If you need a custom economy as your server economy, please find a suitable economy plugin yourself. **Vault** is not an economy plugin, it is just a dependency plugin for many economy plugins. <mark style="color:red;">After installing Vault on the server, it is also necessary to install the economy plugins that support it</mark>.

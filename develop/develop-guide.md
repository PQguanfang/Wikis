# Develop Guide

#### Get shop object <a href="#user-content-get-shop-object" id="user-content-get-shop-object"></a>

```java
ConfigManager.configmanager.shopConfigs.get(shopID);
```

#### Get product object <a href="#user-content-get-product-object" id="user-content-get-product-object"></a>

```java
ObjectShop shop = ConfigManager.configmanager.shopConfigs.get(shopID);
if (shop == null) {
  return;
}
ObjectItem item = shop.getProduct("TEST");
List<ObjectItem> items = shop.getProductList();
```

#### Stat buy a product <a href="#user-content-stat-buy-a-product" id="user-content-stat-buy-a-product"></a>

```java
BuyProductMethod.startBuy(Inventory inventory, String shop, String product, Player player, boolean quick, boolean test, int multi);
```

* inventory is Bukkit inventory object, for player's inventory, use player.getInventory() method.
* shop is shop ID.
* product is product ID.
* quick is whether send message after buy (will still send if you enable send-message-after-buy option in config.yml)
* test is whether take money or items from player, set it to true if you just want to know whether player has enough money or items.
* multi is buy amount in one time, default set to 1.

#### Start sell a product <a href="#user-content-start-sell-a-product" id="user-content-start-sell-a-product"></a>

```java
SellProductMethod.startSell(Inventory inventory, String shop, String product, Player player, boolean quick, boolean test, boolean ableMaxSell, int multi);
```

* ableMaxSell is whether if player don't have enough money or items for now multi(amount) value, we will try to get max amount that player able to sell. Use for sell all command.

**Get player cache object**

<pre class="language-java"><code class="lang-java"><strong>CacheManager.cacheManager.playerCacheMap.get(player);
</strong></code></pre>

Can get player's buy times, sell times data and so on.

**Get server cache object**

```java
CacheManager.cacheManager.serverCache;
```

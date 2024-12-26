# 💾Saved Item

## Save your item

You can use command `/shop saveitem <saveItemID>` command to save your hold item. There are 2 methods to save item.

* Bukkit: Use BukkitAPI's method to save item. The method only support saving vanilla data and persistent data stored through BukkitAPI, and other custom NBT data from other plugins will not be saved.
* Paper: Use PaperAPI's method to save item, this new method can 100% save item data, no data will lose. **(Paper and 1.15+ server only)**

If you are Paper server users and don't want to use new Paper method one, you need open `config.yml` file and edit the `paper-api.save-item` option to `false`, then we will still use Bukkit method save item even you are running Paper servers.

## Use saved item

You can use saved item in [ItemFormat](../format/itemformat-tm.md). In ItemFormat, there is a option called `material`, by default, you need type vanilla item ID there, but, you can also use saved item id to let plugin directly get the saved item instead of generate a whole new item with that type.

```yaml
display-item:
  material: superior_sword # If saved item id is 'superior_sword'
```

Saved items will be cached in memory continuously after loading to avoid repeatedly reading the saved item file, which may consume too much server performance. However, the cost is that if you have too many saved items, it may correspondingly consume more memory.

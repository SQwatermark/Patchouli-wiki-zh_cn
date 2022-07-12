# ItemStack 字符串格式

在手册中的多个地方，你会看到用 "ItemStack Strings" 填写的值。简而言之，一个 ItemStack String 是可以在游戏中解析成一个 itemstack 实例的文本。这个页面概括了它们的格式。

## 格式

下列格式都是允许的：

- **namespace:path** (e.g. `"minecraft:sword"`)
- **namespace:path#count** (e.g. `"minecraft:stone#64"`)
- **namespace:path{nbt}** (e.g. `"minecraft:diamond_pickaxe{display:{Lore:['A really cool pickaxe']}"`
- **namespace:path#count{nbt}**

要表示包含文本的 NBT 标签，你可以将所有双引号 (`"`) 替换成单引号 (`'`)，或者将其转义 (`\"`)。如果你想写一个单引号，你得转义两次 (`\\'`)

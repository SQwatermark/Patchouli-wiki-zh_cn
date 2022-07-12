# 类别 JSON 格式

这个页面详细列出了类别（Category）json 文件中可以包含的所有键。

因为其不是一个格式键（format key），有必要指出类别的 "category ID" 是相对于 `/en_us/categories` 的路径。所以如果你的类别文件是 `/en_us/categories/misc/cool_stuff.json`，ID 就会是 `patchouli:misc/cool_stuff`。

For modders, the domain used is the domain in which the book is defined.

- **name**（字符串，*必需*）

类别的名字。

- **description**（字符串，*必需*）

类别的简介。它会显示在类别的主页面，可以被[格式化](/docs/patchouli-basics/text-formatting)。

- **icon**（字符串，*必需*）

类别的图标。如果你想用一个物品作为图标，可以填写一个 [ItemStack 字符串](/docs/patchouli-advanced/itemstack-format)，也可以填写一个指向正方形图片的资源路径。如果你想要使用一个资源路径，确保图片的后缀为 `.png`。

- **parent**（字符串）

这个类别的父级类别。如果这是一个子类别，只需要写上父级类别的名字（译注：指 ID），如果不是，不要定义此项。This should be fully-qualified and of the form `domain:name` where `domain` is the same as the domain of your Book ID.

- **flag**（字符串）

一个用于判定类别是否应该存在的配置标记表达式（config flag expression）。阅读[使用配置标记](/docs/patchouli-basics/config-gating)获取更多有关信息。

- **sortnum**（字符串）

此类别的排序等级（sorting number）。默认值为0。类别在主页按照排序等级从低到高的顺序排列，所以如果你为每个类别指定了此项，你可以排出它们显示的次序。（译注：排序等级相同时，按照字母顺序排列）

- **secret**（布尔值）

默认为 false。将其设置为 true 可使其成为一个隐藏类别。隐藏类别在锁定时不会显示一个锁定图标，而是在解锁前什么都不显示。

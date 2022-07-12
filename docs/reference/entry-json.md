# 章节 JSON 格式

这个页面详细说明了你可以在章节（entry）的 json 文件中使用的键（key）。

虽然 "entry ID" 不是一个键，但是它是从 `/en_us/entries` 下找到这个章节的必要路径。所以如果你的章节在 `/en_us/entries/misc/cool_stuff.json` 中，它的 ID 就是 `patchouli:misc/cool_stuff`。

For modders, the domain used is the domain in which the book is defined.

- **name**（字符串，*必需*）

章节的名字。

- **category**（字符串，*必需*）

章节所属的类别。必需为你的类别（category） ID 之一。

The category this entry belongs to. This must be set to one of your categories' ID. For
best results, use a fully-qualified ID that includes your book namespace
`yourbooknamespace:categoryname`. In the future this will be enforced.

- **icon**（字符串，*必需*）

章节的图标。如果你想要一个物品作为图标，这可以是一个[ItemStack 字符串](https://github.com/SQwatermark/Patchouli-wiki-zh_cn/wiki/ItemStack字符串格式)，也可以是一个指向方块材质的资源路径。如果你想要使用资源路径，确保以 .png 结尾。

- **pages**（对象数组，*必需*）

表示这个章节的页面的数组。按照以下格式：

```
[
    {
        "type": "TYPE",
        (type specific data ...)
    },
    {
        "type": "TYPE",
        (type specific data...)
    }
    (...)
]
```

阅读[默认页面类型](/docs/patchouli-basics/page-types)了解 Patchouli 提供的页面类型以及其需要的数据，或者阅读[使用模板](/docs/patchouli-basics/templates)了解如何创建自己的页面类型。

- **advancement**（字符串）

用于锁定这个章节的进度（advancement）的名字。阅读[用进度锁定内容](/docs/patchouli-basics/advancement-locking)获取更多关于锁定内容的信息。

- **flag**（字符串）

一个用于判定章节是否存在的配置标记表达式（config flag expression）。阅读[使用配置标记](/docs/patchouli-basics/config-gating)获取更多有关信息。

- **priority**（布尔值）

默认为 false。如果设置为 true，章节将会显示一个斜体的标题，并且总会显示在类别顶端。用于你想要显示在最上方的确实重要的章节。

- **secret**（布尔值）

默认为 false。如果设置为 true，将会使这个章节变成一个隐藏（secret）章节。隐藏章节不会在被锁定时显示为 "Locked"，直到其被解锁前，都不会显示任何信息。隐藏章节不计入手册的阅读进度，当其被解锁时将会在工具提示（tooltip）中显示附加行。

- **read_by_default**（布尔值）

默认为 false。如果你不想让这个章节显示在未读时显示未读标记（"(!!)"），将其设置为 true。

- **sortnum**（整数）

这个章节的排序等级（sorting number）。默认值为0，拥有相同排序等级的章节会按照字母顺序排列，拥有不同排序等级的章节将按照排序等级从低到高的顺序排列。"priority" 设为 true 的章节总会显示在最上方。

建议你不要使用此项，因为打乱字母顺序可能会让事情变得迷惑，仅将此保留为一个可选项。

- **turnin**（字符串）

为了 "完成（complete）" 这个章节，玩家需要完成的进度的 ID。直到进度完成前，章节将会显示在列表顶端，附带一个 (?) 图标。这可以用作一个任务系统，或者只是帮助指引玩家了解游戏进程。

- **extra_recipe_mappings**（对象，字符串 ->整数）

章节的页面介绍的物品列表，用于在游戏中右键快速查找。键是 ItemStack 字符串，值是从 0 开始计数的页码。

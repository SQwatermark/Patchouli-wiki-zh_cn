# 用配置标记控制内容

配置标记（Config Flags）是一个允许基于配置和游戏环境动态地热交换手册中的内容的系统。在 Patchouli 手册的 json 文件的一些地方，你可以找到 "flag" 标签，可以用一个配置标记表达式（config flag expression）填写。

标记（flags）是布尔值（true 或 false），表达式可以是一些标记连接起来形成的一个语句。通常情况下，你不需要自己编写表达式，只需要写标记本身。如果你没有写标记的名字，这一项就不会被设置，默认值为 false。

如果其被赋予了一个标记表达式并且其值为 false，任意内容（包括类别、章节、页面，甚至是模板组件）都会被禁用。

## 默认标记

* **debug**：当游戏在 IDE Debug 模式加载时，此项为 true
* **advancements_disabled**：当帕秋莉手册配置文件中的 "Disable Advancement Locking" 选项为 true 时，此项为 true
* **testing_mode**：当帕秋莉手册配置文件中的 "Testing Mode" 选项为 true时，此项为 true
* **mod:MODID**：当某个 ID 的模组在游戏中被加载时，此项为 true（e.g. "mod:quark" 会在 Quark 模组被加载时设置为 true）

## 标记表达式

* `!flag`：当 flag 为 false 时为 true（非）
* `&flag1,flag2,flag3...`：当 flag1, flag2, flag3... 都为 true 时为 true（与）
* `|flag2,flag2,flag3...`：当 flag1, flag2, flag3... 至少有一个为 true 时为 true（或）

## 添加你自己的标记

相比整合包作者，这个系统更适合模组作者，因为其允许他们基于自己的配置需求动态地改变手册内容。这可以通过 [Patchouli API](https://github.com/Vazkii/Patchouli/tree/master/src/main/java/vazkii/patchouli/api) 的钩子实现。

# 用进度控制内容

可以在特定进度达成前锁定帕秋莉手册的一些章节。这个页面将会初步介绍实现方式。

- 首先，创建你的进度。如果你是模组作者，用你通常会用的方法制作（[Minecraft Wiki reference](https://minecraft.gamepedia.com/Advancements)），并将其放在 `/data/MODID/advancements` 文件夹下。如果你是整合包作者，你需要使用其他模组读取进度，例如 [OpenLoader](https://www.curseforge.com/minecraft/mc-mods/open-loader)。
- 进度做好后，复制它的 ID（按照 namespace:path 格式）。为了方便演示，我们假定 ID 是 "mymod:myadv"。
- 打开章节的 JSON 文件，用 ID `"advancement": "mymod:myadv"` 填写 `"advancement"` 字段。
  - 阅读[章节 JSON 格式](https://github.com/SQwatermark/Patchouli-wiki-zh_cn/wiki/章节JSON格式)获取更多信息。
- （Patchouli 1.15.2-1.2-28 之后的版本不需要这一步）打开 book.json 文件。
  - 如果 "advancement_namespaces" 数组还不存在，创建它：`"advancement_namespaces": []`
  - 将命名空间添加到 "advancement_namespaces" 数组：`"advancement_namespaces": [ "mymod" ]`
  - 添加命名空间告诉帕秋莉手册需要跟踪对应命名空间的进度。每个命名空间只需要写一次。如果你有多手册，只要一个手册中指定就可以了，但最好还是在所有手册中指定。
  - 在 Patchouli 1.15.2-1.2-28 版本之后，这不再必要，所有进度都可以直接用于锁定内容。
  - 阅读[手册 JSON 格式](https://github.com/SQwatermark/Patchouli-wiki-zh_cn/wiki/手册JSON格式)获取更多信息。
- 你还可以用进度锁定单独的页面。这是允许的但是并不鼓励这么做，因为如果你没能合适地表达信息，这可能会让玩家困惑。
  - 要锁定一个页面，只需要在页面的 `"type"` 字段旁填写 `"advancement"` 字段，和锁定章节的方法是一样的。
  - 锁定的页面不会显示任何 "锁定（locked）" 标志，它们仅仅是完全隐藏了。
  - 阅读[默认页面类型](/docs/patchouli-basics/page-types)获取更多信息。
- 最后一些要点：
  - 所有进度的锁定都可以被玩家在配置文件中禁用。
  - 除非其中至少有一个未锁定的章节，否则章节将被锁定。（译注：大概是指在其中有章节被解锁前，类别会被锁定。原文为：Entries show up locked unless there's at least one unlocked entry within them.）
  - 你可以通过不在进度的 JSON 文件中包含 `"display"` 块制作隐藏的进度，如果你想要制作许多锁定页面，但是不想要一个凌乱的界面，这会很有用。

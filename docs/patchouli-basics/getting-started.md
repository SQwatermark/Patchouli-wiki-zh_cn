---
sidebar_position: 1
---

# 入门

这篇文章是一个快速入门指南，告诉你如何着手制作自己的 Patchouli 手册，仔细阅读，并跟着做吧！

### 0. 安装 Patchouli
很明显，如果你是模组作者，可以作为 mod 项目的一个库加载它，或者仅仅把它丢进工作空间的 mods 文件夹。推荐使用 maven，你可以在仓库的 readme 中找到地址。如果你不是模组作者，可以通过正常的发布渠道（例如 curseforge）获取模组。

### 1. 定位 patchouli_books 文件夹
所有手册和它们的内容都将会放在 `patchouli_books` 文件夹下，所有你应该找到这个文件夹的位置。

* 对于整合包作者，它会在 Minecraft 实例文件夹下（在 mods, config 诸如此类的文件夹旁边）。注意，你需要在安装 patchouli 的情况下运行一次游戏，这个文件夹才会出现（或者你自己直接新建一个）。
* 对于模组作者，路径是 `/data/modid/patchouli_books`（译注：对于1.12版本，路径是 `/assets/modid/patchouli_books`），你必须手动创建此文件夹。

### 2. 建立文件夹结构
找到了 `patchouli_books` 文件夹，就要为你的手册取一个名字了。只允许使用英文小写字母和下划线。这是个内部标识名，我们建议尽量取个特殊点的名字。For mods, you should name it after what the book is for
(e.g. `lexicon` for Botania). For modpacks, name it something with your modpack's name,
for example `crucial_2_guide_book`. 等你想好名字，在 patchouli_books 文件夹下按照如下层次创建文件夹和文件：

* `patchouli_books`
    * `<你先前决定的名字>` （文件夹）
        * `book.json` （空文件）
        * `en_us` （文件夹）
            * `entries` （空文件夹）
            * `categories` （空文件夹）
            * `templates` （空文件夹）

即便是在同一个模组（或整合包）中，你也可以写很多本手册。每本手册都有一个[命名空间ID](https://minecraft.fandom.com/zh/wiki/%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4ID)。如果手册是模组的一部分，命名空间是模组的 ID。如果手册位于外部的 `patchouli_books` 文件夹下，命名空间是 `patchouli`。命名空间ID的名称部分是你之前取的名字。

注意创建一个 `en_us` 文件夹意味着你在为你的手册制作英语版本。放在 `en_us` 文件夹下的内容永远都是 "主要" 读取的文件，所以即便你不打算用英语写这本手册，你也应该把主要的东西放在这里。（译注：`en_us` 文件夹下的文件内容可以胡乱写，但是它得有。你用中文写一个页面，但是 `en_us` 下没有对应的文件，这个页面是不会被读取的。如果不打算做英文版的话也可以直接在 `en_us` 下用中文写）

任何翻译者都可以创建他们的语言的文件夹并在其中重写任何他们希望翻译的文件。当游戏语言改变时，这些文件会被自动读取。如果你是翻译者，请不要在你的语言的文件夹下写任何原文没有的页面。（译注：因为不会被读取）

### 3. 填写 book.json
用你喜欢的文本编辑器打开 book.json 文件，并按照下面的格式填写：

```json
{
	"name": "BOOK NAME",
	"landing_text": "LANDING TEXT",
	"version": 1
}
```

"BOOK NAME" 是手册将会显示的名字，"LANDING TEXT" 是将显示在手册左侧页面中的文字。`version` 字段声明了手册的版本。每当你更新手册时，也应该更新版本号。如果你是模组作者，可以在 `name` 和 `landing_text` 中使用本地化键。

参考：

![](https://i.imgur.com/lsdDrrk.png)

有关更多自定义选项，请阅读[手册 JSON 格式](/docs/reference/book-json)。（非常推荐！）

### 4. 在游戏内检查
加载游戏，检查你的手册在不在游戏中。除非你自己指定了一个物品栏，否则它应该在杂项物品栏中，你也可以在搜索栏中搜索。

如果你没找到，检查 patchouli 是否正常加载了，运行日志（log）中是否有报错。

这之后的一切都可以在不关闭游戏的情况下热重载，所以进一步编辑时可以放心地开着游戏。（译注：如果你是模组作者，可以先放在模组外的文件夹中方便热重载）

### 5. 添加子内容
现在可以往你的手册中添加内容了。打开 `en_us` 文件夹，在其中创建如下文件夹和文件：

- en_us
  - entries (文件夹)
    - test (文件夹)
      - test_entry.json (空文件)
  - categories (文件夹)
    - test_category.json (空文件)
  - templates (空文件夹)

打开 `test_entry.json` 和 `test_category.json` 并填写如下的内容：

```json title="test_entry.json"
{
    "name": "Test Entry",
    "icon": "minecraft:writable_book",
    "category": "yourbooknamespace:test_category",
    "pages": [
        {
            "type": "patchouli:text",
            "text": "This is a test entry, but it should show up!"
        }
    ]
}
```

```json title="test_category.json"
{
	"name": "Test Category",
	"description": "This is a test category for testing!",
	"icon": "minecraft:writable_book"
}
```

You'll need to edit the "category" key in the test entry. If you are a modder, "yourbooknamespace:test_category" should be replaced with the namespace for your mod (with test_category tacked on, of course). If you're just making a modpack, it should be replaced with "patchouli:test_category"

保存文件，然后返回游戏打开手册。按住 shift 键点击左下角的铅笔图标。这么做会重载手册内容，你会看到你刚才定义的类别和章节出现了。（译注：1. 如果类别下没有章节，该目录会被锁定。2. book.json 文件无法热重载）

### 6. 了解更多！

你已经完成了初始设置，现在可以学习更多可以用帕秋莉手册实现的东西了。查阅以下页面：

* [用进度锁定内容](/docs/patchouli-basics/advancement-locking)
* [文本样式 101](/docs/patchouli-basics/text-formatting)
* [手册 JSON 格式](/docs/reference/book-json)
* [类别 JSON 格式](/docs/reference/category-json)
* [章节 JSON 格式](/docs/reference/entry-json)
    * [默认页面类型](/docs/patchouli-basics/page-types)
* [使用模板](/docs/patchouli-basics/templates)

### 7. 使用手册物品

下面是一些使用手册物品的例子。请用手册的 ID（包含 book.json 的文件夹的名字）替换 `YOURBOOKID` 。如果文件夹叫 "coolbook"，那么 ID 是：

- `patchouli:coolbook` （如果你是整合包作者）
- `YOURMODID:coolbook` （如果你是模组作者）

**CraftTweaker**：`<patchouli:guide_book>.withTag({"patchouli:book": "YOURBOOKID"});`
或者用 `/ct hand`

**原版合成表/进度**：

```json
"item": "patchouli:guide_book",
"nbt": {
    "patchouli:book": "YOURBOOKID"
}
```

### 8. 一些要点

* 对于整合包作者来说，如果你想要使用自定义的图片、材质、声音或其他资源，你需要一个工具来加载它们，例如 [Resource Loader](https://minecraft.curseforge.com/projects/resource-loader)。
* To grant your book to new players automatically, see [this page](/docs/patchouli-basics/giving-new)
* 如果要重载 book.json 文件，你需要重启游戏，但是重载手册的内容不需要重启游戏。
* 手册的内容完全是客户端的，然而 book.json 文件还会被服务端读取。
* 你不需要将章节放在命名为其所属类别的文件夹下，这样做只是便于管理！
* 如果你是模组作者 ，不需要添加任何依赖，甚至不需要添加任何代码。帕秋莉手册会自行在资源（assets）文件夹下寻找文件。

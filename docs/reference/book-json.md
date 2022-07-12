# 手册 JSON 格式

这个页面详细介绍了你可以在 book.json 文件中设置的每一个键。

- **name**（字符串，*必需*）

手册物品和 GUI 中显示的手册名。对于模组作者来说，可以是一个本地化键。

- **landing_text**（字符串，*必需*）

将会显示在手册的扉页上的文本。可以[使用样式](/docs/patchouli-basics/text-formatting)。对于模组作者来说，可以是一个本地化键。

- **advancement_namespaces**（字符串数组）

**在 Patchouli 1.15.2-1.2-28 版本后，这个字段没用了，任何进度都可以用于锁定内容。**

用于锁定章节的进度的命名空间。任何要使用的命名空间都应该在这里声明，使帕秋莉手册知道去跟踪并监听它们来解锁手册内容。例如，如果你在一个章节中使用了 "yourmod:cooladvancement"，你需要在这个数组中添加 "yourmod"。查阅[用进度锁定内容](https://github.com/SQwatermark/Patchouli-wiki-zh_cn/wiki/用进度锁定内容)来获取更多有关信息。

不允许向数组中添加 "minecraft"，这是为了防止不必要的大量数据传输。

- **book_texture**（字符串）

手册的 GUI 的背景纹理。你可以使用任何资源路径（resource location），但是 *强烈建议* 你使用内置的纹理之一，以便于当新元素被添加时，你可以立刻更新。帕秋莉手册内置的纹理如下：

1. patchouli:textures/gui/book_blue.png
2. patchouli:textures/gui/book_brown.png（默认纹理）
3. patchouli:textures/gui/book_cyan.png
4. patchouli:textures/gui/book_gray.png
5. patchouli:textures/gui/book_green.png
6. patchouli:textures/gui/book_purple.png
7. patchouli:textures/gui/book_red.png

如果你想要使用自制纹理，你可以复制上述任何一个纹理并随意进行修改。

- **filler_texture**（字符串）

页面填充图案的纹理（章节页数为奇数时，最后一个空白页显示的方块图案）。如果你想在空白页显示别的内容，可以定义此项。

- **crafting_texture**（字符串）

合成表的纹理。如果你想修改合成表的背景图案，定义此项。虽然大多数情况下这么做不太值当，但是如果你想要显得又酷又时髦，你可以这么做。

- **model**（字符串）

手册物品的模型。这可以是任何你定义的基础物品模型。帕秋莉手册提供了一些可直接使用的模型：

1. patchouli:book_blue
2. patchouli:book_brown（默认值）
3. patchouli:book_cyan
4. patchouli:book_gray
5. patchouli:book_green
6. patchouli:book_purple
7. patchouli:book_red

模组作者请注意：不要使用上述任何模型。不同模组使用相同的基础材质是很糟糕的事情，为了便于区分，请自己做一个！上述模型是给整合包作者提供的。帕秋莉手册可以自动注册你传入的任何模型，所以你不必为它们敲任何代码。

An [item predicate](https://minecraft.fandom.com/wiki/Model#Item_predicates)
called `patchouli:completion` is provided for book models, whose value is equal to
the fraction of entries unlocked in the book, which allows book models to change their
display as they're more completed.

我们给手册模型提供了一个叫 `patchouli:completion` 的[物品谓词](https://minecraft.fandom.com/wiki/Model#Item_predicates)，它的值等于手册中解锁的章节的比例，这使得手册可以在解锁更多内容时改变模型。

- **text_color**（字符串）

普通文本的颜色，十六进制（"RRGGBB", 可不写#）。默认值为 "000000"。

- **header_color**（字符串）

页眉文本的颜色，十六进制（"RRGGBB", 可不写#）。默认值为 "333333"。

- **nameplate_color**（字符串）

扉页的手册的铭牌的文字颜色，十六进制（"RRGGBB", 可不写#）。默认值为 "FFDD00"。

- **link_color**（字符串）

链接文本的颜色，十六进制（"RRGGBB", 可不写#）。默认值为 "0000EE"。

- **link_hover_color**（字符串）

悬停链接文本的颜色，十六进制（"RRGGBB", 可不写#）。默认值为 "8800EE"。

- **progress_bar_color**（字符串）

进度进度条的颜色，十六进制（"RRGGBB", 可不写#）。默认值为 "FFFF55"。

- **progress_bar_background**（字符串）

进度进度条的背景颜色，十六进制（"RRGGBB", 可不写#）。默认值为 "DDDDDD"。

- **open_sound**（字符串）

手册开启时播放的音效。这是一个指向声音文件的资源路径（对于模组作者来说，需要正确注册）。

- **flip_sound**（字符串）

手册翻页时播放的音效。这是一个指向声音文件的资源路径（对于模组作者来说，需要正确注册）。

- **index_icon**（字符串）

手册的总目录显示的图标。如果你想用一个物品作为图标，可以填写一个 [ItemStack 字符串](/docs/patchouli-advanced/itemstack-format)，也可以填写一个指向正方形图片的资源路径。如果你想要使用一个资源路径，确保图片的后缀为 .png。这一项是可选的，如果你不想设置此项，默认值为此手册的图标（这也是推荐值）。

* **pamphlet**（字符串）

Available in Patchouli 1.18.2-68 or above.

Defaults to false. If true, marks this book as a [pamphlet](../patchouli-basics/pamphlets.md).

- **show_progress**（布尔值）

默认值为 true。即便启用了进度，将其设置为 false 可以禁用进度进度条。

- **version**（字符串）

手册的版本号（edition）。默认值为 "0"，将其设置为任何其它数值（这里用 X 表示）将会在手册的工具提示（tooltip）和扉页上显示 "X Edition"（例如，X 为 3 的时候，会显示 "3rd Edition"）。将其设置为 "0" 或者什么都不设置将会显示 "subtitle" 的值。如果值为非数字，会显示为 "编者版（Writer's Edition）"。

对于模组作者。这是一个可以用 gradle 填充的地方。你可以在这里写上类似于 ${book_version} 的文字并添加进你的构建脚本（build script）中。可以使用非数字的值，不会造成任何问题。

- **subtitle**（字符串）

手册的副标题，如果 "version" 被设置为 "0" 或什么都不设置，它将会显示在工具提示（tooltip）和扉页的手册名下方。

- **creative_tab**（字符串）

手册物品所在的物品栏。默认是杂项（Miscellaneous），你可以随意将其移动到其他物品栏。下面是原版物品栏的名字：

1. buildingBlocks
2. decorations
3. redstone
4. transportation
5. misc（默认值）
6. food
7. tools
8. combat
9. brewing

对于模组作者，只需要填写构造物品栏时填写的字符串即可。

For modders, simply put in the same string you use when constructing your creative tab here, and the book will show up there.
On Fabric, use the name of the `Identifier` you registered your tab with, but with the `:`
replaced with a `.`.

- **advancements_tab**（字符串）

手册关联的进度栏。如果设置了此项，扉页将会显示一个进度按钮，点击可以进入进度栏。

- **dont_generate_book**（布尔值）

默认值为 false。如果你不想让帕秋莉手册自动为你的手册生成一个物品，可将此项设置为 true。当且仅当你是模组作者且确实需要一个自定义的物品类时，可以设置此项。

- **custom_book_item**（字符串）

这是接着上一个键的，如果你确实有一个自定义的手册物品，在这里设置。需要填写一个 [ItemStack 字符串](/docs/patchouli-advanced/itemstack-format)。

- **show_toasts**（布尔值）

默认值为 true。如果你不想让你的手册在有新的可阅读的章节时显示滚动通知（toast），将此项设置为 false。

- **use_blocky_font**（布尔值）

默认值为 false。如果要使用原版像素字体（译注：ascii.png）而不是更细的字体（译注：unicode_page_xx.png），将这一项设置为true。如果你有一个字体 mod，无论怎么设置都会使用字体mod提供的字体。

- **i18n**（布尔值）

默认为 false。如果设置为 true，在渲染前将会尝试在语言文件中寻找类别、章节、页面标题以及页面的本地化键。

- **macros**（对象）

手册应该使用的样式宏（formatting macros）。阅读[文本样式 101](/docs/patchouli-basics/text-formatting)获取更多有关信息。

- **pause_game**（布尔值）

默认值为true。在单人游戏中打开手册GUI会暂停游戏。

* **text_overflow_mode** (`overflow`, `resize`, `truncate`)

Added in Patchouli 1.18.2-71

Allows the `textOverflow` config option to be customized per-book, controlling how text
pages that have overflowing contents are handled:

`overflow` lets the text run off the page, `truncate` discards all overflowed text, and `resize`
attempts to shrink the text to fit in the page.

### 拓展键

- **extend**（字符串）

用于将此手册定义为另个手册的拓展，拓展的手册不会创建手册物品，它们也并不实际 "存在"。它们的任务就是为另一本实际存在的手册添加更多内容。主要用于想要为其前置模组的手册添加更多内容附属模组。

这里的值就是你想要拓展的手册的 ID。以 `modid:path` 的格式，modid 是要拓展的手册所属的模组 ID，path是其所在的文件夹。例如，如果你想要拓展一本 "patchouli" 模组的手册，它在 `/data/patchouli/patchouli_books/coolbook/book.json`" 路径下，这里的值应该是 "`patchouli:coolbook`。(译注：path 理解成手册 json 文件的文件名就行了)

如果设置了此项，文件中的所有其他项都会被忽略。手册将会从其要拓展的手册中继承所有章节、类别、模板和宏，所以需要时请随意使用。

- **allow_extensions**（布尔值）

默认值为 true。如果你不愿意你的手册被其他手册拓展，将其设置为 false。

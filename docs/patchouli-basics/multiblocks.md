# 定义多方块结构

帕秋莉手册提供了一个系统，让你可以定义多方块结构（Multiblock），并在世界中将其可视化。这些多方块结构可以被模组作者用代码定义（使用 API）或在章节（entry）数据中用 JSON 文本定义。

这个页面写得像一个教程，以帮助你理解多方块结构的构成，因为写成一个正式的对象结构并不能清楚地表述如何去构造它。

这个页面集中阐述如何用 JSON 文本创建多方块结构，但是其原理也是适用于代码的。用代码制作多方块结构允许你用任意谓词创建方块状态匹配器，将多方块结构用于服务端的确认和放置（如果你将 Patchouli 作为必要的前置）。你可以查看 [Patchouli API](https://github.com/Vazkii/Patchouli/tree/master/src/main/java/vazkii/patchouli/api) 了解如何去做，或者看[此处](https://github.com/Vazkii/Patchouli/blob/master/Xplat/src/main/java/vazkii/patchouli/common/multiblock/MultiblockRegistry.java)的一个例子。

## Multiblock 格式

一个多方块结构（multiblock）由一个二维字符串数组（表示三维图案），和一个用以将图案中的字母映射到方块状态匹配器（state matchers）的映射表（mapping）构成。

我们将用下面这个东西作为创建多方块结构的示例：

![](https://i.imgur.com/M6Fw6nP.png)

一个多方块结构可以用一个 JSON 对象定义。首先让我们创建一个空对象。

```json
"multiblock": {

}
```

### 映射

首先考虑这里用了哪些方块。看看上面这张图片：

- 金块
- 红色陶瓦
- 品红色羊毛（在这个例子中我们要允许它是任意颜色的羊毛）
- 音符盒（音高为4）
- 空气
- 一些我们看不到的角落，但我们这样说：它们可以是任意方块。

一旦我们知道了这个结构使用了哪些方块，我们就为每种方块分配一个字符：

- **G**: 金块
- **B**: 音符盒 (note 4)
- **R**: 红色陶瓦
- **W**: 任意羊毛

帕秋莉手册模组已经提供了空气和 “任意方块” 对应的字符，分别是一个空格和下划线，所以我们不需要声明这两类方块。

现在，我们需要将数据转换成游戏程序可以识别的格式。帕秋莉手册使用原版逻辑来解析方块状态谓词（blockstate predicate），和 `/execute if block ~ ~ ~ <PREDICATE>` 相同。这意味着你可以使用方块 ID，标签（tags），和特定你想要限制的方块状态属性。所以，我们写成这样：

- **G**: minecraft:gold_block
- **B**: minecraft:note_block[note=4]
- **R**: minecraft:red_terracotta
- **W**: #minecraft:wool

看上去不错，让我们用一个 "mapping" 语句块把映射表放进 json 文件：

```json
"multiblock": {
    "mapping": {
         "G": "minecraft:gold_block",
         "B": "minecraft:note_block[note=4]",
         "R": "minecraft:red_terracotta",
         "W": "#minecraft:wool"
     }
}
```

### 图案

既然我们已经告诉了多方块结构要使用哪些方块，我们需要告诉它结构的形状。要做到这一点，我们要从上到下，一层一层，将每一层转换为一个字符串数组。

Terse explanation of the format: the pattern attribute is an array of array of strings. It
is indexed in the following order: y (top to bottom), x (west to east), then z (north to
south).

Full explanation:

让我们从有着用陶瓦组成的加号图案的第一层开始。它看上去是这样的：

```json
[
" GRG ",
"GGRGG",
"RRRRR",
"GGRGG",
" GRG "
]
```

G 是金块，R是红色陶瓦，空格表示空气。我们可以稍稍压缩这个数组让它看上去不是那么臃肿：

```json
[ " GRG ", "GGRGG", "RRRRR", "GGRGG", " GRG " ]
```

现在它看起来不是那么可读了，因为我们没有把它写成俯视图的样式，但是别担心，很快你就会觉得这很好。现在，我们把它放进 "pattern" 数组，然后继续添加接下来的所有层：

```json
"pattern": [
    [ " GRG ", "GGRGG", "RRRRR", "GGRGG", " GRG " ],
    [
        "GG GG",
        "G   G",
        "     ",
        "G   G",
        "GG GG"
    ],
    [
        "G   G",
        "     ",
        "     ",
        "     ",
        "G   G"
    ], 
    [
        "G   G",
        "     ",
        "     ",
        "     ",
        "G   G"
    ], 
    [
         "_WWW_",
         "WWWWW",
         "WWWWW",
         "WWWWW",
         "_WWW_"
    ]
]
```

......然后压缩它们：

```json
"pattern": [
    [ " GRG ", "GGRGG", "RRRRR", "GGRGG", " GRG " ], 
    [ "GG GG", "G   G", "     ", "G   G", "GG GG" ],
    [ "G   G", "     ", "     ", "     ", "G   G" ], 
    [ "G   G", "     ", "     ", "     ", "G   G" ], 
    [ "_WWW_", "WWWWW", "WWWWW", "WWWWW", "_WWW_" ]
]
```

看！我们现在有了结构的侧视图。还有一件事要做。我们需要告诉游戏结构的中心在哪。凭直觉来说可能是结构的几何中心，但是在某些情况下你可能有向外延伸的结构，导致中心并不是几何中心。

我们把图案中的的一个字符换成 0 来指定旋转中心。默认情况下 0 被映射到空气，但是如果你需要把它映射为别的东西，你可以在映射表中添加 "0" 的映射。

多方块结构的 "0" 将会位于放置方块时玩家的准星位置。换句话说，如果你要放置一个方块，它放置的位置就是 0 的位置。

知道了这一点，理想的 0 的位置是多方块的结构的几何中心，但是向下移动一个方块，使得它刚好在 W 上方：

```json
"pattern": [
    [ " GRG ", "GGRGG", "RRRRR", "GGRGG", " GRG " ], 
    [ "GG GG", "G   G", "     ", "G   G", "GG GG" ],
    [ "G   G", "     ", "     ", "     ", "G   G" ], 
    [ "G   G", "     ", "  0  ", "     ", "G   G" ], 
    [ "_WWW_", "WWWWW", "WWWWW", "WWWWW", "_WWW_" ]
]
```

### Extra Notes on the Pattern
Observe carefully that the pattern directions conform to programming conventions, not to the cardinal directions.
For example, to lay out stairs with their `facing` property set to the appropriate side of the multiblock, you would have to do this:
```
"pattern": [
  [
    " W ",
    "N S",
    " E "
  ]
],
"mapping": {
  "W": "minecraft:oak_stairs[facing=west]",
  "N": "minecraft:oak_stairs[facing=north]",
  "S": "minecraft:oak_stairs[facing=south]",
  "E": "minecraft:oak_stairs[facing=east]",
}
```
This is due to the fact that the inner array is indexed by x (later entries being further east), then the strings are indexed by z (later characters being further south).

### 一些额外的东西

多方块结构还可以有其他一些值：

- **symmetrical**（布尔值）

默认为 false。如果多方块结构中心对称的（如果旋转 90° 不会改变它的样子），将其设置为 true。这不是强制的，但如果你这样做，Patchouli 不会检查所有的旋转，所以性能会好一些。

- **offset**（长度为3的整数数组）

有三个值的整数数组 ([X, Y, Z]) 用于设置多方块结构相对于中心的偏移。

在我们的例子中，我们将会把 symmetrical 设置为 true，不设置 offset，因为我们已经将 0 放在了正确的位置。

### 把一切组合起来

让我们把图案（pattern）、映射（mapping）和其他值放在一起，我们得到了：

```json
"multiblock": {
    "pattern": [
        [ " GRG ", "GGRGG", "RRRRR", "GGRGG", " GRG " ], 
        [ "GG GG", "G   G", "     ", "G   G", "GG GG" ],
        [ "G   G", "     ", "     ", "     ", "G   G" ], 
        [ "G   G", "     ", "  0  ", "     ", "G   G" ], 
        [ "_WWW_", "WWWWW", "WWWWW", "WWWWW", "_WWW_" ]
    ],
    "mapping": {
        "G": "minecraft:gold_block",
        "W": "minecraft:wool",
        "R": "minecraft:stained_hardened_clay[color=red]"
    },
    "symmetrical": true
}
```

如果我们翻到一个 "multiblock" 页面（参阅[默认页面类型](/docs/patchouli-basics/page-types#multiblock-pages)），并点击可视化（Visualize），他将在游戏中显示！

![](https://i.imgur.com/1lfoaA1.png)

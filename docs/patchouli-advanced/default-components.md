# 默认的模板组件

这个页面详细说明了帕秋莉手册内置的各种模板组件。这些组件应该在模板的 "components" 数组中使用，在每个对象中用 "type" 键指定组件类型。你可以在[使用模板](/docs/patchouli-basics/templates)中了解更多信息。

下面几种属性在每种组件类型中都适用：

* **type** (String, _mandatory_)

What type this component is. This isn't used by the component itself, but rather by the
loader to determine what component should be loaded. For example, if you want a text
component, you set this to "patchouli:text". This should be fully-qualified and of the
form `domain:name` where `domain` is the same as the domain of your Book ID.

- **x**（整数）

组件在页面中的横坐标，默认值为 0。

- **y**（整数）

组件在页面中的纵坐标，默认值为 0。

- **advancement**（字符串）

一个指向进度的资源路径，组件将在进度达成之后出现。阅读[用进度锁定内容](/docs/patchouli-basics/advancement-locking)获取更多有关信息。不设置此属性或者填写空字符串都会让组件一直显示。

- **negate_advancement**（布尔值）

默认值为 false。如果设置为 true，*advancement* 字段会用于否定，组件会在进度未达成时显示。

- **guard**（字符串）

一个用于判定这个组件是否应该出现的[变量函数](/docs/patchouli-advanced/template-variable-usage#string-derivation)。如果函数得出 "false" 或空字符串，组件不会显示。

- **flag**（字符串）

一个用于判定这个组件是否应该出现的配置标记表达式（config flag expression）。阅读[使用配置标记](/docs/patchouli-basics/config-gating)了解更多有关信息。

- **group**（字符串）

仅供模组作者使用：这个组件属于的组。组仅用于允许[组件处理器](/docs/patchouli-advanced/component-processors)基于代码层面的情况隐藏个别组件。

## 示例用法

使用文本组件的示例：

```json
{
    "type": "patchouli:text",
    "text": "This is an example",
    "x": 20,
    "y": 30
}
```

## 文本组件

组件类型：**"patchouli:text"**

绘制一个文本框，支持[格式化](/docs/patchouli-basics/text-formatting)。

**属性：**

- **text**（字符串，*必需*）

要显示的文本，可以是变量。

- **color**（字符串）

文本的颜色，按照16进制格式（e.g. "FF0000" 表示纯红色）。如果未设置，默认值为手册的文本颜色。可以是一个变量。

- **max_width**（整数）

文本框中一行文字的最大宽度。如果未设置，默认为页面的完整宽度。

- **line_height**（整数）

每一行的高度。默认值为 9。如果设置了大于 9 的值，两行文字之间就会出现空隔。如果设置为更小的值，两行文字会出现重叠的部分，看起来很糟糕。

## 物品组件

组件类型：**"patchouli:item"**

绘制一个物品，当鼠标准星悬停在物品图标上时会看到它的工具提示，可以点击查看此物品的配方页（译注：参阅下方的 link_recipe 和 默认页面类型#聚焦页面#link_recipe）。

**属性：**

- **item**（字符串，*必需*）

一个用于表示你想要显示的物品的 [ItemStack 字符串](/docs/patchouli-advanced/itemstack-format)。可以是一个变量。

这个值有高级用法。你可以使用 `ore:ORENAME` 来显示所有匹配矿物词典键 ORENAME 的物品，你还可以用逗号将物品隔开来显示多个 itemStack（e.g. `minecraft:diamond,minecraft:emerald`）。在这两种情况下，物品都会轮流显示。

- **framed**（布尔值）

默认值为 false。如果设置为 true，将会在物品周围绘制一个小边框，和配方页的输出物品的边框相同。

- **link_recipe**（布尔值）

默认值为 false。设置为 true 可将使用了这个组件的页面标记为物品的 "配方页（recipe page）"。当查看其他显示了这个物品的页面时，你可以按下 shift 并单击物品跳转到此页面。

## 图片组件

组件类型：**"patchouli:image"**

绘制一张图片，或其一部分。

**属性：**

- **image**（字符串，*必需*）

一个指向一张图片的资源路径。可以是一个变量。**警告**：不要使用宽度和高度不是 2 的幂的图片，否则会导致错误。

- **width**（整数，*必需*）

用于绘制图片的区域的宽度。从左侧开始。

- **height**（整数，*必需*）

用于绘制图片的区域的高度。从顶部开始。

- **u**（整数）

从原图片的左侧第多少个像素开始绘制图片。如果你未设置此项，默认值为 0，从最左侧开始绘制。

- **v**（整数）

从原图片的顶部第多少个像素开始绘制图片。如果你未设置此项，默认值为 0，从最顶端开始绘制。

- **texture_width**（整数）

原图片的宽度。如果你未设置此项，默认值为 256。如果图片宽度不是256，你应该设置这个值，否则看起来会很怪异。

- **texture_height**（整数）

原图片的高度。如果你未设置此项，默认值为 256。如果图片高度不是256，你应该设置这个值，否则看起来会很怪异。

- **scale**（单精度浮点数）

图片的显示尺寸，默认值为 1。

## 页眉组件

组件类型：**"patchouli:header"**

绘制一个页眉文本，类似于类别和章节的标题文本。但是不包括出现在标题下方的分隔线（分隔线是另一个组件）。

**属性：**

- **text**（字符串，*必需*）

要显示的文本。它_不可以_ 被添加格式。可以是一个变量。

- **color**（字符串）

文本的颜色，按照16进制格式（e.g. "FF0000" 表示纯红）。如未设置，默认值为手册的页眉颜色。可以是一个变量。

- **centered**（布尔值）

默认值为 true，即居中显示。将其设置为 false 可将文本左对齐。

- **scale**（单精度浮点数）

页眉的尺寸。默认值为 1。

- 这个组件的 "x" 值可以被设置为 -1，这会默认为页面的水平中心。
- "y" 值也可以被设置为 -1，如果这么做，其默认位置和默认页面的页眉相同。

## 实体组件

组件类型：**"patchouli:entity"**

渲染一个来回旋转的实体。

**属性：**

- **entity**（字符串，*必需*）

实体的 ID。例如，要展示鸡应该使用 "minecraft:chicken"。你可以向实体附加 NBT 数据，方法和使用 [ItemStack 字符串](/docs/patchouli-advanced/itemstack-format)的方法相同。可以是一个变量。

- **render_size**（整数）

用于展示实体的画布的大小。默认值为 100，这表示实体会在一个 100x100 的方框中渲染。

- **rotate**（布尔值）

实体是否来回旋转，默认值 true。

- **default_rotation**（单精度浮点数）

实体的旋转角度。只有当 "rotate" 设置为 false 时这一项才生效。默认值 为 -45。

## 分隔线组件

组件类型：**"patchouli:separator"**

使用手册的材质绘制一条分隔线。

**此组件没有任何附加属性。**

- 这个组件的 "x" 值可以被设置为 -1，这会默认为页面的水平中心。
- "y" 值也可以被设置为 -1，如果这么做，其默认位置和默认页面的分隔线相同。

## 边框组件

组件类型：**"patchouli:frame"** 用手册的材质绘制一个 200x200 的边框。默认页面类型的图片的边框就是此边框。

**此组件没有任何附加属性。**

- 这个组件的 "x" 值可以被设置为 -1，这会默认为页面的水平中心。
- "y" 值也可以被设置为 -1，如果这么做，其默认位置和默认页面的边框相同。

## 工具提示组件

组件类型：**"patchouli:tooltip"** 当鼠标准星悬停在组件上时，让 GUI 渲染一个工具提示。

**属性：**

- **tooltip**（字符串数组，*必需*）

工具提示显示的字符串数组。数组中的每个字符串都可以是变量。空字符串和缺失值的变量都会被忽略。你可以用 & 而不是 § 输入原版样式代码。

- **width**（整数，*必需*）

工具提示区域的宽度。

- **height**（整数，*必需*）

工具提示区域的高度。

## 自定义组件

组件类型：**"patchouli:custom"**

仅供模组作者使用：制作任何你想要的页面！你可以传入 patchouli API 的一个接口的实现，将其实例化并传递一些东西。

这里有一个可参考的[测试示例](https://github.com/Vazkii/Patchouli/blob/master/Xplat/src/main/java/vazkii/patchouli/client/book/template/test/ComponentCustomTest.java)。

**属性：**

- **class**（字符串，*必需*）

一个完整的类名（package.name.ClassName），指向 [ICustomComponent](https://github.com/Vazkii/Patchouli/blob/master/Xplat/src/main/java/vazkii/patchouli/api/ICustomComponent.java) 接口的一个实现，不需要在代码的任何地方注册这个类，只需要创建它，加载器将会寻找并加载它。

- 更多值！任何你放在 ICustomComponent 实现中的非瞬态值（non-transient values）都会被读取为组件的值。

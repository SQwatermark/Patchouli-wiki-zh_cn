# 使用模板变量

正如[使用模板](/docs/patchouli-basics/templates)中解释的，变量可用于将章节文件的数据传递给模板渲染器。

如果你不熟悉模板或其中的变量，请先阅读[使用模板](/docs/patchouli-basics/templates)页面，因为这个页面提到的案例更为复杂。注意，此页面仅介绍模板设计，而不介绍如何从章节 json 文件中传递变量。

## 内联变量

变量可以内联到模板的任何字符串中。你需要用 # 包装变量，就像下面演示的这样：

```json
{
	"type": "text",
	"text": "String interpolation with #inline_text# in the middle of the string!",
	"x": 20,
	"y": 30
} 
```

然后就可以在章节 json 文件中定义变量的值：

```json
	"inline_text": "anything you want"
```

游戏中你看到的文本块将会是 *"String interpolation with anything you want in the middle of the string!"*。你可以内联任意多的变量。

## 字符串推导（String Derivation）

变量可以推导出其他数据。例如，用 [ItemStack 字符串](/docs/patchouli-advanced/itemstack-format)填写的变量可以推导出物品的名字。

可以通过对其使用函数以推导出其他变量。为此，你要将 `->func` 附加到变量，并将 "func" 替换为你想使用的函数。例如，如果 "item" 是一个带有 ItemStack 字符串的变量，要获得它的物品名，你需要使用 `#item->iname`。

**函数列表**

- **iname**: 用于包含 ItemStack 字符串的变量。导出物品的显示名。
- **icount**: 用于包含 ItemStack 字符串的变量。导出 ItemStack 中物品的数量。
- **ename**: 用于包含实体 ID 的字符串。导出实体的显示名。
- **upper**: 导出变量的_大写_ 值。
- **lower**: 导出变量的_小写_ 值。
- **trim**: 导出变量的值，去掉首尾的空格。
- **capital**: 导出变量的值，*第一个词首字母大写*。
- **fcapital**: 导出变量的值，*所有单词首字母大写*。
- **exists**: 如果变量的值是空字符串，导出 "false"，否则导出 "true"。
- **iexists**: 如果变量包含一个 ItemStack 字符串且字符串表示的 ItemStack 存在且非空，导出 "true"，否则导出 "false"。
- **inv**: 如果变量的值为 "false"（不区分大小写）导出 "true"，反之导出 "false"。

**其他要点**

- 你可以推导内联变量，所以 `This recipe produces #item->iname#.` 是有效的。
- 你可以多次推导一个变量，所以 `#item->iname->capital` 是有效的。
- 导出值为 "true" 和 "false" 的函数可以用于[模板组件](/docs/patchouli-advanced/default-components)中的 "guard" 属性。

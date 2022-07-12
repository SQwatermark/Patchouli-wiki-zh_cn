# 使用模板

除了可以使用帕秋莉手册自带的[默认页面类型](/docs/patchouli-basics/page-types)，你还可以创建你自己的页面类型！可以使用帕秋莉手册的模板系统（template system）创建新的页面类型。

模板是以类似于章节和分类的方式被创建和引用的，因此，它们在 `/patchouli_books/YOURBOOK/en_us/templates/yourtemplate.json` 之类的文件中，它们可以在 `/templates/` 的子文件夹中分门别类。

## 你的第一个模板

让我们从一个小教程开始学习如何创建一个模板。

- 进入 `/patchouli_books/YOURBOOK/en_us/templates` 文件夹，创建一个文件，按照如下方式填写：

```json title="/patchouli_books/YOURBOOK/en_us/templates/test_template.json"
{
	"components": [
		{
			"type": "patchouli:text",
			"text": "Hello this is a test of the template system!",
			"x": 20,
			"y": 30
		}
	]
}
```

* Create a new entry for your book, and lay it out in any way you like. In one of the
  pages, set the page type to be `yourbooknamespace:test_template`.

```json
{
    "type": "yourbooknamespace:test_template"
}
```

* Try it out ingame. Your page should show the text you set it to. Feel free to change the
  text and the x and y positions.
* Go back to your `test_template.json` file, and change the value of `text` to `"#text"`. This
  is a _variable_, and we can set its value from the entry!
* Go back to the entry that's using your template, and change the page to this:

```json
{
    "type": "yourbooknamespace:test_template",
    "text": "We just passed in the text from a variable!"
}
```

* Try the edited look ingame, and you'll see your template took the `"text"` value from your
  page and put it where `"#text"` was. This is how you load in variable values onto your
  template.
  

Some notes on variables:
 * You can have as many variables as you want, so you could have two text components in
   different positions with either the same `"#text"` value (if you want them to say the
   same thing), or for example, `#upper_text` and `#lower_text`.
 * You can't use any variables such that their names are already common keys for
   pages. This means you can't use any of the names described in the first section of
   [Default Page Types](/docs/patchouli-basics/page-types).
 * You can learn about more advanced variable usage such as inlining them in strings or
   deriving them in the [Template Variable
   Usage](/docs/patchouli-advanced/template-variable-usage) page.

## Template JSON Format

* **components** (Object Array, _mandatory_)

The array of components this template comes with. In the following format:

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

See [Template Components](/docs/patchouli-advanced/default-components) for the components
that Patchouli comes with and what data each one requires.

Note that the components are drawn in the order they appear here, so if you want one to
overlap another, put them in the right order.

* **include** (Object Array)

A list of templates to include in this one. See [Template
Nesting](/docs/patchouli-advanced/template-nesting) for how to do this.

* **processor** (String)

For modders only: A class name for the processor class that takes care of this template. A
processor class can derive data from your code into variables defined in the template. See
[Component Processors](/docs/patchouli-advanced/component-processors) for how to use them.

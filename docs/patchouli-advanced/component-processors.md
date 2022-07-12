# 组件处理器
**这个页面是给模组作者使用的。**

在数据可能存储在你的模组代码的数据结构中的情况下，你可以使用一个组件处理器（Component Processor）来方便地将数据导入你的组件，而不需要在 json 中复制数据。下面是操作流程：

- 决定模板中使用的哪些变量可以从代码中推导出，以及要创建哪些变量来推导它们。例如，如果模板的作用是显示一个有多个输入的配方，你可以将其替换成一个 "recipe" 变量，用其推导出所有的 itemStack 变量。
- 创建实现了 [IComponentProcessor](https://github.com/Vazkii/Patchouli/blob/master/Xplat/src/main/java/vazkii/patchouli/api/IComponentProcessor.java) 的类，然后根据 javadoc 编写方法。
  - 这儿有[一个例子](https://github.com/Vazkii/Patchouli/blob/master/Xplat/src/main/java/vazkii/patchouli/client/book/template/test/RecipeTestProcessor.java)，还用使用它的[模板文件](https://github.com/Vazkii/Patchouli/blob/master/Xplat/src/main/resources/data/patchouli/patchouli_books/testbook2/en_us/templates/include/recipetest.json)。
- 将 `"processor": "package.name.ClassName"` 添加到你的模板文件，引用你创建的类。
- 在章节中使用模板，添加你需要的变量。前面展示的示例中有一大堆变量，但感谢处理器，你只需要声明 "recipe" 处理器。注意此示例还有一个[嵌套模板](/docs/patchouli-advanced/template-nesting)，它使用的变量也可以被推导。

# loader
尝试去实现一个任意后缀的loader ，这里是一个markdown的loader  

关于 webpack loader
---
首先得理解 webpack 的 loader 的功能和原理。          

> loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 import CSS文件！（摘自 webpack 官方中文文档）

    
由此可见，loader 就像是一个“处理器”，输入特定的内容，处理后进行输出。当必要时，可以把一些合适的 loader 串起来使用，使前一个 loader 的输出变成后一个 loader 的输入，最终得到自己想要的结果。
<br>
对于本文要提到的 markdown-loader 来说，它需要进行的处理就是，将 markdown 文件内容解析并包装成一个与 vue 单文件组件内容相似的，然后传给它后面的 vue-loader, 所以一个最简单的 vue markdown-loader 可以长这德性：
```js
module.exports = function (src) {
  const res = (
    `<template>\n` +
    `<h1>hello world</h1>\n` +
    `</template>`
  )
  return res
}
```
当然，这个 loader 看起来有点儿智障，因为不管传给它什么，最后输出来的都一样的玩意儿。但它确实做一个 loader 通常做的事…… 
<br>
下面进入正题，要做一个处理 markdown 的 loader 其逻辑要复杂得多，但实质与上面的差不多，首先我们需要安装一些必要的包。

安装需要的包
---
```bash
yarn install  markdown-it markdown-it-anchor markdown-it-container markdown-it-emoji markdown-it-table-of-contents
```
包名称|功能说明
---|---
markdown-it	| 渲染 markdown 基本语法
markdown-it-anchor |	为各级标题添加锚点
markdown-it-container |	用于创建自定义的块级容器
markdown-it-emoji |	渲染 emoji
markdown-it-table-of-contents  | 自动生成目录
highlight.js  |	代码高亮





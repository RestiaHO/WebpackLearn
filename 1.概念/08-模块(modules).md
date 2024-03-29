# 模块（modules）
在模块化编程中，开发者将程序分解成离散功能块(*discrete chunks of functionality*)，并称之为模块。

每个模块具有比完整程序更小的接触面，使得校验、调试、测试轻而易举。 精心编写的模块提供了可靠的抽象和封装界限，使得应用程序中每个模块都具有条理清楚的设计和明确的目的。

Node.js 从最一开始就支持模块化编程。然而，在 web，模块化的支持正缓慢到来。在 web 存在多种支持 JavaScript 模块化的工具，这些工具各有优势和限制。webpack 基于从这些系统获得的经验教训，并将模块的概念应用于项目中的任何文件。

## 1. 什么是webpack模块
对比 Node.js 模块，webpack 模块能够以各种方式表达它们的依赖关系，几个例子如下：

ES2015 import 语句
- CommonJS require() 语句
- AMD define 和 require 语句
- css/sass/less 文件中的 @import 语句。
- 样式(url(...))或 HTML 文件(<img src=...>)中的图片链接(image url)

**webpack 1 需要特定的 loader 来转换 ES 2015 import，然而通过 webpack 2 可以开箱即用。**

## 2. 支持的模块类型
webpack 通过 loader 可以支持各种语言和预处理器编写模块。loader 描述了 webpack 如何处理 非 JavaScript(non-JavaScript) `_模块_`，并且在 bundle 中引入这些依赖。 webpack 社区已经为各种流行语言和语言处理器构建了 loader，包括：

- CoffeeScript
- TypeScript
- ESNext (Babel)
- Sass
- Less
- Stylus

总的来说，webpack 提供了可定制的、强大和丰富的 API，允许任何技术栈使用 webpack，保持了在你的开发、测试和生成流程中无侵入性(non-opinionated)。
有关完整列表，请参考 loader 列表 或 自己编写。*在LOADERS中详细描述*


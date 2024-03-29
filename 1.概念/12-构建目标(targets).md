# 构建目标(targets)

## 用法
因为服务器和浏览器代码都可以用 JavaScript 编写，所以 webpack 提供了多种构建目标(target)，你可以在你的 webpack 配置中设置。

**webpack 的 target 属性不要和 output.libraryTarget 属性混淆。有关 output 属性的更多信息，请查看我们的指南。**

webpack.config.js
```js
module.exports = {
  target: 'node'
};
```

在上面例子中，使用 node webpack 会编译为用于 [类 Node.js] 环境 (使用 Node.js 的 require, 而不是使用任意内置模块 ( 如 fs 或者 path ) 来加载 chunk )。

每个 target 都有各自部署 (deployment) / 环境 (environment) 特定的附加项，以支持满足其需求。

*查看target的可用值(详见配置)*

## 多个 Target

尽管 webpack 不支持向 target 传入多个字符串，你可以打包两份分离的配置来创建同构的库。

webpack.config.js
```js
var path = require('path');
var serverConfig = {
  target: 'node',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.node.js'
  }
  //…
};

var clientConfig = {
  target: 'web', // <=== 默认是 'web'，可省略
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.js'
  }
  //…
};

module.exports = [ serverConfig, clientConfig ];
```

上面的例子将在你的 `dist` 文件夹下创建 `lib.js` 和 `lib.node.js` 文件;

## 资源

从上传的选项可以看出有多个不同的部署 _目标_ 可供选择。下面一个示例列表，以及你可以参考的资源。

- `compare-webpack-target-bundles`：有关「测试和查看」不同的 webpack target 的大量资源。也有大量 bug 报告。
- `Boilerplate of Electron-React Application`：一个 electron 主进程和渲染进程构建过程的很好的例子。

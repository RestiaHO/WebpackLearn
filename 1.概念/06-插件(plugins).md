# 插件（plugins）
插件是 webpack 的支柱功能。webpack 自身也是构建于，你在 webpack 配置中用到的相同的插件系统之上！
插件目的在于解决 loader 无法实现的其他事。

## 1. 剖析
webpack 插件是一个具有 `apply` 属性的 JavaScript 对象。 `apply` 属性会被 webpack compiler 调用，并且 `compiler` 对象可在整个编译生命周期访问。

ConsoleLogOnBuildWebpackPlugin.js
```js
const pluginName = 'ConsoleLogOnBuildWebpackPlugin';

class ConsoleLogOnBuildWebpackPlugin {
    apply(compiler) {
        compiler.hooks.run.tap(pluginName, compilation => {
            console.log("webpack 构建过程开始！");
        });
    }
}
```

**compiler hook 的 tap 方法的第一个参数，应该是驼峰式命名的插件名称。建议为此使用一个常量，以便它可以在所有 hook 中复用。**

## 2. 配置
webpack.config.js
```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //通过 npm 安装
const webpack = require('webpack'); //访问内置的插件
const path = require('path');

const config = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader'
      }
    ]
  },
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

module.exports = config;
```

## 3. Node API
**即便使用 Node API，用户也应该在配置中传入 plugins 属性。compiler.apply 并不是推荐的使用方式。**

some-node-script.js
```js
  const webpack = require('webpack'); //访问 webpack 运行时(runtime)
  const configuration = require('./webpack.config.js');

  let compiler = webpack(configuration);
  compiler.apply(new webpack.ProgressPlugin());

  compiler.run(function(err, stats) {
    // ...
  });
```


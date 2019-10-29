# 使用不同语言进行配置(configuration languages)

webpack 接受以多种编程和数据语言编写的配置文件。支持的文件扩展名列表，可以在 node-interpret 包中找到。使用 node-interpret，webpack 可以处理许多不同类型的配置文件。

## TypeScript

为了用 TypeScript 书写 webpack 的配置文件，必须先安装相关依赖：

```txt
npm install --save-dev typescript ts-node @types/node @types/webpack
```

之后就可以使用 TypeScript 书写 webpack 的配置文件了：

webpack.config.ts
```ts
import path from 'path';
import webpack from 'webpack';

const config: webpack.Configuration = {
  mode: 'production',
  entry: './foo.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'foo.bundle.js'
  }
};

export default config;
```

注意，你还需要核对 tsconfig.json 文件。如果 tsconfig.json 中的 compilerOptions 中的 module 字段是 commonjs ，则配置是正确的，否则 webpack 将因为错误而构建失败。发生这种情况，是因为 ts-node 不支持 commonjs 以外的任何模块语法。

这个问题有两种解决方案：

- 修改 tsconfig.json。
- 安装 tsconfig-paths。

__第一个选项_是指，打开你的 tsconfig.json 文件并查找 compilerOptions。将 target 设置为 "ES5"，以及将 module 设置为 "CommonJS"（或者完全移除 module 选项）。

__第二个选项_是指，安装 tsconfig-paths 包：

```txt
npm install --save-dev tsconfig-paths
```

然后，为你的 webpack 配置，专门创建一个单独的 TypeScript 配置：

tsconfig-for-webpack-config.json
```ts
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "es5"
  }
}
```
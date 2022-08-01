# bundleConfigFile

## 参数

`fileName`：配置文件的路径
`isESM`：是否是ESM模式

## 流程

1. 使用 esbuild 捆绑配置文件，将vite的config文件进行编译，编译过程中插入两个插件，其中一个插件的作用是确保在 monorepo 模式中正确的获取依赖项目，第二个插件则是在 vite 配置文件中注入全局变量，函数的结果是返回 vite config 中所需要的依赖和编译后的代码。

# loadConfigFromFile

## 参数

`configEnv`：[[vite-Config_resolveConfig#^319860]]
`configFile`：配置文件文件路径
`configRoot`：终端当前的路径
`logLevel`：日志的级别 'error' | 'warn' | 'info' | 'silent'

## 流程

1. 记录 `loadConfigFromFile` 方法开始的时间，并且声明 getTime 函数来计算 `loadConfigFromFile` 方法内区域的执行时长，同时还要声明下文保存下文找到的配置文件的路径 `resolvedPath` 变量
==提示==：[[node-perf_hooks#performance now]]
```ts
const start = performance.now()
const getTime = () => `${(performance.now() - start).toFixed(2)}ms`
let resolvedPath: string | undefined
```
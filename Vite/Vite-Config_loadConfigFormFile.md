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

2. 如果 `configFile` 结果为 `true` ，那么直接向 `resolvedPath` 结果，否则就去 `DEFAULT_CONFIG_FILES` 常量中去按数组顺序去获取配置文件，当获取到时停止后续循环
```ts
if (configFile) {
	resolvedPath = path.resolve(configFile)
} else {
	for (const filename of DEFAULT_CONFIG_FILES) {
		const filePath = path.resolve(configRoot, filename)
		if (!fs.existsSync(filePath)) continue
		resolvedPath = filePath
		break
	}

}

export const DEFAULT_CONFIG_FILES = [
	'vite.config.js',
	'vite.config.mjs',
	'vite.config.ts',
	'vite.config.cjs',
	'vite.config.mts',
	'vite.config.cts'
]
```

3. 如果 `resolvePath` 仍未解析到则终止 `loadConfigFromFile` 方法的执行
```ts
if (!resolvedPath) {
	debug('no config file found.')
	return null
}
```


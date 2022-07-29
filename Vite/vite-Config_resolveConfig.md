# resoveConfig

## 参数

`inlineConfig`： [[VIte-Cli#获取的配置]]
`command`： 'build' | 'serve'
`defaultMode`：'development'

## 执行流程

1. 解析存放 `config`、`configFileDependencies`、`mode`
```TS
let config = inlineConfig
let configFileDependencies: string[] = []
let mode = inlineConfig.mode || defaultMode
```

2. 判断当面的mode是否是 `production`，条件成立后将全局的 `NODE_ENV`修改成 `production` 模式。
```ts
if (mode === 'production') {
	process.env.NODE_ENV = 'production'
}
```

3. 如果 `command` 等于 serve，并且全局模式为 `production` 生产模式，则将全局的模式改成 `development` 开发模式 
```ts
if (command === 'serve' && process.env.NODE_ENV === 'production') {
	process.env.NODE_ENV = 'development'
}
```

4. 创建环境配置对象 `configEnv` ^319860
```ts
const configEnv = {
	mode,
	command,
	ssrBuild: !!config.build?.ssr
}
```

5. 判断是否 `config` 中是否有用户指定的配置文件的路径，如果“等于 `undefind`或者 `string`”则去执行 `loadConfigFromFile` 方法获取。并且判断配置是否获取成功，成功后执行 `mergeConfig` 方法将 `cli` 传递的配置和用户书写的配置进行合并。
==提示==：undefind不等于false，成立
```ts
let { configFile } = config

if (configFile !== false) {
	const loadResult = await loadConfigFromFile(
		configEnv,
		configFile,
		config.root,
		config.logLevel
	)
	if (loadResult) {
		config = mergeConfig(loadResult.config, config)
		configFile = loadResult.path
		configFileDependencies = loadResult.dependencies
	}
}
```
[[Vite-Config_loadConfigFormFile]]
[[Vite-Config_mergeConfig]]
### dev

> 运行脚本

#### 获取的配置

```ts
const options = {
	host, // 指定主机名称
	prot, // 指定端口号码
	https, // 使用 https
	open, // 启动时打开浏览器
	cors, // 启用 cors
	strictPort, // 如果指定的端口已经被使用那么就会退出服务
	force, // 强制优化器忽略缓存并重新捆绑
}
```

#### 流程

1. read `server/index.ts` file get `createServe` function
```ts
const { createServer } = await import('./server')

const server = await createServer({
	root,
	base: options.base,
	mode: options.mode,
	configFile: options.config,
	logLevel: options.logLevel,
	clearScreen: options.clearScreen,
	optimizeDeps: { force: options.force },
	server: cleanOptions(options)
})
```
[[Vite-Server_createServer|server流程]]
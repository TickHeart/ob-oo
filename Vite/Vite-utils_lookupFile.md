# lookupFile
	查找文件选项

## 参数

`dir`：文件夹路径
`formats`： 格式（文件名称）
`options`：LookupFileOptions

```ts
interface LookupFileOptions {
	pathOnly?: boolean
	rootDir?: string
}
```

## 流程

1. 循环遍历 `formats` 如果 formats 中存在数据，会根据 `options.pathOnly` 去决定返回文件的路径还是，文件的内容
```ts
for (const format of formats) {
	const fullPath = path.join(dir, format)
	if (fs.existsSync(fullPath) && fs.statSync(fullPath).isFile()) {
		return options?.pathOnly ? fullPath : fs.readFileSync(fullPath, 'utf-8')
	}
}
```

2. [ ] 没看懂，看懂补上
```ts
const parentDir = path.dirname(dir)
if (
parentDir !== dir &&
(!options?.rootDir || parentDir.startsWith(options?.rootDir))
) {
	return lookupFile(parentDir, formats, options)
}
```
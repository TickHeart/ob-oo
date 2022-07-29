# creeateServer

> 创建服务
---
## 参数

`inleneConfig`: [[VIte-Cli#获取的配置]]

## 流程

1. resolve config
```ts
const config = await resolveConfig(inlineConfig, 'serve', 'development')
```
[[vite-Config_resolveConfig]]
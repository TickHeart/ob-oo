## Dockerfile

```Dockerfile
FROM node:14 as builder

RUN curl -f https://get.pnpm.io/v6.16.js | node - add --global pnpm

WORKDIR /code

COPY package.json .npmrc pnpm-lock.yaml /code/

RUN pnpm i --frozen-lockfile

# Bundle app source
COPY . /code/

# build
RUN pnpm build

# step 2: nginx alpine
FROM nginx:mainline

# 挂载文件
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /code/dist /usr/share/nginx/html
```

1. 使用名为 `node:14` 的镜像环境，并命名为 `builder`
2. 配置 pnpm 的环境
3. 进入工作目录
4. 复制文件到工作目录
5. 执行安装依赖
6. 复制文件到工作目录
7. 执行打包
8. 切换到 nginx 的镜像环境中
9. 挂载配置
10. 挂载打包后的文件

---

## docker-compose.yaml

``` yaml
version: '3'
services:
	huaan-center:
		build:
			context: .
			dockerfile: Dockerfile
		ports:
			- 8080:80
```

---

## .npmrc

```shell
frozen-lockfile=true
shamefully-hoist=true
```
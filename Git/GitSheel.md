1. [x] 撤销上一次 `commit` 但是不会撤销 `git add`

```shell
git reset --soft head~1
```

2. 撤销上一次 `commit` 同时撤销 `git add`

```shell
git reset head~
```
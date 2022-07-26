---
creation date: 2022-07-23 20:47
modification date: 星期六 23日 七月 2022 20:47:47
tag: 正则表达式
---
正则表达式的分组尤为重要，他可以帮助我们获取我们想到的数据从而做一些替换、收集、换算等操作。
分组在[[-Logic#子表达式]]中我们是见过的`()`就是分组的符号。
## 反向引用

>反向引用指通过`\组号`引用**之前**的分组，可以把分组理解成一个**变量**，在通过变量名(组号)引用

如何收集正确的HTML闭合标签
在代码`<h2>三级标题</h3>`中明显发现这个闭合标签是错误的，如何正确的验证标签反向引用可以做到这一点 `/<(h[1-6])>.+?<\/\1>/gm`[[-RegExpImage#6|可视化图解]]

前半部分很清晰的匹配了标题标签，但是后半部分的尖括号内`\1`的含义如下图所示【[[-RegExpImage#7|图例]]】

## 命名分组
语法是`(?<名称> )`
通过命名分组收集的信息在 js 中是可以通过对应的命名获取到对应的信息。
但是要注意的是即使你是用了命名分组你在使用[[-Groups#反向引用]]的逻辑时仍需通过`\组号`获取信息

## 忽略（移除）分组
语法是`(?: )`
就比如我们在[[-Logic#逻辑或]]里面举出的例子匹配 http 或者 https 的时候我们使用的那个子表达式，如果我们只是配合逻辑表达式使用并不想收集信息的情况下我们就可以将其移除。

## 嵌套分组
看图就懂[[-RegExpImage#8|图！]]





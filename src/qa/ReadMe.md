# 常见问题

## 自动关闭Issue

在`github`的提交信息中使用下面的关键字+`issue`id，可以自动关闭`issue`。

关键字：
* close
* closes
* closed
* fix
* fixes
* fixed
* resolve
* resolves
* resolved

## 如何查看一个创建的大小

如果我们要在github上查看某个仓库的大小，可以通过api的形式查看：`https://api/github.com/repos/{user}/{repo}`，把其中的`user`和`repo`替换为仓库的user和repo就行。
返回值是一个`Json`。其中的`size`字段就是其仓库的大小，其单位为`kb`。

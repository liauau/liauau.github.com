---
title: git添加两个repo
date: 2021-11-04 19:01:56
tags: 工具
---

# 问题描述

我有一个local repo，和remote repo_a一直保持同步，但remote repo_a是其他人在维护，所以我本地的修改一般不会进行push到remote。但是我希望本地的修改也能长期保留，而且多个设备互相同步。那么目前的问题就是:
- local repo能够和其他人维护的remote repo_a保持更新
- local repo的修改能够保留而且多设备同步

因此，需要建立remote repo_b, 本地repo能够push修改。数据流如下:

```
 _______________
|               |
| remote repo_a |
|_______________|
                \
                 \ pull
                 _\|
                 _______________
                |               |
                |   local repo  |
                |_______________|
                  /
                 / push
 ______________|/_
|               |
| remote repo_b |
|_______________|

```


# 解决方法

1. 创建`remote repo_b`，假设地址为`git@github.com:xxx/b.git`
2. 添加repo_b: `git remote add repo_b git@github.com:xxx/b.git`, 使用`git remote -v`可以看到两个repo，`origin`和`repo_b`
3. 推送到远端: `git push -u repo_b <branch_name>`。注意，此时可能会出错`shallow update not allowed`。如果出现这个错误，说明`origin`的内容可能不全，需要重新拉取`origin`: `git fetch --unshallow origin`。然后再使用之前的push命令重新操作即可成功。

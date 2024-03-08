---
title: Git相关知识
date: 2024-03-07 08:53:58
tags: Git
---

git rebase

情况
![](https://img-blog.csdnimg.cn/36efc2704d174acab598c4b9addd3694.png?)

此时我们切换到feature分支上，执行rebase命令，相当于是想要把master分支合并到feature分支（这一步的场景就可以类比为我们在自己的分支feature上开发了一段时间了，准备从主干master上拉一下最新改动。模拟了git pull --rebase的情形）

# 这两条命令等价于git rebase master feature
git checkout feature
git rebase master

执行后

![](https://img-blog.csdnimg.cn/12b959efcc454da5a15b9fdec493d61b.png?)

最后把提取的C和D接到M后面，注意这里的接法，官方没说清楚，实际是会依次拿M和C、D内容分别比较，处理冲突后生成新的C’和D’

无论是个人单机开发，还是公司协作开发，只要没有特殊需求，用merge准没错！！！

不要用rebase。

# Git blame
git blame用来追溯一个指定文件的历史修改记录
git blame filename


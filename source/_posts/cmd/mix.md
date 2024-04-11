---
title: 随手记
date: 2024-02-10 22:33:02
tags: 
- cmd
- 随笔
---
总算找到个能放一堆杂七杂八知识的地方了

# tabs outliner 删掉所有的Crash
```
let i = 0; let t = setInterval(() => { let n = treeView.treeModel.currentSession_rootNode.subnodes[i]; if (n.getNodeText().includes(" (crashed ")) { console.log(`Removing node ${n.getNodeText()}`, n); n.removeOwnTreeFromParent(); } else { i++; } if (i == treeView.treeModel.currentSession_rootNode.subnodes.length) { clearInterval(t); } }, 100);

```
[git如何避免”warning: LF will be replaced by CRLF“提示？](https://www.zhihu.com/question/50862500)
最简单办法 git config --global core.autocrlf false


[Jenkins+gitlab自动化部署java应用（适合初学者）](https://blog.csdn.net/qq_42933340/article/details/131059727)

私服能做的事情 [某乎](https://www.zhihu.com/question/40854395)
- 博客
- 私服
- ss
- Nextcloud 私人云盘 部署方式 https://zhuanlan.zhihu.com/p/62987726 https://zhuanlan.zhihu.com/p/31035773
- frp，树莓派，物联网
- Emby?看电影
- uptimeRobot 服务监控
- netData监控


# 一些杂七杂八的玩意
奥卡姆剃刀原理
“如无必要，勿增实体” （Entities should not be multiplied unnecessarily）
Numquam ponenda est pluralitas sine necessitate.（避重趋轻）
Pluralitas non est ponenda sine necessitate.（避繁逐简）
Frustra fit per plura quod potest fieri per pauciora.（以简御繁）
Entia non sunt multiplicanda praeter necessitatem.（避虚就实）

康威定律（Conway Law）
任何系统的构成，都反映了设计这个系统的组织结构。
Melvin Conway 观察到，软件系统的架构看起来与构建它的开发团队的组织结构非常相似。

# 书籍
《写给大家看的设计书》：设计相关
《点石成金》：Web 用户体验相关
《鸟哥的Linux私房菜》：Linux 系统相关
大型网站技术架构 https://e.dangdang.com/pc/reader/index.html?id=1900450642
Devops https://e.dangdang.com/pc/reader/index.html?id=1901321311

单元测试

# 网络安全相关

春秋云镜WP https://github.com/superlink996/chunqiuyunjingbachang?tab=readme-ov-file

各种平台地址 https://www.zhihu.com/question/267204109

靶场攻略 | 网络安全靶场合集 https://blog.csdn.net/Python_0011/article/details/133759740

工具 How I get there https://how-did-i-get-here.net/


## 大型网站技术架构 读书笔记
小型网站最需要考虑的是活下去，为用户提供好服务创造价值，也蛮生长。

驱动大型网站技术发展的主要力量是网站的业务发展



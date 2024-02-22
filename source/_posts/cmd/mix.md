---
title: 常用命令
date: 2024-02-10 22:33:02
tags: cmd
---
总算找到个能放一堆杂七杂八知识的地方了

# tabs outliner 删掉所有的Crash
```
let i = 0; let t = setInterval(() => { let n = treeView.treeModel.currentSession_rootNode.subnodes[i]; if (n.getNodeText().includes(" (crashed ")) { console.log(`Removing node ${n.getNodeText()}`, n); n.removeOwnTreeFromParent(); } else { i++; } if (i == treeView.treeModel.currentSession_rootNode.subnodes.length) { clearInterval(t); } }, 100);

```
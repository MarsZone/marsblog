---
title: MarkDown知识
date: 2024-02-10 21:56:33
tags: 笔记
---

- [官方教程](https://markdown.com.cn/)
- [官方例子](https://markdown.com.cn/editor/)

Markdown是一种轻量级标记语言，排版语法简洁，让人们更多地关注内容本身而非排版。
可与HTML混编，可导出 HTML、PDF 以及本身的 .md 格式的文件。因简洁、高效、易读、易写，Markdown被大量使用，如Github、Wikipedia、简书等。

千万不要被「标记」、「语言」吓到，Markdown的语法十分简单，常用的标记符号不超过十个，用于日常写作记录绰绰有余，不到半小时就能完全掌握。

就是这十个不到的标记符号，却能让人优雅地沉浸式记录，专注内容而不是纠结排版，达到「心中无尘，码字入神」的境界。

## Markdown 标题语法
`#`的数量代表了标题的级别。 用``包住就能写#号`例如，添加三个 # 表示创建一个三级标题 (<h3>) (例如：### My Header)。`

可以和html混合用。

还可以在文本下方添加任意数量的 == 号来标识一级标题，或者 -- 号来标识二级标题。

header 1
====
header 2
----

# Markdown 段落
要创建段落，请使用空白行将一行或多行文本进行分隔。
不要用空格（spaces）或制表符（ tabs）缩进段落。

# Markdown 换行语法
在一行的末尾添加两个或多个空格，然后按回车键,即可创建一个换行(<br>)。

# 强调
# 引用
要创建块引用，请在段落前添加一个 > 符号。
> Dorothy followed her through many of the beautiful rooms in her castle.

块引用可以包含多个段落。为段落之间的空白行添加一个 > 符号。
> Dorothy followed her through many of the beautiful rooms in her castle.
>
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

块引用可以嵌套。在要嵌套的段落前添加一个 >> 符号。
> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

块引用可以包含其他 Markdown 格式的元素。并非所有元素都可以使用，你需要进行实验以查看哪些元素有效。

# Markdown 列表语法
要创建有序列表，请在每个列表项前添加数字并紧跟一个英文句点。数字不必按数学顺序排列，但是列表应当以数字 1 起始。
1. First item
2. Second item
3. Third item
4. Fourth item

要创建无序列表，请在每个列表项前面添加破折号 (-)、星号 (*) 或加号 (+) 。缩进一个或多个列表项可创建嵌套列表。
- First item
- Second item
- Third item
- Fourth item

要在保留列表连续性的同时在列表中添加另一种元素，请将该元素缩进四个空格或一个制表符，如下例所示：
*   This is the first list item.
*   Here's the second list item.

    I need to add another paragraph below the second list item.

*   And here's the third list item.

引用块 >

代码块
代码块通常采用四个空格或一个制表符缩进。当它们被放在列表中时，请将它们缩进八个空格或两个制表符。
1.  Open the file.
2.  Find the following code block on line 21:

        <html>
          <head>
            <title>Test</title>
          </head>

3.  Update the title to match the name of your website.
4.  
图片
` ![Tux, the Linux mascot](/assets/images/tux.png)`

# Markdown 代码语法
要将单词或短语表示为代码，请将其包裹在反引号 (`) 中。

如果你要表示为代码的单词或短语中包含一个或多个反引号，则可以通过将单词或短语包裹在双反引号(``)中。

要创建代码块，请将代码块的每一行缩进至少四个空格或一个制表符。

# Markdown 分隔线语法
要创建分隔线，请在单独一行上使用三个或多个星号 (***)、破折号 (---) 或下划线 (___) ，并且不能包含其他内容。
*** 
---
___
# Markdown 链接语法
链接文本放在中括号内，链接地址放在后面的括号中，链接title可选。

超链接Markdown语法代码：`[超链接显示名](超链接地址 "超链接title")`

对应的HTML代码：`<a href="超链接地址" title="超链接title">超链接显示名</a>`

链接title是当鼠标悬停在链接上时会出现的文字，这个title是可选的，它放在圆括号中链接地址后面，跟链接地址之间以空格分隔。

这是一个链接 [Markdown语法](https://markdown.com.cn "最好的markdown教程")。

使用尖括号可以很方便地把URL或者email地址变成可点击的链接。
<https://markdown.com.cn>
<fake@example.com>

# Markdown 图片语法
# Markdown 转义字符语法
要显示原本用于格式化 Markdown 文档的字符，请在字符前面添加反斜杠字符 \ 。

# Markdown 内嵌 HTML 标签


# Markdown 围栏代码块
Markdown基本语法允许您通过将行缩进四个空格或一个制表符来创建代码块。如果发现不方便，请尝试使用受保护的代码块。根据Markdown处理器或编辑器的不同，您将在代码块之前和之后的行上使用三个反引号（(```）或三个波浪号（~~~）。

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
许多Markdown处理器都支持受围栏代码块的语法突出显示。使用此功能，您可以为编写代码的任何语言添加颜色突出显示。要添加语法突出显示，请在受防护的代码块之前的反引号旁边指定一种语言。
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
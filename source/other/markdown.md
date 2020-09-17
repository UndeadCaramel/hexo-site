---
title: Markdown学习笔记
date: 2020-09-17 20:42:58
---

# 介绍

Markdown是一种轻量级标记语言，创始人为约翰·格鲁伯(英语：John Gruber)。Markdown是面向Web写作者的文本到HTML转换工具。Markdown允许使用易于阅读和编写的纯文本格式进行编写，然后将其转换为结构上有效的XHTML(或HTML)。

# 基本

## 段落
段落是一个或多个连续的文本行，由一个或多个空行分隔(空行看起来像空白的任何行，仅包含空格或制表符的行被视为空白行)。普通段落不应该以空格或制表符缩进。

## 标题
Markdown提供了两种标题样式：Setext和atx。对于Setext风格的标题< h1 >和< h2 >，使用等号(=)和连字符(-)区分。创建atx样式的标题，则通过在行开头放置1-6个井号(#)，井号数量等于HTML标题级别

## 块引用
块引用使用电子邮件样式的尖括号(>)表示。

###### Markdown code：
```
A First Level Header
====================

A Second Level Header
---------------------

Now is the time for all good men to come to
the aid of their country. This is just a
regular paragraph.

The quick brown fox jumped over the lazy
dog's back.

### Header 3

> This is a blockquote.
> 
> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote
```

###### HTML code:
```
<h1>A First Level Header</h1>

<h2>A Second Level Header</h2>

<p>Now is the time for all good men to come to
the aid of their country. This is just a
regular paragraph.</p>

<p>The quick brown fox jumped over the lazy
dog's back.</p>

<h3>Header 3</h3>

<blockquote>
    <p>This is a blockquote.</p>

    <p>This is the second paragraph in the blockquote.</p>

    <h2>This is an H2 in a blockquote</h2>
</blockquote>
```

## 短语强调
Markdown使用星号(*)和下划线(_)表示强调。
- 星号(*):对应HTML(< em >),斜体强调标签，更强烈的强调，表示内容的强调点。
- 下划线(_):对应HTML(< strong >),粗体强调标签，强调，表示内容的重要性。

###### Markdown code：
```
Some of these words *are emphasized*.
Some of these words _are emphasized also_.

Use two asterisks for **strong emphasis**.
Or, if you prefer, __use two underscores instead__.
```

###### HTML code:
```
<p>Some of these words <em>are emphasized</em>.
Some of these words <em>are emphasized also</em>.</p>

<p>Use two asterisks for <strong>strong emphasis</strong>.
Or, if you prefer, <strong>use two underscores instead</strong>.</p>
```

### 列表
列表分为无序列表(项目符号)和有序列表(编号)。

#### 无序列表
无序列表(项目符号)使用星号(*)，加号(+)和连字符(-)作为列表标记。

###### Markdown code：
* 星号(*)：
```
*   Candy.
*   Gum.
*   Booze.
```
+ 加号(+)：
```
+   Candy.
+   Gum.
+   Booze.
```
- 连字符(-)：
```
-   Candy.
-   Gum.
-   Booze.
```

全部输出相同HTML代码：
###### HTML code:
```
<ul>
<li>Candy.</li>
<li>Gum.</li>
<li>Booze.</li>
</ul>
```

#### 有序列表
有序列表(编号)使用常规数字后跟句点(.)作为列表标记。

###### Markdown code：
```
1.  Red
2.  Green
3.  Blue
```

###### HTML code:
```
<ol>
<li>Red</li>
<li>Green</li>
<li>Blue</li>
</ol>
```

如果在项目间插入空白行，则将获得列表项目段落标签< p >，可以通过将段落缩进4个空格或一个制表符来创建多段落列表项：
###### Markdown code：
```
*   A list item.

    With multiple paragraphs.

*   Another item in the list.
```
###### HTML code:
```
<ul>
<li><p>A list item.</p>
<p>With multiple paragraphs.</p></li>
<li><p>Another item in the list.</p></li>
</ul>
```

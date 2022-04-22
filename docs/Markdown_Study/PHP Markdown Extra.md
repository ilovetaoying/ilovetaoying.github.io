---
title: '8# PHP Markdown Extra'
created: '2022-04-20T16:12:12.409Z'
modified: '2022-04-21T16:53:58.218Z'
---

8# PHP Markdown Extra


> 2022-04-20 18:37:15 
> <br>本教程英语文档源自于JOHN GRUBER的[Daring Fireball](https://daringfireball.net/projects/markdown/basics)
> <br>本教程中文翻译由CY爱TY翻译和撰写，仅供学习交流目的。未经许可，不得擅自转载以及作为商业用途。欢迎发送电邮到<43522623@qq.com>与我交流。


Markdown Extra 是 PHP Markdown 的扩展，实现了一些当前使用普通 Markdown 语法无法实现的增强功能。Markdown Extra 在PHP Markdown Lib中作为单独的解析器类提供。

本文档解释了Markdown Extra实现的Markdown语法的更改和补充。

## 阅读前的准备
阅读本文档之前，您应该已经熟悉：

* [Markdown基础][MD_basic]
* [Markdown语法][MD_syntax]

# 目录
+ [内联 HTML](#内联HTML)
+ [HTML块内的Markdown](#HTML块内的Markdown)
+ 特殊属性
+ 围栏代码块
+ 表
+ 定义列表
+ 脚注
	+ 输出
+ 缩写
+ 有序列表
+ 强调
+ 反斜杠转义

## 内联HTML ##
常见的HTML“块级元素”包括： `<div>`, `<table>`, `<pre>`,`<p>`， 原来Markdown对块级元素有严格的限制要求（比如，必须前后都有空行区分，块级元素的开头和结尾标签也不能带有任何缩进）。

Markdown Extra做了一些改进：

1. 块元素的开始标签的缩进不能超过三个空格。因为根据标准 Markdown 规则，任何缩进超过该值的标签都将被视为代码块。
2. 当在列表中出现块元素时，其所有内容的缩进量应与列表项的缩进量相同。（只要第一个开始标签没有缩进超过4个空格或者一个`Tab`变成一个代码块，多缩进3个空格内都不会有任何问题。）

## HTML块内的Markdown
以前Markdown无法作用于块元素中，如`<div>`。

Markdown Extra 在块元素中添加了一个新标签"markdown"，当markdown="1"时，markdown etra可以作用于该块元素——如下所示：

    <div markdown="1">
    This is *true* markdown text.
    </div>

当markdown="1"，Markdown 会渲染HTML的块元素。最终结果将如下所示：

<div markdown="1">
This is *true* markdown text.
</div>

相当于HTML输出了：
    
    <div>
    <p>This is <em>true</em> markdown text.</p>
    </div>

Markdown Extra 会智能判断放置markdown属性的块元素应用正确的格式。例如，如果将markdown属性应用于<p>标签，它只会在内部生成跨度级别的元素——它不会允许列表、块引用、代码块。

但在某些情况下，这是模棱两可的，例如：

<table>
<tr>
<td markdown="1">This is *true* markdown text.</td>
</tr>
</table>
表格单元格可以包含跨度和块元素。在这种情况下，Markdown Extra 只会应用跨度级规则。如果您希望启用块构造，只需编写即可markdown="block"。

## 特殊属性 ##
使用 Markdown Extra，您可以使用属性块在某些元素上设置 id 和 class 属性。例如，将所需的 id 以#开头放在行尾标头之后的大括号内，如下所示：
    
    Header 1	{#header1}
    ========
    
    ## Header 2 ##  	{#header2}

然后，您可以创建指向同一文档不同部分的链接，如下所示：


    [Link back to header 1](#header1)

如果要添加一个类名，则以.class名表示：
    
    ## The Site ##	{.main}

也可以通过指定“属性=值”（不能包含空格）来添加具有简单值的自定义属性：
    
    ## Le Site ##	{lang=fr}
id、多个类名和其他自定义属性可以通过将它们全部放在同一个特殊属性块中来组合：
    
    ## Le Site ##	{.main .shine #the-site lang=fr}

特殊属性代码块可用于：

+ 标头，
+ 围栏代码块，
+ 链接，以及
+ 图片

![logo](/img/logo.png){width=200%}

对于图像和链接，将特殊属性块紧跟在包含地址的括号之后：

[link](url){#id .class}  
![img](url){#id .class}
或者，如果使用引用样式的链接和图像，请将其放在定义行的末尾，如下所示：

[link][linkref] or [linkref]  
![img][linkref]

[linkref]: url "optional title" {#id .class}

## 围栏代码块 ##
Markdown Extra 中，语法代码块可以使用三个以上的波浪号~字符在代码块的开始和结束行表示当中的部分为代码。。例如：

This is a paragraph introducing:
    
    ~~~~~~~~~~~~~~~~~~~~~
    单行代码
    ~~~~~~~~~~~~~~~~~~~~~
表示为：

~~~~~~~~~~~~~~~~~~~~~
单行代码
~~~~~~~~~~~~~~~~~~~~~
新样式.css
也可以使用反引号`代替波浪号，形成代码标签的效果：

``````````````````
another code block
``````````````````

与缩进相对应，围栏代码块到处是可以让代码开头和结尾拥有空行：

~~~

blank line before
blank line after

~~~

缩进的代码块不能紧跟在列表之后，因为列表缩进优先；围栏代码块没有这样的限制：

1.  List item

    Not an indented code block, but a second paragraph
    in the list item

~~~~
1. This is a code block, fenced-style
~~~~

如果您需要将一些代码粘贴到没有用于增加文本块缩进的命令的编辑器（例如 Web 浏览器中的文本框）中，则围栏代码块也是理想的选择。

您可以指定将应用于代码块的类名。如果您想根据语言设置不同的代码块样式，这很有用。或者你也可以用它来告诉语法高亮器使用什么语法。

~~~~~~~~~~~~~~~~~~~~~~~~~~~~ .html
<p>paragraph <b>emphasis</b>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
类名放在第一个栅栏的末尾。它前面可以有一个点，但这不是必需的。您还可以使用特殊的属性块：

~~~~~~~~~~~~~~~~~~~~~~~~~~~~ {.html #example-1}
<p>paragraph <b>emphasis</b>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在 HTML 输出中，代码块属性将应用于code元素；如果您想在pre元素上看到它们，请将code_attr_on_pre解析器上的配置变量设置为true. 有关详细信息，请参阅配置参考。

表
Markdown Extra 有自己的简单表格语法。一个“简单”的表格如下所示：

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell
第一行包含列标题；第二行包含标题和内容之间的强制分隔线；以下每一行都是表格中的一行。列始终由竖线 ( |) 字符分隔。转换为 HTML 后，结果如下：

<table>
<thead>
<tr>
  <th>First Header</th>
  <th>Second Header</th>
</tr>
</thead>
<tbody>
<tr>
  <td>Content Cell</td>
  <td>Content Cell</td>
</tr>
<tr>
  <td>Content Cell</td>
  <td>Content Cell</td>
</tr>
</tbody>
</table>
如果您愿意，您可以在表格的每一行添加一个前导和尾随管道。使用您喜欢的形式。作为说明，这将给出与上述相同的结果：

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |
注意：一个表的每一行至少需要一个管道，以便 Markdown Extra 正确解析它。这意味着创建单列表的唯一方法是在每一行中添加前导管道或尾管道，或两者都添加。

您可以通过在分隔线中添加冒号来指定每列的对齐方式。分隔线左侧的冒号将使列左对齐；行右侧的冒号将使列右对齐；两侧的冒号表示该列居中对齐。

| Item      | Value |
| --------- | -----:|
| Computer  | $1600 |
| Phone     |   $12 |
| Pipe      |    $1 |
alignHTML 属性应用于相关列的每个单元格。

您可以使用常规 Markdown 语法将跨度级格式应用于每个单元格的内容：

| Function name | Description                    |
| ------------- | ------------------------------ |
| `help()`      | Display the help window.       |
| `destroy()`   | **Destroy your computer!**     |
定义列表
Markdown Extra 实现定义列表。定义列表由术语和这些术语的定义组成，就像在字典中一样。

Markdown Extra 中的简单定义列表由单行术语、后跟冒号和该术语的定义组成。

Apple
:   Pomaceous fruit of plants of the genus Malus in 
    the family Rosaceae.

Orange
:   The fruit of an evergreen tree of the genus Citrus.
术语必须用空行与先前的定义分开。定义可以跨越多行，在这种情况下它们应该缩进。但你并不一定要这样做：如果你想变得懒惰，你可能会忘记缩进一个跨越多行的定义，它仍然可以工作：

Apple
:   Pomaceous fruit of plants of the genus Malus in 
the family Rosaceae.

Orange
:   The fruit of an evergreen tree of the genus Citrus.
前面的每个定义列表都会给出相同的 HTML 结果：

<dl>
<dt>Apple</dt>
<dd>Pomaceous fruit of plants of the genus Malus in 
the family Rosaceae.</dd>

<dt>Orange</dt>
<dd>The fruit of an evergreen tree of the genus Citrus.</dd>
</dl>
作为定义标记的冒号通常从左边距开始，但最多可以缩进三个空格。定义标记后面必须跟一个或多个空格或制表符。

定义列表可以有多个与一个术语相关的定义：

Apple
:   Pomaceous fruit of plants of the genus Malus in 
    the family Rosaceae.
:   An American computer company.

Orange
:   The fruit of an evergreen tree of the genus Citrus.
您还可以将多个术语与一个定义相关联：

Term 1
Term 2
:   Definition a

Term 3
:   Definition b
如果定义前面有一个空行，Markdown Extra 会将定义包装在<p>HTML 输出中的标签中。例如，这个：

Apple

:   Pomaceous fruit of plants of the genus Malus in 
    the family Rosaceae.

Orange

:    The fruit of an evergreen tree of the genus Citrus.
会变成这样：

<dl>
<dt>Apple</dt>
<dd>
<p>Pomaceous fruit of plants of the genus Malus in 
the family Rosaceae.</p>
</dd>

<dt>Orange</dt>
<dd>
<p>The fruit of an evergreen tree of the genus Citrus.</p>
</dd>
</dl>
就像常规列表项一样，定义可以包含多个段落，并包括其他块级元素，例如块引用、代码块、列表，甚至其他定义列表。

Term 1

:   This is a definition with two paragraphs. Lorem ipsum 
    dolor sit amet, consectetuer adipiscing elit. Aliquam 
    hendrerit mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus.

:   Second definition for term 1, also wrapped in a paragraph
    because of the blank line preceding it.

Term 2

:   This definition has a code block, a blockquote and a list.

        code block.

    > block quote
    > on two lines.

    1.  first list item
    2.  second list item
脚注
脚注的工作方式主要类似于参考样式的链接。脚注由两部分组成：文本中将成为上标数字的标记；将放置在文档末尾的脚注列表中的脚注定义。脚注如下所示：

That's some text with a footnote.[^1]

[^1]: And that's the footnote.
脚注定义可以在文档中的任何位置找到，但脚注将始终按照它们在文本中链接到的顺序列出。

每个脚注必须有一个不同的名称。该名称将用于将脚注引用链接到脚注定义，但对脚注的编号没有影响。id名称可以包含任何在 HTML 属性中有效的字符。

脚注可以包含块级元素，这意味着您可以在一个脚注中放置多个段落、列表、块引用等。它与列表项的工作方式相同：只需在脚注定义中将以下段落缩进四个空格：

That's some text with a footnote.[^1]

[^1]: And that's the footnote.

    That's the second paragraph.
如果您想让事情更好地对齐，您可以将脚注的第一行留空，并将您的第一段放在下面：

[^1]:
    And that's the footnote.

    That's the second paragraph.
输出
单个脚注标记可能无法满足所有人的需求，这可能是真的。未来的版本可能会提供一个编程接口以允许生成不同的标记。但是今天，输出遵循在 Daring Fireball 上可以看到的内容，稍作修改。这是上面第一个示例的默认输出：

<p>That's some text with a footnote.
   <sup id="fnref:1"><a href="#fn:1" class="footnote-ref" role="doc-noteref">1</a></sup></p>

<div class="footnotes" role="doc-endnotes">
<hr />
<ol>

<li id="fn:1" role="doc-endnote">
<p>And that's the footnote.
   <a href="#fnref:1" class="footnote-backref" role="doc-backlink">&#8617;</a></p>
</li>

</ol>
</div>
有点神秘，但在浏览器中它看起来像这样：

这是一些带脚注的文本。1

这就是脚注。 ↩

链接上的class="footnote-ref"和class="footnote-backref">属性表示它们与链接到的元素之间的关系。它们可用于使用 CSS 规则设置元素的样式，例如：

a.footnote-ref { ... }
a.footnote-backref { ... }
该role属性使可访问性工具可以理解脚注标记。有关角色定义，请参阅WAI-ARIA。

您可以自定义脚注链接和反向链接的class和title属性。有关详细信息，请参阅配置参考。

缩写
Markdown Extra 添加了对缩写的支持（HTML 标签<abbr>）。它的工作原理非常简单：创建一个这样的缩写定义：

*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
然后，在文档的其他地方，写下如下文本：

The HTML specification
is maintained by the W3C.
并且文本中这些词的任何实例都将变为：

The <abbr title="Hyper Text Markup Language">HTML</abbr> specification
is maintained by the <abbr title="World Wide Web Consortium">W3C</abbr>.
缩写是区分大小写的，并且在这样定义时将跨越多个单词。缩写也可能有一个空定义，在这种情况下，<abbr>标签将添加到文本中，但title属性将被省略。

Operation Tigra Genesis is going well.

*[Tigra Genesis]:
缩写定义可以在文档中的任何位置。它们被从最终文件中删除。

有序列表
如果有序列表以不同于 1 的数字开头，Markdown Extra 将在 HTML 输出中采用该数字。

强调
强调的规则与原来的 Markdown 语法略有不同。使用 Markdown Extra，单词中间的下划线现在被视为文字字符。下划线强调仅适用于整个单词。如果您只需要强调某个单词的一部分，仍然可以使用星号作为强调标记。

例如，有了这个：

Please open the folder "secret_magic_box".
Markdown Extra 不会将下划线转换为强调，因为它们位于单词的中间。Markdown Extra 的 HTML 结果如下所示：

<p>Please open the folder "secret_magic_box".</p>
只要您像这样强调整个单词，使用下划线强调仍然有效：

I like it when you say _you love me_.
这同样适用于强调强调：使用 Markdown Extra，您不能再使用下划线在单词中间设置强调强调，您必须使用星号作为强调标记。

## 反斜杠转义
Markdown Extra 将冒号 ( :) 和竖线 ( |) 添加到您可以使用反斜杠转义的字符列表中。这样可以防止它们触发定义列表或表格。

+ \: 冒号
+ \| 竖线

谢谢
这里实现的许多想法之前已经在Markdown 讨论列表中讨论过。我要感谢所有参与这些讨论并起草解决方案和改进 Markdown 语法的人。

[MD_basic]: /notes/基础 "Markdown基础"
[MD_syntax]: /notes/语法 "Markdown语法"

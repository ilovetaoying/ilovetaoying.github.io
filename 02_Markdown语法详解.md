# Markdown语法详解


> 2022-04-20 18:37:15 
> <br>本教程英语文档源自于JOHN GRUBER的[Daring Fireball](https://daringfireball.net/projects/markdown/basics)
> <br>本教程中文翻译由CY爱TY翻译和撰写，仅供学习交流目的。未经许可，不得擅自转载以及作为商业用途。欢迎发送电邮到<43522623@qq.com>与我交流。

+ 概述
	+ [根本思想](#根本思想)
	+ [内联 HTML](#内联-HTML)
	+ [特殊字符的自动转义](#特殊字符的自动转义)
+ 块元素
	+ [段落和换行符](#段落和换行符)
	+ [标题](#标题)
	+ [块引用](#块引用)
	+ [列表](#列表)``
	+ [代码块](#代码块)
	+ [水平线](#水平线)
+ 跨度元素
	+ [链接](#链接)
	+ [强调](#强调)
	+ [代码](#代码)
	+ [图片](#图片)
+ 其他
	+ [反斜杠转义](#反斜杠转义)
	+ [自动链接](#自动链接)

*注意：本文档本身是使用 Markdown 编写的；您可以通过在 URL 中添加“.text”来查看它的来源。*


----------

# 概述 #
## 根本思想 
Markdown 旨在尽可能地易于阅读和编写，Markdown 的语法完全由标点字符组成。最大灵感来源是纯文本电子邮件的格式。


## 内联 HTML
Markdown 的语法有一个目的：用作网络写作的一种格式。

Markdown 不是 HTML 的替代品，甚至不能和它相提并论，它的语法非常小，只对应非常小的 HTML 标记子集。编写的初衷旨在让阅读、编写和编辑散文变得容易。HTML 是一种发布格式；Markdown 是一种写作格式。因此，Markdown 的格式化语法只解决了可以用纯文本表达的问题。

对于 Markdown 语法未涵盖的任何标记，您只需使用 HTML 标签即可实现。无需任何其他声明。

唯一的限制是**块级 HTML 元素**（例如`<div>`、`<table>`、`<pre>`、`<p>`等）必须与周围的内容用空行分隔，并且块的开始和结束标记不应使用`<tab>`或`空格`缩进。Markdown不会在 HTML块级标签周围添加额外的（不需要的）标签。

例如，要将HTML表格添加到 Markdown 文章：

	这是一个常规段落。
	
	<table>
	    <tr>
	        <td>Foo</td>
	    </tr>
	</table>
	
	这是另一个常规段落。

这是一个常规段落。

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

这是另一个常规段落。

请注意，Markdown 格式化语法不会在块级HTML标记中处理。例如，您不能*emphasis*在HTML块中使用Markdown样式。

span级别的HTML标记——例如`<span>`、`<cite>`或`<del>` ——可以在 Markdown 段落、列表项或标题中的任何位置使用。如果你愿意，你甚至可以使用HTML标签代替Markdown格式；例如，如果您更喜欢使用 HTML`<a>`或`<img>`标签而不是Markdown的链接或图像语法，你可以随心所欲地使用。

与块级HTML标签不同，Markdown语法在span级的标签内运行。

## 特殊字符的自动转义
在 HTML 中，有两个字符需要特殊处理：< 和&。 Markdown 允许自然地使用这些字符，并会智能地进行所有必要的转义。如果你使用 & 符号作为HTML实体的一部分，它保持不变；否则会被翻译成`&amp`;



# 块元素 #
## 段落和换行符
段落只是一个或多个连续的文本行，由一个或多个空行分隔。（空行是任何看起来像空行的行——只包含空格或制表符的行被视为空白。）普通段落不应使用空格或制表符缩进。


## 标题
Markdown 支持两种样式的标题，Settext和atx。

Setext 样式的标题使用等号（用于一级标题）和“下划线”（用于二级标题）。任何数量的下划线=' 或-' 都可以。例如：

    这是一级标题
    =============
    
    这是二级标题
    -------------
这是一级标题
=============

这是二级标题
-------------

Atx 样式的标头在行首使用 1-6 个"#"，对应于标头级别 1-6。例如：
    
    # 这是1级标题 H1
    
    ## 这是2级标题 H2
    
    ###### 这是6级标题 H6

# 这是1级标题 H1

## 这是2级标题 H2

###### 这是6级标题 H6


## 块引用
Markdown 使用电子邮件样式的>字符进行块引用。在块元素每行开始以>开头，则会开启块引用：

> 这是一个块引用的范例。


> Markdown 允许你偷懒，只在块元素第一行使用>，也可表示块引用：

>  通过添加额外的级别，可以嵌套块引用（即块引用中的块引用）>：

> 这是第一级别引用.
>
> > 这是次级引用，以> > 开头，会缩进。
>
> 引用也可以包含和其他 Markdown 元素混合使用，包括标题、列表和代码块：

> ## 这是2级标题引用
> 
> 1.   这是第1个序列引用
> 2.   这是第2个序列引用
> 
> ### **也可以用于引用代码:**
> 
>     return shell_exec("echo $input | $markdown_script");


## 列表
Markdown 支持有序（编号）和无序（项目符号）列表。

无序列表使用*、+和-（可互换）作为列表标记：

    *   Red
    *   Green
    *   Blue
相当于：

    +   Red
    +   Green
    +   Blue
和：

    -   Red
    -   Green
    -   Blue
有序列表使用数字后跟句点：
    
    1.  Bird
	    1.  chicken
    2.  McHale
    3.  Parish
请务必注意，用于标记列表的实际数字对 Markdown 生成的 HTML 输出没有影响。

列表项可能包含多个段落。列表项中的每个后续段落必须缩进 4 个空格或一个制表符：

1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.
	
	Vestibulum enim wisi, viverra nec, fringilla in, laoreet
	vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
	sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.
但是Markdown 只需要你缩进硬段落的第一行就可以。

*   如果块引用，只需要第一行包含列表符号，后续引用需要一个`Tab`制表符加>引用符即可:

    > This is a blockquote
    > inside a list item.

*	要将代码块放在列表项中，代码块需要缩进两次——8 个空格或两个制表符：

        <code goes here>

*	*值得注意的是，下面这类内容可能会意外触发有序列表：
    
    	1986. What a great season.
换句话说，一行开头的数字-周期-空间序列。为避免这种情况，可以使用反斜杠转义句点：
	    
	    1986\. What a great season.

## 代码块
预先格式化的代码块用于编写有关编程或标记源代码的内容。Markdown 在`<pre>`和`<code>`标签中包装了一个代码块。**Markdown 中生成代码块，只需将块的每一行缩进至少 4 个空格或 1 个制表符。**例如，给定这个输入：

这是一个常规段落:

    这是一个代码块。

Markdown 将生成：

    <p>This is a normal paragraph:</p>
    
    <pre><code>This is a code block.
    </code></pre>

从代码块的每一行中删除一级缩进 - 4 个空格或 1 个制表符。例如，这个：

Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell
将变成：

    <p>Here is an example of AppleScript:</p>
    
    <pre><code>tell application "Foo"
    beep
    end tell
    </code></pre>

代码块一直持续到它到达没有缩进的行（或文章的结尾）。


## 水平线
您可以通过在一行上单独放置三个或更多-、*或_ 来生成水平线`<hr />`。也可以在连字符或星号之间使用空格。以下每一行都会产生一条水平线：
    
    * * *
    
    ***
    
    *****
    
    - - -
    
    ---------------------------------------

# 跨度元素 #
## 链接 ##
Markdown支持两种样式的链接：内联和引用。

在这两种样式中，**链接文本由 [方括号] 表示**。

要创建**内联链接**，请在链接文本中括号后立即用一组小括号。在括号内放URL，以及链接的可选标题，并用引号括起来。例如：
    
    这是[内联链接](http://example.com/ "我是内联")的例子。

这是[内联链接](http://example.com/ "我是内联")的例子。

如果指向的是同一服务器上的本地资源，可以使用相对路径：
    
    See my [About](/about/) page for details.   

**引用链接**使用第二组方括号，您可以在其中放置您选择的标签来标识链接：

    这是一个 [引用链接][id]的语法.

这是一个 [引用链接][id]的语法.

然后，在文档中的任何位置，您都可以像这样在一行上定义链接标签：
    
    [id]: http://example.com/  "Optional Title Here"
    
[id]: http://example.com/  "我是引用链接的例子"

语法：
1. 包含链接标识符的方括号（可选从左边距缩进最多三个空格）；
2. 后跟一个冒号；
3. 后跟一个或多个空格（或制表符）；
4. 后跟链接的 URL；
5. 可选地后跟链接的标题属性，用双引号或单引号括起来，或者用括号括起来。


链接 URL 可以选择用尖括号括起来：
    
    [id]: <http://example.com/>  "Optional Title Here"

您可以将 title 属性放在下一行并使用额外的空格或制表符进行填充，这对于较长的 URL 看起来会更好：
    
    [id]: http://example.com/longish/path/to/resource/here
    	"Optional Title Here"

链接定义仅用于在Markdown处理期间创建链接，并在HTML输出中从您的文档中删除。

**链接定义名称可能包含字母、数字、空格和标点符号——但它们不区分大小写。**

例如这两个链接是等价的：
>     [link text][a]
>     [link text][A]

**隐式链接**名称快捷方式允许您省略id，在这种情况下，链接文本本身用作名称。只需使用一组空方括号——例如，将“Google”这个词链接到 google.com 网站，你可以简单地写：

>     [Google][]
>然后定义链接：
    
>     [Google]: http://google.com/

链接名称中可包括空格，比如：

>    Visit [Daring Fireball][] for more information.
>然后定义链接：
>    
>    [Daring Fireball]: http://daringfireball.net/
>        
链接定义可以放在 Markdown 文档中的任何位置。推荐放在使用它们的每个段落之后，也有人习惯将它们全部放在文档的末尾，有点像脚注。

以下是实际参考链接的示例：
    
    I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].
    
      [1]: http://google.com/"Google"
      [2]: http://search.yahoo.com/  "Yahoo Search"
      [3]: http://search.msn.com/"MSN Search"

使用隐式链接名称快捷方式，您可以改为编写：
    
    I get 10 times more traffic from [Google][] than from
    [Yahoo][] or [MSN][].
    
      [google]: http://google.com/"Google"
      [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
      [msn]: http://search.msn.com/"MSN Search"
上述两个示例都将产生以下 HTML 输出：
I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].

  [1]: http://google.com/"Google"
  [2]: http://search.yahoo.com/  "Yahoo Search"
  [3]: http://search.msn.com/ "MSN Search"


## 强调 ##
- *星号包裹表示斜体*
- _下划线包裹表示斜体_：
    
>        *single asterisks*    
>        _single underscores_

- **双星号包裹表示粗体**
- __双下划线包裹也表示粗体__


**空格包围*or _**，它将被视为文字星号或下划线。

要在原本用作强调分隔符的位置生成文字星号或下划线，需要**使用\反斜杠转义**：

\*this text is surrounded by literal asterisks\*

## 代码 ##
要表示一段代码，请用反引号 ( `) 将其括起来。与预先格式化的代码块不同，代码跨度表示正常段落内的代码。例如：
    
    Use the `printf()` function.

将产生：
    
    <p>Use the <code>printf()</code> function.</p>

要在代码范围内包含反引号字符，可以使用多个反引号作为开始和结束分隔符：
    
    `` (`) 在这里。``

这将产生：
    
    <p><code>There is a literal backtick (`) here.</code></p>

围绕代码跨度的反引号分隔符可能包含空格——一个在开始之后，一个在结束之前。这允许您在代码跨度的开头或结尾放置文字反引号字符：
    
>        单个反引号表示: `` ` ``
>
>    单个反引号表示: `` ` ``
    
    A backtick-delimited string in a code span: `` `foo` ``

将产生：
    
    <p>A single backtick in a code span: <code>`</code></p>

## 图片 ##
Markdown 使用的图像语法旨在类似于链接的语法，允许两种样式：内联和引用。

内联图像语法如下所示：
    
    ![Alt text](/path/to/img.jpg)
    
    ![Alt text](/path/to/img.jpg "Optional title")

>	语法为：
>	
>	1. 感叹号：!;
>	
>	2. 后跟一组方括号，包含alt 图像的属性文本；
>	
>	3. 后跟一组括号，包含图像的 URL 或路径，以及title用双引号或单引号括起来的可选属性。

引用链接的语法：
    
    ![Alt text][id]
    
**其中“id”是定义的图像引用的名称。*

*图像引用使用与链接引用相同的语法定义：
    
    [id]: url/to/image  "Optional title attribute"

**在撰写本文时，Markdown 没有用于指定图像尺寸的语法。如果这对您很重要，您可以简单地使用常规 HTML<img>标记。**

# 其他 #
## 反斜杠转义 ##
反斜杠转义来生成文字字符，否则这些字符在 Markdown 的格式化语法中具有特殊含义。例如，如果您想用文字星号（而不是 HTML<em>标记）包围一个单词，您可以在星号之前使用反斜杠，如下所示：

\*literal asterisks\*
Markdown 为以下字符提供反斜杠转义：

\\   反斜杠

\`   反引号

\*   星号
   
\_   下划线

\{}  花括号

\[]  中括号

\()  小括号

\#   井号

\+   加号

\-   减号、连接号

\.   点

\!   感叹号


## 自动链接 ##
只需将 URL 或 电子邮件地址用尖括号括起来，即可为之创建**自动链接**。

例如:
    
    <http://example.com/>

Markdown 会将其变成：
    
    <a href="http://example.com/">http://example.com/</a>

电子邮件地址的自动链接的工作方式类似，此外 Markdown 还将执行一些随机的十进制和十六进制实体编码，以帮助从地址收集垃圾邮件机器人中隐藏邮件地址。例如，Markdown 会变成这样：
    
    <address@example.com>

实际会变成这样：
    
    <a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;
    &#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;
    &#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;
    &#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>

它将在浏览器中呈现为“地址@example.com ”的可点击链接。

（这种实体编码技巧确实会欺骗许多（但不是全部）地址收集机器人）


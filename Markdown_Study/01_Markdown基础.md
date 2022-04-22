# Markdown基础语法


> 2022-04-20 18:37:15 
> <br>本教程英语文档源自于JOHN GRUBER的[Daring Fireball](https://daringfireball.net/projects/markdown/basics)
> <br>本教程中文翻译由CY爱TY翻译和撰写，仅供学习交流目的。未经许可，不得擅自转载以及作为商业用途。欢迎发送电邮到<43522623@qq.com>与我交流。


<br>

## 段落 ##
一段话就是一行或连续多行文字内容，
 
另起一段就是当中有一个空行。


## 标题 ##
Markdown提供了两种标题h1和h2

    方法1：
    # ad #
    
    方法2：
    ad
    =

效果：

ad
=

## 块引用 ##
blockquote标签，或者使用引号按钮

<blockquote>块引用</blockquote>


> <p>This is a blockquote.</p>
> 
> <p>This is the second paragraph in the blockquote.</p>
> 
> <h2>This is an H2 in a blockquote</h2>


## 强调 ##

*星号之间内容斜体*

_下划线之间内容斜体_

    *星号之间内容斜体*
    
    _下划线之间内容斜体_

**双星号之间内容粗体**

__双下划线之间内容粗体__

    **双星号之间内容粗体**
    
    __双下划线之间内容粗体__

## 无序列表 ##
*、+、-开头表示列表项
Tab表示子项缩进

* 手机
* 手提电脑
* pad
	* Apple
	* Samsung
		* ipad1
		* ipad2

## 有序列表 ##
以数字序号开头。

1. 手机
2. 手提电脑
3. 麦克风
	1. 劳斯莱斯  

## 超链接 ##
Markdown支持两种超链接的样式： "行内链接" 和 "引用链接"
使用中括号[]将你要的链接文字包裹起来。

- **行内链接**

例如： 欢迎来到[贴易](http://www.tie-easy.com)!
>     代码：
>     欢迎来到[贴易](http://www.tie-easy.com)!

- **引用链接**
引用链接方法1是用**索引号**，允许根据索引号引用对应超链接地址，写法是正常些句子，再单独列出多个超链接地址，使用索引号一一对应起来。

例如： 我常用的搜索引擎包括[百度][1]、[谷歌][2]。
[1]: https://www.baidu.com	"百度"
[2]: https://www.google.com "谷歌"

    > 代码：
    > 我常用的搜索引擎包括[百度][1]、[谷歌][2]。
    > [1]: https://www.baidu.com	"百度"
    > [2]: https://www.google.com "谷歌"

引用链接另一种方法是用**索引名**，大小写不敏感。

例如：我们常用的搜索引擎包括[百度][Baidu]、[谷歌][Google]。
[baidu]: https://www.baidu.com	"百度"
[google]: https://www.google.com "谷歌"

    > 代码：
    > 我们常用的搜索引擎包括[百度][Baidu]、[谷歌][Google]。
    > [baidu]: https://www.baidu.com	"百度"
    > [google]: https://www.google.com "谷歌"

## 图片 ##
图片链接很像超链接"行内链接"的写法。

    > 语法：
    > ![替换文字](/img/logo.png#pic_left "标题")

语法：
![logo](/img/logo.png "Markdown笔记")

如果需要调整大小位置的，可以使用html代码。

	<img src="/img/logo.png" width="20%" align="right">

<img src="/img/logo.png" width="20%" align="right">

<br>
<br>
<br>
<br>

## 代码 ##
**使用反引号可以轻松输出指令标签。**

我强烈推荐使用 `<blink>` 表示标签.

I wish SmartyPants used named entities like `&mdash;`
instead of decimal-encoded entites like `&#8212;`.

如果你要将你的代码在html显示出来，则在代码块前加4个空格或者一个`tab`

	<blockquote>
	 	<p>举例说明</p>
	</blockquote>
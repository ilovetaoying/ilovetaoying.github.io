由于 github page 默认不支持流程图工具，所以得使用脚本渲染的方式来支持。

使用 Mermaid 工具可以让用户以类似 markdown 文本的方式创建流程图和框图。

举个例子，使用下面的 Mermaid 格式的文本将画出流程图：

    ```mermaid
        graph TD;
        A-->B;
        A-->C;
        B-->D;
        C-->D;
    ```


```mermaid
    graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

## 使用 Mermaid 方法

为了加速网页访问速度，我们只在有需要画流程图的文章中添加 mermaid 脚本支持。

在文章的开头配置

    mermaid: true

例如本篇文章的配置：
```
---
layout: post
title: Github 博客画流程图
category: how2blog
tags: [tools, study, markdown]
mermaid: true
---
```

流程图使用以下语句( 使用 typera 编辑器支持 mermaid 语法)

    ​```mermaid
    画图语句...
    ​```

## 支持 Mermaid 方法
在 html 主题模板文件的头部加入以下内容加载 mermaid 脚本（如果文章的 mermaid 配置项打开脚本加载）：
```
{% if page.mermaid %}
        <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/7.1.0/mermaid.min.js"></script>
        <script>
            var config = {
                startOnLoad:true,
                flowchart:{
                    useMaxWidth:false,
                    htmlLabels:true
                }
            };
            mermaid.initialize(config);
            $(function(){
                var elements = document.getElementsByClassName("language-mermaid");
                for (var i = elements.length; i--;) {
                    element = elements[i];
                    var graphDefinition = element.innerText;
                    if (graphDefinition) {
                        var svg = mermaid.render('ha_mermaid_' + i, graphDefinition, function(svg){});
                        if (svg) {
                            var svgElement = document.createElement('div');
                            preNode = element.parentNode;
                            svgElement.innerHTML = svg;
                            svgElement.setAttribute('class', 'mermaid');
                            svgElement.setAttribute('data-processed', 'true');
                            preNode.parentNode.replaceChild(svgElement, preNode);
                        }
                    }
                }
            });
        </script>
{% endif %}
```

<br>
<br>
<br>


# Mermaid语法

## 流程图
开头以 graph 声明，流程图的语法如下：

```
```mermaid
graph LR
  单独节点
  开始 -- 带注释写法1 --> 结束
  开始 -->|带注释写法2| 结束
  实线开始 --- 实线结束
  实线开始 --> 实线结束
  实线开始 -->|带注释| 实线结束
  虚线开始 -.- 虚线结束
  虚线开始 -.-> 虚线结束
  虚线开始 -.->|带注释| 虚线结束
  粗线开始 === 粗线结束
  粗线开始 ==> 粗线结束
  粗线开始 ==>|带注释| 粗线结束
  subgraph 子图标题
    子图开始 --> 子图结束
  end
  节点1[方形文本框] --> 节点2{菱形文本框}
  节点3(括号文本框) --> 节点4((圆形文本框))
```

显示效果如下图所示：
```mermaid
graph LR
  单独节点
  开始 -- 带注释写法1 --> 结束
  开始 -->|带注释写法2| 结束
  实线开始 --- 实线结束
  实线开始 --> 实线结束
  实线开始 -->|带注释| 实线结束
  虚线开始 -.- 虚线结束
  虚线开始 -.-> 虚线结束
  虚线开始 -.->|带注释| 虚线结束
  粗线开始 === 粗线结束
  粗线开始 ==> 粗线结束
  粗线开始 ==>|带注释| 粗线结束
  subgraph 子图标题
    子图开始 --> 子图结束
  end
  节点1[方形文本框] --> 节点2{菱形文本框}
  节点3(括号文本框) --> 节点4((圆形文本框))
```

+ 图的方向支持一下几种方式：
```
graph LR

TB - 从上到下(top buttom)
BT - 从下到上(buttom top)
LR - 从左到右(left right)
RL - 从右到左(right left)
TD - 跟 TB 相同
```
+ 三种线类型
```
--- : 实现
-.- : 虚线
=== : 粗线
```
+ 虚线带箭头的话加 > ，实线和粗线则最后一个字符替换成 >
+ 注释的两种写法(中间加注释，后边加注释)
```
-- 中间加注释写法 -->
-->|后边加注释写法|
```
+ 文本框类型
```
[] - 方形文本框
{} - 菱形文本框
() - 边角圆滑文本框
(()) - 圆形文本框
```
+ 子图
```
  subgraph 子图标题
    子图开始 --> 子图结束
  end
```
## 时序图
时序图以 `sequenceDiagram` 开头声明，语法如下所示:
```
sequenceDiagram
    participant Alice
    participant John
    Alice ->> John:  实线带箭头: ->>
    John -->> Alice: 虚线带箭头: -->>
    Alice -> John : 实线不带箭头: ->
    activate John
    Note over Alice,John: 这个注释在两个人的上方
    John --> Alice : 虚线不带箭头: -->
    deactivate John
    Alice -x John : 实线结尾带X: -x
    John --x Alice : 虚线结尾带X: --x
```
显示效果如下：
```mermaid
sequenceDiagram
    participant Alice
    participant John
    Alice ->> John:  实线带箭头: ->>
    John -->> Alice: 虚线带箭头: -->>
    Alice -> John : 实线不带箭头: ->
    activate John
    Note over Alice,John: 这个注释在两个人的上方
    John --> Alice : 虚线不带箭头: -->
    deactivate John
    Alice -x John : 实线结尾带X: -x
    John --x Alice : 虚线结尾带X: --x
```
+  参与者（participant）
```
participant 名称1
participant 名称2
participant A as Alice  : 通过 as 定义别名，后续使用 A 比较方便 
```
**注：声明的顺序与画图的顺序一致**

+ 箭头类型（一个`>`不带箭头, 两个`>`带箭头; 一个`-`实线，两个`-`虚线）

|类型|  描述   |
|--|-------|
|->|实线不带箭头 |
|–>|虚线不带箭头 |
|-»| 实线带箭头 |
|–»| 虚线带箭头 |
|-x|实线结尾带X |
|–x|虚线结尾带X |

+ 激活参与者
```
activate John    : 激活参与者
deactivate John  : 去激活参与者

也可以通过在 > 后面使用 +/- 符号表示激活和去激活，例如：

Alice->>+John: Hello John, how are you?
```

+ 注释

```
Note [ right of | left of | over ] [Actor]: Text in note content

注: Actor 可以是多个，通过逗号分割，例如：

Note over Alice,John: A typical interaction
```

+ 循环序列
```
loop 描述文本
... 时序图语句 ...
end
```

例子
```
sequenceDiagram
    Alice->John: Hello John, how are you?
    loop Every minute
        John-->Alice: Great!
    end
```

显示效果
```mermaid
sequenceDiagram
    Alice->John: Hello John, how are you?
    loop Every minute
        John-->Alice: Great!
    end
```

+ 条件时序
```
alt 描述文本
... statements ...
else
... statements ...
end
```

例子：
```
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    alt is sick
        Bob->>Alice: Not so good
    else is well
        Bob->>Alice: Feeling fresh like a daisy
    end
```

显示效果：
```mermaid
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    alt is sick
        Bob->>Alice: Not so good
    else is well
        Bob->>Alice: Feeling fresh like a daisy
    end
```

+ 可选时序
```
opt 描述文本
... statements ...
end
```

例子:

```
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    opt Extra response
        Bob->>Alice: Fine,Thanks
    end
```

显示效果

```mermaid
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    opt Extra response
        Bob->>Alice: Fine,Thanks
    end
```

## 甘特图
甘特图以 gantt 开头，用 section划分任务集，语法如下：
```
gantt
    title 甘特图的标题
    dateFormat  YYYY-MM-DD
    section Section
    A task           :a1, 2014-01-01, 30d
    Another task     :after a1  , 20d
    section Another
    Task in sec      :2014-01-12  , 12d
    another task      : 24d
```

例子：
```
gantt
       dateFormat  YYYY-MM-DD
       title Adding GANTT diagram functionality to mermaid

       section A section
       Completed task            :done,    des1, 2014-01-06,2014-01-08
       Active task               :active,  des2, 2014-01-09, 1d
       Future task               :         des3, after des2, 1d
       Future task2              :         des4, after des3, 1d

       section Critical tasks
       Completed task in the critical line :crit, done, 2014-01-06,24h
       Implement parser and jison          :crit, done, after des1, 1d
       Create tests for parser             :crit, active, 1d
       Future task in critical line        :crit, 10h
       Create tests for renderer           :1d
       Add to mermaid                      :1d

       section Documentation
       Describe gantt syntax               :active, a1, after des1, 1d
       Add gantt diagram to demo page      :after a1  , 20h
       Add another diagram to demo page    :doc1, after a1  , 8h

       section Last section
       Describe gantt syntax               :after doc1, 30h
       Add gantt diagram to demo page      :20h
```

显示效果：
```mermaid
gantt
       dateFormat  YYYY-MM-DD
       title Adding GANTT diagram functionality to mermaid

       section A section
       Completed task            :done,    des1, 2014-01-06,2014-01-08
       Active task               :active,  des2, 2014-01-09, 1d
       Future task               :         des3, after des2, 1d
       Future task2              :         des4, after des3, 1d

       section Critical tasks
       Completed task in the critical line :crit, done, 2014-01-06,24h
       Implement parser and jison          :crit, done, after des1, 1d
       Create tests for parser             :crit, active, 1d
       Future task in critical line        :crit, 10h
       Create tests for renderer           :1d
       Add to mermaid                      :1d

       section Documentation
       Describe gantt syntax               :active, a1, after des1, 1d
       Add gantt diagram to demo page      :after a1  , 20h
       Add another diagram to demo page    :doc1, after a1  , 8h

       section Last section
       Describe gantt syntax               :after doc1, 30h
       Add gantt diagram to demo page      :20h
```

## 其他
Mermaid 反意字符使用 #hex; 表示。
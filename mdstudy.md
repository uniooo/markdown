# Markdown基础学习
## Markdown

Markdown是一种轻量级标记语言，就跟HTML很像，但是没有HTML功能那么强大，但也没那么繁琐，故而很适合用来写笔记之类的东西。可以很容易地边写边控制格式，也不会担心所见即所得编辑器搞得乱七八糟的。

学习Markdown的时候建议找一个Markdown的编辑阅读器。可以实时看到Markdown写出来的效果。一些挺不错的推荐列在文末Links里。

这篇文章就是使用Markdown写出来的。(本文使用[作业部落][3]的编辑器编辑)
本文的源码可以从https://github.com/uniooo/markdown 获得

---

## Markdown的基本语法
### 标题：
Markdown提供了两种标题的写法——`Setext`样式的和`atx`样式的。
Setex样式使用底线来标识标题，用`=`（一级标题）和`-`（二级标题）：
> 一只喵

> ====
>两只喵

> \-------

(注意，`=`及`-`的数量都是任意的)
结果如下：
>一只喵
>====
>两只喵
>---

atx样式使用`#`号来标注，`#`（一级标题），`##`（二级标题），以此类推……Markdown一共提供个了六级标题:
> \# 一只喵

> \#\# 两只喵

> \#\#\# 三只喵

> \#\#\#\# 四只喵

> \#\#\#\#\# 五只喵

> \#\#\#\#\#\# 六只喵

结果如下：
> # 一只喵
> ## 两只喵
> ### 三只喵
> #### 四只喵
> ##### 五只喵
> ###### 六只喵

（注意：如果你觉得用`#`将标题闭合起来比较好看的话，也可以写成`#一只喵#`这种样子，后面的`#`数量是任意的。）

### 列表
Markdown支持无序列表（用`*`、`+`或`-`表示，可以混用，不过用一种的代码看起来比较舒服哇）和有序列表（用数字加`.`表示）
#### 无序列表
> \* 喵

> \+呜

> \- 汪

结果如下：
> * 喵
> + 呜
> - 汪

#### 有序列表
目前，有序列表前面的数字是可以乱写的，如下面所写的：
> 13\. 喵

> 250\. 呜

> 65536\. 汪

结果如下：
> 13. 喵
> 250. 呜
> 65536. 汪

但是不推荐这么写哇。毕竟看源码的时候会觉得这是多么二百五&十三点的行为。

### 链接
Markdown有两种形式的链接——`行内式` & `参考式`。
#### 行内式：
格式如：`[显示的文字](URL)` 或者：`[显示的文字](URL "title")`
例如：
> \[Baidu\](http://www.baidu.com)

> \[Baidu\](http://www.baidu.com "Baidu")

结果如下：
> [Baidu](http://www.baidu.com)
> [Baidu](http://www.baidu.com "Baidu")

#### 参考式：
格式为：
`[显示的文字][id]`
`[id]:URL`
例如：
> \[Markdown: Syntax\]\[1\]

> \[1\]:http://daringfireball.net/projects/markdown/syntax

结果就不演示啦，本文后面所附的链接就是使用的这种方式。

### 图片
插入图片和插入链接很像，不过是把前面的`[]`替换为`![]`就好了。
形如（参考自[Markdown: Syntax][1]）：
>!\[Alt text](/path/to/img.jpg)

>\!\[Alt text](/path/to/img.jpg "Optional title")


### 分割线
在一行中，用三个以上的`*`、`-`或者`_`表示分割线。中间可以有空格间隔。
例如：
> \---

> \***

都可以，本文中的分割线就是使用的`---`。

### 强调
Markdown使用`*`或者`—`来表示强调。
被`*`或者`_`包起来的效果如同HTML中`<em>`标签(通常是斜体)。
被`**`或者`__`包起来的效果如同HTML中的`<strong>`标签（通常是加粗）。
例如：
> \*emphasis\*

> \**strong\**

结果如下：

> *emphasis*
> **strong**

### 转义字符
Markdown中有类似C中字符串里的转意字符的`\`，用于显示Markdown中具有特殊含义的符号，比如之前的`#`、`>`等。`\`也可以用来转义自己，比如`\\`显示的是`\`
例如：
> \\# 喵呜

> \\\ 喵呜

结果如下：
> \# 喵呜
> \\ 喵呜

### 代码
利用 `` ` `` (反引号) 来引用代码，显示标注出来的东西。用反引号括起来的东西会被Markdown的解释器转成`<code>`标签括起来的样式。本文中好多地方那它来做标注。
注意：如果要在反引号中插入反引号，可以用 ``` `` ` `` ```这样的形式，注意中间的空格。

### 区块引用
Markdown使用`>`符号表示区块引用。也就是显示出我上面举例子、写结果的的地方的样子。
`>`的里面还可以嵌套`>`。
>>>> miaowu


### 代码区块
Markdown里面，以四个空格，或者一个制表符，作为开头的段落被认为是代码区块。（注意要与前面的段落隔开一行）
例如：

    sudo apt-get install firefox
   
---

## 其他
### 自动链接
Markdown 提供了自动链接的方式书写超级链接和邮箱地址，使用`<`符号括起地址区域：
> <p>&lthttp://www.baidu.com&gt</p>
> <p>&ltkarljk@sina.com&gt </p> 

但是貌似并非所有的Markdown解释器对此都有很好的支持。大多数解释器可以直接将URL翻译成链接，而不需要`<>`。同时，部分解释器无法解释`<>`括起来的email地址。

### 内嵌HTML代码
Markdown支持内嵌HTML代码

Markdown着重提供内容。样式之类的东西则交由解释器等来实现。如果要实现一些特殊的样式，或者Markdown本身无法实现的东西，可以考虑利用内嵌HTML的方式来实现。
例如：
> <p style="color:red"> 喵呜，这句话永远是红色的。 </p>

###代码染色
大多数Markdown解释器支持代码的染色。
可以使用`` ```ProgramLanguage ``的方式来标注染色代码段的开始，
用`` ``` ``标注结尾。
如：

> \```cpp
    #include <iostream>
    using namespace std;
    int main()
    {
        printf("Hello Markdown!");
    }
> \```

结果显示：
```cpp
    #include <iostream>
    using namespace std;
    int main()
    {
        printf("Hello Markdown!");
    }
```
###表格支持
Markdown原生木有带表格，所以建议使用HTML来写。
部分解释器支持如下的写法：
```
A0 | B0 | C0
---|----|---
A1 | B1 | C1
A2 | B2 | C2
A3 | B3 | C3
```
显示为：
A0 | B0 | C0
---|----|---
A1 | B1 | C1
A2 | B2 | C2
A3 | B3 | C3

---
##Links:
### Markdown语法介绍：
[Markdown: Syntax][1]
[Markdown 语法说明(简体中文版)][2]
### Markdown在线编辑器：
[作业部落][3]
[简书][4]
[MaHua][5]
[Dillinger][6]
[StackEdit][7]
### Markdown编辑器下载：
[Markpad][9]
[MarkdownPad][10]

[1]:http://daringfireball.net/projects/markdown/syntax
[2]:http://wowubuntu.com/markdown/
[3]:http://www.zybuluo.com
[4]:http://jianshu.io/
[5]:http://mahua.jser.me/
[6]:http://dillinger.io/
[7]:https://stackedit.io/
[9]:http://code52.org/DownmarkerWPF/
[10]:http://www.markdownpad.com/

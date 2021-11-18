# XML

###### 独立于软件和硬件的信息传输工具。

* XML 指可扩展标记语言（EXtensible Markup Language）。
* XML 是一种很像HTML的标记语言。
* XML 的设计宗旨是传输数据，而不是显示数据，被设计用来结构化、存储以及传输信息。
* XML 标签没有被预定义，需要自行定义标签。
* XML 被设计为具有自我描述性，包含了发送者和接受者的信息，同时拥有标题以及消息主体。

#### XML树结构

* XML 文档必须包含根元素。
* 根元素是所有其他元素的父元素。
* XML 文档中的元素形成了一棵文档树。这棵树从根部开始，并扩展到树的最底端。
* 所有的元素都可以有子元素。

#### XML语法规则

1. 必须有根元素

2. 可选的xml声明，如`<?xml version="1.0" encoding="utf-8"?>`   ?

3. 所以XML元素都必须有一个关闭标签，不可省略

4. 声明不属于XML文档本身的一部分，它没有关闭标签

5. 大小写敏感

6. 必须正确嵌套

7. 属性**必须**加引号（单引号、双引号均可）

8. 实体引用
   | 实体引用 | 符号 |
   | -------- | ---- |
   | &lt      | <    |
   | &gt      | >    |
   | &amp     | &    |
   | &apos    | '    |
   | &quot    | "    |

9. 注释`<!-- This is a comment -->`

10. 不同于HTML，XML保留空格

11. 用换行符(LF)储存换行

#### XML元素

> XML 元素指的是从（且包括）开始标签直到（且包括）结束标签的部分。
>
> 一个元素可以包含：
>
> * 其他元素
> * 文本
> * 属性
> * ……

#### 命名规则

* 名称可以包含字母、数字以及其他的字符
* 名称**不能以数字或者标点符号开始**
* 名称**不能以字母 xml（或者 XML、Xml 等等）开始**
* 名称**不能包含空格**
* 可使用任何名称，**没有保留的字词**。

> 避免 "-" 字符。"first-name"，一些软件会认为要从 first 里边减去 name。

> 避免 "." 字符。"first.name"，一些软件会认为 "name" 是对象 "first" 的属性。

> 避免 ":" 字符。冒号会被转换为命名空间来使用

XML 文档经常有一个对应的数据库，其中的字段会对应 XML 文档中的元素。

#### XML属性

> 属性通常提供不属于数据组成部分的信息

属性难以阅读和维护。请尽量使用元素来描述数据。

元数据（有关数据的数据）应当存储为属性，而数据本身应当存储为元素。

#### XML验证

e.g. `<!DOCTYPE note SYSTEM "Note.dtd">`

DOCTYPE 声明是对外部 DTD 文件的引用

DTD 的目的是定义 XML 文档的结构。它使用一系列合法的元素来==定义文档结构==

e.g.

~~~xml-dtd
<!DOCTYPE note
[
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
]>
~~~

> W3C 支持一种基于 XML 的 DTD 代替者，XML Schema
>
> e.g.
>
>~~~xml
><xs:element name="note">
>
><xs:complexType>
><xs:sequence>
><xs:element name="to" type="xs:string"/>
><xs:element name="from" type="xs:string"/>
><xs:element name="heading" type="xs:string"/>
><xs:element name="body" type="xs:string"/>
></xs:sequence>
></xs:complexType>
>
></xs:element>
>~~~



#### 用CSS修饰XML

直接通过标签名设置样式。

默认行内元素

#### 使用 XSLT 显示 XML

XSLT 是在浏览器显示 XML 文件之前，先把它转换为 HTML

#### XMLHttpRequest 对象

* 在不重新加载页面的情况下更新网页
* 在页面已加载后从服务器请求数据
* 在页面已加载后从服务器接收数据
* 在后台向服务器发送数据

创建 XMLHttpRequest 对象的语法：`xmlhttp=new XMLHttpRequest();`

#### XML Parser

> XML 解析器把 XML 文档转换为 XML DOM 对象 ——可通过 JavaScript 操作的对象。

#### XML DOM

DOM（Document Object Model 文档对象模型）定义了访问和操作文档的标准方法。

#### XML 命名空间

###### 使用前缀来避免命名冲突

在 XML 中的命名冲突可以通过使用名称前缀从而容易地避免。

e.g.

~~~xml
<h:table>
<h:tr>
<h:td>Apples</h:td>
<h:td>Bananas</h:td>
</h:tr>
</h:table>

<f:table>
<f:name>African Coffee Table</f:name>
<f:width>80</f:width>
<f:length>120</f:length>
</f:table>
~~~

###### xmlns 属性

当在 XML 中使用前缀时，一个所谓的用于前缀的命名空间必须被定义。

命名空间是在元素的开始标签的 **xmlns 属性**中定义的。

可以在他们被使用的元素中或者在 XML 根元素中声明，命名空间声明的语法如下：

xmlns:前缀="URI"。

~~~xml
<root>

<h:table xmlns:h="http://www.w3.org/TR/html4/">
<h:tr>
<h:td>Apples</h:td>
<h:td>Bananas</h:td>
</h:tr>
</h:table>

<f:table xmlns:f="http://www.w3cschool.cc/furniture">
<f:name>African Coffee Table</f:name>
<f:width>80</f:width>
<f:length>120</f:length>
</f:table>

</root>


<root xmlns:h="http://www.w3.org/TR/html4/"
xmlns:f="http://www.w3cschool.cc/furniture">
//…………
</root>
~~~

命名空间 URI 不会被解析器用于查找信息，其目的是赋予命名空间一个惟一的名称。

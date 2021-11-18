# PHP

### 简介

> 一种服务器端的HTML，脚本/编程语言，面向对象的、解释性的。

###### 静态网站

* 易被检索
* 独立文件
* 没有数据库支持
* 交互性差

###### 动态网站

* 交互性
* 自动更新

### 网站的基本概念

###### 服务器

> 能够提供服务的机器，取决于机器上安装的软件（服务软件）。

web服务器：提供web服务（网站访问）。

###### IP

> 网络之间的互联协议，__为计算机网络互相连接进行通信而设计的协议__。

> IP地址具有唯一性。
>
> > 特殊IP：127.0.0.1 本机



###### 域名

> Internet上某一台计算机或计算机组的名称。
>
> > 特殊域名：localhost 本机

###### DNS

> 域名系统

###### 端口

> 设备与外界通讯交流的出口。

* 虚拟端口（计算机内部或交换机路由器的端口，不可见）

  区分访问的软件（？

  > 用户输入域名localhost:端口

* 物理端口（接口）

### web程序访问流程

> 浏览器发起访问--》DNS解析域名--》服务器电脑--》服务软件

###### 静态网站

![](D:\txy\University\New_Thread\GEEK\笔记\静态网站访问.JPG)

###### 动态网站

![](D:\txy\University\New_Thread\GEEK\笔记\动态网站访问.JPG)

###### 站点根目录

http://localhost/

http://laocalhost/index.php

同样的效果

访问某个文件夹，默认访问文件夹下的index.php或index.html

### 基础语法

##### 1.  `<?php ?>`之间为PHP代码

   * PHP代码可以嵌入到HTML代码中，但需要是一个PHP文件

   * 文件结尾处的`?>`可以省略，`?>`隐含`;`

   * 结构定义语句后无需使用分号，功能执行语句必须以分号结尾。

   * 注释
     * 单行`//`
     * 多行`/**/`
   * 空白符无任何影响

##### 2.  变量

   * 变量不需要声明

   * 变量使用：`$变量名`

   * ~~~php
     <?php
         $a=5;
         $b=6;
         $c=$a+$b;
         echo $c;
         ?>
     //输出结果为
     /*
     11
     */
     ~~~

   * 变量名不能包含空格，区分大小写

   * 弱类型语言

   * 变量作用域

     * local

     * global 在函数中访问__全局变量__

     * static 每次调用该函数时，该变量将会**保留着函数前一次被调用时的值**

     * parameter（参数）

     * ~~~php
       <?php
       $x=5; // 全局变量
       
       function myTest()
       {
           $y=10; // 局部变量
           echo "<p>测试函数内变量:<p>";
           echo "变量 x 为: $x";
           echo "<br>";
           echo "变量 y 为: $y";
       } 
       
       myTest();
       
       echo "<p>测试函数外变量:<p>";
       echo "变量 x 为: $x";
       echo "<br>";
       echo "变量 y 为: $y";
       ?>
       //输出结果为
       /*
       测试函数内变量:
       
       
       Notice: Undefined variable: x in D:\www\study\test.php on line 8
       变量 x 为:
       变量 y 为: 10
       
       测试函数外变量:
       
       变量 x 为: 5
       
       Notice: Undefined variable: y in D:\www\study\test.php on line 18
       变量 y 为:
       */
       ~~~

     * ~~~php
       <?php
       $x=5;
       $y=10;
       function myTest()
       {
           global $x,$y;
           $y=$x+$y;
       }
       myTest();
       echo $y; 
       ?>
       //输出结果为
       /*
       15
       */
           
       <?php
       $x=5;
       $y=10;
       function myTest()
       {
           $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
       } 
       myTest();
       echo $y;
       ?>
       ~~~

     * PHP 将所有全局变量存储在一个名为 `$GLOBALS[index] `的数组中。` index`保存变量的名称。这个数组可以在函数内部访问，也可以直接用来更新全局变量。

     * ~~~php
       <?php
       function myTest($x)//有参数的函数
       {
           echo $x;//参数为局部变量
       }
       myTest(5);
       ?>
       ~~~

     * 

##### 3. 基础指令

   * 输出`echo`，`print`
   
     * `echo`可以输出一个或多个字符串，无返回值
       * 语言结构
       
       * `echo`或`echo()`
       
       * 用`,`分隔字符串
       
       * 解释内嵌的变量和转义符号——不带引号（输出变量）与带双引号；
       
       不解释内嵌的变量和转义符号——带单引号。
   * `print`输出一个字符串，返回值总为1
     * 语言结构
     * `print`或`print()`

   > echo输出速度更快。字符串可以包含HTML标签。

   * EOF使用
   
     `PHP EOF(heredoc)`是一种在命令行`shell`（如`sh`、`csh`、`ksh`、`bash`、`PowerShell`和`zsh`）和程序语言（像`Perl`、`PHP`、`Python`和`Ruby`）里定义一个字符串的方法。
   
     * 必须后接`;`
     
     * EOF可以用任意其它字符代替，需保证结束标识与开始标识一致。
     
     * 结束标识必须__定格独占一行__，前后不能衔接任何空白和字符。
     
     * 当内容需要内嵌引号时，不需要加转义符，本身对单双引号转义
     
     * 位于开始标记和结束标记之间的变量可以被正常解析，但是函数则不可以。
     
     * 在` heredoc `中，变量不需要用连接符` . `或` , `来拼接。
     
     * `<<<EOF   EOF`
     
     * 开始标识可以不带引号或带单双引号；
     
       不带引号与带双引号效果一致，解释内嵌的变量和转义符号；
     
       带单引号则不解释内嵌的变量和转义符号。
     
     * ~~~php
       //开始标识带单引号；
       <?php
       $name="runoob";
       $a=<<<'EOF'
               'abc$name'
               "123"
       EOF;
       // 结束需要独立一行且前后不能空格
       echo "$a";
       ?>
       //'abc$name' "123"
           
       //开始标识可以不带引号或带双引号；
       <?php
       $name="runoob";
       $a=<<<EOF
               'abc$name'
               "123"
       EOF;
       // 结束需要独立一行且前后不能空格
       echo "$a";
       ?>
       //'abcrunoob' "123"
       <?php
       $name="runoob";
       $a=<<<"EOF"
               'abc$name'
               "123"
       EOF;
       // 结束需要独立一行且前后不能空格
       echo "$a";
       ?>
       //'abcrunoob' "123"
       ~~~



##### 4. 数据类型

> var_dump() 函数返回变量的数据类型和值

* 整型

  * ~~~php
    <?php 
    $x = 5985;
    var_dump($x);
    echo "<br>"; 
    $x = -345; // 负数 
    var_dump($x);
    echo "<br>"; 
    $x = 0x8C; // 十六进制数
    var_dump($x);
    echo "<br>";
    $x = 047; // 八进制数
    var_dump($x);
    ?>
    ~~~

  * 可正可负

  * 八进制/十进制/十六进制

* 浮点型

  * ~~~php
    <?php 
    $x = 10.365;
    var_dump($x);
    echo "<br>"; 
    $x = 2.4e3;
    var_dump($x);
    echo "<br>"; 
    $x = 8E-5;
    var_dump($x);
    ?>
    ~~~

  * 

* 字符串

  * ~~~php
    <?php 
    $x = "Hello world!"; 
    $y = 'Hello world!';
    ?>
    ~~~

  * 

* 布尔型

  * `true` or `false`

* 数组

  * ~~~php
    <?php 
    $cars=array("Volvo","BMW","Toyota");
    var_dump($cars);
    ?>
    //array(3) { [0]=> string(5) "Volvo" [1]=> string(3) "BMW" [2]=> string(6) "Toyota" }
    ~~~

  * 

* 对象

  * 在 PHP 中，对象必须声明。

  * ~~~php
    //类的定义
    <?php
    class Car
    {
      var $color;
      function __construct($color="green") {
        $this->color = $color;
      }
      function what_color() {
        return $this->color;
      }
    }
    ?>
    ~~~

* NULL

  * 数据类型为NULL
  * 表示变量没有值
  * 可以通过设置变量值为 NULL 来清空变量数据

##### 5. 类型比较

* 松散比较：使用两个等号`==`比较，只比较值，不比较类型。

* 严格比较：用三个等号` === `比较，除了比较值，也比较类型。

* ~~~php
  <?php
  if(42 == "42") {
      echo '1、值相等';
  }
   
  echo PHP_EOL; // 换行符
   
  if(42 === "42") {
      echo '2、类型相等';
  } else {
      echo '3、类型不相等';
  }
  ?>
  //1、值相等 3、类型不相等
  ~~~

* > PHP中 比较 0、false、null、“0”、“”
  >
  > ~~~php
  > 0 == false: bool(true)
  > 0 === false: bool(false)
  > 
  > 0 == null: bool(true)
  > 0 === null: bool(false)
  > 
  > false == null: bool(true)
  > false === null: bool(false)
  > 
  > "0" == false: bool(true)
  > "0" === false: bool(false)
  > 
  > "0" == null: bool(false)
  > "0" === null: bool(false)
  > 
  > "" == false: bool(true)
  > "" === false: bool(false)
  > 
  > "" == null: bool(true)
  > "" === null: bool(false)
  > ~~~

##### 6. PHP常量

* 常量是一个简单值的标识符。该值在脚本中不能改变。

* 常量名不需要加 $ 修饰符。

* 常量在整个脚本中都可以使用。

* 设置常量，使用 define() 函数

  ~~~php
  //bool define ( string $name , mixed $value [, bool $case_insensitive = false ] )
  define("GREETING", "hello world!");
  define("PI", 3.14);
  ~~~

* name：必选参数，常量名称，即标志符。
  value：必选参数，常量的值。
  case_insensitive ：可选参数，如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的。

##### 7. 字符串变量

* 并置运算符
  并置运算符 `.` 用于把两个字符串值连接起来。

  > `,`也可以

* strlen() 函数
  返回字符串的长度（字节数）。

* strpos() 函数
  在字符串内查找一个字符或一段指定的文本。

  如果在字符串中找到匹配，该函数会返回第一个匹配的字符位置。

  如果未找到匹配，则返回 FALSE。

##### 8. 逻辑运算符

* 与
  * &&
  * and
* 或
  * or
  * ||
* 异或
  * xor
* 非
  * ！

##### 9. 三元运算符

```php
(expr1) ? (expr2) : (expr3) 
//true返回expr2，false返回expr3
(expr1) ?  (expr3) 
////true返回expr1，false返回expr3
```

##### 10. 组合比较符

~~~php
$c = $a <=> $b;
//如果 $a > $b, 则 $c 的值为 1。
//如果 $a == $b, 则 $c 的值为 0。
//如果 $a < $b, 则 $c 的值为 -1。
~~~

##### 11. 数组

* ~~~php
  <?php
  $cars=array("Volvo","BMW","Toyota");
  echo "I like " . $cars[0] . ", " . $cars[1] . " and " . $cars[2] . ".";
  ?>
  //通过array()函数创建数组
  ~~~

* 获取数组长度

  ~~~php
  echo count($cars);//count()
  ~~~

* 遍历数组

  通过for循环

* 关联数组

  ~~~php
  $age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
  
  $age['Peter']="35";
  $age['Ben']="37";
  $age['Joe']="43";
  ~~~

* 用foreach循环遍历关联数组

  ~~~PHP
  <?php
  $age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
   
  foreach($age as $x=>$x_value)
  {
      echo "Key=" . $x . ", Value=" . $x_value;
      echo "<br>";
  }
  ?>
      
  <?php
  $x=array("Google","Runoob","Taobao");
  foreach ($x as $value)
  {
      echo $value . PHP_EOL;
  }
  ?>
  ~~~



##### 12. 排序

* ~~~php
  sort()//对数组进行升序排列
  rsort()//对数组进行降序排列
      
  asort()//根据关联数组的值，对数组进行升序排列
  ksort()//根据关联数组的键，对数组进行升序排列
  arsort()//根据关联数组的值，对数组进行降序排列
  krsort()//根据关联数组的键，对数组进行降序排列
  ~~~



##### 13. 超级全局变量

* $GLOBALS

  $GLOBALS 是一个包含了全部变量的全局组合数组。变量的名字就是数组的键。

  `$GLOBALS['x']`

* $_SERVER

  一个包含了诸如头信息(header)、路径(path)、以及脚本位置(script locations)等等信息的数组

  ~~~php
  <?php 
  echo $_SERVER['PHP_SELF'];
  echo "<br>";
  echo $_SERVER['SERVER_NAME'];
  echo "<br>";
  echo $_SERVER['HTTP_HOST'];
  echo "<br>";
  echo $_SERVER['HTTP_REFERER'];
  echo "<br>";
  echo $_SERVER['HTTP_USER_AGENT'];
  echo "<br>";
  echo $_SERVER['SCRIPT_NAME'];
  ?>
  ~~~

  

* $_REQUEST

  用于收集HTML表单提交的数据。

  ~~~php+HTML
  <html>
  <body>
   
  <form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
  Name: <input type="text" name="fname">
  <input type="submit">
  </form>
   
  <?php 
  $name = $_REQUEST['fname']; 
  echo $name; 
  ?>
   
  </body>
  </html>
  ~~~

  

* $_POST

  收集表单数据，在HTML form标签的指定该属性："method="post"。

* $_GET

  收集表单数据，在HTML form标签的指定该属性："method="get"。

* $_FILES

* $_ENV

* $_COOKIE

* $_SESSION

##### 14. 函数

~~~php
<?php
function functionName()
{
    // 要执行的代码
}
?>
~~~



##### 15.魔术常量

* `__LINE__`

  文件中的当前行号

* `__FILE__`

  文件的完整路径和文件名；

  如果在被包含文件中，则返回被包含的文件名。

* `__DIR__`

  文件所在目录；

  如果用在被包括文件中，则返回被包括的文件所在的目录。

  * 等价于 `dirname(__FILE__)`

* `__FUNCITON__`

  函数名称。

* `__CLASS__`

  返回该类被定义时的名字（区分大小写）。

  * 对 `trait` 也起作用。当用在` trait `方法中时，`__CLASS__ `是调用 trait 方法的类的名字

* `__TRAIT__`

  Trait 的名字。

  >自 PHP 5.4.0 起，PHP 实现了代码复用的一个方法，称为 traits。
  >
  >Trait 名包括其被声明的作用区域。

  >php从以前到现在一直都是单继承的语言，无法同时从两个基类中继承属性和方法，为了解决这个问题，php出了Trait这个特性；
  >
  >用法：通过在类中使用use 关键字，声明要组合的Trait名称，具体的Trait的声明使用Trait关键词，Trait不能实例化。
  >
  >~~~php
  ><?php
  >trait Dog{
  >    public $name="dog";
  >    public function bark(){
  >        echo "This is dog";
  >    }
  >}
  >class Animal{
  >    public function eat(){
  >        echo "This is animal eat";
  >    }
  >}
  >class Cat extends Animal{
  >    use Dog;
  >    public function drive(){
  >        echo "This is cat drive";
  >    }
  >}
  >$cat = new Cat();
  >$cat->drive();
  >echo "<br/>";
  >$cat->eat();
  >echo "<br/>";
  >$cat->bark();
  >?>
  >~~~
  >
  >

  > Trait中的方法会覆盖 基类中的同名方法，而本类会覆盖Trait中同名方法

  >一个类可以组合多个Trait，通过逗号相隔，如下
  >`use trait1,trait2`
  >
  >当不同的trait中，却有着同名的方法或属性，会产生冲突，可以使用`insteadof`或 `as`进行解决，`insteadof `是进行替代，而`as`是给它取别名
  >
  >
  >
  >`as `还可以修改方法的访问控制
  >
  >~~~php
  >class Dog{
  >    use Animal{
  >        eat as protected;
  >    }
  >}
  >~~~
  >
  >

* `__METHOD__`

  类的方法名，返回该方法被定义时的名字（区分大小写）。

* `__NAMESPACE__`

  当前命名空间的名称。

##### 16.命名空间

* 解决问题

  * 用户编写的代码与PHP内部的类/函数/常量或第三方类/函数/常量之间的名字冲突。
  * 为很长的标识符名称(通常是为了缓解第一类问题而定义的)创建一个别名（或简短）的名称，提高源代码的可读性。

* 定义

  * 默认情况下，所有常量、类和函数名都放在全局空间下。

  * 命名空间通过关键字`namespace `来声明。如果一个文件中包含命名空间，它必须在其它所有代码之前声明命名空间。

  * 可以在同一个文件中定义不同的命名空间代码。

    ~~~PHP
    <?php
    namespace MyProject {
        const CONNECT_OK = 1;
        class Connection { /* ... */ }
        function connect() { /* ... */  }
    }
    
    namespace AnotherProject {
        const CONNECT_OK = 1;
        class Connection { /* ... */ }
        function connect() { /* ... */  }
    }
    ?>
    ~~~

  * 将全局的非命名空间中的代码与命名空间中的代码组合在一起，只能使用大括号形式的语法。

    全局代码必须用一个不带名称的 `namespace `语句加上大括号括起来。

  * 在声明命名空间之前唯一合法的代码是用于**定义源文件编码方式**的__declare 语句__。

  * 子命名空间
    与目录和文件的关系很像，PHP 命名空间也允许指定层次化的命名空间的名称。

    因此，命名空间的名字可以使用分层次的方式定义：

    ~~~php
    <?php
    namespace MyProject\Sub\Level;  //声明分层次的单个命名空间
    const CONNECT_OK = 1;
    class Connection { /* ... */ }
    function Connect() { /* ... */  }
    ?>
    ~~~

    

### 表单

> 处理 HTML 表单时，PHP 能把来自 HTML 页面中的表单元素自动变成可供 PHP 脚本使用。

##### PHP 获取下拉菜单的数据

**PHP表单验证**

###### `$_SERVER["PHP_SELF"] `变量

`$_SERVER["PHP_SELF"]`是超级全局变量，返回当前正在执行脚本的文件名，与 document root相关。

~~~php
//指定以下表单文件名为 "test_form.php":
<form method="post" action="<?php echo $_SERVER["PHP_SELF"];?>">
    
//现在，我们使用URL来指定提交地址 "test_form.php",以上代码修改为如下所示:
<form method="post" action="test_form.php">

//但是，考虑到用户会在浏览器地址栏中输入以下地址:
http://www.runoob.com/test_form.php/%22%3E%3Cscript%3Ealert('hacked')%3C/script%3E
//该地址替换action=""引号中的内容，利用了$_SERVER["PHP_SELF"]

//以上的 URL 中，将被解析为如下代码并执行：
<form method="post" action="test_form.php/"><script>alert('hacked')</script>">
~~~

`$_SERVER["PHP_SELF"] `可以通过 `htmlspecialchars() `函数来避免被利用。

验证

`preg_match()`进行正则表达式匹配。

~~~PHP
//语法：
int preg_match ( string $pattern , string $subject [, array $matches [, int $flags ]] )
//在 subject 字符串中搜索与 pattern 给出的正则表达式相匹配的内容。
//如果提供了 matches ，则其会被搜索的结果所填充。
//$matches[0] 将包含与整个模式匹配的文本，$matches[1] 将包含与第一个捕获的括号中的子模式所匹配的文本，以此类推。
//e.g.
$name = test_input($_POST["name"]);
if (!preg_match("/^[a-zA-Z ]*$/",$name)) {
  $nameErr = "只允许字母和空格"; 
}
~~~

`$_GET `变量
预定义的 `$_GET `变量用于收集来自 `method="get"` 的表单中的值。

从带有 GET 方法的表单发送的信息，对任何人都是可见的（会显示在浏览器的地址栏），并且对发送信息的量也有限制。

`$_POST` 变量
预定义的` $_POST `变量用于收集来自 `method="post" `的表单中的值。

从带有 POST 方法的表单发送的信息，对任何人都是不可见的（不会显示在浏览器的地址栏），并且对发送信息的量也没有限制。

> 默认情况下，POST 方法的发送信息的量最大值为 8 MB（可通过设置 php.ini 文件中的 post_max_size 进行更改）。

`$_REQUEST `变量
预定义的 `$_REQUEST` 变量包含了` $_GET`、`$_POST `和` $_COOKIE` 的内容。

`$_REQUEST `变量可用来收集通过` GET` 和 `POST `方法发送的表单数据。
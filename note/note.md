#### 2021.11.7

##### 大数据第一课

1T(太) = 1024G 1P(拍) = 1024T 1E(艾) = 1024P 1Z(泽) = 1024Z

1Y(尧) = 1024Z 1B(布) = 1024Y 1N(诺) = 1024B 1D(刀) = 1024N

##### 大数据概念

大数据，是指无法在一定时间范围内用常规软件工具进行捕捉、管理和处理的数据集合，是需要新处理模式才能具有更强的决策力、洞察发现力和流程优化能力的海量、高增长率和多样化的信息资产

##### 大数据的特点

大，多，值，快，信

大：数据的采集，计算，存储量都非常庞大，是数据体量巨大

多：种类和来源多样化，种类有：结构化、半结构化和非结构化数据等，常见的来源有：网络日志、音频、视频、图片等等。

值：大数据价值密度相对较低

快：数据增长速度快，处理速度也快，获取数据的计算也要快

信：数据的准确性和可信赖度，即数据的质量

##### 大数据的应用场景

电商方面

传媒方面

金融方面

交通方面

电信方面

安防方面

医疗方面

##### 大数据业务分析基本步骤

1、明确分析目的和思路·

2、数据采集

3、数据处理

4、数据分析

5、数据展现

6、报告撰写

mobastorm password:123qwe

---

### 2021.11.8

##### 大数据第二课

###### 解压 tar.gz

```shell
tar -zxvf snappy.tar.gz #默认解压到当前目录
tar -xvf snappy.tar.gz #默认解压到当前目录,不指定解压方式
tar -xvf snappy.tar.gz -C /opt #将压缩包解压到/opt目录下
```

###### 解压zip

```shell
unzip snappy.zip #默认解压到当前目录
unzip -d /opt snappy.zip #解压到指定文件夹
```

###### 压缩tar.gz

```shell
tar -czvf snappy.tar.gz snappy #将snappy文件夹进行打包压缩,z参数为压缩参数
```

###### 压缩zip

```shell
zip -r snappy.zip snappy #将snappy文件夹进行打包压缩
```

###### find指令

```shell
fing / -name 'ins*' #查找/目录下以文件名ins开头的文件
find / -type f -size +100M #查找/目录下文件大小大于100M的文件
```

###### grep指令

```shell
grep lang anaconda-ks.cfg #在文件中查找lang
grep a anaconda-ks.cfg --color #在文件中查找a 高亮显示
```

###### 用户管理指令

```shell
useradd gkjuanmao #创建用户
password 123456
userdel -r gkjuanmao #删除用户
```

---

### 2021.11.9

##### vim

```shell
yy #复制一行
2yy #复制两行
p #粘贴
u #撤销
dd #删除
5dd #删除5行
gg #回到文件顶部
G #回到文件末尾
/str #查找str
:x #保存退出
shift + z + z #保存退出
:%s/Hello/Haha #将Hello改成Haha
```

##### 数据库

###### sql分类

数据定义语言：简称DDL，用来定义数据库对象：数据库，表，列等。关键字：creat,alter,drop等

数据操作语言：简称DML，用来对数据库中表的记录进行更新。关键字：insert,delete,update等

数据控制语言：简称DCL，用来定义数据库的访问权限和安全级别，及创建用户。

数据查询语言：简称DQL，用来查询数据库中表的记录。关键字：select,from,where等

##### sql中的数据类型

整型：tinyint,int,bigint

浮点型：float,double,decimal(10,,2)

日期类型：data,datatime

文本二进制类型：char,varchar

##### 创建数据库

```mysql
create database bigdata_db; #直接创建数据库，如果存在则报错
create database if not exists bigdata_db; #如果数据库不存在则创建
create database bigdata_db character set utf8; #创建数据库时设置字符集
```

查看当前使用数据库

```mysql
select database();
```

---

### 2021.11.10

#### DDL

#### 创建分类表

```mysql
create table category(cid varchar(20) primary key, cname varchar(100)); #primary key 代表唯一主键，不可重复,不能为空
```

#### 查看表结构

```mysql
desc tablename; #查看表结构
```

#### 给表添加列

```mysql
alter table tablename add  `desc` varchar(200); #给表添加列，注意反引号
```

#### 修改表列名

```mysql
alter table tablename change `desc` description varchar(30);
```

#### 删除列

```mysql
alter table tablename drop description;
```

#### 修改表名

```mysql
rename table tablename1 to tablename2;
```

#### DML

#### 插入表数据

```mysql
insert into category (field1,field2,field3) values (value1,value2,value3);
insert into tablename values (value1,value2,value3); #除了数值类型的之外，其他类型的值需要用引号括起来，插入空值可以不写字段或者插入null
```

#### 更新表数据

```mysql
update tablename set field = values where list = values;
```

#### 删除记录

```mysql
delete from tablename where list = value;
```

#### 清空表

```mysql
truncate tablename; #直接将表删除，重新建表，auto_increment将置为零，从新开始
```

#### 自增字段

```mysql
create table category(cid varchar(20) primary key auto_increment, cname varchar(100)); #auto_increment为自增字段，插入时会自动加一，手动设置可以占用之前已经被删除的id
alter table tablename auto_increment=100; #自增字段从100开始
```

#### 主键约束

##### 单一主键

PRIMARY KEY 约束唯一标识数据库表中的每条数据

```mysql
create table preson4
(
 id int PRIMARY KEY,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City vatchar(255)
);
```

主键必须包含唯一的值

主键列不能包含null值

每个表都应该有一个主键，并且每个表只能有一个主键

##### 联合主键

```mysql
create table preson4
(
 id int,
 LastName varchar(255),
 FirstName varchar(255),
 Address varchar(255),
 City vatchar(255)
 CONSTRAINT pk_PersonID PRIMARY KEY (FirstName,LastName) #CONSTRAINT给联合主键起名字，删除主键约束用
);
```

##### 删除主键约束

```mysql
alter table tablename drop primary key
```

#### 非空约束

```mysql
create table preson5
(
    id int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City vatchar(255)
);
```

---

### 2021.11.11

#### 唯一约束

UNIQUE约束唯一标识数据库表中的每条记录，可以为null

UNIQUE和PRIMARY KEY约束均为列或列集合提供了唯一性的保证

每个表可以有多个UNQUE约束，但是每个表只能有一个PRIMARY KEY约束

---

### 2021.11.12

#### DQL查询语言

```mysql
select [distinct]
* #列名，列名
from #表
where #条件

#1.查询所有的商品
select * from product;
#2.查询商品名和商品价格
select pname,price from product;
#3.别名查询，使用的关键字是as(as可以省略)
#3.1表别名
select * from product as p;
#3.2列别名
select pname as pn from product;
#4.去掉重复的值
select distinct price from product;
#4.1去重时列名如果是*，则代表查出来的所有列只要有一列全部不相同，就不做去重
select distinct * from product;
#5.查询结果是表达式（运算查询）：将所有商品的价格+10元进行展示
select pname,price+10 from product;
```

##### 条件查询

###### 比较运算符

| 比较运算符         | 意义                                                                                      |
| ------------------ | ----------------------------------------------------------------------------------------- |
| < > <= >= = <> !=  | 大于、小于、大于（小于）等于、不等于                                                      |
| BETWEEN  ...AND... | 显示在某一区间的值（含头含尾）                                                            |
| IN（set）          | 显示在in列表中的值，例如：in(100,200)                                                     |
| LIKE '张%'         | 模糊查询，like语句中，%代表零个或多个任意字符，_代表一个字符，例如：first_name like '_a%' |
| IS NULL            | 判断为空                                                                                  |
| IS NOT NULL        | 判断不为空                                                                                |

###### 逻辑运算符

| 逻辑运算符 | 意义                                 |
| ---------- | ------------------------------------ |
| and        | 多个条件同时成立                     |
| or         | 多个条件任一成立                     |
| not        | 不成立，例如：where not(salary>100); |

##### 排序查询

```mysql
select * from tablename order by filed asc|desc;  #asc 升序（默认） desc 降序，跟两个列名则是一个主要条件一个次要条件
```

##### 聚合查询

| 聚合函数 | 作用                                                               |
| -------- | :----------------------------------------------------------------- |
| count()  | 统计指定列不为NULL的记录行数                                       |
| sum()    | 计算指定列的数值和，如果指定列类型不是数值类型，那么计算结果为0    |
| max()    | 计算指定列的最大值，如果指定列是字符串类型，那么使用字符串排序运算 |
| min()    | 计算指定列的最小值，如果指定列是字符串类型，那么使用字符串排序运算 |
| avg()    | 计算指定列的平均值，如果指定列类型不是数值类型，那么计算结果为0    |

实例：

```mysql
#1 查询商品的总条数
select count(*) from product; #1和*是一样的，如果指定列有值为NULL，则这一记录不会被统计
#2 查询价格大于200商品的条数
select count(*) from product where price > 200;
#3 计算价格总值
select sum(price) from product;
#4 查询商品的最大价格和最小价格
select max(price),min(price) from product;
```

##### 分组查询

分组查询是指使用group by关键字对查询信息进行分组

格式：

```mysql
SELECT filed1,filed2 FROM tablename GROUP BY group_filed HAVING group_condition;
```

分组操作中的having子语句，是用于在分组后对数据进行过滤的，作用类似于where条件

having和where的区别：

1)having是在分组后对数据进行过滤，where实在分组前对数据进行过滤

2)having后面可以使用分组函数（统计函数），where后面不可以使用分组函数

分组之后，SELECT后面只能跟分组字段和聚合函数

实例：

```mysql
#1 统计各个分类商品的个数
SELECT category_id,COUNT(*) FROM product GROUP BY category_id;
#2 统计各个分类商品的个数，且只显示个数大于1的信息
SELECT category_id,COUNT(*) FROM product GROUP BY category_id HAVING count(*)>1;
```

#### sql语句的执行顺序

from > where > group by > 聚合函数 > having > select > order by > limit

##### 分页查询

分页查询在项目开发中常见，由于数据量很大，显示屏长度有限，因此对数据需要采取分页显示方式。例如数据共有30条，每页显示5条，第一页显示1-5条，第二页显示6-10条

格式：

```mysql
SELECT filed1,filed2 FROM tablename LIMIT M,N;
#M：整数，表示从第几条索引开始，计算方式：（当前页-1）*每页显示条数
#N：整数，表示查询多少条数据
SELECT filed1,filed2 FROM tablename LIMIT 0,5;
SELECT filed1,filed2 FROM tablename LIMIT 5,5;

#查询product表的前5条数据
SELECT * FROM product LIMIT 0,5;
```

---

### 2021.11.13

#### INSERT INTO SELECT语句

INSERT INTO SELECT 语句从一个表复制数据，然后把数据插入到一个已存在的表中

##### 基本语法

```mysql
INSERT INTO table2
SELECT column_name(s)
FROM table1;
```

##### 实例

```mysql
CREAT TALBLE product2(
 pid INT PRIMARY KEY,
 pname VARCHAR(20),
 price double
);

INSERT INTO product2 SELECT pid,pname,price FROM product WHERE category_id = 'c001';
```

#### 多表操作

##### 表于表之间的关系

一对一的关系

一对多的关系

多对多的关系

##### 外键约束

声明外键约束

语法

```mysql
ALTER TABLE 从表 ADD [CONSTRAINT] [外键名称] FOREIGN KEY (从表外键字段名) REFERENCES 主表(主表的主键)；
```

[外键名称]  用于删除外键约束的，一般建议  "_fk"  结尾

删除外键：

```mysql
ALTER TABLE 从表 DROP FROEIGN KEY 外键名称;
```

注：在创建外键约束时遇到报错：Failed to add the foreign key constraint. Missing index for constraint 'product_fk' in the referenced table 'category'，问题是出在主表中的主键不是primary key导致的，进行外键约束时必须保证主表中的约束列为主键

##### 一对多操作

插入：主表可以随意插入数据，从表插入数据必须受主表限制

删除：主表的数据如果受到从表依赖，则不能删除，从表数据可以随意删除

#### 多表查询

##### 1、交叉连接查询（基本不会使用，得到的是两个表的乘积）

```mysql
SELECT * FROM A,B;
```

##### 2、内连接查询（使用的关键字 inner join --inner可以省略,求的是两张表的交集）

```mysql
SELECT * FROM A,B WHERE 条件 #隐式内连接
SELECT * FROM A INNER JOIN B ON 条件 #显示内连接
#这两种查询方式只有写法上的区别作用上没有区别
```

##### 3、外连接查询（使用的关键字 outer join --outer可以省略）

```mysql
SELECT * FROM A LEFT OUTER JOIN B ON 条件 #左外连接：left outer join,以左边表为主，右表有对应数据则输出，没有则补null
SELECT * FROM A RIGHT OUTER JOIN B ON 条件 #右外连接：right outer join，以右边表为主，左表有对应数据则输出，没有则补null
```

#### 子查询

一条select语句结果作为另一条select语法一部分（查询条件，查询结果，表等），

##### 实例

```mysql
SELECT * FROM products WHERE category_id = (SELECT cid FROM category WHERE cname = '化妆品'); #作为查询条件
SELECT * FROM products p, (SELECT * FROM category WHERE cname = '化妆品') c WHERE p.category_id = c.cid; #作为另一张表
```

#### MySql索引

##### 索引的分类

根据索引储存方式不同分为：

1、B-树索引

B-树索引又称为BTREE索引，目前大部分的索引都是采用B-树索引来储存的，B-树索引是一个典型的数据结构，基于这种树形结构，表中的每一行都会在索引上有一个对应值，因此，在表中进行数据查询时，可以根据索引值一步一步定位到数据所在行。

2、哈希索引

哈希（Hash）一般翻译为“散列”，也有直接音译成“哈希”的，就是把任意长度的输入（又叫做预映射，pre-image）通过散列算法变换成固定长度的输出，该输出就是散列值，Hash索引不是基于树形的数据结构查找数据，而是根据索引列对应的哈希值的方法获取表的记录行。

根据索引的具体用途不同可以分为：

1、普通索引

普通索引是最基本的索引类型，唯一任务是加快对数据的访问速度，没有任何限制，创建普通索引时，通常使用的关键字时INDEX或KEY，有三种创建方法

```mysql
--创建索引
CREATE INDEX price_index ON products(price); #第一种
ALTER TABLE products ADD INDEX price_index(price); #第二种
CREATE TABLE products ( #第三种
 id NOT NULL,
    username VARCHAR(20) NOT NULL,
    INDEX username_index(username)
);
--查询索引
SHOW INDEX FROM tablename; #查看表中所有的索引
SELECT * FROM mysql.`innodb_index_stats` a WHERE a.`database_name` = '数据库名';
SELECT * FROM mysql.`innodb_index_stats` a WHERE a.`database_name` = '数据库名' AND a.table_name LIKE '%表名%';
--删除索引
DROP INDEX [indexname] ON tablename;
ALTER TABLE tablename DROP INDEX indexname;
```

2、唯一性索引

唯一性索引时不允许索引列具有相同索引值的索引，如果能确定某个数据列只包含彼此各不相同的值，在为这个数据列创建索引的时候就应该用关键字UNIQUE把它定义为一个唯一性索引，创建唯一性索引的目的往往不是为了提高访问速度，而是为了避免数据出现重复。

```mysql
--创建索引
--方式一:直接创建
CREATE UNIQUE INDEX indexname ON tablename(username);
--方式二：修改表结构（添加索引）
ALTER TABLE tablename ADD UNIPUE indexname (username);
--方式三:创建表时直接指定
CREATE TABLE tablename (
 id INT NOT NULL,
    username VARCHAR(20) NOT NULL,
    UNIQUE indexname (username)
);
--删除索引
DROP INDEX indexname ON tablename;
ALTER TABLE tablename DROP INDEX indexname;
```

3、主键索引

主键索引是一种唯一性索引，即不逊于值重复或者值为空，并且每个表只能有一个主键，主键可以在创建表的时候指定，也可以通过修改表的方式添加，必须指定关键字PRIMARY KEY

#### MySql开窗函数

##### 开窗函数语法结构

<开窗函数> over ([PARTITION by <列清单>] order by <排序用列清单>)

row_number(), rank(), dense_rank()

##### 三者区别

row_number()：不管排名是否有相同的，都按照顺序1，2，3，。。。

rank()：排名相同的名次一样，同一排名有几个，后面排名就会跳过几次

dense_rank()：排名相同的名次一样，且后面名次不跳跃

##### 实例

```mysql
create table employee
(
    empid  int,
    ename  varchar(20),
    deptid int,
    salary decimal(10, 2)
);

insert into employee
values (1, '刘备', 10, 5500.00);
insert into employee
values (2, '赵云', 10, 4500.00);
insert into employee
values (2, '张飞', 10, 3500.00);
insert into employee
values (2, '关羽', 10, 4500.00);

insert into employee
values (3, '曹操', 20, 1900.00);
insert into employee
values (4, '许诸', 20, 4800.00);
insert into employee
values (5, '张辽', 20, 6500.00);
insert into employee
values (6, '徐晃', 20, 14500.00);

insert into employee
values (7, '孙权', 30, 44500.00);
insert into employee
values (8, '周瑜', 30, 6500.00);
insert into employee
values (9, '陆逊', 30, 7500.00);

select empid,
       ename,
       deptid,
       salary,
       row_number() over (partition by deptid order by salary desc ) as row_number1,
       rank() over (partition by deptid order by salary desc )       as rank2,
       dense_rank() over (partition by deptid order by salary desc ) as dense_rank3
from employee;
```

查询三个分组中薪资最高的人：

```mysql
select * from (select empid,
       ename,
       deptid,
       salary,
       row_number() over (partition by deptid order by salary desc ) as row_number1,
       rank() over (partition by deptid order by salary desc )       as rank2,
       dense_rank() over (partition by deptid order by salary desc ) as dense_rank3
from employee) t where t.row_number1 = 1 ;
##这里要注意子查询中的表需要有别名之后才能进行使用
```

---

### 2021.11.14

#### 可视化平台ETL平台--Kettle

##### 1.Kettle介绍

###### 1.1 数据仓库

数据仓库是一个很大的数据存储集合，处于企业的分析性报告和决策支持目的儿创建的，对多样的业务数据进行筛选与整合。它为企业提供一定的BI能力，指导业务流程改进，监视时间成本、质量以及控制。

###### 1.2 ETL

ETL，是应为Extract-Transform-Load的缩写，用来描述将数据从来源端经（extrac过抽取t）、转换、加载至目的端的过程，ETL是将业务系统的数据经过抽取、清洗、转换之后加载到数据仓库的过程，目的是将企业中分散、凌乱、标准不统一的数据整合到一起

---

### 2021.11.15

kettle安装，JDK版本不宜过高，使用jre可以正常使用

---

### 2021.11.17

kettle使用，从txt转换为exel表格，按照讲义写的过程进行操作

excel到mysql数据库

mysql表到mysql表

mysql表的插入更新

---

### 2021.11.18

kettle删除组件

排序记录组件

switch/case组件

sql脚本组件

sql脚本设置转换参数，可以将参数带入到sql脚本中去

注意！！！参数需要$美元符号和{}花括号进行引用

---

### 2021.11.22

#### Superset介绍

superset是一款开源的现代化企业级BI，它是目前开源的数据分析和可视化工具中比较好用的，功能简单但可以满足我们对数据的基本需求，支持多种数据源，图标类型多，易维护，易进行二次开发

#### mysql docker run语句

docker run -d -v /opt/data/mysql/:/var/lib/mysql --network host --name gkjuanmao_mysql -e MYSQL_ROOT_PASSWORD=123456  mysql

查看docker详细信息

docker inspect CONTAINER ID

superset 测试数据库连接时报错：

superset /usr/lib/x86_64-linux-gnu/mariadb18/plugin/caching_sha2_password.so: cannot open shared obj

要对数据库的连接认证方式进行更改，更改见贴：[https://blog.csdn.net/qq_41538097/article/details/106905416](https://blog.csdn.net/qq_41538097/article/details/106905416)

---

### 2021.11.28

进行可视化展示的时候运行查询后没有结果，需要先对标题进行修改，之后在Chrats栏中选择刚刚进行的查询，此时才能显示出刚刚完成的可视化展示

```mysql
#案例一，按照性别统计人数
select
 case when gender = 0 then '男' #将gender为零的显示为男
     when gender = 1 then '女'
  else '保密'
    end as gender,
 count(id) as total_cnt
from
 t_user
group by gender
#案例二，按照时间统计销售额
select
 str_to_date(date1,'%Y-%m-%d') date1,
 sum(price) total_price
from
 dm_sales
group by date1;
#案例三，根据日期、渠道统计订单总额
select
 date1,
 channelname,
 sum(price) total_price
from
 dm_sales
group by
 date1,
 channelname
#案例四，根据日期、区域、渠道、产品统计订单总额
select date1,
       regionname,
       channelname,
       productname,
       sum(price) as total_price
from dm_sales
group by date1,
         regionname,
         channelname,
         productname;
#案例五.根据日期、区域统计订单总额
select str_to_date(date1, '%Y-%m-%d') date1,
       regionname,
       sum(amount) as                 total_amount,
       sum(price)  as                 total_price
from dm_sales
group by date1,
         regionname;
```

---

### 2022.2.17

#### java学习

> 特点：开源，跨平台，JVM不能跨平台，每种平台对应一种JVM

+ 多态
+ 多线程
+ 面向对象

---

### 2022.2.19

#### java学习

JDK（Java开发工具包）包含JRE（java runtime environment），JRE包含JVM（Java运行虚拟机）

#### 变量

> 在程序的执行过程中，其值可以在某个范围内发生变化的量就叫变量

基本数据类型

> 整型：

+ 字节型（byte）:1个字节 -2^7 ~ 2^7-1
+ 短整型（short）:2个字节 -2^15 ~ 2^15-1
+ 整型（int）:4个字节 -2^31 ~ 2^31-1
+ 长整型（long）:8个字节 -2^63 ~ 2^63-1

> 浮点型：

+ 单精度浮点型（float）:4个字节 3.4*10^(-38) ~ 3.4*10(+38)
+ 双精度浮点型（double）:8个字节 1.7*10^(-308) ~ 1.7*10(+308)

> 字符型：

+ 字符型（char）:2个字节 0 ~ 2^16-1

> 布尔型：

+ 布尔类型（boolean）:1个字节 true,false

---

### 2022.2.20

#### 命名规范

1. 类、接口的命名规范:每个单词的首字母都大写，其他字母全部小写(大驼峰命名法)
   例如:HellowWorld,VariableDemo
2. 变量,方法的命名规范:从第二个单词开始,每个单词的首字母大写,其他字母全部小写(小驼峰命名法)
   例如:zhangSanAge,studentName
3. 常量(指的是:自定义常量)的命名规范:所有字母都大写,单词直接用_隔开
   例如:MAX_VALUE,MIN_VALUE,PI
4. 包的命名规范:所有字母全部小写,多级包之间用\.隔开,
   例如:cn.itcast,com.itheima

#### 数据类型转换

##### 分类

+ 自动(隐式)类型转换
  > 指的是小类型转大类型,会自动提升为大类型,运算结果是大类型
  > 细节:因为int是默认的整形,所以只要是数字运算,你能得到的最小类型就是int
  >
+ 强制(显式)类型转换
  > 指的是手动将大类型转换成小类型,运算结果是小类型
  >

ASII码表特殊字符对应的数字:
a -> 97
A -> 65
0 -> 48

---

### 2022.2.21

#### 运算符

==自增和自减包含强制类型转换==

```java
byte b1 = 10;
    b1 ++ ;    //等价于 b1 = (byte)(b1 + 1)
```

扩展的赋值运算符:

```java
+=, -= ,*=, /=, %=
```

> 例如:+=的意思是,把左边的和右边的数据相加,结果复制给左边
> ==注意:赋值运算的左边不能是常量,包含强制类型转换==

#### 短路逻辑运算符

| 符号 | 作用   | 说明                                                     |
| :--- | :----- | :------------------------------------------------------- |
| &&   | 短路与 | 作用和&相同,但是有短路的效果,前边出现false,后边不执行    |
| \|\| | 短路或 | 作用和\|相同，但是有短路的效果，前边出现true，后边不执行 |

#### 三元运算符

> 格式:关系表达式 ? 表达式1 : 表达式2
> 执行流程:
>
> 1. 先判断关系表达式,看其结果是true还是false
> 2. ture,执行表达式1
> 3. false,执行表达式2

---

### 2022.2.22

### 2022.2.23

switch语句

1. 格式

```java
switch (表达式){
    case 值1:
        语句体1;
        break;
    case 值1:
        语句体1;
        break;
    case 值1:
        语句体1;
        break:
    default:
        语句体n:
        break;
        }
```

case穿透

> 在switch语句中，如果case的后面不写break，将出现case穿透现象，也就是不会再判断下一个case的值，直接向后运行，直到遇到break，或者整体switch结束

### 2022.2.24

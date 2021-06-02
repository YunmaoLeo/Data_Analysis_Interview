# 目录
- [目录](#目录)
  - [SQL](#sql)
    - [排序](#排序)
      - [使用多个列排序，不同的列使用的顺序不同](#使用多个列排序不同的列使用的顺序不同)
      - [使用ODER BY 和 LIMIT组合获取最N值](#使用oder-by-和-limit组合获取最n值)
    - [过滤](#过滤)
      - [WHERE 子句可操作内容](#where-子句可操作内容)
      - [获取范围值：](#获取范围值)
      - [空值检查](#空值检查)
      - [IN操作符](#in操作符)
      - [LIKE 操作符](#like-操作符)
        - [百分号通配符](#百分号通配符)
        - [下划线通配符(_)](#下划线通配符_)
      - [正则表达式搜索](#正则表达式搜索)
        - [匹配字符类](#匹配字符类)
        - [匹配多个实例](#匹配多个实例)
    - [创建计算字段](#创建计算字段)
      - [拼接字段](#拼接字段)
      - [执行算术运算](#执行算术运算)
    - [使用数据处理函数](#使用数据处理函数)
      - [一些字符串函数](#一些字符串函数)
      - [日期和事件处理函数](#日期和事件处理函数)
      - [数值处理函数](#数值处理函数)
    - [汇总数据](#汇总数据)
      - [聚合函数](#聚合函数)
      - [AVG()](#avg)
      - [COUNT()](#count)
      - [聚集不同值](#聚集不同值)
    - [分组数据](#分组数据)
      - [创建分组](#创建分组)
      - [过滤分组](#过滤分组)
      - [分组和排序](#分组和排序)
      - [SELECT子句顺序](#select子句顺序)
    - [联结表](#联结表)
      - [内部链接](#内部链接)
      - [联结多个表](#联结多个表)
    - [创建高级联结](#创建高级联结)
      - [自联结](#自联结)
      - [自然连接](#自然连接)
      - [外部联结 OUTER JOIN](#外部联结-outer-join)
    - [组合查询 UNION](#组合查询-union)
    - [全文本搜索](#全文本搜索)
      - [布尔文本搜索](#布尔文本搜索)
    - [插入数据](#插入数据)
    - [修改数据](#修改数据)
    - [删除数据](#删除数据)
    - [引擎类型](#引擎类型)
    - [MySQL事务](#mysql事务)
    - [更新表](#更新表)
    - [使用视图](#使用视图)
    - [导出数据](#导出数据)
    - [窗口函数](#窗口函数)
      - [按班级分类，将成绩降序排序](#按班级分类将成绩降序排序)
      - [dense_rank() row_number() rank()](#dense_rank-row_number-rank)
      - [查找重复的电子邮件](#查找重复的电子邮件)
      - [CUME_DIST()](#cume_dist)
      - [FIRST_VALUE()](#first_value)
      - [LAG()](#lag)
      - [LEAD()](#lead)
  - [统计学知识](#统计学知识)
    - [抽取样本](#抽取样本)
    - [推断统计](#推断统计)
      - [获取P值](#获取p值)
      - [假设检验的三种类型](#假设检验的三种类型)
      - [不同的检验方法](#不同的检验方法)
      - [第一类错误和第二类错误](#第一类错误和第二类错误)
  - [数据分析思维读书笔记](#数据分析思维读书笔记)
    - [业务指标](#业务指标)
    - [如何选择指标](#如何选择指标)
  - [关键词](#关键词)
  - [精益数据分析读书笔记](#精益数据分析读书笔记)
    - [第一章](#第一章)
      - [什么是好的数据指标](#什么是好的数据指标)
      - [如何选择好的指标](#如何选择好的指标)
      - [市场细分 同期群分析 A/B测试和多变量分析](#市场细分-同期群分析-ab测试和多变量分析)
    - [以数据为导向与通过数据获取信息](#以数据为导向与通过数据获取信息)
      - [数据科学家的思维方式：](#数据科学家的思维方式)
    - [数据分析框架](#数据分析框架)
      - [海盗指标：AARRR](#海盗指标aarrr)
      - [增长引擎说](#增长引擎说)
      - [长漏斗](#长漏斗)
    - [第一关键指标的约束力](#第一关键指标的约束力)
    - [商业模式：免费移动应用](#商业模式免费移动应用)
    - [商业模式：用户生成内容（User-generated Content, UGC)](#商业模式用户生成内容user-generated-content-ugc)
    - [用户生成内容：底线在哪里](#用户生成内容底线在哪里)
## SQL

### 排序
+ ORDER BY默认使用升序排列
#### 使用多个列排序，不同的列使用的顺序不同
```mysql
SELECT prod_id, prod_price, prod_name
FROM product
ORDER BY prod_price DESC, prod_name;
```
+ DESC关键字只应用到直接位于前面的列名

#### 使用ODER BY 和 LIMIT组合获取最N值
```mysql
SELECT prod_price
FROM products
ORDER BY prod_price DESC
LIMIT 1;
```

### 过滤

#### WHERE 子句可操作内容
|操作符|说明|
|------|----|
|=||
|<>|不等于|
|!=|不等于|
|<||
|<=||
|>||
|>=||
|BETWEEN|指定两个值之间

#### 获取范围值：
```
SELECT prod_name, prod_price
FROM products
WHERE prod_price BETWEEN 5 AND 10;
```
#### 空值检查
```
SELECT prod_name
FROM products
WHERE prod_price IS NULL
```

#### IN操作符
+ IN取的合法值由逗号分隔的清单
```
SELECT prod_name, prod_price
FROM products
WHERE vend_id IN (1002,1003)
ORDER BY prod_name
```
+ IN操作符一般比OR操作符速度更快
+ 此外，IN可以包含其他SELECT语句，能够动态简历WHERE子句

#### LIKE 操作符
+ 通配符搜索花费的时间更多
+ 在确定是要通配符时，除非绝对有必要，不要把他们放在搜索模式的开始处，否则搜索起来是最慢的
##### 百分号通配符
+ %表示任何字符出现的任意次数
+ 以下代码找出所有以词jet开头的铲平
```
SELECT prod_id, prod_name
FROM products
WHERE prod_name LIKE 'jet%'
```
+ 同样，也可以是
```
WHERE prod_name LIKE '%anvil%'
```

##### 下划线通配符(_)
+ 用处与%一样，但是只能匹配单个字符

#### 正则表达式搜索
```
WHERE prod_name REGEXP '1000'
```
+ 如上代码中，如果对应的列中出现了REGEXP后面的字符串，则返回它
+ 正则字符串匹配不区分大小写，如果需要区分可以使用``REGEXP BINARY 'JetPack'``

<br>

+ 正则表达式中要匹配``. -``等特殊字符需要加反义字符``\\``

+ 一些元字符
  + \\f 换页
  + \\n 换行
  + \\r 回车
  + \\t 制表符
  + \\v 纵向制表符

##### 匹配字符类
+ [:alnum:] 任意字母和数字
+ [:aplha:]
+ [:blank:] 空格和制表
+ [:cntrl:] ASCII控制字符 0-31和127
+ [:digit:] 数字
+ [:lower:]
+ [:space:]
+ [:upper:]
+ [:xdigit:]

##### 匹配多个实例
+ * 0个或多个
+ + 1个或多个
+ ? 0个或1个
+ {n} 指定n个匹配
+ {n,} 大于等于n个
+ {n,m} 匹配数目的范围，m不超过255

<br>

+ 匹配连在一起的四位数字：
```
WHERE prod_name REGEXP '[[:digit:]]{4}'
```

+ 简单的正则表达式测试
```
SELECT 'hello' REGEXP '[0-9]'
```
正确会返回1，否则0

### 创建计算字段

#### 拼接字段
+ 使用Concat()函数
```
SELECT Concat(vend_name, '(', vend_country, ')' ) --可以添加字符
FROM vendors
ORDER BY vend_name;
```
+ RTrim()函数实现删除数据右侧多余的空格来整理数据
  + 同样亦可以使用LTrim去掉左边的空格
  + 当然，也可以使用Trim()去掉左右两边的空格
```
SELECT Concat(RTrim(vend_name), '(', RTrim(vend_country) ,')' )
FROM vendors
ORDER BY vend_name;
```

#### 执行算术运算
```
SELECT prod_id,
       quantity,
       item_price,
       quantity*item_price AS expanded_price
FROM orderitems
WHERE order_num = 200005;
```

### 使用数据处理函数
#### 一些字符串函数
+ Upper()将文本转换为大写
+ Left() 返回串左边的字符
+ Length() 返回串的长度
+ Locate() 找出串的第一个字串
+ SubString() 返回字串的字符
+ Soundex() 返回串的SOUNDEX值 （发音相似的）

#### 日期和事件处理函数
+ AddData() 增加一个日期，天周等
+ AddTime() 增加一个时间， 时，分
+ CurDate() 当前日期
+ CurTime() 当前时间
+ DateDiff() 计算两个日期的差
+ Hour()
+ Minute()
+ Month()
+ Now()
+ Second() 返回秒的部分
+ 日期的格式：
  + yyyy-mm-dd

+ 检索一个日期时，
  + 如果要的是日期，一定要使用Date()
```
SELECT cust_id, order_num
FORM orders
WHERE Date(order_date) = '2005-09-01';
```
+ 检索一段时间的
```
WHERE Date(order_date) BETWEEN '2005-09-01' AND '2005-09-30';
```

或者

```
WHERE Year(order_date) = 2005 AND Month(order_date) = 9;
```

#### 数值处理函数
+ Abs()
+ Cos()
+ Exp()
+ Mod()
+ Pi()
+ Rand()
+ Sin()
+ Sqrt()


### 汇总数据

#### 聚合函数
+ AVG() 平均值
+ COUNT() 列数
+ MAX()
+ MIN()
+ SUM()

#### AVG()
```
SELECT AVG(prod_price) AS avg_price
FROM products;
```

#### COUNT()
+ 使用COUNT(*)对表中行的数目进行计数，不管包含的是空值还是非空值
+ 使用COUNT(column)对特定列中具有值得行进行计数，忽略NULL
```
SELECT COUNT(*) AS num_cust
FROM customers;
```
+ 上述代码计算所有的数目
+ 以下代码计算cust_emial列中的非空值
```
SELECT COUNT(cust_email) AS num_cust
FROM customers;
```

#### 聚集不同值
+ 如果需要只包含不同的值，指定DISTINCT参数，否则ALL会被作为默认
```
SELECT AVG(DISTINCT prod_price) AS avg_price
FROM products
WHERE vend_id = 1003;
```

### 分组数据

#### 创建分组
```
SELECT vend_id, COUNT(*) AS num_prods
FROM products
GROUP BY vend_id
```
+ 如上代码中，groupby将会对vend_id进行排序并分组数据
  + 如果分组列中有NULL值，则NULL会被作为一个分组返回，如果列中有多行NULl值，他们会被分成一组
+ GROUP BY子句必须出现在WHERE之后，ORDER BY之前

+ 使用``WITH ROLLUP``关键字可以得到每个分组以及每个分组汇总级别（针对每个分组）的值
```
GROUP BY vend_id WITH ROLLUP;
```

#### 过滤分组
+ HAVING 子句
  + WHERE过滤行，HAVING过滤分组
  + 同样可以理解为，WHERE在数据分组前进行过滤，HAVING在数据分组后进行过滤
```
SELECT cust_id, COUNT(*) AS orders
FROM orders
GROUP BY cust_id
HAVING COUNT(*) >= 2; 
```

+ 同时进行WHERE和HAVING
```
SELECT vend_id, COUNT(*) AS num_prods
FROM products
WHERE prod_price >= 10 --首先限制需要的产品价格是10以上的
GROUP BY vend_id
HAVING COUNT(*) >= 2; --然后限制分组后数量需要大于等于2
```

#### 分组和排序
+ 在使用GROUP BY子句的同时，也应该给出ORDER BY子句
  + 这是保证数据正确排序的唯一方法
```
SELECT order_num, SUM(quantity*item_price) AS ordertotal
FROM orderitems
GROUP BY order_num
HAVING SUM(quantity*item_price) >= 50
ORDER BY ordertotal;
```

#### SELECT子句顺序
+ 1. SELECT
+ 2. FROM
+ 3. WHERE
+ 4. GROUP BY
+ 5. HAVING
+ 6. ORDER BY
+ 7. LIMIT

### 联结表

#### 内部链接
```
SELECT vend_name, prod_name, prod_price
FROM vendors INNER JOIN products
  ON vendors.vend_id = products.vend_id;
```

#### 联结多个表
```
SELECT prod_name, vend_name, prod_price, quantity
FROM orderitems, products, vendors
WHERE products.vend_id = vendors.vend_id
  AND orderitems.prod_id = products.prod_id
  AND order_num = 123;
```
+ 此种关联处理是相当耗费资源的


### 创建高级联结
+ 通过``AS``关键字使用别名，两点好处
  + 缩短SQL语句
  + 允许在单挑SELECT语句中多次使用相同的表

#### 自联结
```
SELECT p1.prod_id, p1.prod_name
FROM products AS p1, products AS p2
WHERE p1.vend_id = p2.vend_id
  AND p2.prod_id = 'DTNTR'
```
+ 如上代码中使用两个相同的表分别作为p1, p2
  + WHERE中选取p2中产品ID为DTNTR的列，此时p2.vend_id就是DTNTR的生产商
  + p1.vend_id = p2.vend_id 此时意味在p1选取DTNTR的生产商

#### 自然连接
+ 无论如何对表进行联结，应该至少有一列出现在不止一个表中。
  + 标准的联结返回所有数据，甚至相同的列多次出现。
  + 自然联结排除多次出现，使每个列只返回一次

#### 外部联结 OUTER JOIN
+ 外部联结还包括没有关联行的行。在使用OUTER JOIN语法时，必须使用RIGHT 或者LEFT关键字指定包括其所有行的表


### 组合查询 UNION
+ UNION必须由两条或两条以上的SELECT语句组成，语句之间用关键字UNION分割
+ UNION中的每个查询必须包含相同的列，表达式或聚集函数
  + UNION从查询结果中集中自动去除了重复的行
    + 如果不想改变这种默认去除的行为，可以使用UNION ALL

+ 如果需要对组合查询的结果进行排序，只能放在最后一条SELECT语句中ORDER BY，不允许使用多条ORDER BY

### 全文本搜索
+ 创建表的时候使用FULLTEXT(note_text),这里的FULLTEXT索引单个列
  + 在索引之后，使用两个函数Match()指定被搜索的列，Against()指定要使用的搜索表达式

```
SELECT note_text
FROM productnotes
WHERE Match(note_text) Against('rabbit');
```
+ 全文本搜索的一个重要部分是对结果排序，具有较高等级的行先返回


#### 布尔文本搜索
```
WHERE Match(note_text) Against('heavy -rope*' IN BOOLEAN MODE);
```
+ 如上代码中IN BOOLEAN MODE表示使用布尔类型的文本搜索
  + -rope*表示配出包含任何以rope开始的词的行

+ 全文本布尔操作符
  + + 包含，词必须存在
  + - 排除，词不存在
  + > 包含，增加等级值
  + < 不包含，减少等级值
  + ~ 取消排序值
  + * 词尾通配符

### 插入数据
+ 使用INSERT插入数据是很耗时的
+ 为了提高服务器内SELECT语句的性能
  + 使用INSERT LOW_PRIORITY INTO降低INSERT的优先级
    + 同样也适用于UPDATE和DELETE


### 修改数据
```
UPDATE customers
SET cust_email = 'elmer@fudd.com'
WHERE cust_id = 10005;
```

### 删除数据
+ 如果需要从表中删除所有行，不要使用DELETE，
  + 而是使用TRUNCATE TABLE语句，他会删除原来的表并重新创建一个表

### 引擎类型
+ 默认引擎是MyISAM
+ InnoDB是一个可靠的事务处理引擎，支持全文搜索
+ MEMORY在功能等同于MyISAM，但由于数据存储在内存，速度很快，特别适合临时表
+ MyISAM性能极高，支持全文本搜索，但不支持事务处理
+ 然而，混用引擎类型的一个问题就是，外键不可以跨引擎使用


### MySQL事务
+ 原子性：一个事务中的所有操作，要么全部完成，要么全部不完成，如果事务过程中发生错误，会被回滚到开始的状态
+ 一致性：事务执行前后，数据库的完整性没有被破坏，这意味着写入的所有信息都要符合预设的规则
+ 隔离性：数据库允许多个并发事务同时进行读写和修改，隔离性可以放置多个事务并发执行时由于交叉执行导致数据不一致
+ 持久性：事务处理结束后，对数据的修改是永久的，即使系统故障也不会丢失
+ 使用BEGIN来开始一个事务
+ ROLLBACK事务回滚
+ COMMIT事务确认
+ SET AUTOCOMMIT = 0 禁止自动提交

### 更新表
```
ALTER TABLE vendors
ADD vend_phone CHAR(20)
DROP COLUMN vend_phone;
ADD CONSTRAINT fk_orderitems_orders
FOREIGN KEY (order_num) REFERENCES orders (order_num);
```

### 使用视图
+ 视图不包含表中应该有的任何列或数据，只包含一个SQL查询
+ 视图使用CREATE VIEW语句来创建
+ SHOW CREATE VIEW viewname; 来查看创建视图的语句
+ CREATE OR REPLACE VIEW来更新视图

```
CREATE VIEW productcustomers AS
SELECT cust_name, cust_contact, prod_id
FROM customers, orders, orderitems
WHERE customers.cust_id = orders.cust_id
  AND orderitems.order_num = orders.order_num
```

+ 以上视图联结了三个表，返回了已经订购任意产品的所有客户的列表
```
SELECT cust_name, cust_contact
FROM productcustomers
WHERE prod_id = 'TNT2';
```
+ 或者也可以使用视图来重新格式化出检索出来的数据
```
CREATE VIEW vendorlocations AS
SELECT Concat(RTrim(vend_name), '(',RTrim(vend_country),')')
       AS vend_title
FROM vendors
ORDER BY vend_name
```

### 导出数据
```
SELECT * FROM runoob_tbl
INTO OUTFILE 'runoob.txt'
FIELDS TERMINATED BY ',' ENCLOSED BY ''''
LINES TERMINATED BY '\r\n';
```

### 窗口函数
+ 窗口函数的窗口表示范围，可以理解为将原数据划分范围，及分组，然后用函数实现某些目的
  + 相比于GROUP BY , 窗口函数不会减少原来的行数
+ 语法: SELECT 窗口函数 over (partition by 用于分组的列名，order by 用于排序的列)
+ 专用窗口函数
  + rank(), dense_rank(), row_numer()

#### 按班级分类，将成绩降序排序
```
SELECT *,
rank() over ( PARTITION BY class_id ORDER BY SCORE DESC ) AS ranking
FROM class
```

#### dense_rank() row_number() rank()
+ 三个函数的主要区别是如何处理并列情况
+ rank()中的并列情况会占用下一个名词的位置, 1,1,1,4
+ dense_rank() 不会占用下一个名词 1,1,1,2
+ row_number()中，会忽略并列的情况, 1,2,3,4
  

#### 查找重复的电子邮件
```
SELECT email, COUNT(email)
FROM contacts_test
GROUP BY email
HAVING COUNT(email)>1
```

+ 删除重复的电子邮件
```
DELETE t1
FROM contacts_test AS t1 INNER JOIN contacts_test AS t2
WHERE t1.id<t2.id AND t1.email = t2.email
```

#### CUME_DIST()
+ 表示值小于等于行的值除以总行数的行数
```
SELECT
name,score,CUME_DIST() OVER (ORDER BY score) cume_dist_val
FROM scores;

```

#### FIRST_VALUE()
+ 选取第一行的数据
```
SELECT employee_name,
       FIRST_VALUE(employee_name) OVER (
         PARTITION BY department
         ORDERED BY hours DESC
       ) least_over_time
FROM overtime;
```

#### LAG()
+ 从同一结果集中的当前行访问上一行的数据
+ 以下代码中返回特定年份和上一年度中每个产品系列的订单:

#### LEAD()
+ 选取当前行的后续行
```
SELECT customerName, orderDate,
       LEAD(orderDate, 1) OVER (
         PARTITION BY customerNumber
         ORDER BY orderDate
       ) nextOrderDate
FROM orders
INNER JOIN customers USING (customerNumber)
```



## 统计学知识

### 抽取样本
+ 样本均值的抽样分布近似服从正态分布，且样本量越大，近似性越强
+ 样本量大于30的时候符合中心极限定理，样本服从正态分布，样本量小于30的时候，总体近似正态分布，样本服从t分布

### 推断统计
+ 提出假设
+ 确定显著性水平
+ 选择检验统计量
+ 建立决策准则
+ 下结论

#### 获取P值
+ 首先计算样本标准差StandardError: 样本标准差/sqrt(n) n:样本的大小
+ t = (样本值-总体均值)/标准误差

#### 假设检验的三种类型
+ 单样本检验：检验单个样本的平均值是否等于目标值
+ 相关匹配检验：检验相关或配对检测之差的平均值是否等于目标值
+ 独立双样本检验：检验两个独立样本的平均值之差是否等于目标值

#### 不同的检验方法
+ Z检验：用于大样本平均值差异性检验的方法，用标准正态分布的理论来推断差异发生的概率
+ T检验：用于样本含量较小，总体标准差未知的正态分布样本
+ F检验：方差齐性检验，在两个样本t检验中要用到F检验，检验两个样本的方差是否有显著性差异
  + T检验用来检测数据的准确度，检测系统误差；F检验用来检测数据的精密度，检测偶然误差
+ 卡方检验：主要用于检验两个或两个以上样本率或构成比之间的差别的显著性，可用于检验两类事物之间存在一定的关系

#### 第一类错误和第二类错误
+ 第一类错误是拒绝了实际正确的假设
+ 第二类错误是接受了实际上不成立的假设
+ 当置信水平高的时候，总体值均值落在置信区间的可能性就更大，这个时候不容易拒绝正确的假设，但更容易接受不成立的假设
+ 实际过程中我们更害怕第一类错误，所以会尽可能设置高的置信水平


## 数据分析思维读书笔记
### 业务指标
+ 用户数据指标
  + 日新增用户数：各渠道来源
  + 活跃率：活跃用户数/总用户数
  + 留存率：第一天新增用户中，在第N天使用过产品的用户数
    + 次日留存率40， 7日20， 30日10是比较好的
+ 行为数据指标
  + PV：Page View 访问次数
  + UV：Unique Visitor 访问人数 
  + 转化率：广告转化率：点击广告的人数/看到广告的人数
  + K因子：
    + K因子等于平均每个用户像多少人发出邀请 * 接收到邀请的人转化为新用户的转化率
    + K因子用来衡量推荐的效果，K>1，新增用户数就会像滚雪球一样增大
+ 产品数据指标
  + 总量
    + GMV成交总额
    + 成交数量
    + 访问市场
  + 人均
    + 人均付费APRU
    + 付费用户人均付费ARPPU
    + 人均访问时长
  + 付费
    + 付费率
    + 复购率

### 如何选择指标
+ 要找出正确的指标要记得五点：
  + 1. 定性指标与定量指标的收集整理和分析
    +  定性数据吸纳主观因素，定量数据排斥主观因素
  + 2. 虚荣指标与可付诸行动的指标的判别
    + 比如总用户数就是个虚荣指标，因为它值会随着时间增长，类似的，还有总活跃用户数
    + 而活跃用户占总用户数的百分比，就是个可付诸行动指标
    + 其他的还有需要提防的虚荣指标还有：
      + 点击量，页面浏览量，赞的数量，网站停留时间，下载量
  + 3. 探索性指标与报告性指标
  + 4. 先见性指标和后见性指标
    + 前者预测未来，后者提示当前问题所在
  + 5. 相关性指标与因果性指标
















## 关键词
PEST、4P、5W2H、SWOT、公式化思维、下钻分析思维、逻辑树思维、对比思维、费米思想、RFM模型、漏斗模型、AARRR模型、用户生命周期模型、熵权法、TGI分析法、双重差分法、AHP层次分析法、拐点法、Abtest、用户画像、增长黑客、北极星指标、OSM指标体系构建。









## 精益数据分析读书笔记

### 第一章
``无论你的妄想多么有说服力，都经不起数据的严格考验``  
``你可以通过直觉得知需要设计何种试验来测试你的创业假设，然后利用数据来验证这些假设``

#### 什么是好的数据指标
+ 简单易懂
+ 是一个比率
  + 比率可操作性强，是行动的向导
  + 是天生的比较性指标，如果将日数据和月数据进行比较，就是会知道该数据当前经历的是短期还是长期的变化
  + 比率还适用于比较各种因素之间的关联（正相关和负相关）
+ 会改变行为

#### 如何选择好的指标
+ 要找出正确的指标要记得五点：
  + 1. 定性指标与定量指标的收集整理和分析
    +  定性数据吸纳主观因素，定量数据排斥主观因素
  + 2. 虚荣指标与可付诸行动的指标的判别
    + 比如总用户数就是个虚荣指标，因为它值会随着时间增长，类似的，还有总活跃用户数
    + 而活跃用户占总用户数的百分比，就是个可付诸行动指标
    + 其他的还有需要提防的虚荣指标还有：
      + 点击量，页面浏览量，赞的数量，网站停留时间，下载量
  + 3. 探索性指标与报告性指标
  + 4. 先见性指标和后见性指标
    + 前者预测未来，后者提示当前问题所在
  + 5. 相关性指标与因果性指标
    + 因果关系测试：找到一个相关性，进行控制变量实验并测量因变量的变化

#### 市场细分 同期群分析 A/B测试和多变量分析
+ 市场细分
  + 简单来说细分市场就是一群拥有相同特征的人
+ 同期群分析
  + 比较相似群体随时间的变化，或是，根据用户的体验来划分数据
+ A/B和多变量测试
  + 假设其他条件不变，仅考虑体验中的某一属性，如链接的颜色，对被试用户的影响，就是A/B测试
  + A/B测试看似简单易行，实际上，只有用户流量巨大的大型网站，能对单一因素进行测试并迅速得到答案。
  + 进行一连串的单独测试会延长你走向成熟的周期，与其如此，不如采用多变量分析法同时对多个属性进行测试
    + 多变量分析法的原理就是，用统计学方法剥离出单个影响因子与结果中某一指标提升的相关性

### 以数据为导向与通过数据获取信息
+ ``人类提供灵感，机器负责验证``

#### 数据科学家的思维方式：
+ 1. 要懂得为数据去除噪声，虽然耗时，但回报通常是很大的
+ 2. 不要忘记归一化
+ 3. 不要轻易排除异常点
+ 4. 异常点也不能全然保留
+ 5. 不要忽略季节性，要重视时间规律的影响
+ 6. 不要抛开技术谈增长
+ 7. 数据呕吐：如果你不知道什么数据对你重要，多大的数据统计版都没有意义
+ 8. 谎报军情的指标：不要设置太多的警报
+ 9. 把数据和其他来源的数据合在一起能带来很多独到的见解
+ 10. 人类与生俱来的模式识别能力，容易使我们误以为无规律的事物是有规律的，把虚荣指标放在一边，退后一步，站在更高的角度看问题

### 数据分析框架

#### 海盗指标：AARRR
+ AARRR：获取用户，提高活跃度，提高留存率，获取营收和自传播

#### 增长引擎说
+ 黏着式增长引擎
  + 其重点在于让用户成为回头客，并且持续使用你的产品
  + 如果你的用户粘性不大，流失率会很高。
  + ``用户参与度是预测产品成功的最佳指示剂之一``
  + 衡量粘性最重要的KPI就是``客户留存率，流失率，使用频率``
  + 长期粘性往往来自用户在使用产品过程中为自身所创造的价值
+ 病毒式增长引擎
  + 病毒式传播之所以吸引人，在于它的指数性本质，如果每个用户能带来1.5个新用户，那么用户数会无限地增长到饱和
  + 其中的一个关键指标是``病毒式传播系数``, 及每个用户带来的新用户
  + 同时还需要衡量``病毒传播周期（循环）``
    + 比如，大部分社交网络都会在注册的时候问你是不是要同步通讯录，然后诱导你邀请他们。还有就是用户完成一次邀请所需的时间
+ 付费式增长引擎
  + 第三种驱动增长的引擎是消费，同查那个在确定产品有黏着性和病毒性前开动这个引擎是比较仓促的行为。
    + 机甲世界这款游戏中先专注于提高使用量，黏着性，然后致力于游戏的病毒性，最后才是付费，让玩家通过购买增值服务提升游戏体验
  + 赚钱本身不是一个驱动增长的引擎，只有把一部分营收再用于获取客户时，营收才有助于增长
  + 业务增长机器上有两个调节旋钮，分别是``客户众生价值(CLV)``和``客户获取成本(CAC)``：客户盈亏平衡时间：收回获取一位客户的成本所需的时间


#### 长漏斗
+ 长漏斗是一种分析方法，可以帮助我们理解最初是如何获得客户的注意力的，以及客户从最初得知该网站到发生你所期望的行为的全过程。
  + 在整个漏斗的全阶段进行监控，这样用户在网站中走到哪儿，追踪到哪儿
    + 比如注册获取通知邮件，点击商品页面，查看评价，和客服对话

### 第一关键指标的约束力
+ 在数据分析的世界里，挑选一个唯一的指标，该指标对你当前所处的创业阶段无比重要，我们称之为``OMTM(One Metric That Matters, 第一关键指标)``
+ 你可以捕捉所有的数据，但只关注其中重要的那些

### 商业模式：免费移动应用
+ 重要指标
  + 下载量
  + 客户获取成本（CAC）
  + 应用运行率
    + 有多少下载的用户真正开启了该项应用
  + 活跃用户数量比率和日活DAU，月活MAU
  + 付费用户率
  + 首次付费时间
    + 用户激活后需要多久才会开始付费
  + 用户平均每月营收ARPU
    + 购买和广告的收入总和的平均
    + 这个指标可以给出我们真实的用户参与度。通常是以月为单位计算的
  + 点评率，在应用商店评分或评论的用户比例
  + 病毒性
    + 每位用户可以邀请多少新用户
  + 流失率
    + 卸载应用或在一定时间段内没有开启过应用的用户比例
  + 客户终身价值
    + 用户在使用应用期间贡献的营收
    + 测算每位流失用户的平均消费金额
+ 比如现在每月流失用户占总用户数的15%，这意味着平均每位玩家的游戏寿命是（1/0.15），6.67个月
  + 付费用户比例，了解付费人群和非付费人群之间的差异很重要
    + 假设知道某种广告吸引进来的用户更可能花费，那么就应该多打些类似的广告
  + 流失率：跟踪一日，一周，一月
    + 一日可能是软件的使用体验过于糟糕，有明显的问题
    + 产品使用起来新鲜感很快就结束了，不够耐玩
    + 产品有更好的替代品，或者是规划处理得不好  
+ 一个软件的大部分营收可能来自于一小部分用户，应该将部分用户单独划分一组进行分析处理，虽然关键指标是平均每位用户营收，但最好同时跟踪平均每位付费用户营收，因为这些特殊用户和其他大部分用户的行为想法往往相差甚远

### 商业模式：用户生成内容（User-generated Content, UGC)
+ 此类商业模式重点关注优质内容的生成
+ UGC指优质内容和糟糕内容之间以及内容生成者和潜水者之间的比例，这是一个参与度漏斗，与传统电商的转化漏斗十分相似。
  + 二者的区别在于，转化漏斗的目的是让大家买东西，而参与度漏斗旨在让用户提高参与度，让潜水者参与投票，投票者参与评论等
+ 应该关注的关键指标
  + 访客参与度：
    + 衡量这一指标地简易方法是计算一个比值
      + 在今天的访客里，曾经在本周早些时候访问过该网站的人数的比例，不论有没有创建过帐户
  + 另一个指标是距离上次访问/点赞/评论/发视频的平均时间
  + 活跃访客数
    + 访客回访频率，以及每次来访的停留时间
  + 内容生成与互动
    + 以某种方式与内容进行互动的访客比例，包括生成内容以及顶/踩行为
  + 参与度漏斗的变化
    + 应用是否有效地增加了用户参与度
    + 按月为单位或用户群展示漏斗内容，重要级别高的内容放在下面
  + 生成内容的价值
    + 内容的商业价值
    + 最好按照用户群或流量来源分开比较，这样可以提高获取新用户的投资收益比
  + 内容分享和病毒性
    + 内容是如何被分享的
    + 用于了解有没有达到足够的病毒式传播水平
    + 需要了解内容的分享方式和分享人群
    + 有助于了解是否应该考虑将付费门槛作为变现策略
  + 消息提醒的有效性
    + 看到推送通知、邮件通知或其他提醒时，给与回应的用户比例

### 用户生成内容：底线在哪里
+ 内容上传成功率
  + 对于这样的功能要持续优化，直到所有用户都能使用它
+ 平均每日应用停留时间
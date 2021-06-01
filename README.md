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










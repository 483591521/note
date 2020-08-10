### 查询语言分类

1. 数据定义语言：简称`DDL` (Data Definition Language)，用来定义数据库对象:数据库、表、列等；
2. 数据操作语言：简称`DML` (Data Manipulation Language)，用来对数据库中表的记录进行更新。关键字：insert、update、delete等
3. 数据控制语言：简称`DCL`(Data Control Language)，用来定义数据库访问权限和安全级别，创建用户等。关键字：grant等
4. 数据查询语言：简称`DQL`(Data Query Language)，用来查询数据库中表的记录，关键字：select from where等

### Mysql三大设计范式

- 1NF

不可分割性，只要字段值还可以继续拆分，就不满足第一范式。

不可分割的意思就按字面理解就是最小单位，不能再分成更小单位了。

字段只能是一个值，不能被拆分成多个字段，否则的话，它就是可分割的，就不符合一范式。

- 2NF

第二范式就是要有主键，要求其他字段都依赖于主键。

为什么要有主键？没有主键就没有唯一性，没有唯一性在集合中就定位不到这行记录，所以要主键。

在满足第一范式的前提下，主键外的每一列都必须完全依赖于主键。如果出现不完全依赖，只可能发生在联合主键的情况下。

- 3NF

在满足第二范式的前提下，除了主键列之外，其他列之间不能有传递依赖关系，即“消除冗余”。

消除冗余，就是各种信息只在一个地方存储，不出现在多张表中。

范式总结：范式，其实是用来学习参考的，设计的时候根据情况，未必一定要遵守，要灵活结合业务实际情况决定。

### Mysql常用函数

> **字符函数**

- length:获取字节个数(utf-8 一个汉字为3个字节,gbk为2个字节)

```mysql
SELECT LENGTH('cbuc') # 4
SELECT LENGTH('中文') # 6
```

- concat：拼接字符串

```mysql
SELECT CONCAT('C','_','BUC')   # 输出 C_BUC
```

- upper：将字母变成大写

```mysql
SELECT UPPER('cbuc')    # 输出 CBUC
```

- lower：将字母变成小写

```mysql
SELECT LOWER('CBUC')   # 输出 cbuc
```

- substr / substring：裁剪字符串

```mysql
substr(str,pos)       # str:要裁剪的字符串 ， pos:要裁剪的长度
substr(str,pos,len)   # str:要裁剪的字符串 , pos/len:从哪个位置开始裁剪几位
# substring同理
```

- instr：返回子串第一次出现的索引，如果没有则返回0

```mysql
SELECT INSTR('中不中','中')        # 输出 1 （mysql是从1开始算位数）
```

- trim：字符串去空格

```mysql
SELECT TRIM('  cbuc  ')                 # 输出 cbuc
SELECT TRIM('a' from 'aaaacbucaaaa')    #输出 cbuc
```

- rpad：用指定字符实现右填充指定长度

```mysql
SELECT RPAD('cbuc',6,'*')            # 输出 cbuc**
```

- replace 替换

```mysql
SELECT REPLACE('小明爱睡觉','睡觉','吃饭')        # 输出 小明爱吃饭
```

> ##### 数学函数

- round：四舍五入

```mysql
SELECT round(1.5)        # 输出  2
SELECT round(-1.5)        # 输出 -2 该四舍五入计算方式为：绝对值四舍五入加负号
```

- ceil：向上取整,返回>=该参数的最小整数

```mysql
SELECT CEIL(1.5);        # 输出  2
SELECT CEIL(-1.5);        # 输出 -1
```

- floor：向下取整，返回<=该参数的最大整数

```mysql
SELECT FLOOR(1.5);        # 输出  1
SELECT FLOOR(-1.5);        # 输出 -2
```

- truncate：截断

```mysql
SELECT TRUNCATE(3.1415926,2);        # 输出 3.14
```

- mod：取余

```mysql
SELECT MOD(10,3);        # 输出 1
SELECT MOD(10,-3);        # 输出 1
```

> 日期函数

- now：返回当前系统日期+时间

```mysql
SELECT NOW()               # 输出 2020-07-19 11:43:21
```

- curdate：返回当前系统日期，不包含时间

```mysql
SELECT CURDATE()        # 输出 2020-07-19
```

- curtime：返回当前时间，不包含日期

```mysql
SELECT CURTIME()        # 输出 11:45:35
```

- year/month/day 可以获取指定的部分，年、月、日、小时、分钟、秒

```mysql
SELECT YEAR(NOW())        # 输出 2020   其他用法一致
```

- str_to_date：将字符通过指定的格式转换成日期

```mysql
SELECT STR_TO_DATE('07-19 2020','%c-%d %Y')      # 输出 2020-07-19
```

- date_format：将日期转换成字符

```mysql
SELECT DATE_FORMAT(NOW(),'%Y年%m月%d日')        # 输出 2020年07月19日
```

- datediff：两个日期天数之差

```mysql
SELECT DATEDIFF(NOW(),'2020-07-14')           # 输出    5
```

> 其他函数

- VERSION：查看mysql 版本

```mysql
SELECT VERSION();           # 输出 8.0.21
```

- USER：查看当前用户

```mysql
SELECT USER()               # 输出 root@localhost
```


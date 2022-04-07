#### mysql索引

1. ​	对于任何DBMS，索引都是进行优化的最主要的因素
2. **如果对多列进行索引(组合索引)，列的顺序非常重要，MySQL仅能对索引最左边的前缀进行有效的查找。**
3. 索引是快速搜索的关键。MySQL索引的建立对于MySQL的高效运行是很重要的。
4. 

#### mysql索引类型包括：

1. 普通索引	

2.    这是最基本的索引、它没有任何限制、

3. 创建索引   create index indexName on Mytable( username(length) )

4. 修改表结构：alter mytable add index[ indexName ] on (username(length))

5. 创建表的时候直接指定

6. 

7. ```sql
   CREATE TABLE mytable( 
      ID INT NOT NULL, 
      username VARCHAR(16) NOT NULL, 
      INDEX [indexName] (username(length)) 
   ); 
   ```

8. 删除索引的语法：drop  index [indexName] on mytable

------

2.唯一索引

1. 它与前面的普通索引类似、不同的就是：索引列的值必须唯一、但允许有空值。如果是组合索引，则则列值的组合必须唯一

2. 实现方式：

3. 创建索引：create unique index indexName on mytable(username(length))

4. 修改表结构：alter mytable add unique [indexName] on (username(length))

5. 创建表的时候直接指定

6. 

7. ```sql
   CREATE TABLE mytable( 
      ID INT NOT NULL, 
      username VARCHAR(16) NOT NULL, 
      UNIQUE [indexName] (username(length)) 
   ); 
   ```

#### 主键索引

1. 它是一种特殊的唯一索引、不允许有空值。一般是在建表的时候同时创建主键索引

2. 

3. ```sql
   CREATE TABLE mytable( 
     ID INT NOT NULL, 
     username VARCHAR(16) NOT NULL, 
     PRIMARY KEY(ID) 
   ); 
   ```

**4.组合索引**

为了形象地对比单列索引和组合索引，为表添加多个字段：

```sql
CREATE TABLE mytable( 
   ID INT NOT NULL, 
   username VARCHAR(16) NOT NULL, 
   city VARCHAR(50) NOT NULL, 
   age INT NOT NULL 
); 
```

为了进一步榨取MySQL的效率，就要考虑建立组合索引。就是将 username, city, age建到一个索引里：

```sql
alter table mytable add index name_city_age(username(10),city,age);
```

建表时，usernname长度为16，这里用10。这是因为一般情况下名字的长度不会超过10，这样会加速索引查询速度，还会减少索引文件的大小，提高INSERT的更新速度。

如果分别在 usernname，city，age上建立单列索引，让该表有3个单列索引，查询时和上述的组合索引效率也会大不一样，远远低于我们的组合索引。虽然此时有了三个索引，但MySQL只能用到其中的那个它认为似乎是最有效率的单列索引。

建立这样的组合索引，其实是相当于分别建立了下面三组组合索引：
usernname,city,age
usernname,city
usernname

为什么没有city，age这样的组合索引呢？这是因为MySQL组合索引“最左前缀”的结果。简单的理解就是只从最左面的开始组合。并不是只要包含这三列的查询都会用到该组合索引，下面的几个SQL就会用到这个组合索引：

```sql
SELECT * FROM mytable WHREE username="admin" AND city="郑州"
SELECT * FROM mytable WHREE username="admin"
```

**二、使用索引的注意事项**
使用索引时，有以下一些技巧和注意事项：

**1.索引不会包含有NULL值的列**
只要列中包含有NULL值都将不会被包含在MySQL索引中，复合索引中只要有一列含有NULL值，那么这一列对于此复合索引就是无效的。所以我们在数据库设计时不要让字段的默认值为NULL。

**2.使用短索引**
对串列进行索引，如果可能应该指定一个前缀长度。例如，如果有一个CHAR(255)的列，如果在前10个或20个字符内，多数值是惟一的，那么就不要对整个列进行索引。短索引不仅可以提高查询速度而且可以节省磁盘空间和I/O操作。

**3.索引列排序**
MySQL查询只使用一个索引，因此如果where子句中已经使用了索引的话，那么order by中的列是不会使用索引的。因此数据库默认排序可以符合要求的情况下不要使用排序操作；尽量不要包含多个列的排序，如果需要最好给这些列创建复合索引。

**4.like语句操作**
一般情况下不鼓励使用like操作，如果非使用不可，如何使用也是一个问题。like “%aaa%” 不会使用MySQL索引而like “aaa%”可以使用索引。

**5.不要在列上进行运算**

```sql
select * from users where YEAR(adddate)<2007; 
```

将在每个行上进行运算，这将导致索引失效而进行全表扫描，因此我们可以改成

```sql
select * from users where adddate<‘2007-01-01’;  
```

**6.不使用NOT IN和<>操作**
NOT IN和<>操作都不会使用索引将进行全表扫描。NOT IN可以使用NOT EXISTS代替，id<>3则可以使用id>3 or id<3来代替。

**三、建立索引的时机**
到这里我们已经学会了建立索引，那么我们需要在什么情况下建立索引呢？一般来说，在WHERE和JOIN中出现的列需要建立索引，但也不完全如此，因为MySQL只对<，<=，=，>，>=，BETWEEN，IN，以及某些时候的LIKE才会使用索引。例如：

```
SELECT t.Name
FROM mytable t LEFT JOIN mytable m 
ON t.Name=m.username WHERE m.age=20 AND m.city='郑州'
```

此时就需要对city和age建立索引，由于mytable表的userame也出现在了JOIN子句中，也有对它建立索引的必要。
刚才提到只有某些时候的LIKE才需建立索引。因为在以通配符%和_开头作查询时，MySQL不会使用索引。例如下句会使用索引：

```
SELECT * FROM mytable WHERE username like'admin%'
```

而下句就不会使用：

```
SELECT * FROM mytable WHEREt Name like'%admin'
```

因此，在使用LIKE时应注意以上的区别。

**四、索引的不足之处**
上面都在说使用索引的好处，但过多的使用索引将会造成滥用。因此索引也会有它的缺点：
(1)虽然索引大大提高了查询速度，同时却会降低更新表的速度，如对表进行INSERT、UPDATE和DELETE。因为更新表时，MySQL不仅要保存数据，还要保存一下索引文件。
(2)建立索引会占用磁盘空间的索引文件。一般情况这个问题不太严重，但如果你在一个大表上创建了多种组合索引，索引文件的会膨胀很快。
索引只是提高效率的一个因素，如果你的MySQL有大数据量的表，就需要花时间研究建立最优秀的索引，或优化查询语句。

**排序对索引的影响**
order by是经常用的语句，排序也遵循最左前缀列的原则，比如key(a, b)，下面语句可以用到（测试为妙）

```
select * from tab where a > 1 order by b
select * from tab where a > 1 and b > '2015-12-01 00:00：00' order by b
select * from tab order by a, b
```

以下情况用不到
(1).非最左列，select * from tab order by b;
(2).不按索引列顺序来的，select * from tab where b > '2015-12-01 00:00:00' order by a;
(3).多列排序，但列的顺序方向不一致，select * from tab a asc, b desc。
初步了解以上内容后，就知道了索引冗余了，比如有了(a,b)索引，(a)就是冗余的，需要创建(a)索引时，直接创建(a)就行，而不是(id,a)，id指主键，主键primary key已经是UNIQUE KEY了，不用加唯一限制。

#### Mysql数据类型：

**1、整型**

#### Mysql存储过程

一、存储过程基本用法
1、创建存储过程

MySQL中，创建存储过程的基本形式如下：

```sql
CREATE PROCEDURE  存储过程名 (参数列表)
BEGIN
    SQL语句代码块
END
```
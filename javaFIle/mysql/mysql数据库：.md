### mysql数据库：

##### mysql：有点开源免费

1. mysql：唯一

2. 关键字的顺序

   ```sql
   select 
       .....(字符比如数字或字符串、表达式、调用内建函数、用户自定义的函数调用)
   from 
       .....
   where
       ....
   order by 
       .....
   ```

   ```sql
   select (5)
       .....
   from (1)
       .....
   where (2)
       ....
   group by (3)（它用于根据列值对数据进行分组）
       ....
   having  (4)
       ....
   order by (6)（用于对结果集中的原始列数据进行排序）
       .....
   limit startIndex,lingth (7)
       ......
   ```
   
   从某张表中查询数据、先经过where条件筛选出有价值的数据、对这些有价值的数据进行分组、分组之后可以使用having继续筛选 select 查询出来。最后排序属输出！

##### 一：概念 什么是数据库？ 什么是数据库管理系统？什么是Sql? 他们之间的关系是什么？

​       数据库：英文单词DataBase、简称 DB

​		数据库管理系统：DataBaseManagement、简称DBMS

​		数据库管理系统是专门用来管理数据库中数据的、数据库管理系统可以对数据库当中的数据进行增删改查

​		常见的数据库管理系统：mysql 、oracle、DB2、

##### 二：Sql  结构化查询语言、程序员需要学习SQl语句、程序员通过编写SQl语句、然后DBMS负责执行SQL语句

		1. 字符编码方式？设置mysql数据库的字符编码方式为UTF8
		1. mysql超级管理员用户名不能改、一定是：root

##### 三：mysql数据库的完美卸载！

1. 双击安装包进行卸载删除。
2. 删除目录：C:\ProgramData下面的mysql目录干掉。
3. net stop 服务名称；   net  start     服务名称

##### 四：mysql的常用命令：exit     desc table  查看表结构、mysql的结束语句  \c(用来终止一条命令的)

##### 五：数据库当中最基本的单元是表：table

	1. 什么是表table
	1. 数据库当中是以表格的形式表示数据的、因为数据比较直观。任何一张表都有行和列
	1. 行( row ) : 被称为数据 / 记录。                列（ column ）: 被称为字段。
	1. 约束：约束也有很多、其中一个叫做唯一性约束、这种约束添加之后、该字段中的数据不能重复。

##### 六：关于SQL语句的分类？

1. sql语句有很多、最好进行分门别类、这样更容易记忆。
2. 分为：
3. DQL：数据查询语言(凡是带有select关键字的都是查询语言)  select
4. DML：数据操作语言(凡是对表当中的数据进行增删改的都是DML)insert delete update
5. DDL：数据定义语言、凡是带有create、drop、alter、都是DDL、DDL主要操作的是表的结构
6. TCL：事务控制语言 事务提交：commit(事务提交)、rollback(事务回滚)
7. DCL：是数据控制语言。授权grant、撤销权限 revoke......

##### 七：导入数据 source   D:\cources\b.sql(路径中不要有中文)

##### 八：DQL（简单查询）查询一个字段？select 字段名  from 表名

1. 查询所有的字段怎么办？select a,b,c,d,   from  tablename;    select  *   from tablename;(效率低、可读性差)

2. 给查询的 列  起别名？ 列 as(关键字) 名字  不用as关键字也可以起别名'one'、中文使用  '年薪'

3. 可以进行运算  X、+、-、/、行字段可以使用数学表达式

4. 条件查询(=、<>、!= （不等于）<（小于）>= (大于等于)、between ....  and .... （遵循做小右大）、is null、

     and（并且）、or（或者）、in(包含，相当于多个or)、not   not 可以取非  like  %匹配任意个字符、下划线只匹配一个字符)

   1. and  和   or  同时出现的话、有优先级问题吗？and 优先级高于 or、括号的优先级高
   2. in 不是区间、in后面跟的是具体的值 in(800,50000)
   3. not 示例 is null    is not null   in    not  in 
   4. like称为模糊查询、支持 % 或 下划线 匹配、%（匹配任意的字符）、下划线(一个下划线只匹配一个字符)
   5. \  用来转义 、处理   _   下划线

##### 九：排序   order  by

1. 格式：select * from logs order by num desc;   降序   升序 asc
2. 可以两个字段排序吗？或者说按照多个字符排序？ 先按最左边的排序，然后在按后面的字段排序
3. 根据字段的位置也可以排序
   1. 格式：select ename  from logs order by 2;//2表示第二列
4. order by （排序总是在最后执行！！！）

##### 十：数据处理函数

1. 数据处理函数又被称为单行处理函数。（处理完行不变）

2. 单行处理函数有哪些

   1. lower  转换小写  示例：select lower(ename) from ....
   2. upper  转换大写  示例：select upper(ename) from ....
   3. substr  取子串     示例：select lower(ename，index1，length2) from ....(substr 被截取的字符串、起始下标(从1开始)、截取的长度)
   4. length()   取长度
   5. trim       去空格
   6. str_to_date 将字符串转换成日期
      1. str_to_date('字符串日期'、'日期格式')
      2. mysql的日期格式
      3. %Y 年、%m 月、%d 日、%h 时、%i 分、%s 秒
   
   7. data_format 格式化日期
      1. 格式 date_format(birth，'%m/%d/%Y')
   
   8. format  设置千分位
   9. round(参数1，保留几位小数)   四舍五入 （负数向前保留、正数向后保留）
   10. rand()   生成随机数
   11. ifnull     可以将null转换成一个具体值  null参与运算就是null
       1. 格式：ifnull(数据，被当做哪个值处理)如果为空被当作那个值处理
   12. concat(列1，列2)   字符串拼接
   13. case..when..then..when..then..else..end

   ##### 十一：分组函数（多行处理函数）
   
   1.  特点 多行处理函数 输入多行、最终输出一行
   
   2. count    计数
   
      1. 分组函数中count(*)和count(具体字段)有什么区别？
      2. count(*) 统计表当中总行数、、count(具体字段)：表示统计该字段下所有不为null的元素的总和

   3. sum     求和

   4. avg       平均值

   5. max       最大值  列column_name中的数据可以是数值、字符串或是日期时间数据类型。

   6. min        最小值 列column_name中的数据可以是数值、字符串或是日期时间数据类型。

   7. 注意：分组函数在使用的时候必须进行分组、然后才能用。如果你没有对数据进行分组、整张表默认为一组。
   
   8. 第一点：分组函数自动忽略null、你不需要提前对null进行处理。（null不能用=）
   
   9. 分组函数不能够直接使用在where子句中。
   
      

##### 十二：分组查询(非常重要)

1. 概要：在实际的应用中、可能有这样的需求、需求先进行分组、然后在对每一组的数据进行操作

   1. 格式:

      ```sql
      select 
            .........
      from 
            .......
      group by
            ........
      ```

2. 重点结论：在一条select语句当中、如果有group by语句的话、select后面只能跟：参加分组的字段、以及分组函数。其他的一律不能跟。

3. 使用having可以对分完组的数据进行过滤。having不能单独使用必须和group by 使用

4. 优化策略：where 和 having、优先选择where、where实在完成不了、在使用having

##### 十三：distinct

1. 把查询结果去除重复记录、注意：原表数据不会被修改、只是查询结果去重、
2. distinot 只能出现在所有字段的最前方
3. 统计工作岗位的数量？select  count(distinct) from emp;


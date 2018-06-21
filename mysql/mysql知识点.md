mysql基础

//mysql -uroot -ppassword

//show databases

//use database

//show tables

//创建表

create table `表名`(

```
\`id\` int\(10\) unsigned not null comment \`主键ID\`,


'name' varchar\(10\) not null comment \`姓名\`,


'age' int\(3\) unsigned not null comment \`年龄\`,


\`create\_time\` datatime not null comment \`创建时间\`,


\`update\_time\` timestamp not null comment \`更新时间\`,


 primary key \`id\`,


 unique key \`username\` \(\`name\`\),


 index  \`create\_time\` \(\`列名1\`,\`列名2\`\) 
```

);

//添加字段

alter table `表名` add column 字段名 int(3) unsigned default null after `字段名` comment `备注`;

//修改字段类型

alter table `表名` modify column 字段名 int(4);

//修改字段名称需要重新指定字段类型

alter table `表名` change column 字段名 字段名2 int(4);

//删除字段

alter table `表名` drop column 字段名;

//删除表中数据，可以返回删除行数，自增键初始值归为1

delete from 表名;

//删除表中数据，自增键初始值不归为1

delete from 表名 where 1=1;

//删除表中数据,不返回删除的记录数

truncate table 表名

//delete和truncate的区别

1delete可以指定删除的记录

2truncate删除全部

3delete返回删除记录数

4truncate不返回输出记录数

5delete删除是遍历删除，效率没有truncate高

mysql索引

索引是在存储引擎中实现的，不同的存储引擎支持的索引也是不一样的。

MyISAM引擎：B-TREE索引类型，R-TREE索引，FULL-TEXT索引

InnoDB引擎：B-TREE索引

Memory引擎：B-TREE索引，HASH索引

B-TREE索引

普通索引

create table 表名 (列名，列名，index 索引名 (`索引列`,`索引列`));

alter table 表名 add index 索引 (`索引列`,`索引列`);

create index on table 索引名 (`索引列`,`索引列`);

唯一索引

create table 表名 (列名,列名, unique 索引名 (`索引列`,`索引列`));

alter table 表名 add unique 索引名 (`索引列`);

create unique on table 索引名 (`索引列`);

主键索引

create table 表名 (列名，列名, primary key 索引名 (`索引列`));

alter table 表名 add primary key 索引名 (`索引列`);

删除索引

drop index 索引名 on table 表名;

alter table 表名 drop index 索引名;

alter table 表名 drop primary key;

删除列对于索引的影响：

删除某一列，该列所在的索引上也会删除该列，如果删除了某个索引上的所有列，该索引也会被删除;

查看索引

show index from 表名

show keys from 表名



索引选择原则

1where条件后面的字段，join关联的字段，使用索引，不是select 后面的字段建立索引

2索引列的基数越大，效果越好，比如出生日期，很容易区分，而表示性别的列，不建议索引

3使用短索引，比如一个200长度的字符串，前10个字符多数是唯一的，那么前10个字符建立索引即可

4利用最左前缀原则

5表记录过少不建议建立索引，2000为限

6索引选择性，指不重复的索引值，计算规则，count(distinct 列)/count(*)

7<,<=,=,>,>=和like情况(不是以%开头)情况下，该列索引才会有效

8索引不要建立太多，频繁修改的字段不建议索引，因为索引的建立是占用额外的磁盘空间的，建立太多或者频繁更新字段都会影响效率

sql常用函数

ifnull(expr1,expr2):如果expr1不为null返回expr1,否则返回expr2；

if(expr1,expr2,expr3):如果expr1为true(expr1<>0,expr1<>null)返回expr2,否则返回expr2；

isnull()用在where语句后面，select * from table_name where isnull(列)；

is null 和 is not null 也是用在where后面, select * from table_name where 列 is null或select * from table_name where 列 is not null

# 
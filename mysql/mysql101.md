1. 创建数据库

   ```
   create database ${db_name};
   
   create database atlantis_db;
   ```

1. 创建用户

   ```
   create user '${user_name}'@'${host}' identified by '${password}';
   
   create user 'yhyc'@'%' identified by 'Yhyc@Mysql0.';
   
   drop user 'yhyc@%';
   ```

1. 赋予相应权限

   ```
   grant all on ${db_name}.* to '${user_name}' identified by '${password}';
   
   grant all on atlantis_db.* to 'yhyc'@'%' identified by '${password}';
   ```

   



vm1:

username:	test@%

password:	test_Mysql0.

db_name:	test

## Mysql 常用操作

### Example

```mysql
mysql> alter table redis_choose
    -> add column machine_key varchar(50) not null comment "机器标识",
    -> add column random_master varchar(20)  not null default 0 comment "主随机数",
    -> add column random_slave varchar(20) not null default 0 comment "备随机数",
    -> add column enforce int(2) default 0 comment '强制',
    -> add column run_machinekey varchar(20) comment "标识" after machine_key
    -> ;

mysql> alter table redis_choose
    -> add primary key(id),
    -> add unique(machine_key),
    -> change run_machinekey run_machine_key varchar(50),	change用于改名
    -> modify id int not null auto_increment				modify用于修改列属性
    -> ;
```

### database

1. show

   ```mysql
   show databases;
   ```

1. create

   ```mysql
   create database ${db_name};
   ```

1. drop

   ```mysql
   drop database ${db_name};
   ```

### 表

1. show all tables

   ```mysql
   show tables;
   ```

1. show table struct

   ```mysql
   desc `${table_name}`;
   ```

1. create

   ```mysql
   create table [${database_name}.].${table_name} (
   	`id` int not null auto_increment,
   	`name` varchar(128) default "" comment "姓名",
   	`age` int not null default 0 comment "年龄",
   	primary key(`id`),
     unique index `name_unique_index`(`name`)
   )engine=innodb default charset=utf8;
   ```

    显示建表语句

   ```mysql
   show create table `${table_name}`;
   ```

   ```mysql
   CREATE TABLE `user` (
     `id` int(11) NOT NULL AUTO_INCREMENT,
     `name` varchar(128) NOT NULL DEFAULT '' COMMENT '姓名',
     `age` int(11) DEFAULT '0',
     PRIMARY KEY (`id`),
     UNIQUE KEY `name_unique_index` (`name`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8
   ```

1. alter

   1. 添加表注释

      ```mysql
      alter table `${table_name}` comment "";
      
      alter table `user` comment "用户表";
      ```

   1. 新建列

      ```mysql
      alter table `${table_name}` add column `${column_name}` ${column_desc} after `${column_name}`;
      
      alter table `user` add column `gender` int not null default 0 comment "性别：0-male;1-female" after `name`;
      ```

   1. 删除列

      ```mysql
      alter table `${table_name}` drop column `${column_name}`;
      
      alter table `user` add column `test` int;
      alter table user drop column `test`;
      ```

   1. 更新列

      更改列名/添加列注释/调整列顺序

      modify/change区别：change 更改为新列名字；modify只能修改列描述，不能改列名称。

      ```mysql
      alter table `${table_name}` modify `${column_name}` ${column_desc} after `${another_column}`;
      alter table `${table_name}` change `${column_name}` `${new_column_name}` ${column_desc} after `${another_column}`;
      ```

1. drop

   ```mysql
   drop table if exists [${database_name}.]${table_name};
   ```

### 索引

1. show

   ```mysql
   show index from `${table_name}`;
   ```

1. create

   ```mysql
   create [unique] index `${index_name}` on `${table_name}`(`${column_name}`[,`${column_name_2}`]);
   
   alter table `${table_name}` add constraint `${index_name}` unique(`${column_name}`[,`${column_name_2}`]);
   ```

1. drop

   ```mysql
   drop index `${index_name}` on `${table_name}`;
   alter table `${table_name}` drop index `${index_name}`;
   ```




## mysql 通配符

```
% 0-n 个字符
_ 1 个字符
[abc] 其中一个字符
[^abc] [!abc] 不是abc的一个字符
```



## mysql 细节相关

1. 查看日志位置

   > select @@log_error;

1. 查看当前用户

   > select user();

1. 更改自动递增列的起始值

   ```sql
   alter table `${table_name}` auto_increment=${start_value}
   
   alter table `user` auto_increment=1000
   ```

1. 时间相关操作

   ```sql
   mysql> select now(), curdate(),curtime();
   +---------------------+------------+-----------+
   | now()               | curdate()  | curtime() |
   +---------------------+------------+-----------+
   | 2019-04-16 17:10:46 | 2019-04-16 | 17:10:46  |
   +---------------------+------------+-----------+
   1 row in set (0.00 sec)
   ```

   对于datetime类型的字段判等时必须是**yyyy-MM-dd hh:MM:ss 全部相同**，用between时可以**省略**yyyy-MM-dd hh:MM:ss中的一些字段，省略的字段默认以**0替代**。

1. null相关操作

   ```sql
   `${column}` is null / `${column}` is not null 判断一个字段是否为null
   '' is null 返回false
   0 is null 返回false
   
   select ifnull(`${column}`, 0) 可以把null值转换成0值
   ```

1. 聚合查询

   ```
   select count(*) from `${table_name}`
   select count(`${column}`) from `${table_name}` // 按某列聚合时，会忽略字段为null的行
   select count(distinct(`${column}`)) from `${table_name}`
   
   ```

   
#create table
```sql
create table if not exists 'table_name' {
    id int unsigned auto_increment,
    title varchar(100) not null,
    author varchar(40) not null,
    created date,
    primary key ('id')
} engine=InnoDB default charset=utf8;
```

#insert
```sql
insert into table_name (field1, field2, field3)
    values ( value1, value2, value3, value4);
```

# insert field
```sql
alter table table_name add 'column_name' after 'column_name2';
```

# add index
```sql
#primary key
alter table table_name add primary key index_name(column_name);

#unique index
alter table table_name add unique index_name(column_name);

#normal index
alter table table_name add index index_name(column_name);
alter table table_name add index index_name(column_name, column_name2);

# fulltext index
alter table table_name add fulltext index_name(column_name);
```

#delete
```sql
# delete
delete from table_name where column_name = '';


# truncate table
truncate table table_name;

# drop table
drop table table_name;

# drop field
alter table table_name drop column_name;

# drop index
alter table table_name drop index index_name(column_name);
```


#update
```sql
#update record
update table_name set column_name=value where column_name=value;

#change fieldname
alter table table_name change column_name new_column_name;
```

#query
```sql
# normal query
select field1, field2 from table_name where column_name=value;

# join, left join, right join, inner join
select * from table as a join table2 as b where a.field1=b.field2;

select * from class c left join students s on c.id = s.class_id;
select * from class c left join students s on c.id = s.class_id where s.class_id is null;

select * from class c inner join students s on c.id = s.class_id;

select * from students s right join class c on  c.id = s.class_id; 
select * from students s right join class c on  c.id = s.class_id where s.class_id is null;


# query index
show index from table_name;
```

# copy table and data
```sql
create table table_name like table_name2;

insert into table_name select * from table_name2;
```


# other
```bash
# connection
mysql -h host -u root -p

# import sql
mysql -u root -p123456 < runboo.sql

# export sql
mysqldump -h host -u root -p "db_name" "table_name" > file_name.sql

# slow log
mysqldumpslow -s [c:按记录次数排序/t:时间/l:锁定时间/r:返回的记录数] -t [n:前n条数据] -g "正则"　/path

# mysql函数
select now() as now;
select uuid() as uuid;
select md5('123') as pass;
select concat(name,'__',email) from users;

#mysql触发器
delimiter $

create trigger some_trigger "before|after" "insert|load data|replace|update|delete"
on students for each row
begin
    set class_id = old.class_id; //old.name 删除行的某列数据, new.name 新增行的某列数据
    update class set name=students.name where id=students.class_id;
end $

delimiter ;

#mysql存储函数
#存储函数有且只有一个返回值，而存储过程不能有返回值
#存储函数只能有输入参数
#存储函数可以作为查询语句的一个部分来调用
#调用: select get_users_by_id(2);
delimiter $

create function get_users_by_id (user_id int) returns varchar(20)
begin
    return (select name from users where id=user_id);
end $

delimiter ;

#mysql存储过程
#调用: call get_users_by_id(4);
delimiter $

create procedure get_users_by_id (IN user_id int)
begin
    select * from users where id=user_id;
end $

delimiter ;

# explain
# 关注查询结果的rows
# https://segmentfault.com/a/1190000008131735
explain select * from users;
```

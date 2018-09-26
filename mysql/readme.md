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

# explain
explain select * from users;
```

# web_programming_final
web_programming_final

```php
create table student_tbl (
id char(6) PRIMARY KEY,
name char(4) NOT NULL,
gender char(1),
age tinyint(3) unsigned,
depart varchar(8) NOT NULL,
year tinyint(2) unsigned,
address varchar(15)
);
```

```php
create table subject_tbl (
subject varchar(10),
code char(5),
credit tinyint(2) unsigned NOT NULL,
classify char(4) DEFAULT '일반선택',
PRIMARY KEY(subject)
);
```

```php
create table score_tbl (
number mediumint(6) KEY AUTO_INCREMENT,
id char(6) NOT NULL,
subject varchar(10) NOT NULL,
point tinyint(3)  NOT NULL,
FOREIGN KEY(id) REFERENCES student_tbl(id) 
ON UPDATE CASCADE ON DELETE CASCADE ,
FOREIGN KEY(subject) REFERENCES subject_tbl(subject) 
ON DELETE CASCADE ON UPDATE CASCADE
);
```

```php
load data infile 'student_comma' into table student_tbl
fields terminated by ','
lines terminated by '\r\n';
```

```php
load data infile 'subject_comma' into table suject_tbl
fields terminated by ','
lines terminated by '\r\n';
```

```php
load data infile 'score_comma' into table score_tbl
fields terminated by ','
lines terminated by '\r\n';
```

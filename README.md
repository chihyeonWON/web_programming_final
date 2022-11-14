# web_programming_final
web_programming_final

## 생성할 테이블 구조도
![image](https://user-images.githubusercontent.com/58906858/201564260-1420c2fe-49b8-4342-9727-c272a235f87e.png)


## 테이블 생성

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
point tinyint(3)  NOT NULL
);
```

## 연결 설정(Foreign key 설정한 score_tbl)
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
## 테이블에 데이터를 파일로 입력
  
```php
load data infile 'student_comma.dat' into table student_tbl
fields terminated by ','
lines terminated by '\r\n';
```

```php
load data infile 'subject_comma.dat' into table suject_tbl
fields terminated by ','
lines terminated by '\r\n';
```

```php
load data infile 'score_comma.dat' into table score_tbl
fields terminated by ','
lines terminated by '\r\n';
```

## 필드 데이터 업데이트 (연관성있는 것도 변경) Primary key와 Foreign 키 설정

```php
update subject_tbl set subject = "중세한국사" where code = 'C2084';
```

## 데이터 삭제 

```php
delete from table명
```

## 테이블 삭제

```php
drop table table명
```

## auto_increment 값 조정
```php
alter table table명 auto_incremnt=1;
```

## 규칙

![image](https://user-images.githubusercontent.com/58906858/201563700-01dcfba7-c12a-45fd-bb82-ba3f64c87702.png)


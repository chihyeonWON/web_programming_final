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

## PHP와 MySQL 연동

MySQLi 확장은 절차지향적, 객체지향적 API를 함께 제공하고 목적에 따라 적절한 방식을 선택하여 사용 가능합니다.

## MySQLi API <- 함수에 접근하는 유형(절차지향, 객체지향) 코딩 스타일

(1) 절차지향 방식
```PHP
$host = "localhost";
$user = "root";
$link = mysqli_connect($host, $user);
mysqli_select_db($link, "friend");
$result = mysqli_query($link, "SELECT name FROM friend");
$number = mysqli_num_rows($result);
mysqli_close($link);
?>

(2) 객체주어(중심) 방식
```PHP
$host = "localhost";
$user = "root";
$link = new mysqli($host, $user);
$link->select_db("friend"); // link는 데이터베이스 friend를 선택
$result = $link->query("SELECT name FROM friend"); // link는 다음의 쿼리를 실행
$number = $result->num_rows; // result는 num의 개수를 계산
$link->close();
?>

(3) 혼합형
```PHP
$host = "localhost";
$user = "root";
$link = new mysqli($host, $user);
$link->select_db("friend"); // link는 데이터베이스 friend를 선택

$result = mysqli_query($link, "SELECT name FROM friend"); <- 절차지향 방식 혼합

$number = $result->num_rows; // result는 num의 개수를 계산
$link->close();
```
 
두 방식은 큰 차이가 없습니다. 사용자는 개인 취향에 따라 선택할 수 있습니다.

## 사용자 계정의 비밀번호 설정

비밀번호 관련 xampp/mysql/data/mysql 안에 user 테이블에 있음

desc user

비밀번호 설정 명령어 : set password = password('');

## user 테이블의 password 필드
![image](https://user-images.githubusercontent.com/58906858/201844354-790fa85e-62f4-4a54-8a33-ea8473092b2a.png)

localhost = 127.0.0.1 자기주소
::1 -> IPv6 주소

select host, user, password from user; << 비밀번호 확인

![image](https://user-images.githubusercontent.com/58906858/201845407-287015e9-2725-40c2-8e49-544275aab72f.png)

비밀번호 설정 명령어 : set password = password('설정할 패스워드');

flush privileges : 이 계정과 비밀번호로 접속했을 때모든 권한을 주겠다.

## MySQLi 확장 함수와 상수

https://www.php.net/manual/en/mysqli.summary.php


```php
$mysqli::query() => $mysqli->query()
$mysqli_result::affected_rows => $mysqli_result->affected_rows
```

일반적으로 mysqli 객체 변수명칭을 쓰지만 개발자가 원하는 명칭을 사용해도 됩니다.
```PHP
$link = new mysqli($host, $user);
$link->select_db("friend);
$result = $link->query("SELECT name FROM friend);
$number = $result->fetch_array(MYSQLI_BOTH);
$link->close();
```





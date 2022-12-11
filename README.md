# web_programming_final
web_programming_final
```
테이블의 구조(필드) 변경

column 옵션은 써도되고 안써도됨

alter table 테이블명 add(추가) drop(삭제) modifiy(데이터타입만) change(이름, 데이터타입)
적용할 필드명 데이터타입

데이터타입 수정modify
alter table table_name modify name int(10);

이름수정 change // 과거 필드이름 쓰고 데이터타입도 지정 둘다 바꿀려면 change 써야함
alter table table_name change old_name name int(10);

테이블의 이름 변경 rename table old_table new_table와 같은 기능

alter table 과거 테이블이름 rename 바꿀 이름

날짜형 데이터는 칸수를 지정하지 않습니다. (YYYY-MM-DD)으로 데이터 입력

숫자형 데이터는 0칸이거나 지정안해도 숫자가 그대로 표시(기본값이 있음)

실수형 decimal(값, 소수 자릿수) 가변

필수 데이터인 경우 not null 지정

다른 레코드와 중복값이 없는 필드 <- primary key로 지정 자동으로 not null 지정
2개이상 지정 -> primary key가 2개가 아니라 2개가 합쳐져서 하나의 primary key 역할

default 데이터 <- 데이터가 없을 때 기본값 지정

auto_increment : 자동 증가값 옵션
반드시 primary key를 같이 지정

데이터 입력
insert into 테이블명(필드 나열) values (데이터 나열)

필드명 없이 모든 데이터 입력
insert into 테이블명 values(데이터 나열)

일부 필드에만 데이터 입력
insert into 테이블명 (필드 나열) values (필드 순에 맞게 나열)

load data infile ‘데이터파일.data’ into table 테이블명 
fields terminated by ‘,’   
lines terminated by ‘\r\n’;
select 연산 as ‘더하기’ // 콜롬명 지정

특정 필드 데이터 검색
select 검색하고자 하는 필드명 from 테이블명

필드 이름 변경해서 검색 AS 생략가능
select 필드명 AS ‘바꾸고자하는 필드명’, 필드명 AS ‘바꾸고자하는 필드명’ from 테이블명

조건문을 이용한 데이터 검색
select 필드명 from 테이블명 where 조건문

함수를 이용한 데이터 검색
AVG(평균), COUNT(개수)

select AVG(필드명) FROM 테이블

와일드 카드 LIKE를 이용한 데이터 검색
% : 0개 이상
_ : 1개

서울시로 시작하는 필드 데이터 출력
select 필드명 from 테이블명 where 필드명 like ‘서울시%’;

그룹 by: 그룹별로 계산

score_tbl 테이블에서 학번(id)별로 취득 과목수(subject), 평균값 출력
select id ‘학번’, count(point) ‘과목 수, avg(point) ’평균‘ from score_tbl group by id;

score_tbl 테이블에서 과목별(subject)로 점수(point) 취득 학생수 출력
select subject ‘과목명’, count(subject) ‘학생수’ from score_tbl group by subject;

having : 그룹별로 계산한 결과에서 조건 추가

score_tbl 테이블에서 학번(id)별로 평균이 90 이상인 학번 출력
select id ‘학번’, avg(pooint) ‘평균’ from score_tbl group by id having avg(point) >= 90;

score_tbl 테이블에서 과목별(subject)로 점수(point) 취득 학생수가 8이상 출력
select subject ‘과목명’, count(subject) ‘학생수’ from score_tbl group by subject having count(subject) >=8;

order by : 데이터 정렬

필드명이 적은 순으로 정렬 : 오름차순 order by 필드명 asc
필드명이 높은 순으로 정렬 : 내림차순 order by 필드명 desc


2개 이상의 정렬 기준을 적용 나이 같을 때 최근 학번순으로 정렬

select name ‘이름’, age ‘나이’, id ‘학번’ from student_tbl order by age asc, id desc;

limit 출력 개수 지정
최근 학번 순으로 3개의 레코드 출력 (order by, limit 이용)
select * from student_tbl order by id desc limit 3;

into outfile ; 출력 결과의 저장
select 쿼리문의 출력 결과를 파일로 생성할 수 있고 이 파일을 다시 데이터 파일로 사용할 수 있음
기본으로는 ‘\r\n’, ‘\t’으로 생성되지만 변경할 수 있음

select id, avg(point) from score_tbl group by id 
into outfile ‘avg_comma.dat’ fileds terminated by ‘,’;

중복 데이터 하나만 출력
select distinct subject from score_tbl;
과목 데이터 중복은 하나만 출력

테이블 여려개 검색 table명.필드명

select 테이블명.필드명, 다른테이블명,다른필드명 from 테이블명, 다른테이블명 where 테이블명.필드명 = 테이블명.필드명

데이터 값 수정 update

update 테이블명 set 필드명=‘바꿀데이터’ where 조건문

score_tbl에서 프레임워크 과목의 점수를 5점 감점

update score_tbl set point = point-5 where subject=“프레임워크”;

데이터 삭제

delete from 테이블명 where 조건문;

데이터삭제해도 숫자가 이어지는 문제는 auto_increment =1로 수정
alter table score_tbl auto increment = 1;







사용자 계정 비밀번호 설정

set password = password(‘1234’);
flush privileges; // 바로 적용

(1) 1개 DB에 2개 테이블 생성

create table 상위테이블 {
	id char(6) Primary key
}

create table 하위테이블 {
	id char(6) not null,
	foreign key(id) reference 상위테이블(id) on delete cascade on update cascade
}	
(2) foreign key 생성
(3) 2개의 테이블을 이용한 select 검색
student_tbl에는 id, name이 있고 score_tbl에는 id, subject, point가 있습니다. id라는 공통점이 두 테이블에 존재

문제 : student_tbl, score_tbl의 id이 동일한 레코드를 찾아서 student_tbl에서 name을 score_tbl에서 subject, point를 찾아서 출력


1. where 사용 select 찾고자하는테이블명.필드 from 두 테이블명 where 조건 
select student_tbl.name, score_tbl.subject, score_tbl.point from student_tbl, score_tbl where 
student_tbl.id = score_tbl; 


2. join 사용 select 찾고자하는테이블명.필드 from 테이블명 join 다른테이블명 on 조건
select student_tbl.name, score_tbl.subject, score_tbl.point from student_tbl join score_tbl on student_tbl = score_tbl;

1. select score_tbl.id, subject_tbl.SUM(subject) from score_tbl, student_tbl where subject_tbl.subject = score_tbl.subject group by id

2. select score_tbl.id, subject_tbl.SUM(subject) from score_tbl join student_tbl on score_tbl.subject = student_tbl.subject group by id

(4) 데이터 추가 폼파일을 학생이 직접 생성
form.php, insert.php 활용
```
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

## PHP와 MySQL 연동

1. MySQL 접속
2. 데이터베이스 선택
3. 쿼리문 실행
4. MySQL 종료

*Apache 서버를 실행시켜야 합니다.

1. MySQL 접속

객체 중심 : $link = new mysqli('localhost', 'user', 'password', 'dbname');
절차 지향 : $link = mysqli_connect('localhost', 'user', 'password', 'dbname');

```php
<?php
//$link = new mysqli("localhost", "root", "1234");
$host = "localhost";
$user = "root";
$password = "1234";
$link = new mysqli($host, $user, $password);
//$link = mysqli_connect($host, $user, $password);
?>
```

접속 성공하면 DB 접속 성공
```PHP
<?php
$host = "localhost"; $user = "root"; $password = "1234";
$link = new mysqli($host, $user, $password);
if (!$link) {
    die("DB 접속 실패" . $link->connect_error); // die -> 출력하고 프로그램 종류
} else echo "DB 접속 성공<br>";
?>
```

## 기존 데이터베이스 선택
```PHP
<?php
$host = "localhost"; $user = "root"; $password = "1234";
$dbname = "mysql";
$link = new mysqli($host, $user, $password, $dbname);
if (!$link) {
    die("DB 접속 실패" . $link->connect_error); // die -> 출력하고 프로그램 종류
} else echo "DB 접속 성공<br>";
?>
```

## 접속 후 데이터 베이스 선택 : select_db()
```PHP
<?php
$host = "localhost"; $user = "root"; $password = "1234";
$link = new mysqli($host, $user, $password);
$mydb = $link->select_db("mysql"); // return 되는 값 : 0 또는 1
// db접속이 되었는지 추가 확인
```

## PHP로 데이터 베이스 생성 (쿼리문 작성)
```PHP
<?php
$host = "localhost"; $user = "root"; $password = "1234";
$link = new mysqli($host, $user, $password);
$link->query("create database abc");
//mysqli_query($link, "create database testdb");
?>
```

## DBMS 종료 : close()

객체 중심 : $link->close()
절차 지향 : $mysqli_close($link);

## 기말고사 프로젝트

https://www.dothome.co.kr/
![image](https://user-images.githubusercontent.com/58906858/201856822-e8d36973-36ef-4bbc-8ec9-1e4b06b169b7.png)

id : heungeob1003
pw : h!

http://114.71.72.35/grade/

11월 21일 다음 주 월요일까지 제출
12월 15일까지 기획서(테이블, 용도, 목적 명시) 제출 도메인잡아서 제출

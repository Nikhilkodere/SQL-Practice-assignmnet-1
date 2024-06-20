**Task 1 :create database if not exists assignments;**

 create table shopping_history(
product  varchar(40) not null,
quantity int not null,
Unit_price int not null);

insert into shopping_history values
("Apple",10,20),
("Biscuit",2,50),
("Apple",2,25),
("shoe Polish",1 ,60),
("shoe", 1,1500),
("Shirt",2,1499),
("Biscuit",10,155);

with a as (
select product, quantity,Unit_price,(quantity * Unit_price)as total_price from shopping_history group by 1,2,3
) 
select product,sum(total_price)as total_price from a group by product order by 1;



**Task 2.1**
create table telecommunication_phone
(`Name` varchar(10),
phone_number int);

insert into telecommunication_phone values("Nikhil",12345),
("Rahul",56789),
("Abhi",13579),
("Jay",24680);

select * from telecommunication_phone
create table telecommunication_call
(idd int,
caller_phone int,
Callee_phone int,
duration int)

insert into telecommunication_call values(01,12345,24680,8),
(12,56789,13579,1),
(32,13579,12345,4),
(42,13579,56789,4),
(244,13579,12345,2),
(268,24680,12345,6),
(118,56789,12345,2);

select * from telecommunication_call;
select y.`Name`, z.* from(with a as(select  caller_phone,sum(duration)duration from telecommunication_call group by caller_phone
union
select  callee_phone,sum(duration)duration from telecommunication_call group by callee_phone)
select caller_phone,sum(duration)duration from a group by caller_phone) as z inner join telecommunication_phone y on y.phone_number = z.caller_phone
where duration >= 10;



**Task 2.2**
use assignments;
create table telecommunication_phone
(`Name` varchar(10),
phone_number int);

insert into telecommunication_phone values("Nikhil",12345),
("Rahul",56789),
("Abhi",13579);

select * from telecommunication_phone
create table telecommunication_call
(idd int,
caller_phone int,
Callee_phone int,
duration int)

insert into telecommunication_call values(01,12345,24680,8),
(12,56789,13579,1),
(32,13579,12345,4),
(42,13579,56789,4),
(244,13579,12345,1),
(268,24680,12345,1),
(118,56789,12345,2);

select * from telecommunication_call;
select y.`Name` from(with a as(select  caller_phone,sum(duration)duration from telecommunication_call group by caller_phone
union
select  callee_phone,sum(duration)duration from telecommunication_call group by callee_phone)
select caller_phone,sum(duration)duration from a group by caller_phone) as z inner join telecommunication_phone y on y.phone_number = z.caller_phone;


**Task 3.1 :**
create database if not exists Practices;
use practices ;
create table if not exists transactions
(amount int not null,
date_info date);

insert into transactions values (
 1000, '2020-01-06' ) ,
(-10, '2020-01-14' ) ,
(-75, '2020-01-20' ),
(-5, '2020-01-25' ) 
, (-4, '2020-01-29' ) 
,( 2000, '2020-03-10' )  
, (-75, '2020-03-12' )  
, (-20, '2020-03-15' )  
, ( 40, '2020-03-15' )  
,(-50, '2020-03-17' )  
,(200, '2020-10-10' ) 
, (-200, '2020-10-10' ) ;

select * from transactions;

### monthly transcation atleast 3 and credit card transaction <= -100

	select (sum(amount)-(12 -(with a as(select sum(amount)as amount,substring(date_info,6,2) as month,count(amount)as payment_count from transactions where amount < 0 group by 2)select count(*) from a where  payment_count >= 3 and amount <= -100))*5) balance from transactions;



**Task 3.2**
create database if not exists Practices;
use practices ;
create table if not exists transactions2
(amount int not null,
date_info date);

insert into transactions2 values (
 1, '2020-06-29' ) ,
(35, '2020-02-20' ) ,
(-50, '2020-02-03' ),
(-1, '2020-02-26' ) 
, (-200, '2020-08-01' ) 
,( -44, '2020-02-07' )  
, (-5, '2020-02-25' )  
, (1, '2020-06-29' )  
, (1, '2020-06-29' )  
,(-100, '2020-12-29' )  
,(-100, '2020-12-30' ) 
, (-100, '2020-12-31' ) ;

select * from transactions2;

### monthlt transcation atleast 3 and credit card transaction ><= -100

select (sum(amount)-(12 -(with a as(select sum(amount)as amount,substring(date_info,6,2) as month,count(amount)as payment_count from transactions2 where amount < 0 group by 2)
select count(*) from a where  payment_count >= 3 and amount <= -100))*5) balance from transactions2;



**Task 3.3**
create table if not exists transactions3
(amount int not null,
date_info date);

insert into transactions3 values (	
 6000, '2020-04-03' ) ,
(5000, '2020-04-02' ) ,
(4000, '2020-04-01' ),
(3000, '2020-03-01' ) 
, (2000, '2020-02-01' ) 
,( 1000, '2020-01-01' )  ;


select sum(amount)-(12*5) from transactions3;

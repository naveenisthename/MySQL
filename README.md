# MySQL

Introduction:

This repository contains SQL queries for basic database management operations like create, insert, select, delete, update, import, and advanced operations like between, like, group by, and many more. These queries are helpful for beginners as well as intermediate level SQL learners.


SQL Queries :

1.CREATE :

CREATE DATABASE supermart;
USE supermart;
CREATE TABLE customer_table (
id int,
First_Name varchar(30),
age int
);


2.INSERT :

INSERT into customer_table (id,First_Name,age) values (1,'Raja',23);

INSERT into customer_table values (2,'Ram',25);

INSERT into customer_table values (2,'Ram',25),(3,'Giri",24);


3.IMPORT :

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/textfile.txt' INTO
TABLE customer_table
FIELDS TERMINATED BY
IGNORE 1 ROWS;


4.SELECT :

SELECT * FROM customer_table;

SELECT First_Name from customer_table;

SELECT First_Name,age from customer_table;


5.DISTINCT : (remove dublicates)

SELECT DISTINCT First_Name from customer_table;

SELECT DISTINCT First_Name,age from customer_table;


6.WHERE :

select First_name,age from customer_table where age=23;

select First_name,age from customer_table where First_Name='Naveen';


7.LOGICAL OPERATORS :

select First_Name from customer_table where age>20 and age<25;

select First_Name from customer_table where age>26 or age<30 or First_Name="Naveen";

select First_Name,Last_Name from customer_table where not age>22 and not
First_Name="Madhu";


8.UPDATE :

UPDATE customer_table set First_Name="Ganesh" where cus_id=3;

set sql_safe_updates=0; (OFF the safe mode in SQL)

Update customer_table set mail_id="ganeshtharan@gmail.com" where First_Name='Ganesh';

set sql_safe_updates=1; (ON the safe mode in SQL)


9.DELETE :

DELETE from customer_table; (All)

delete from customer_table where cus_id=5; (Single)

delete from custome_table where age>24; (Multiple)


10.ALTER :

ALTER TABLE customer_table ADD Test varchar(30); (add a new column)

ALTER TABLE customer_table DROP Test; Delate a column)

ALTER TABLE customer_table MODIFY COLUMN age varchar(20); (Modify a new column)

ALTER TABLE customer_table CHANGE age age_varchar varchar(20); (Change the name of
the column)

ALTER TABLE customer_table ADD CONSTRAINT cus_id CHECK(cus_id>0); (it will add or
modify values according to the condition only)

ALTER TABLE customer_table ADD PRIMARY KEY (cus_id); (Adding primary key ,can't allow
to the duplicate values)

INSERT INTO customer_table
values(1,"Saravana","Kumar","sravanakumar@gmail.com",27),(1,"Saravana","Kumar","sravana
kumar@gmail.com",27);


11.IN :

SELECT * from customer where state IN ('California','New York'); (Instead of OR)


12.BETWEEN :

select * from customer where age BETWEEN 25 and 40; (Instead of AND)

select * from customer where age not BETWEEN 25 and 40;


13.LIKE :

select * from sales WHERE Customer_ID like '%5';

select * from sales WHERE Product_ID like "OFF%";

select * from sales WHERE Ship_Date like "%-11-%";

select * from customer WHERE Customer_Name like "_____ %";

select Order_ID ,Customer_ID,Profit from sales where Profit like '50%';

select Postal_Code,State from customer where State not like "New York%";

select * from product where Product_Name like "G\%";


14.ORDER :

select * from customer order by age ;

select * from customer order by 2 asc

select * from customer where State="california" order by age ;

select Customer_Name,City,age from customer where age>25 order by Customer_Name desc;


15.LIMIT :

select Order_ID , Customer_ID, Product_ID,profit,ship_mode
from sales
where ship_mode="First class"
order by profit desc limit 10;

select * from customer where age<=18 order by Postal_Code asc limit 10;


16.AS :

select Customer_ID as id ,customer_name as name, age as customer_age from customer ;


17.COUNT :

select count(*) from customer;

select count(order_id) as "Number of product ids" , count(distinct customer_name) as "number
of orders" from logistics;


18.SUM :

select sum(profit) as "Sum of profit" from sales;

select sum(quantity) as "Sum of Quantity" from sales where Order_id="CA-2016-152156";


19.AVEARGE :

select avg(sales) as "Avg of Sales" from sales ;

select avg(sales*0.10) as "Avg of Sales" from sales ;


20.MIN and MAX :

select min(Profit) as "Min Profit" from sales ;

select max(profit) as "Max Profit of Second class" from sales where Ship_Mode="Second
class";


21.GROUP :

select City , count(customer_id) from customer group by city ;

select Customer_Id ,avg(profit) as "Avg of profits" , Ship_mode from Sales group by Ship_mode
order by Profit asc;

select customer_id ,min(Sales) as "Min sales",max(Sales) as "Max sales",avg(Sales) as "Avg
sales",count(Sales) as "Total sales" from sales group by customer_id order by sales desc limit 5;


22.HAVING :

select region ,count(customer_id) as count_of_customer_id from customer group by region
HAVING count(customer_id)>200;

select region ,count(customer_id) as "customer count" from customer where Customer_Name
like "A%" group by region ;


23.CASE WHEN :

select * ,
CASE WHEN age>40 THEN "YOUTH"
WHEN age<60 THEN "Senior Citizen"
ELSE "Middle Age Peoples"
END as age_category
from customer;


24.JOINS :

INNER JOIN :

SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
INNER JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID;

LEFT JOIN :

SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
LEFT JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID;

or

SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID as Customer_ID_Sales,
b.Customer_ID as Customer_ID_Customer,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
LEFT JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID_Sales,Customer_ID_Customer;

RIGHT JOIN :

SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
RIGHT JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID;

FULL OUTER JOIN :

We can't use FULL OUTER JOIN as a Keyword , We can achieve via UNION Keyword.
(SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
LEFT JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID)
UNION
(SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
RIGHT JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID);

or

(SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID as Customer_ID_Sales,
b.Customer_ID as Customer_ID_Customer,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
LEFT JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID_Sales)UNION
(SELECT
a.Order_line,
a.Order_Date,
a.Customer_ID as Customer_ID_Sales,
b.Customer_ID as Customer_ID_Customer,
a.product_id,
a.sales,
a.profit,
b.customer_name,
b.age,
b.region
from sales_2015 as a
RIGHT JOIN customer_20_60 as b on a.Customer_ID=b.Customer_ID
order by Customer_ID_Sales );

CROSS JOIN :

select a.YYYY,b.MM
from Year_Values as a,
Month_values as b
order by a.YYYY,b.MM;
25.INTERSECT :
INTERSCT is does not exist in MySQL and there is no alternative for that ,
26,EXCEPT :
EXCEPT is also does not in MySQL.But, NOT IN is an alternative for that.
SELECT distinct customer_id
from sales_2015
where customer_id NOT IN (select customer_id from customer_20_60) order by Customer_id;


27.UNION :

SELECT customer_id from sales_2015
UNION
select customer_id from customer_20_60
order by Customer_id;

UNION also used when we connecting LEFT JOIN AND RIGHT JOIN for the FULL OUTER JOIN


28.STRING FUNTONS :

select customer_name ,length(customer_name) as Characters from customer;

select customer_name ,UPPER(customer_name) as CAPS from customer;

select LOWER("NAVEEN");

select customer_name , replace(country,"United States", "US")as Country from customer;

select TRIM(" Naveen Kumar ");

select TRIM(Both ' ' from ' Naveen kumar ');

SELECT RTRIM(' Naveen Kumar ');

select TRIM(leading ' ' from ' Naveen kumar ');

select LTRIM(" Naveen Kumar ");

select TRIM(trailing ' ' from ' Naveen kumar ');

select customer_name , concat(city," ," ,state," ,",country) as Address from customer;

select customer_id , customer_name , substr(customer_id,1,2) as Customer_id_starting from

customer where substr(customer_id,1,2)="AB";

select order_id ,group_concat(product_id separator " , ")as "Number of products" from sales
group by order_id;


29.MATHEMETICAL FUNTIONS :

select Order_id,sales, ceil(sales),floor(sales) from sales group by order_id;

select rand()+(100/4)-25 ;

select floor(rand()*35/5+67);

select ceil(rand()*36+67);

select round(12.2);

select power(3,4);

select age , power(age,2) as "square of age" from customer;


30.TIME AND DATE FUNTIONS :

select current_time();

select current_date();

select current_time(3);

select current_timestamp();

select EXTRACT(day from current_date());

select EXTRACT(month from current_date());

select EXTRACT(week from current_date());

select current_timestamp, EXTRACT(hour from current_timestamp());

select unix_timestamp();

select timestampdiff(year,"2000-04-13",current_date());

select Order_id,order_date,ship_date,

timestampdiff(day,order_date,ship_date) as delivery_days
from sales
order by delivery_days desc;

select Order_id,order_date,ship_date,
datediff(ship_date,order_date) as delivery_days
from sales
order by delivery_days desc;

select Order_id,order_date,ship_date,
unix_timestamp(ship_date)-unix_timestamp(order_date) as delivery_days
from sales ;


31.DATATYPE CONVERTION :

select sales ,convert(sales,char )from sales;

select sales ,concat("$",convert(sales,char)) from sales;

select convert("2023/04/12",date) ;

select convert('1222.45',signed);

select convert(substr("$2345.345",2),decimal(10,1));

select date_format("2013/04/23","%D %M %Y");

select date_format('2014/04/30',"%d/%b/%Y , %T , %S , %w , %W");

select str_to_date("11111111","%y%m%d");

select str_to_date("11111111","%h%i%s");


32.PATTERNS :

it have 3 types .LIKE ,SIMILAR TO and Regular expression (REGEX) . REGEX are preferred
over SIMILAR TO.

select Customer_Name from customer where customer_name regexp '^(n|z|a)+[a-z\\s]+$';

select Customer_Name from customer where customer_name regexp '^(n|z|a)+[a-z\\s]+$';

select * from customer where customer_name regexp '^(a|b|c)[a-z]{3}\\s(a|b)[a-z]{4}$';

select * from email where name regexp '[a-z0-9\.\-\_\]+@[a-z0-9\-\]+.[a-z{3-5}]'; 



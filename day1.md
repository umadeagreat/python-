一、初步
USE sql_store; #选择所需要的数据库#

SELECT * #*代表检索数据库中所有内容#
From customers #数据库中的数据库#
-- WHERE customer_id = 1 #检索筛选的条件，--代表注释内容#
ORDER BY first_name #排序#
（注意，语句顺序必须遵从：SELECT-FROM-WHERE-ORDER BY，否则会出现语法错误）

二、关于select语句的使用

1.简单的相关使用
SELECT last_name,   '选择多个属性（列名），属性满足四则运算条件，""代表将文字字符串化'
first_name,
points, 
(points + 10) * 0.1 AS 'new points' #AS代表将此列赋予名字#
FROM customers

2.从中选择不重复的元素
SELECT DISTINCT state --DISTINCT代表筛选该列中不重复的元素，更改完列表记得apply，更新新的列表
FROM customers

3.练习：
SELECT name, 
unit_price, 
unit_price * 1.1 AS 'new price'
From products

三、关于WHERE子句（其中的一些运算符）的使用
1.简单的相关使用：
SELECT *
FROM customers
WHERE birth_date >= '2019-01-01' OR points > 1000 AND state = 'va'
（AND是一个优先运算符，NOT运算符需要放到WHERE后面，排除符合条件对象的使用，
如果为了增强代码的可读性，还可以像四则运算那样加括号，''中字母的大小写并不影响筛选）

2.练习：关于AND运算符的使用
SELECT   *
FROM order_items
WHERE order_id = 6 AND quantity * unit_price > 30

3.关于IN运算符的使用：
SELECT   *
FROM customers
WHERE state NOT IN('VA', 'CA', 'GA')#IN运算符可以简化WHERE子句#

4.IN运算符使用的练习：
SELECT *
FROM products
WHERE quantity_in_stock IN ('49', '38', '72') #就算筛选条件是数值也可以这样使用#

5.BETWEEN运算符的使用：
SELECT *
FROM customerS
WHERE points BETWEEN 1000 AND 3000 #这是一个闭区间#

6.BETWEEN练习：
SELECT *
FROM customers
WHERE birth_date BETWEEN '1985-01-01' AND '2000-01-01' #sql中的日期有固定的格式，属于字符串变量，需要加引号#

7.LIKE的使用：不区分筛选条件中字母的大小写
SELECT *
FROM customers
WHERE last_name LIKE 'b____y' #以b开头y结尾，中间为四个字符的单词#
%b:以b结尾
y%：以y开头
%b%:只要该单词中含b就可以，b在开头在结尾，在中间都可以

8.LIKE和NOT LIKE的练习：
SELECT *
FROM customers
WHERE  phone NOT LIKE '%9'  AND
(address LIKE '%TRAIL%' OR address LIKE '%AVENUE%')

9.正则表达式：REGEXP
SELECT *
FROM customers
WHERE  last_name REGEXP '^field|rose|brush'
-- ^ 以...开始，加在单词开头
-- $ 以...结束，加在单词末尾
-- [],从中选取任意一个元素（不用逗号隔开）
-- [a-g]，从中选择a-g的任意一个元素

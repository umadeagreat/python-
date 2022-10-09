一、NULL语句的使用
SELECT *
FROM orders
WHERE shipped_date IS NULL --若要排除则在is后加NOT即可

二、排序、DESC的使用：
SELECT *, quantity * unit_price AS total_price
FROM order_items
WHERE order_id = 2
ORDER BY total_price DESC, product_id --DESC代表降序排列，该行内容表示先按照total_price排列，
--若有相同的值，再将这些相同的值按照product_id进行排序

三、LIMIT语句的使用

SELECT *
FROM customers
LIMIT 6, 3
-- page1:1-3
-- page2:4-6
-- page3:7_9
-- LIMIT 6,3表示的是跳过前面6条记录，选择3条记录
-- LIMIT 3表示的是选择该表格中的前三条记录

练习：
SELECT *
FROM customers
ORDER BY points DESC
LIMIT 3
-- 注意这些子句的顺序

四、采用JOIN和ON合并列表，（INNER）JOIN是执行语句，ON是条件

SELECT order_id, o.customer_id, first_name --选择的时候需要将共同属性加上表单名称
FROM customers c -- 为了简化书写过程，可以将表单名称空格+简化名称
JOIN orders o ON o.customer_id = c.customer_id --JOIN代表要添加的列表，后面的共同属性必须带上各自表单名称

练习：
SELECT o.product_id, name, quantity, o.unit_price
FROM order_items o
JOIN products p ON o.product_id = p.product_id

五、跨数据库将表连接到一起：
USE sql_inventory;
SELECT * 
FROM products p
JOIN sql_store.order_items AS oi -- 若为另一个数据库的表，则应在表单前加上数据库的名字
ON oi.product_id = p.product_id

六、将自身的的表连接到一起：
USE sql_hr;
SELECT e.employee_id, e.first_name, m.first_name AS manager
FROM employees e
JOIN employees m ON
e.reports_to = m.employee_id --虽然是连接条件，但可简单理解为一一对应关系，这一步表明将m表的哪些部分的方式
连接到e表中

七、如何实现两张表以上（多表连接）

USE sql_store;
SELECT order_id, order_date, order_date first_name, last_name, name --可以先选择全部，再从中选取自己需要的列
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id --添加两张表或以上需要将JOIN、ON分开写
JOIN order_statuses os ON os.order_status_id = o.status

练习：
USE sql_invoicing;
SELECT  p.client_id, p.invoice_id, date, amount, pm.name --注意看清每张表的列名是否有重复
FROM payments p
JOIN clients c ON c.client_id = p.client_id
JOIN payment_methods pm ON pm.payment_method_id = p.payment_method

八、复合连接条件：
USE sql_store;
SELECT *
FROM order_items oi
JOIN order_item_notes oin ON oin.order_id = oi.order_id
		AND oin.product_id = oi.product_id --是一种多对多的关系
    
 九、隐式连接法：
 SELECT *
FROM customers c, orders o
WHERE c.customer_id = o.customer_id -- 不要忘记输入WHERE语句，否则两个表会交叉连接，形成笛卡尔积，
WHERE语句其实就是ON的内容
   
   
  十、外连接语法：最大的作用就是可以返回条件中为空值的项
 SELECT c.customer_id, o.order_id, first_name
FROM orders o
RIGHT JOIN customers c -- LEFT等同于返回FROM表格中的所有信息，不管是否符合条件，RIGHT等同于返回JOIN
表格中的所有信息，不管是否符合条件
ON c.customer_id = o.customer_id
ORDER BY c.customer_id

练习：
SELECT p.product_id, name, quantity --若为o.product_id，则由于有些并没有产品订购记录，会返回空值，而不是全部的商品
FROM products p
LEFT JOIN order_items o ON p.product_id = o.product_id --根据想要返回的内容是什么来确定是LEFT还是RIGHT
-- 不能返回空值内容的外连接，返回结果跟内连接相同

十、多表外连接：
SELECT c.customer_id, o.order_id, first_name, o.shipper_id --一定要记住，此处输出的列应该为包含空值的列
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
LEFT JOIN shippers s ON s.shipper_id = o.shipper_id -- 尽量使用LEFT JOIN语句，不然一会左一会右很容易搞混，这里的LEFT指的是上一个表单

练习：
SELECT order_date, o.order_id, first_name, s.name AS shipper, os.name
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
LEFT JOIN shippers s ON s.shipper_id = o.shipper_id
JOIN order_statuses os ON os.order_status_id = o.status --不涉及是否存在缺失值，用内连接即可

十一、自外连接：
USE sql_hr;
SELECT e.employee_id, e.first_name, m.first_name
FROM employees e
LEFT JOIN employees m ON e.reports_to = m.employee_id

十二、USING语句：
USE sql_store;
SELECT o.customer_id, o.order_id, c.first_name, s.shipper_id
FROM orders o
JOIN customers c
	USING(customer_id)  --使用USING语句时，括号内的列名称一定要是FROM表单和JOIN表单中所共有的
JOIN shippers s
	USING(shipper_id)
  
  2.对于复合连接关系，USING语句可将其简化：
SELECT *
FROM order_items o
JOIN order_item_notes oin
USING(order_id, product_id)

3.练习：
USE sql_invoicing;
SELECT p.date,  c.name, amount, pm.name
FROM payments p
JOIN clients c
	USING(client_id)
JOIN payment_methods pm ON pm.payment_method_id = p.payment_method --虽然是同样的列，但是列名不一样，不能使用USING语句

十三、自然连接：
USE sql_store;
SELECT o.order_id, c.customer_id, first_name
FROM orders o
NATURAL JOIN customers c --数据库根据相同的列名进行自然连接，不过比较危险，谨慎使用

十四、交叉连接：笛卡尔积

SELECT c.first_name, p.name
FROM customers c, order o --隐式连接
-- CROSS JOIN products p
ORDER BY c.first_name --显式连接

练习：
显式：
SELECT s.name, p.name
FROM shippers s
CROSS JOIN products p
ORDER BY s.name
隐式：
SELECT s.name, p.name
FROM shippers s,products p
ORDER BY s.name

十五、用UNION合并SELECT语句：

SELECT order_date,"Active" AS state
FROM orders
WHERE order_date >= "2019-01-01"
UNION
SELECT order_date,"Archived" AS state
FROM orders
WHERE order_date < "2019-01-01"
ORDER BY order_date -- 前提是两个SELECT语句选择的列的数量要相同（一一对应）

练习：
SELECT customer_id, first_name, points, "Bronze" AS "type"
FROM customers
WHERE points < 2000
UNION
SELECT customer_id, first_name, points, "Silver" AS "type"
FROM customers
WHERE points BETWEEN 2000 AND 3000
UNION
SELECT customer_id, first_name, points, "Gold" AS "type"
FROM customers
WHERE points > 3000
ORDER BY first_name

十六、往表格中添加行：
INSERT INTO customers(first_name, last_name, address, city, state ) --要往x表格中添加的列
VALUES('John', 'Smith', 'Hollinton Street', 'Boston', 'CA') --对应上述列，输入要添加的值，若有默认值或者允许为空值的，可以不用输入

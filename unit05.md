### Putting it all together

Using the Dellstore2 database, complete the following queries based on requests from the CEO at your company.
Items in *italics* are to be included in an aggregate email of all of your responses to the instructor.

1 => "Get me a list of all of our products with above average sales".
*Send me the number of items in this list.*   
**ANS: 4305**  
// SELECT AVG(sales) FROM inventory; //12.0719  
// SELECT inventory.sales, inventory.prod_id, products.prod_id, products.title FROM inventory, products WHERE inventory.sales > 12.0719 AND inventory.prod_id=products.prod_id ORDER BY sales;

2 => Based on the first list, *tell me the top 3 selling titles*.  
**ANS: AIRPLANE ROLLERCOASTER, AFFAIR ALAMO, ACADEMY ANTHEM**

3 => Get me a list of how many orders have been placed by Sam Williams.
*How many total orders Have been placed?*  
**ANS: 120**  
// SELECT * FROM customers WHERE customers.firstname='Sam' AND customers.lastname='Williams';

*When was Sam Williams most active ?*   
**ANS: On 6 days he placed two orders each day:  
3/17/2004  
5/12/2004  
5/20/2004  
6/26/2004  
11/15/2004  
12/19/2004**   
// SELECT customers.firstname, customers.lastname, customers.customerid, orders.customerid, orders.orderdate FROM customers, orders WHERE customers.firstname='Sam' AND customers.lastname='Williams' AND customers.customerid=orders.customerid ORDER BY orders.orderdate;

(When did he place his orders) ?

4 => What are the two cheapest PINOCCHIO movies? (PINOCCHIO is the second part of the title of many of our movies).

*send me the names and prices of the two cheapest PINOCCHIO movies*  
**AGENT PINOCCHIO 9.99 and ALABAMA PINOCCHIO 9.99**

*send me the PINOCCHIO query so I can re-use it later*  
// SELECT * FROM products WHERE products.title LIKE '%PINOCCHIO%' ORDER BY products.price;

 5 => Add an auto-incrementing 'id' column to the "reorder" table, then populate that table
with two or three lines of data. Remember that when you add rows to an auto-incrementing table,
you don't have to include 'id' as one of the columns to populate. It should do it for you.
In postgres,  SERIAL is the equivalent to auto-increment.
(Hint: syntax for this is back on Unit01.md)  
// ALTER TABLE reorder ADD COLUMN id SERIAL;

Question:  if you delete the final record of an auto-incrementing table, and that final record's auto-incremented
value (id) was 9, what will be the the value of the next record inserted into the table?  In other words, delete 9,
and what will the next record be?   
**ANS: 10, doesn't reuse the id that was deleted.**

*send me the answer to this question*

Email all of your answers **IN ONE EMAIL** to complete this assignment.

-- This is the solution for 1st case study of the challenge
-- CREATING DATA SET
CREATE TABLE sales (
  "customer_id" VARCHAR(1),
  "order_date" DATE,
  "product_id" INTEGER
);

INSERT INTO sales
  ("customer_id", "order_date", "product_id")
VALUES
  ('A', '2021-01-01', '1'),
  ('A', '2021-01-01', '2'),
  ('A', '2021-01-07', '2'),
  ('A', '2021-01-10', '3'),
  ('A', '2021-01-11', '3'),
  ('A', '2021-01-11', '3'),
  ('B', '2021-01-01', '2'),
  ('B', '2021-01-02', '2'),
  ('B', '2021-01-04', '1'),
  ('B', '2021-01-11', '1'),
  ('B', '2021-01-16', '3'),
  ('B', '2021-02-01', '3'),
  ('C', '2021-01-01', '3'),
  ('C', '2021-01-01', '3'),
  ('C', '2021-01-07', '3');
 

CREATE TABLE menu (
  "product_id" INTEGER,
  "product_name" VARCHAR(5),
  "price" INTEGER
);

INSERT INTO menu
  ("product_id", "product_name", "price")
VALUES
  ('1', 'sushi', '10'),
  ('2', 'curry', '15'),
  ('3', 'ramen', '12');
  

CREATE TABLE members (
  "customer_id" VARCHAR(1),
  "join_date" DATE
);

INSERT INTO members
  ("customer_id", "join_date")
VALUES
  ('A', '2021-01-07'),

  ('B', '2021-01-09');

Select *
From members
Select *
From menu
Select *
From Sales

-- SOLUTIONS

--1 Total amount spend by each customer---

SELECT 
   customer_id,  
   SUM(price) as total_spent
  FROM sales INNER JOIN menu
  ON sales.product_id=menu.product_id
  GROUP BY customer_id;


--2 How manu dats customer visited the restauraunt----

SELECT 
   customer_id,
   COUNT(DISTINCT order_date) as no_of_days 
  FROM sales
  GROUP BY customer_id;


-- 3. What was the first item from the menu purchased by each customer?

WITH CTE AS(
SELECT customer_id, 
       product_name,
	   order_date,
    DENSE_RANK() OVER(
    PARTITION BY customer_id
    ORDER BY order_date) as ranking
    FROM sales INNER JOIN menu
    ON sales.product_id=menu.product_id
   GROUP BY customer_id, 
       product_name,
	   order_date)
SELECT customer_id, 
       product_name FROM CTE 
	   where ranking=1;


-- 4. What is the most purchased item on the menu and how many times was it purchased by all customers?---

SELECT TOP 1
	product_name,
	 COUNT(sales.product_id) AS max_ordered_product
    FROM sales INNER JOIN menu
    ON sales.product_id=menu.product_id
	GROUP BY product_name
	Order by COUNT(sales.product_id) DESC;



--- 5. Which item was the most popular for each customer?---

	 WITH CTE AS (
   SELECT customer_id,
       product_name,
	   COUNT(sales.product_id) as product_count,
	   DENSE_RANK() OVER(
	   PARTITION BY customer_id
	   ORDER BY COUNT(sales.product_id)DESC) AS ranking
    FROM sales INNER JOIN menu
    ON sales.product_id=menu.product_id
	GROUP BY 
	   customer_id,
	   sales.product_id,
	   product_name)
  SELECT 
       customer_id,
       product_name,
	   product_count
	   FROM CTE
	    where ranking=1



-- 6. Which item was purchased first by the customer after they became a member?

WITH rank_table AS (
  SELECT sales.customer_id, 
       order_date, 
	   join_date, 
	   product_name,
	   DENSE_RANK() OVER(
	   PARTITION BY sales.customer_id
	   ORDER BY order_date) AS ranking
	   FROM sales INNER JOIN menu
	   ON sales.product_id=menu.product_id
	   JOIN members
	   ON sales.customer_id=members.customer_id
	   where order_date>=join_date)
	SELECT * FROM  rank_table 
	  where ranking=1;


-- 7. Which item was purchased just before the customer became a member?---

WITH rank_table AS (
    SELECT sales.customer_id, 
       order_date, 
	   join_date, 
	   product_name,
	   DENSE_RANK() OVER(
	   PARTITION BY sales.customer_id
	   ORDER BY order_date DESC) AS ranking
	   FROM sales INNER JOIN menu
	   ON sales.product_id=menu.product_id
	   JOIN members
	   ON sales.customer_id=members.customer_id
	   where order_date<join_date)
	SELECT 
	  customer_id,
	  product_name
	 FROM  rank_table 
	 where ranking=1;	  



-- 8. What is the total items and amount spent for each member before they became a member?



SELECT sales.customer_id, 
	   COUNT(product_name) as total_items,
	   SUM(price) as amount_spent
	   FROM sales INNER JOIN menu
	   ON sales.product_id=menu.product_id
	   JOIN members
	   ON sales.customer_id=members.customer_id
	   where order_date<join_date
	   GROUP BY sales.customer_id;



---9.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?---

 WITH CTE AS (
     SELECT customer_id, 
	   product_name,
	   price,
	   CASE WHEN product_name='sushi' then price*20 
	   else price*10 END AS points_earned
	   FROM sales INNER JOIN menu
	   ON sales.product_id=menu.product_id)
	 SELECT customer_id,
	        SUM(points_earned)
	    FROM CTE 
		GROUP BY customer_id;


-- 10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?----


WITH CTE AS (
      SELECT sales.customer_id, 
	       sales.product_id,
		   order_date,
		   join_date,
	       product_name,
	       price,
		   (CASE WHEN product_name='sushi' OR   
		   (DATEDIFF(DAY,join_date,order_date) BETWEEN 0 AND 6) then price*20
		   ELSE price*10 END) AS points  
	   FROM sales INNER JOIN menu
	   ON sales.product_id=menu.product_id
	   INNER JOIN members
	   ON sales.customer_id=members.customer_id
	   )
	 SELECT customer_id, 
	        SUM(points) AS total_points
		from CTE
		where  order_date <'2021-02-01'
		GROUP BY customer_id;

----Creating table 1----

SELECT    
           sales.customer_id, 
		   order_date,
		   product_name,
		   price,
		   CASE WHEN sales.customer_id=members.customer_id AND 
		    order_date >=join_date THEN 'Y' 
		    ELSE 'N' END AS member  
	   FROM sales LEFT JOIN menu
	   ON sales.product_id=menu.product_id
	   LEFT JOIN members
	   ON sales.customer_id=members.customer_id

----Creating table 2----

WITH CTE AS ( SELECT    
           sales.customer_id, 
		   order_date,
		   product_name,
		   price,
		   CASE WHEN sales.customer_id=members.customer_id AND 
		    order_date >=join_date THEN 'Y' 
		    ELSE 'N' END AS member  
	   FROM sales LEFT JOIN menu
	   ON sales.product_id=menu.product_id
	   LEFT JOIN members
	   ON sales.customer_id=members.customer_id)
 SELECT *,
	   CASE WHEN member='N' then NULL
	   ELSE DENSE_RANK() OVER(
	   PARTITION BY customer_id, member
	   ORDER BY order_date) END AS ranking
	   FROM CTE
	   ORDER BY customer_id, order_date;



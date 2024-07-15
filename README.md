# Danny's Dinner SQL Challenges

## Introduction

Danny seriously loves Japanese food so in the beginning of 2021, he decides to embark upon a risky venture and opens up a cute little restaurant that sells his 3 favourite foods: sushi, curry and ramen.

Danny’s Diner is in need of your assistance to help the restaurant stay afloat - the restaurant has captured some very basic data from their few months of operation but have no idea how to use their data to help them run the business.

## Problem Statement

Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite. Having this deeper connection with his customers will help him deliver a better and more personalised experience for his loyal customers.

Like: 
  - visiting patterns,
  - how much money they’ve spent, and
  - which menu items are their favourite.

He plans on using these insights to help him decide whether he should expand the existing customer loyalty program - additionally he needs help to generate some basic datasets so his team can easily inspect the data without needing to use SQL.

Danny has provided you with a sample of his overall customer data due to privacy issues - but he hopes that these examples are enough for you to write fully functioning SQL queries to help him answer his questions!

Danny has shared with you 3 key datasets for this case study:
Sales
Menu
Members

Entity Relationship Diagram




[Entity Relationship Diagram](https://github.com/Sumitraadhya/SQL-Project--Danny-s-Dinner/blob/main/Entity%20relationship%20diagram.png)


## Case Study Questions

Each of the following case study questions can be answered using a single SQL statement:

- What is the total amount each customer spent at the restaurant?
- How many days has each customer visited the restaurant?
- What was the first item from the menu purchased by each customer?
- What is the most purchased item on the menu and how many times was it purchased by all customers?
- Which item was the most popular for each customer?
- Which item was purchased first by the customer after they became a member?
- Which item was purchased just before the customer became a member?
- What is the total items and amount spent for each member before they became a member?
- If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
- In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B 
  have at the end of January?


## Insights

From the analysis, we discover a few interesting insights that would be certainly useful for Danny.

- Customer B is the most frequent visitor with 6 visits in Jan 2021.
- Danny’s Diner’s most popular item is ramen, followed by curry and sushi.
- Customer A and C loves ramen whereas Customer B seems to enjoy sushi, curry and ramen equally. Who knows, I might be Customer B!
- Customer A is the 1st member of Danny’s Diner and his first order is curry. Gotta fulfill his curry cravings!
- The last item ordered by Customers A and B before they became members are sushi and curry. Does it mean both of these items are the deciding factor? It must be really 
  delicious for them to sign up as members!
- Before they became members, both Customers A and B spent $25 and $40.
- Throughout Jan 2021, their points for Customer A: 860, Customer B: 940 and Customer C: 360.
- Assuming that members can earn 2x a week from the day they became a member with bonus 2x points for sushi, Customer A has 660 points and Customer B has 340 by the end of 
  Jan 2021.












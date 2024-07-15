# Danny's Dinner SQL Challenges

## Introduction

Danny seriously loves Japanese food so in the beginning of 2021, he decides to embark upon a risky venture and opens up a cute little restaurant that sells his 3 favourite foods: sushi, curry and ramen.

Danny’s Diner is in need of your assistance to help the restaurant stay afloat - the restaurant has captured some very basic data from their few months of operation but have no idea how to use their data to help them run the business.

## Problem Statement

Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite. Having this deeper connection with his customers will help him deliver a better and more personalised experience for his loyal customers.

He plans on using these insights to help him decide whether he should expand the existing customer loyalty program - additionally he needs help to generate some basic datasets so his team can easily inspect the data without needing to use SQL.

Danny has provided you with a sample of his overall customer data due to privacy issues - but he hopes that these examples are enough for you to write fully functioning SQL queries to help him answer his questions!

Danny has shared with you 3 key datasets for this case study:
Sales
Menu
Members

Entity Relationship Diagram




[Live Report Link](https://app.powerbi.com/groups/me/reports/461950aa-6e4a-4a16-a76f-838145ff8ac8/6069fd5166468130bd4a?experience=power-bi)

## Codes for creating Input Data Table
------------------------------
## Introduction
CREATING DATA SET
CREATE TABLE sales (
  "customer_id" VARCHAR(1),
  "order_date" DATE,
  "product_id" INTEGER
);
--------------------------------
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
------------------------
CREATE TABLE menu (
  "product_id" INTEGER,
  "product_name" VARCHAR(5),
  "price" INTEGER
);
------------------------
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
-----------------------
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

------------------


## Case Study Questions & Answers(SQL Codes)






## Overall Report

![Overall Report.gif](https://github.com/Sumitraadhya/Atliq-Hospitality-Analysis/blob/main/Dashboard.png)


## Business related terms

https://github.com/Sumitraadhya/Atliq-Hospitality-Analysis/blob/main/metrics%20list.xlsx

- Realization=URN/BRN
- BRN=URN+ no shows+ cancellation bookings
- Weekends=Friday & Saturday

## Overall Analysis View

![Overall Report.gif](https://github.com/Sumitraadhya/Atliq-Hospitality-Analysis/blob/main/Dashboard.png)



you can find the full report file here : [Report](https://app.powerbi.com/groups/me/reports/461950aa-6e4a-4a16-a76f-838145ff8ac8/6069fd5166468130bd4a?experience=power-bi)


## Project Outcome

-ADR is not fluctuating that clearly indicates this hotel runs on flat pricing.

-RevPar in weekday, weekend varying based on occupancy %, ADR is almost fixed here. That clearly indicates dynamic pricing (price can be variable depends on season, occasion and demand) adoption strategy especially for leisure hotels can be accounted.

-Management can adopt changes for dynamic pricing strategy which can bring furthermore business in the future.










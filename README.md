## Background
This is an assignment that I did before getting a job at the company. The tools I used were MySQL and Spreadsheet to visualize the data. 

Here are attached the questions and queries that I made:

## Questions
A. You are going to import the sql data file and insert that data into the Mysql database.

Download the sample data here: sample wholesale.sql Please import the data into your mysql database

B. Please write in document the query for each question, show the result of the query, and give your
analysis of the data. Make sure your query is the most optimized.

1. Which product is the most bought for each month?
2. What are the sales from each city and what are the top 3 cities?
3. Which product is the top selling for each city?
4. What is the average profit from each order?
5. What information can you give as BI Analyst?

## Queries and Insights (also data visualization)
1. answering question number 1 about which products are most frequently purchased each month
```sql
SELECT
    `Month`,
    `Product_name`,
    `Category`,
    `Total_Sales` AS `Most_Bought_Product`
FROM (
    SELECT
        EXTRACT(MONTH FROM `Order_Date`) AS `Month`,
        `Product_name`,
        `Category`,
        SUM(`Sales`) AS `Total_Sales`,
        ROW_NUMBER() OVER(PARTITION BY EXTRACT(MONTH FROM `Order_Date`) ORDER BY SUM(`Sales`) DESC) AS `Rank`
    FROM `sales`
    GROUP BY `Month`, `Product_name`, `Category`
) ranked_sales
WHERE `Rank` = 1;
```


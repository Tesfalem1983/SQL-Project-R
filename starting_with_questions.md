Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
    SELECT city, country, SUM(totaltransactionrevenue)AS Total_Revenue
    FROM all_sessions where totaltransactionrevenue is not null
    GROUP BY city, country
    ORDER BY Total_Revenue DESC
    LIMIT 10;



Answer:  Among the top countries are USA and Israel. The cities that have the higest contribution to the transaction revenue are 9 USA cities and Telaviv from Israel.



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
    SELECT city, country, AVG(productquantity) as Average_Product_Qty
    FROM all_sessions WHERE productquantity is not null.
    GROUP BY city, country
    ORDER BY Average_Product_Qty DESC;



Answer: Returned 27 rows of Average_Product_Qty of around 27 cities and 10 countries(after filtering out the null values).





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
    SELECT v2productcategory,city, country, SUM(p.orderedquantity) as Ordered_Quantity
    FROM all_sessions as ass
    JOIN products as p
    ON ass.productsku = p.productsku
    GROUP BY v2productcategory,city, country
    ORDER BY Ordered_Quantity DESC



Answer: The pattern show that the product category(Home/Shop/ by Brand/Youtube/) is the highest in demand product category accross many cities and countries.



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
    SELECT city, country,p.name, SUM(p.orderedquantity) as Ordered_Quantity
    FROM all_sessions as ass
    JOIN products as p
    ON ass.productsku = p.productsku
    GROUP BY city, country,p.name
    ORDER BY Ordered_Quantity DESC
    LIMIT 10;



Answer:The top-selling product is Custom decals followed by Kick Ball accross cities in the United States and other cournties.


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
    SELECT city, country, als.productsku,sum(total_ordered * productprice) as Total_Revenue 
    FROM all_sessions as als
    JOIN sales_report as sr ON 
    als.productsku = sr.productsku
    Group by country, city, als.productsku
    Order by Total_Revenue DESC;



Answer: Customers from the United States particularly from cities like Mountain view, Palo Alto and Sanfrancisco contribute lion's share of the revenue. Generally speaking customers from USA followed by customers from United Kingdom are the major contributors to our Total revenue.








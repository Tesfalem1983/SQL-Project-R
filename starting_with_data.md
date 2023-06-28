Question 1: Which channels or marketing campaigns drive the most customers?

SQL Queries:
    SELECT totaltransactionrevenue 
    FROM all_sessions 
    WHERE totaltransactionrevenue is null;
    SELECT channelgrouping as channels,count(channelgrouping) from all_sessions
    GROUP BY channelgrouping
    ORDER BY count DESC
    LIMIT 3;

Answer: Organic Search, direct and referral channels/marketing campaigns were the one's mostly utilized by customers.



Question 2: Which Pagetitle was the most frequently visited by customers;

SQL Queries:
    SELECT pagetitle, count(pagetitle)
    FROM  all_sessions
    GROUP BY pagetitle
    ORDER BY count DESC
    LIMIT 5;

Answer: Five of the most frequently visited pagetitles are as follows:
    1. Youtube/shop by Brand/ Google Merchandise store
    2. Men's T-Shirts/ Apparel/Google merchandise Store
    3. Men's T- Shirts
    4. Electronics/ Google merchandise store
    5. Apparel/Google merchandise store



Question 3: Which products had the higest average stocklevel throughout the years?

SQL Queries:
  
  ```SQL
    SELECT productname,  productsku, AVG(stocklevel) as Average_Stocklevel
    FROM products
    GROUP BY productname,productsku
    ORDER BY Average_Stocklevel DESC
    LIMIT 10;
  ```
  

Answer: The products with the highest average stocklevel throughout the years(Required to analyze whether we are holding stocklevel morethan the required level or else whether some of them are holding our resources that otherwise could have been used for improving bottomline by investing in other more profitable products.)



Question 4: Which are the products that are at the higest risk of out of stock(which is determined by the restocking leadtime)

SQL Queries:
    ```SQL
    SELECT Distinct productname, restockingleadtime
    FROM sales_report
    ORDER BY restockingleadtime DESC
    LIMIT 50;
    ```

Answer: Based on risk associated with the time required to restock a product(restockingleadtime) the products that are at risk of out of stock are the following:
    1. Cam Indoor Security Camera-USA
    2. Stylus pen w/LED light
    3. Recycled Mouse pad
    4. Leatherette journal
    5. Gunmetal Roller Ball Pen



Question 5: 

SQL Queries:

Answer:

What issues will you address by cleaning the data?
The below are issues that will be addressed to clean and transform the data.

      ###1. Removing columns with complete null value.
      ###2. Filling columns with minor missing information with relevant data or data that gives sense.
      ###3. Replacing "not set" values with null values.
      ###4. Transforming the data type of columns with the right data type for the data in the column.
      ###5. Renaming columns to establish consistency.
      ###6. Correct non-uniform data including units of measurement and currency type.
      ### 7. identify duplicate value and take corrective action.


Queries:
# Queries for the table "all_sessions"
######1. Change data type of "productprice" column and divide the values by 1000000.
     
            ALTER TABLE all_sessions
            ALTER COLUMN productprice Type decimal(10,2);
            UPDATE all_sessions
            SET productprice = productprice/1000,000;

###2. Change data type of "fullvisitorid" column in to numeric:
     
            ALTER TABLE all_sessions
            ALTER COLUMN fullvisitorid TYPE numeric
            USING fullvisitorid::numeric

###3. Change the data type of "time" column:
     
            ALTER TABLE all_sessions
            ALTER COLUMN time
            TYPE VARCHAR
            USING LPAD(time::VARCHAR, 6, '0');

            UPDATE public.all_sessions
            SET time = SUBSTR(time, 1, 2) || ':' || SUBSTR(time, 3, 2) || ':' || SUBSTR(time, 5, 2);

            UPDATE public.all_sessions
            SET time = TIME '00:00:00' + 
                 INTERVAL '1 hour' * CAST(SUBSTR(time, 1, 2) AS INTEGER) +
                 INTERVAL '1 minute' * CAST(SUBSTR(time, 4, 2) AS INTEGER) +
                 INTERVAL '1 second' * CAST(SUBSTR(time, 7, 2) AS INTEGER);
           
            ALTER TABLE public.all_sessions
            ALTER COLUMN time TYPE TIME USING time::TIME;
            SELECT CAST(time as timestamp) from all_sessions;
    ###4. Replace the "not set" value in the country column  with Null:
            
            UPDATE all_sessions
            SET country = Null
            WHERE country = '(not set)';
     
    ###5. Replace the "not set" value in the city column  with Null:
     
            UPDATE all_sessions
            SET country = Null
            WHERE country = '(not set)';
     ###6. Change data type of "totaltransactionrevenue" column and divide the values by 1000000.
     
            ALTER TABLE all_sessions
            ALTER COLUMN totaltransactionrevenue TYPE numeric
            USING totaltransactionrevenue::numeric;
            UPDATE all_sessions
            SET totaltransactionrevenue = totaltransactionrevenue/1000000;
   
     ###7. Change data type of "timeonsite" column: 
     
            ALTER TABLE all_sessions
            ALTER COLUMN timeonsite
            TYPE VARCHAR
            USING LPAD(timeonsite::VARCHAR, 6, '0');

            UPDATE public.all_sessions
            SET timeonsite = SUBSTR(timeonsite, 1, 2) || ':' || SUBSTR(timeonsite, 3, 2) || ':' || SUBSTR(timeonsite, 5, 2);

            UPDATE public.all_sessions
            SET timeonsite = TIME '00:00:00' + 
                   INTERVAL '1 hour' * CAST(SUBSTR(timeonsite, 1, 2) AS INTEGER) +
                   INTERVAL '1 minute' * CAST(SUBSTR(timeonsite, 4, 2) AS INTEGER) +
                   INTERVAL '1 second' * CAST(SUBSTR(timeonsite, 7, 2) AS INTEGER);                    
            ALTER TABLE public.all_sessions
            ALTER COLUMN timeonsite TYPE TIME USING timeonsite::TIME;
     ###8. Drop the "productrefundamount" column  as all its data value is Null.
     
            ALTER TABLE all_sessions
            DROP COLUMN productrefundamount;
            
     ###9. Change data type of "productquantity" in to integer:
     
            ALTER TABLE all_sessions
            ALTER COLUMN productquantity TYPE integer
            USING (productquantity::integer);

    ###10. Change data type of "productrevenue" column in to numeric:
    
            ALTER TABLE all_sessions
            ALTER COLUMN productrevenue TYPE numeric
            USING productrevenue::numeric;
            
    ###11. Change the value "not set" in the " productvariant" column in to Null.
    
            UPDATE all_sessions
            SET productvariant = Null
            WHERE productvariant = '(not set)';
    ###12. Replace the null values in the "currencycode" column in to "USD" as it gives sense.
    
            UPDATE all_sessions
            SET currencycode = COALESCE(currencycode, 'USD')
            WHERE currencycode IS NULL;
            
    ###13. Drop the "itemquantity" column as all its values is Null:
            ALTER TABLE all_sessions
            DROP COLUMN itemquantity;
            
    ###14. Drop the "itemrevenue" column as all its values is Null:
    
            ALTER TABLE all_sessions
            DROP COLUMN itemrevenue;
          
    ###15. Change data type of the "transactionrevenue" column in to numeric:
    
            ALTER TABLE all_sessions
            ALTER COLUMN transactionrevenue TYPE numeric
            USING transactionrevenue::numeric;
    ###16. Drop the "searchkeyword" column as all its values are Null.
    
           ALTER TABLE all_sessions
           DROP COLUMN searchkeyword

# Queries for the table "analytics"
    ###1. Change data type of "unit_price" column and divide the values by 1000000.
     
            ALTER TABLE analytics
            ALTER COLUMN unit_price  Type decimal(10,2);
            UPDATE analytics
            SET unit_price = unit_price/1000000;
    ###2. Change the data type of the "visitstarttime" column to timestamp.
     
            ALTER TABLE analytics
            ALTER COLUMN visitstarttime TYPE TIME 
            USING to_timestamp(visitstarttime)::TIME;
    ###3. Change the data type of "fullvisitorid" column in to numeric:
     
            ALTER TABLE analytics
            ALTER COLUMN fullvisitorid TYPE numeric
            USING fullvisitorid::numeric;
            
    ###4.  Drop the "userid" column as all its value is Null:
     
            ALTER TABLE analytics
            DROP COLUMN userid;

    ###5. Change the data type of the "timeonsite" column to timestamp.
     
            ALTER TABLE analytics
            ALTER COLUMN timeonsite TYPE VARCHAR
            USING LPAD(timeonsite::VARCHAR, 6, '0');

            UPDATE public.analytics
            SET timeonsite = SUBSTR(timeonsite, 1, 2) || ':' || SUBSTR(timeonsite, 3, 2) || ':' || SUBSTR(timeonsite, 5, 2);

            UPDATE public.analytics
            SET timeonsite = TIME '00:00:00' + 
            INTERVAL '1 hour' * CAST(SUBSTR(timeonsite, 1, 2) AS INTEGER) +
            INTERVAL '1 minute' * CAST(SUBSTR(timeonsite, 4, 2) AS INTEGER) +
            INTERVAL '1 second' * CAST(SUBSTR(timeonsite, 7, 2) AS INTEGER);  
            
            ALTER TABLE public.analytics
            ALTER COLUMN timeonsite TYPE TIME USING timeonsite::TIME;
    ###6. Change data type of "revenue" column and divide the values by 1000000.
            ALTER TABLE analytics
            ALTER COLUMN revenue Type numeric(10,2);
            UPDATE analytics
            SET revenue = revenue/1000000;  

# Queries for the table "products"
    ###1. Change column name(sku) to productsku to keep consistency in the dataset.
     
            ALTER TABLE products
            RENAME COLUMN sku TO productsku;

## Queries for the Table "Sales_Report":
     ###1. Changed data type and limited digits in to 4 points after decimal point
     
            ALTER TABLE sales_report
            ALTER COLUMN ratio TYPE decimal(10,4);

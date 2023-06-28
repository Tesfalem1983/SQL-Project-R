What are your risk areas? Identify and describe them.
    #The risk areas are :
     ###1. Integrity and Accuracy of Data(Ensuring the accuracy and completeness of data).
            (Typo errors or descrepancies that could affect out of analysis)
     ###2. Data quality issue like invalid value, outliers and data formatting and structure.
            (Data not being consistent with predefined business rules and constraints)
     ###3. Incorrect data type changes, mistakes in calcualtions and agregation.
     ###4. Security and Privacy of data.(Making sure the senstive private information are handles based on privacy act regulation)
     ###5. Missing documenting the validation and the overall QA process.
     ###6. Integration errors that arise froom incompatibility at the time


#QA Process:
    ###1. Checking conformity of data to predifined business rules.
    ###2. Verify data accuracy and consistency
    ###3. Ensuring senstive private information of customers are handled in accordance with rules and regulations.
    ###3. Documenting all the cleaning and transformation process properly(to be able to trace errors)
    ###4  Validate the actions taken in data cleaning and transformation against validation criteria and expected outcomes.
    ###5. Validate data loading and integration in to target database.

#SQL-QUERIES:
    # Assessing overall data to identify potential issues(Including to check if data type maches with the data content)
        SELECT table_name, column_name, data_type
        FROM information_schema.columns
        WHERE table_schema = 'public'
        ORDER BY table_name
    # Compare and Contrast the overall number of rows versus the number of distinct rows in each table to identify duplicates:
        SELECT COUNT(*) FROM all_sessions;
        SELECT DISTINCT fullvisitorid FROM all_sessions;
        SELECT COUNT(*) FROM analytics;
        SELECT DISTINCT visitid FROM analytics;
        SELECT COUNT(*) FROM products;
        SELECT DISTINCT productsku FROM products
        SELECT COUNT(*) FROM sales_by_sku;
        SELECT DISTINCT productsku FROM  sales_by_sku;
        SELECT COUNT(*) FROM sales_report;
        SELECT DISTINCT productsku FROM sales_report;
    # Checking for Null values in a different columns in a table(Will just mention example)
        



# SQL Oracle
## Oracle Database in Use
Oracle 19c Database
SQL Reference - https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/

## SQL*Plus
SQL*Plus is an interactive and batch query tool that comes with every Oracle Database installation. It provides a command-line user interface to interact with the Oracle Database. SQLPlus allows users to enter and execute SQL, PL/SQL, SQLPlus, and operating system commands. It is useful for formatting, performing calculations, storing, and printing query results, examining table and object definitions, developing and running batch scripts, and performing database administration.
https://docs.oracle.com/cd/B14117_01/server.101/b12170/qstart.htm

## SQLcl
Oracle SQLcl (SQL Developer Command Line) is a free command line interface for Oracle Database. It allows users to interactively or batch execute SQL and PL/SQL commands. SQLcl provides a feature-rich experience with in-line editing, statement completion, and command recall, while also supporting previously written SQL*Plus scripts.
https://www.oracle.com/database/sqldeveloper/technologies/sqlcl/

## SQL Developer
Oracle SQL Developer is a free, integrated development environment that simplifies the development and management of Oracle Database in both traditional and Cloud deployments. 
To install SQL Developer...
https://www.oracle.com/database/sqldeveloper/technologies/download/

To install SQL Developer as a VSCode Extension...
https://marketplace.visualstudio.com/items?itemName=Oracle.sql-developer

# SQL (Structured Query Language)
RDBMS - Relational Database Management System -> Uses SQL

## DB Browser for SQLite Installation
To work with SQLite databases, we will use DB Browser for SQLite, a visual open-source tool designed for creating, designing, and editing SQLite database files.
To Install...
https://github.com/sqlitebrowser/sqlitebrowser/releases 

OR

https://sqlitebrowser.org/

## Terms and Definition
**Data** -> Pieces of information
**DB Browser** -> An open-source database creation and management tool compatible with SQLite
**DML (Database Manipulation Language)** -> A subset of SQL used to alter data
**PEMDAS (Parentheses, Exponents, Multiplication, Division, Addition, Subtraction)** -> An acronym for the order of operations performed
**Relational Database** -> Information organized for the systematic use of relationships or correspondence between items
**SQL (Structured Query Language)** -> A standard programming language for the analysis and management of databases
**Table** -> Data organized into columns and rows
**ERD (Entity Relationship Diagram)** -> To View Relationship between Tables

## Queries
https://www.geeksforgeeks.org/sql/sql-tutorial/
```sql
    -- This is a comment
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: THIS IS THE STRUCTURE OF A BASIC QUERY
    */

    -- SELECT, FROM, AS, ORDER BY, LIMIT
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: This query displays all customers first, last names and email addresses
    */

    /* SELECT [attributes]
        FROM [tablename]
        ORDER BY [attribute] [ASC / DESC]
        LIMIT [Number]
    */
    SELECT 
        c.FirstName AS [Customer First Name], /*Aliasing*/
        c.LastName AS 'Customer Last Name', /*Aliasing*/
        c.Email AS EMAIL /*Aliasing*/
    FROM
        Customer AS c /*Aliasing Table Name*/
    ORDER BY
        LastName ASC /*Ascending*/
        FirstName DESC /*Descending*/
    LIMIT 10 /*Limit Results/Rows Shown*/

    --IMPT: Describe Query - Get Information about data in Table
    describe [tablename]
    -- E.g.
    describe Employees
    desc Employees

```

## Discovering Insights in Data
**Operator Types**
    - Arithmetic (+, -, *, /, %)
    - Comparison (==, <>, >, <, >=, <=>)
    - Logical (AND, OR, IN, LIKE, BETWEEN)

```sql
    -- WHERE
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Customers who purchased two songs at $0.99 each
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        total = 1.98
    ORDER BY
        InvoiceDate

    -- BETWEEN, AND
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: How many Invoices do we have that are between $1.98 and $5.00?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        total BETWEEN 1.98 AND 5.00
    ORDER BY
        InvoiceDate

    -- IN
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: How many Invoices do we have that are exactly $1.98 or $3.96?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        total IN (1.98, 3.96)
    ORDER BY
        InvoiceDate

    -- =
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: How many Invoices were billed to Brussels?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        BillingCity = "Brussels"
    ORDER BY
        InvoiceDate

    -- IN
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: How many Invoices were billed to Brussels, Orlando or Paris?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        BillingCity IN ("Brussels", "Orlando", "Paris")
    ORDER BY
        InvoiceDate
    
    -- LIKE, %
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: How many Invoices were billed to cities that start with B?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        BillingCity LIKE "B%" /* % - Don't Care What Comes After*/
    ORDER BY
        InvoiceDate

    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: How many Invoices were billed to cities that have B?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        BillingCity LIKE "%B%" /* % - Don't Care What Comes*/
    ORDER BY
        InvoiceDate

    -- Date, >, <
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Get all invoice billed after 2010-05-22 with a total less than $3.00?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE   /*Two or More Conditions*/
        DATE(InvoiceDate) > "2010-05-22" AND total < 3.00
    ORDER BY
        InvoiceDate
    
    -- OR
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Billing City Starts with P or D?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE   /*Two or More Conditions*/
        BillingCity LIKE "P%" OR BillingCity LIKE "D%" 
    ORDER BY
        InvoiceDate

    -- BEDMAS (Brackets > Exponent > Multiplication/Division > Addition/Subtraction)
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Billing City Starts with P or D that are greater than $1.98?
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE   /*Two or More Conditions*/
        total > 1.98 AND (BillingCity LIKE "P%" OR BillingCity LIKE "D%") 
    ORDER BY
        InvoiceDate
    
    -- CASE, WHEN, THEN, ELSE, END AS
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Set Purchase Types and Get Top Purchase
    */
    
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    CASE
    WHEN total < 2.00 THEN 'Baseline Purchase'
    WHEN total BETWEEN 2.00 AND 6.99 THEN 'Low Purchase'
    WHEN total BETWEEN 7.00 AND 15.00 THEN 'Target Purchase'
    ELSE 'Top Purchase'
    END AS PurchaseType
    FROM
        Invoice
    WHERE
        PurchaseType = 'Top Purchase'
    ORDER BY
        InvoiceDate

    -- *, INNER JOIN, ON
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Join Tables
    */
    
    SELECT
        *
    FROM
        Invoice
    INNER JOIN
        Customer
    ON
        Invoice.CustomerId = Customer.CustomerId

    -- Simplified Join With Aliasing
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Join Tables With Aliasing
    */
    
    SELECT
        c.FirstName,
        c.LastName,
        i.InvoiceId,
        i.InvoiceDate,
    FROM
        Invoice AS i
    INNER JOIN
        Customer AS c
    ON
        i.CustomerId = c.CustomerId
    ORDER BY
        c.CustomerId
    
    --Types of Joins
    /*
    INNER JOIN
    LEFT/RIGHT OUTER/INNER JOIN
    */

    -- Multiple Joins
    /*
    CREATED BY: KABILAN
    CREATE DATE: MM/DD/YYYY
    DESCRIPTION: Join Multiple Tables With Aliasing
    */
    
    SELECT
        c.FirstName,
        c.LastName,
        i.InvoiceId,
        i.InvoiceDate,
    FROM
        Invoice AS i
    INNER JOIN
        Customer AS c
    ON
        i.CustomerId = c.CustomerId
    INNER JOIN
        Employee AS e
    ON
        c.SupportRepId = e.EmployeeId
    ORDER BY
        i.total DESC
    LIMIT 10
    
--String Functions
    SELECT
        FirstName,
        LastName,
        Address,
        FirstName || " " || LastName  || " " || Address, /*Concatenation*/
        LENGTH(postalcode), /*Length of String*/
        SUBSTR(postalcode, 1, 5) AS [5 Digit Postal Code], /*Truncate*/
        UPPER(FirstName) AS [FirstName All UpperCase],
        LOWER(LastName) AS [LastName All LowerCase]
    FROM
        Customer
    WHERE
        Country = "USA"

    --Date Functions
    SELECT
        LastName,
        FirstName,
        BirthDate,
        STRFTIME('%Y-%m-%d', BirthDate) AS [BirthDate No Timecode],
        STRFTIME('%Y-%m-%d', 'now') -  STRFTIME('%Y-%m-%d', BirthDate) AS Age,
    FROM
        Employee

    --Aggregate Functions
    SELECT
        SUM(Total) AS [Total Sales],
        AVG(Total) AS [Average Sales],
        MAX(Total) AS [Maximum Sales],
        MIN(Total) AS [Minimum Sales],
        COUNT(*) AS [Sales Count]
    FROM
        Invoice

    --Nesting Function
    SELECT
        SUM(Total) AS [Total Sales],
        ROUND(AVG(Total), 2) AS [Average Sales], /*Round The Average*/
        MAX(Total) AS [Maximum Sales],
        MIN(Total) AS [Minimum Sales],
        COUNT(*) AS [Sales Count]
    FROM
        Invoice

    -- Grouping (Group By)
    SELECT 
        BillingCity,
        ROUND(AVG(total),2),
    FROM
        Invoice
    GROUP BY
        BillingCity
    ORDER BY
        BillingCity
    
    -- Grouping (Group By) with WHERE
    SELECT 
        BillingCity,
        ROUND(AVG(total),2),
    FROM
        Invoice
    WHERE
        BillingCity LIKE 'L%'
    GROUP BY
        BillingCity
    ORDER BY
        BillingCity

    -- Grouping (Group By) with HAVING
    SELECT 
        BillingCity,
        ROUND(AVG(total),2),
    FROM
        Invoice
    GROUP BY
        BillingCity
    HAVING
        AVG(total) > 5
    ORDER BY
        BillingCity

    -- Grouping (Group By) with WHERE and HAVING
    SELECT 
        BillingCity,
        ROUND(AVG(total),2),
    FROM
        Invoice
    WHERE
        BillingCity LIKE 'B%'
    GROUP BY
        BillingCity
    HAVING
        AVG(total) > 5
    ORDER BY
        BillingCity

    -- Grouping Many Fields
    SELECT 
        BillingCountry,
        BillingCity,
        ROUND(AVG(Total), 2)
    FROM
        Invoice
    GROUP BY
        BillingCountry, BillingCity
    ORDER BY
        BillingCountry

    -- Select Subquery
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity,
        total
    FROM
        Invoice
    WHERE
        total < (SELECT AVG(Total) FROM INVOICE)
    ORDER BY
        total DESC
    
    -- Aggregated Subqueries
    SELECT
        BillingCity,
        AVG(Total) AS [City Average],
        (SELECT AVG(Total) FROM INVOICE) AS [Global Average]
    FROM
        Invoice
    GROUP BY
        BillingCity
    ORDER BY
        BillingCity

    -- Non-aggregate subqueries
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity
    FROM
        Invoice
    WHERE
        InvoiceDate >
        (SELECT
            InvoiceDate
        FROM
            Invoice
        WHERE
            InvoiceId = 251)

    -- IN clause Subquery
    SELECT
        InvoiceDate,
        BillingAddress,
        BillingCity
    FROM
        Invoice
    WHERE
        InvoiceDate IN 
            (SELECT
                InvoiceDate
            FROM
                Invoice
            WHERE
                InvoiceId IN (251, 252, 254))

    -- DISTINCT clause subquery
    SELECT
        TrackId,
        Composer,
        Name
    FROM
        Track
    WHERE
        TrackId
    NOT IN
        (SELECT
            DISTINCT
                TrackId
        FROM
            InvoiceLine
        ORDER BY
            TrackId)
    
    -- Stored Queries (To Reuse Queries)
    CREATE VIEW V_AvgTotal AS
    SELECT
        ROUND(AVG(total), 2) AS [Average Total]
    FROM
        Invoice

    -- To Edit the Stored View
    DROP VIEW "main""V_AvgTotal" /*Drop the View*/
    CREATE VIEW V_AvgTotal AS   /*Modify the View*/
    SELECT
        AVG(total) AS [Average Total]
    FROM
        Invoice
    
    -- Joining Views
    CREATE VIEW V_Tracks_InvoiceLine
    SELECT
        il.InvoiceId,
        il.UnitPrice,
        il.Quantity,
        il.Name,
        t.Composer,
        t.Milliseconds,
    FROM
        Invoiceline il
    INNER JOIN
        Track t
    ON 
        il.TrackId = t.TrackId
    
    --Delete View
    DROP VIEW
        "V_AvgTotal"


    --DML (Data Manipulation Language)
    -- Insert
    INSERT INTO 
        Artist(Name)
    VALUES ("Bob Marley")

    -- Update
    UPDATE Artist
    SET Name = "Damien Marley"
    WHERE
        ArtistId = 276

    -- Delete
    DELETE FROM
        Artist
    WHERE
        ArtistId = 276
    
```

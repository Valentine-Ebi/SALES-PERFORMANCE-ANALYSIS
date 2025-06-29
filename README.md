# KULTRA MEGA STORES (KMS) SALES ANALYSIS 

## ABOUT THE COMPANY
Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and furniture. Its customer base includes individual consumers, small businesses (retail), and large corporate clients (wholesale) across Lagos, Nigeria. 

## PROJECT OVERVIEW
This project aims to analyse the sales performance of Kulta Mega Stores in the Abuja Division to present key findings, insights and recommendations that will support business decision making. 

## Key focus areas include:
  1. Which product category had the highest sales? 

  2. What are the Top 3 and Bottom 3 regions in terms of sales? 

  3. What were the total sales of appliances in Ontario? 

  4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers 

  5. KMS incurred the most shipping cost using which shipping method? 

  6. Who are the most valuable customers, and what products or services do they typically purchase? 

  7. Which small business customer had the highest sales? 

  8. Which Corporate Customer placed the most number of orders in 2009 – 2012? 

  9. Which consumer customer was the most profitable one? 

  10. Which customer returned items, and what segment do they belong to? 

  11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent       shipping costs based on the Order Priority?

## TOOLS USED FOR THIS ANALYSIS
The tool for this analysis is Microsoft SQL Server Management Studio (SSMS) and can be downloaded through this link (https://learn.microsoft.com/en-us/ssms/install/install)

## DATA SOURCE
The data for this project is gotten from Digital SkillUp African (DSA) Learning Management System as part of our final Project.

## ETL PROCESS

### Data Extraction 
As stated above, the data for this analysis is gotten from Digital SkillUp African Learning Management System.

### Data Transformation/Loading
The Data was transformed using SQL Server, changing inappropriate data types (converting Date from Strings back to Date and changing Order ID from Smallint to Int) due to the large volume of data and also replacing missing Values in Profit_Base_Margin Colum, Proft Column and Unit_Price Colum using queries.

## Checking for null values in "PROFIT, PRODUCT BASE MARGIN and UNIT PRICE COLUMNS"

                  select * from [KMS Sql Case Study]
                  Where Product_Base_Margin Is NULL Or Profit is NULL Or
                  Unit_Price is NULL

  After checking for Null Values in the above Columns, 153 Null Values were discovered in total. 72 from Profit Column, 63 from Profit Base Margin Column and 12 from Unit Price Column.

![NULL Values for P U_P](https://github.com/user-attachments/assets/cf3f960a-467f-403d-bff7-cb980cb4265d)

### Replacing the Null Values with Mean

                  update [KMS Sql Case Study]
                  Set Profit = 181.18
                  where Profit is NULL
                  
                  update [KMS Sql Case Study]
                  Set Unit_Price = 89.35
                  where Unit_Price is NULL
                  
                  update [KMS Sql Case Study]
                  Set Product_Base_Margin = 0.51
                  where Product_Base_Margin is NULL

## Main Analysis 

### Key Performance Indicators (KPIs)
  1. Total Sales                   ₦ 14,915,600.83
  
  2. Total Shippimg Cost           ₦ 107,831.04
  
  3. Total Profit                  ₦ 1,537,521.02
 
  4. Total Discount                ₦ 417.19
  
  5. Total Unit Price              ₦ 751442.43
 
  6. Total Orders                  8399
 
  7. Total Product Base Margin     ₦ 4,304.44

 The following Queries wrere used the Extract the above KPIs  

                  Select Sum(Sales) As Total_Sales,
                  Count(Order_ID) As Total_Orders,
                  Sum(Profit) As Total_Profit,
                  Sum(Shipping_Cost) As Total_Shipping_Cost,
                  Sum(Discount) As Total_Discount,
                  Sum(Unit_Price) As Total_Unit_Price,
                  Sum(Product_Base_Margin) As Toatl_Product_Base_Margin
                  From [KMS Sql Case Study]


![KPI](https://github.com/user-attachments/assets/22bebfc3-75d6-4da4-a425-765417d09ec1)

### Finding the Product Category with the Highest Sales

                  Select top 1 Product_Category, Sum(Sales) As TotalSales
                  From [KMS Sql Case Study]
                  Group By Product_Category
                  Order By TotalSales Desc

### The Highest Sales product is Technology


![Top 1 Highest Sales product](https://github.com/user-attachments/assets/0b88453a-71bf-4df7-b028-7e8ca6aea6f4)


### Top 3 Highest Sales Products

                    Select top 3 Product_Category, Sum(Sales) As TotalSales
                    From [KMS Sql Case Study]
                    Group By Product_Category
                    Order By TotalSales Desc

The Top 3 Highest Sales Products are; Technology, Furniture and Office Supplies 

![Top 3 highest sales product](https://github.com/user-attachments/assets/0a69691b-0f16-4e81-b14a-c45cc1dec457)


### Finding the TOP 3 and BOTTOM 3 Region in Trems of Sales

###   Top 3 Region by Sales
                Select top 3 Region, Sum(Sales) As TotalSales
                From [KMS Sql Case Study]
                Group By Region
                Order By TotalSales Desc

The Top 3 Region by Sales are; West, Ontario and Prarie

![Top 3 Region by sales ](https://github.com/user-attachments/assets/42c5716f-f237-4b96-98ff-0f1556e25b85)


###   Bottom 3 Region by Sales
                Select top 3 Region, Sum(Sales) As TotalSales
                From [KMS Sql Case Study]
                Group By Region
                Order By TotalSales Asc
          
The bottom 3 Region by sales are; Nunavut, Northwest Territories and Yukon, with Nunavut having the lowest.

![Bottom 3 Region by sales ](https://github.com/user-attachments/assets/24701c98-b035-4775-b265-8e9575e2b974)

### Determining the Total sales of appliances in Ontario
    
              Select Sum(Sales) As TotalSales
              From [KMS Sql Case Study]
              where Product_Category = 'Appliances'
              And Region = 'Ontario'

They were no Sales of Appliances made in Ontario

![Total sales of Appliances in Ontario](https://github.com/user-attachments/assets/aa6649a9-f90d-4ee8-8a8f-2516724a9b52)

### Determining the bottom 10 customers by Sales
    
            SELECT Top 10 customer_name, SUM(sales) AS total_sales
            FROM [KMS Sql Case Study]
            GROUP BY customer_name
            ORDER BY total_sales ASC

    
![Bottom 10 Customers by sales ](https://github.com/user-attachments/assets/b83836f4-c78a-4d16-b660-6aed41f935d6)

In order to increase the revenue from the bottom 10 customers, the management should Offer exclusive promotions, Target them with discounted bundles
and Launch a re-engagement campaign with incentives or feedback surveys.

### Determining the Highest shipping cost by shipping method

          Select Top 1 Ship_Mode, Shipping_Cost
          From [KMS Sql Case Study]
          Order by Shipping_Cost Desc

The Most expensive Methoed is Delivery Truck.

![Highest Shipping cost by shipping method](https://github.com/user-attachments/assets/e18c3766-3c00-40b6-809f-4d440d1eb3ad)

![Top 1 Highest shipping cost by shipping method ](https://github.com/user-attachments/assets/cb7cf773-683c-4890-af0b-5715408516e3)

### The Most valuable Customers and the product or Services there purchase

                Select * from [KMS Sql Case Study]
                Select Top 10 Customer_Name, Product_Name, Sum(Sales) As Total_Spent
                From [KMS Sql Case Study]
                Group By Customer_Name, Product_Name
                Order By Total_Spent Desc

![Valuable customers and product purchased ](https://github.com/user-attachments/assets/81f7cbec-3e2f-4e6b-8434-91a2a3c7f27e)


### Small Business Customer with the highest Sales

              SELECT Top 10 Customer_Name, SUM(Sales) AS Total_sales
              FROM [KMS Sql Case Study]
              WHERE Customer_Segment = 'Small Business'
              GROUP BY Customer_Name
              ORDER BY Total_sales DESC

![Small Business Custom Top 1](https://github.com/user-attachments/assets/9d815a78-ec7a-43ed-9c66-12c54a756a98)

![Small Business with Highest Sales ](https://github.com/user-attachments/assets/f2b8cabc-8874-40bf-9c56-8e31d8e9134f)


### Corporate customer with the most placed number of orders in 2009 - 2012

              Select Top 1 Customer_Name, Count(Order_ID) As Total_Orders
              From [KMS Sql Case Study]
              WHERE Customer_Segment = 'Corporate'
              And Order_Date Between '2009-01-01' and '2012-12-31'
              Group By Customer_Name
              Order By Total_Orders Desc

![Corporate Customers Top 1](https://github.com/user-attachments/assets/9b487ac6-031c-45bd-b899-e2046c2ffb5a)


### Top 5 Corperate customer that placed the most number of orders in 2009 - 2012

              Select Top 5 Customer_Name, Count(Order_ID) As Total_Orders
              From [KMS Sql Case Study]
              WHERE Customer_Segment = 'Corporate'
              And Order_Date Between '2009-01-01' and '2012-12-31'
              Group By Customer_Name
              Order By Total_Orders Desc

 ![Corporate Customers Top 5](https://github.com/user-attachments/assets/d876d0fb-9cc1-429a-ace0-2b8f373ea7e3)


### Most Profitable Consumer Customer

                SELECT Top 1 Customer_Name, SUM(Profit) AS total_profit
                FROM [KMS Sql Case Study]
                WHERE Customer_Segment = 'Consumer'
                GROUP BY Customer_Name
                ORDER BY total_profit DESC

![Profitable Customers Top 1](https://github.com/user-attachments/assets/c825f90a-e58f-46c7-9229-d5a0c5b08fa0)

### Top 5 Most Profitable Consumer Customer

                SELECT Top 5 Customer_Name, SUM(Profit) AS total_profit
                FROM [KMS Sql Case Study]
                WHERE Customer_Segment = 'Consumer'
                GROUP BY Customer_Name
                ORDER BY total_profit DESC

![Profitable customers top 5](https://github.com/user-attachments/assets/b0afff81-73bd-4a4c-8733-280e10263a79)

### Customer that returned items, and the segment they belong to
      
#### Joining the two tables (KMS Sql Case Study and Order_Status) to determine which customer returned items and from which Segment.

                SELECT DISTINCT [KMS Sql Case Study].customer_name, [KMS Sql Case Study].customer_segment
                FROM [KMS Sql Case Study]
                JOIN Order_Status 
                ON [KMS Sql Case Study].Order_ID = Order_Status.Order_ID
                WHERE [Status] = 'Returned'

![Returned Orders ](https://github.com/user-attachments/assets/784c47d8-dbeb-45d7-b93e-37d5a081f35d)

### QUESTION 10

![Q 10](https://github.com/user-attachments/assets/fb5e8644-cbd9-4a56-a515-542f9b6ea83c)



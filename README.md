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

### Replacing the Null Values with 0

                  update [KMS Sql Case Study]
                  Set Profit = 0
                  where Profit is NULL
                  
                  update [KMS Sql Case Study]
                  Set Unit_Price = 0
                  where Unit_Price is NULL
                  
                  update [KMS Sql Case Study]
                  Set Product_Base_Margin = 0
                  where Product_Base_Margin is NULL

## Main Analysis 

### Key Performance Indicators (KPIs)
  1. Total Sales                  ₦14915600.8311923
  
  2. Total Shippimg Cost           ₦107831.039506674
 
  3. Total Discount                ₦417.190000595525
 
  4. Total Profit                  ₦1523388.97560732
  
  5. Total Unit Price              ₦750370.228812218
 
  6. Total Orders                  8399
 
  7. Total Product Base Margin     ₦4272.30998769403

 The following Queries wrere used the Extract the above KPIs  

                  Select Sum(Sales) As Total_Sales,
                  Count(Order_ID) As Total_Orders,
                  Sum(Profit) As Total_Profit,
                  Sum(Shipping_Cost) As Total_Shipping_Cost,
                  Sum(Discount) As Total_Discount,
                  Sum(Unit_Price) As Total_Unit_Price,
                  Sum(Product_Base_Margin) As Toatl_Product_Base_Margin
                  From [KMS Sql Case Study]

![KPIs](https://github.com/user-attachments/assets/a14a6241-2630-4ce7-a957-4ed598302674)

### Finding the Product Category with the Highest Sales

                  Select top 1 Product_Category, Sum(Sales) As TotalSales
                  From [KMS Sql Case Study]
                  Group By Product_Category
                  Order By TotalSales Desc

### The Highest Sales product is Technology

![Highest Sales Product](https://github.com/user-attachments/assets/a1c22707-bf04-4526-babf-860a1cd44ff9)

### Top 3 Highest Sales Products
The Top 3 Highest Sales Products are; Technology, Furniture and Office Supplies 

![Top 3 Highest Sales Product](https://github.com/user-attachments/assets/681fc4e3-e14c-4c03-86e9-e1d0acb965c5)

### Finding the TOP 3 and BOTTOM 3 Region in Trems of Sales

###   Top 3 Region by Sales
                Select top 3 Region, Sum(Sales) As TotalSales
                From [KMS Sql Case Study]
                Group By Region
                Order By TotalSales Desc
The Top 3 Region by Sales are; West, Ontario and Prarie

![Top 3 Region by Sales](https://github.com/user-attachments/assets/1be4330a-63a5-485c-9088-e8723958155e)

###   Bottom 3 Region by Sales
                Select top 3 Region, Sum(Sales) As TotalSales
                From [KMS Sql Case Study]
                Group By Region
                Order By TotalSales Asc
          
The bottom 3 Region by sales are; Nunavut, Northwest Territories and Yukon, with Nunavut having the lowest.

![Bottom 3 Sales by Region](https://github.com/user-attachments/assets/4f999d08-027d-4a82-8639-ea8ebecfac14)

### Determing the Total sales of appliances in Ontario
    
              Select Sum(Sales) As TotalSales
              From [KMS Sql Case Study]
              where Product_Category = 'Appliances'
              And Region = 'Ontario'

They were no Sales of Appliances made in Ontario

![Toatl Sales of Appliances in Ontario](https://github.com/user-attachments/assets/0c2237b9-d314-4aee-b7bf-453bfad2f861)

### Determining the bottom 10 customers by Sales
    
            SELECT Top 10 customer_name, SUM(sales) AS total_sales
            FROM [KMS Sql Case Study]
            GROUP BY customer_name
            ORDER BY total_sales ASC

    
![Bottom 10 Customers by Sales](https://github.com/user-attachments/assets/ba68db6b-44de-464a-af71-446ca88d16f3)

In order to increase the revenue from the bottom 10 customers, the management should Offer exclusive promotions, Target them with discounted bundles
and Launch a re-engagement campaign with incentives or feedback surveys.

### Determining the Highest shipping cost by shipping method

          Select Top 1 Ship_Mode, Shipping_Cost
          From [KMS Sql Case Study]
          Order by Shipping_Cost Desc

The Most expensive Methoed is Delivery Truck.
![most espensive shipping mode 1](https://github.com/user-attachments/assets/6a8ba052-3e2a-49fd-aed7-322eaee4f9ba)


### The Most valuable Customers and the product or Services there purchase

                Select * from [KMS Sql Case Study]
                Select Top 10 Customer_Name, Product_Name, Sum(Sales) As Total_Spent
                From [KMS Sql Case Study]
                Group By Customer_Name, Product_Name
                Order By Total_Spent Desc

![Most Valuable Customers and product purchased](https://github.com/user-attachments/assets/f291f18c-3e2a-4b17-aea0-80316ed6ca2d)


### Small Business Customer with the highest Sales

              SELECT Top 10 Customer_Name, SUM(Sales) AS Total_sales
              FROM [KMS Sql Case Study]
              WHERE Customer_Segment = 'Small Business'
              GROUP BY Customer_Name
              ORDER BY Total_sales DESC

![Small Business Customer with the highest Sales](https://github.com/user-attachments/assets/fcec9ae0-fa54-406e-a43a-fa08ec8c70c4)


### Corporate customer with the most placed number of orders in 2009 - 2012

              Select Top 1 Customer_Name, Count(Order_ID) As Total_Orders
              From [KMS Sql Case Study]
              WHERE Customer_Segment = 'Corporate'
              And Order_Date Between '2009-01-01' and '2012-12-31'
              Group By Customer_Name
              Order By Total_Orders Desc

![Corporate Customer with the most placed orders ](https://github.com/user-attachments/assets/4236981b-4065-4961-9151-fd81487d54df)


### Top 5 Corperate customer that placed the most number of orders in 2009 - 2012

              Select Top 5 Customer_Name, Count(Order_ID) As Total_Orders
              From [KMS Sql Case Study]
              WHERE Customer_Segment = 'Corporate'
              And Order_Date Between '2009-01-01' and '2012-12-31'
              Group By Customer_Name
              Order By Total_Orders Desc

  ![Corporate Customer with the most placed orders 2 ](https://github.com/user-attachments/assets/aaf62788-bb5c-4bb3-8a79-31f510a753e3)

### Most Profitable Consumer Customer

                SELECT Top 1 Customer_Name, SUM(Profit) AS total_profit
                FROM [KMS Sql Case Study]
                WHERE Customer_Segment = 'Consumer'
                GROUP BY Customer_Name
                ORDER BY total_profit DESC

![Most Profitable Consumer Customer 1 ](https://github.com/user-attachments/assets/3af24b20-8115-40c2-b8af-baa64a1a166f)

### Top 5 Most Profitable Consumer Customer

                SELECT Top 5 Customer_Name, SUM(Profit) AS total_profit
                FROM [KMS Sql Case Study]
                WHERE Customer_Segment = 'Consumer'
                GROUP BY Customer_Name
                ORDER BY total_profit DESC

![Most Profitable Consumer Customer ](https://github.com/user-attachments/assets/f6b08ed2-be24-4fda-860e-07df4e73f84b)

### Customer that returned items, and the segment they belong to
      
#### Joining the two tables (KMS Sql Case Study and Order_Status) to determine which customer returned items and from which Segment.

                SELECT DISTINCT [KMS Sql Case Study].customer_name, [KMS Sql Case Study].customer_segment
                FROM [KMS Sql Case Study]
                JOIN Order_Status 
                ON [KMS Sql Case Study].Order_ID = Order_Status.Order_ID
                WHERE [Status] = 'Returned'


![Returned Orders ](https://github.com/user-attachments/assets/15a541ad-2bae-4b63-aeb7-47bc314f92e2)

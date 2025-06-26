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



## Key Performance Indicators (KPIs)
  1. Total Sales                  ₦14915600.8311923
  
  2. Total Shippimg Cost           ₦107831.039506674
 
  3. Total Discount                ₦417.190000595525
 
  4. Total Profit                  ₦1523388.97560732
  
  5. Total Unit Price              ₦750370.228812218![NULL Values for P U_P](https://github.com/user-attachments/assets/cf3f960a-467f-403d-bff7-cb980cb4265d)
![NULL Values for P U_P](https://github.com/user-attachments/assets/cf3f960a-467f-403d-bff7-cb980cb4265d)

 
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


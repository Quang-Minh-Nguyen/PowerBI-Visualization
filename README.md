# Data visualization in Power BI

In this project, I cleaned, manipulated and visualized the month-to-date sales data from a FMCG brand. To be more specific, descriptive analysis was used to track the sales timeline by regions and products. Besides, the products which have decent performance was also identified in the report. I only used 1 tool in this project which was the Power BI.

## Step 1: Importing & Transforming Data

From my experience, I always want to look into the files before importing them. In this case, the data was a Excel files with 3 sheets: Calendar, Sales and Target

![combine](https://user-images.githubusercontent.com/118095331/216929465-4d91675b-d52a-4d6f-b8bb-1cbf7cf06a5a.png)

Next, I imported 3 sheets into Power BI and began to transforme them. When it comes to transfoming the data, I always began with removing any null rows, promoting headers, making sure that the data type in each column was correct and removing duplicates. Adding new column(s) would depend on different cases. In this case, I only had to add 1 new column named NPP(Nhà phân phối) in the Target table for the modeling relationship.

![basic step](https://user-images.githubusercontent.com/118095331/216938532-aaa78e4e-f24f-4c05-9479-4b49a848af05.jpg)

It is very essential to create Fact tables and Dim tables for the data modeling later.

![DIM + F](https://user-images.githubusercontent.com/118095331/216937259-21470faa-07d5-46c5-8415-fe0feace0648.jpg)

Normally. to create DIM table, I only needed to select columns from Fact table, add thems as a new query, convert to table then remove duplicates which left with not-null and unique value.
![dim](https://user-images.githubusercontent.com/118095331/216941053-8cd0154c-8d19-4f4b-b767-3c529c75c84e.png)

However in this case, I will need to create the calendar DIM table from scracth to have the month-to-date analysis. After I got the date column, I need to create the Weekday column to identify which day is the working day and which day is the resting day. Furthermore, I converted the working day as 1 and resting day as 0 for the time intelligence calculation later

![image](https://user-images.githubusercontent.com/118095331/216940793-1a2cc23a-477e-4689-94de-7b4dd905ed14.png)

# Data visualization in Power BI

**Question: Create a month-to-date report and identify the regions and products that have decent performance.**

In this project, I cleaned, manipulated and visualized the month-to-date sales data from a FMCG brand. To be more specific, descriptive analysis was used to track the sales timeline by regions and products. Besides, the products which have decent performance was also identified in the report. I only used 1 tool in this project which was the Power BI.

## Step 1: Data Importing & Transforming 

From my experience, I always want to look into the files before importing them. In this case, the data was a Excel files with 3 sheets: Calendar, Sales and Target

![combine](https://user-images.githubusercontent.com/118095331/216929465-4d91675b-d52a-4d6f-b8bb-1cbf7cf06a5a.png)

Next, I imported 3 sheets into Power BI and began to transform them. When it comes to transfoming the data, I always began with removing any null rows, promoting headers, making sure that the data type in each column was correct and removing duplicates. Adding new column(s) would depend on different cases. In this case, I only had to add 1 new column named NPP(Nhà phân phối) in the Target table for the modeling relationship.

![basic step](https://user-images.githubusercontent.com/118095331/216938532-aaa78e4e-f24f-4c05-9479-4b49a848af05.jpg)

It was very essential to name and create Fact tables and Dim tables for the data modeling later.

![DIM + F](https://user-images.githubusercontent.com/118095331/216937259-21470faa-07d5-46c5-8415-fe0feace0648.jpg)

Normally. to create DIM table, I only needed to select columns from Fact table, add thems as a new query, convert to table then remove duplicates which left with not-null and unique value.
![dim](https://user-images.githubusercontent.com/118095331/216941053-8cd0154c-8d19-4f4b-b767-3c529c75c84e.png)

However in this case, I needed to create the calendar DIM table from scracth to have the month-to-date analysis. After I got the date column, I added the Weekday column to identify which day is the working day and which day is the resting day. Furthermore, I converted the working day as 1 and resting day as 0 for the time intelligence calculation later. 

![image](https://user-images.githubusercontent.com/118095331/216940793-1a2cc23a-477e-4689-94de-7b4dd905ed14.png)

## Step 2: Data Modeling

After I had all the Fact and DIM tables listed, it was very easy to create relationships in the data modeling and I could get into visualizing the data right away.
![image](https://user-images.githubusercontent.com/118095331/216941943-5c49f9e0-a253-452f-94cc-2b7d6fb49ea2.png)

## Step 3: Data Visualizing
The most important aspect in this report was the month-to-date sales tracking, which means there would be time intelligence calculation involved. When it comes to visualizing, I always start with making a table first if needed. This gives me a holistic view of what I am about to visualize. This was the final table, however, it required new metrics and calculation, which I will explain later.
![image](https://user-images.githubusercontent.com/118095331/216944898-a1bb6f5e-0bf0-4f2b-999a-95d19dd68a99.png)

**For Doanh Số Lũy Kế (Cummulative Revenue)**
```
Doanh số lũy kế = 
 CALCULATE(
     SUM('F SALES'[SALES VALUE]),
     DATESMTD('DIM CALENDAR'[Ngày]))
```
**For Tổng Số Ngày Làm Việc (Total working days)**
```
Tổng số ngày làm việc = 
 NETWORKDAYS(DATE(2021,5,1),DATE(2021,5,31),1,{DATE(2021,5,3)})
 ```
 **For Số ngày đã làm việc (Cummulative working day)**
 ```
 Số ngày đã làm việc = CALCULATE(
    SUM('DIM CALENDAR'[Làm Việc/Nghỉ]),
    DATESMTD('DIM CALENDAR'[Ngày]))
 ```
 **For % deadline**
 ```
 % deadline = 'DIM CALENDAR'[Số ngày đã làm việc]/'DIM CALENDAR'[Tổng số ngày làm việc]
 ```
 
 Then it was all good. Turned into a visualization, the table would look like this:
 ![image](https://user-images.githubusercontent.com/118095331/216945322-699a9a0c-502a-493b-ab29-4fa09eee4c17.png)

All I had to do left was add more charts to answer the questions asked: "What are the products and regions that have decent performances?". Here is the final report:
![image](https://user-images.githubusercontent.com/118095331/216946434-4b150204-ca14-4b77-a5af-70b2dee685cc.png)

## Step 4: Conclusion
> Overall, the brand did a really great job by surpassing the month-to-date target (80M in sales vs 67.50M in target). 

> To be more specific, R1 and R2 region showed decent performance by excessing the deadline 19.43% and 21.12% respectively. On the other hand, given the same target, R3 region fell behind with a -14.76% compared to the deadline. 


> Furthermore, there are 6 product which have outstanding sales which are Monte vani 55g, Monte Schoko 55g, Monte Drink 95g, Cheese Dâu - Chuối 50g, Cheese Dâu - Vani 50g, Phomai Sandwich 200g.
 
 

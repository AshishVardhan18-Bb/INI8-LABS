# INI8 LABS PRIVATE LIMITED PROJECT

### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiY2VlNjE1MmEtNzZjYy00MjQ5LTkzZTAtYTI4Mzk4MWZlMTc4IiwidCI6IjM0ODNhYmVlLWI2MmMtNDcwYS04MTQ2LTczYTAzOTk3NzZiYyJ9

## Problem Statement

The goal is to create a comprehensive Power BI report for analyzing car purchase and employee data. This report will include a date table for temporal analysis and an interactive date slicer for filtering data over time. Key insights to be derived include the count of cars segmented by brand, company, and department, displayed as individual cards. A calculated column will be created in the car table to identify the latest car purchase date for each buyer. Additionally, analytical metrics such as the average salary of employees grouped by country and the car make year with the highest average price will be computed. Lastly, the report will uncover insights on the most popular car brands preferred by each gender. This interactive dashboard aims to facilitate data-driven decision-making by providing actionable insights into car purchases and related employee demographics.

## Steps followed 

-1) So firstly I have imported the data sets in to my power bi desktop and
initially there were few errors which needed to be corrected , there
were error values in Cars Table which I have deleted using power query
editor.
-2) Later I converted some columns which needed to be as numerical but
mistakenly given as text and I have removed few outliers which would
affect the data and I have finished the Data Pre Processing .
-3) So next I have gone in to the model view box and I have made the
relationships between the tables
-4) Later I used the dax query to make a new table called the Date Table and
later I have used a slicer visual for Dates to be kept in it so that we can
use what ever date or year we wanted
-5) As a next step I have created four measures firstly which are Count of
cars, Cars by brand, Cars by Model Name, Cars by Department and I
have used the card visuals for these four measures and next I have
added the slicers for company name,model name and department so
that I will be able to count the number of cars of a particular
brand/company/department.
-6) And in the next step I have created a column in the Cars table called
Latest car brought date using dax, this would give me the latest car
bought date of that particular car and to make it simple I made a matrix
with cars company name showing the latest date when a car has been
purchased based on the buyer details
-7) I have created a measure for Salary column which calculates the average
salary and later to know the average salary of a particular country as it
has small data I have used a line chart showing the average salary of a
country and too know about the average salary of a particular country I
have used a slicer too for country
-8) To Calculate the make year with the highest average price I have used a
line chart and I have displayed only the top 5 make years in it which we

can find our top most make year I have included average price and make
year in the line chart visual which gave me 1980 as the make year with
the highest average price.
-9) Then I wanted to calculate the most popular car brand for each gender I
have used some dax formulas to create the popular cars for each
genders and I have displayed it using the matrix visual.
-10) And my last visual was a pie chart showing sum of the cars price
purchased by each gender I have put these both columns directly in the
pie chart. 

## Key Measures

 ### Average Price

 Average Price = AVERAGE('Cars'[Price])

### Average Salary of country

Average_Salary_of_Country = AVERAGE('Employee Details'[salary])

### Car Count 

Car Count by Brand and Gender = 
COUNTROWS('Employee Details')

### Cars by Brand

Cars by Brand = DISTINCTCOUNT(Cars[Company_Name ])

### Cars by Department

Cars By Department = 
COUNTROWS(RELATEDTABLE('Employee Details'))

### Cars by Model Name

Cars by Model Name = DISTINCTCOUNT(Cars[Model_Name])

### Count of Cars

Count of Cars = COUNT(Cars[Car_ID])



### Make Year with Highest Average Price

Make Year with Highest Average Price = 

VAR MaxAvgPrice = MAXX(ALL('Cars'[Make_Year]), [Average Price])

RETURN

CALCULATE(
    FIRSTNONBLANK('Cars'[Make_Year], 1),

    FILTER('Cars', [Average Price] = MaxAvgPrice)
)

### Popular Car

Popular Car = 

VAR BrandCount = 

    SUMMARIZE(
        'Employee Details',
        'Cars'[Company_Name ],
        "CarCount", [Car Count by Brand and Gender]
    )

VAR MaxBrandCount = 

    CALCULATE(
        MAXX(BrandCount, [CarCount]),
        ALLEXCEPT('Employee Details', 'Employee Details'[gender])
    )

RETURN

    CALCULATE(

        FIRSTNONBLANK('Cars'[Company_Name ], 1),
        FILTER(
            BrandCount,
            [CarCount] = MaxBrandCount
        )
    )


# Snapshot of Dashboard (Power BI Service)


![image](![Screenshot 2024-11-23 002604](https://github.com/user-attachments/assets/beb43b54-f91b-4e42-a561-d573f8087158))



## Insights from the Power BI Report Analysis:

Car Purchase Trends by Brand/Company/Department:

1) The count of cars grouped by brand, company, and department provided a clear overview of the most active segments in car purchases. The slicer functionality enabled filtering and pinpointing specific areas of interest.
Latest Car Purchase Insights:

2) The newly calculated column showing the latest car purchase dates revealed trends in purchasing activity. This helps identify brands or models that have been recently popular.
Salary Insights by Country:

3) The average salary calculated and visualized by country provided valuable demographic insights, highlighting regions with higher salary distributions and potential spending power.
Make Year with Highest Average Price:

4) The analysis showed that 1980 was the make year with the highest average price, which may suggest vintage or classic cars from that year hold higher value in the dataset.
Gender Preferences in Car Brands:

5) The matrix visual displaying the most popular car brands for each gender revealed distinct brand preferences, which could guide targeted marketing or sales strategies.
Gender-Wise Car Purchase Spending:

6) The pie chart depicting the sum of car prices purchased by each gender highlighted differences in spending patterns between genders, offering deeper insights into purchasing behaviors.
Data Cleaning and Preprocessing Benefits:

7) Addressing errors, converting data types, and removing outliers ensured data accuracy, leading to more reliable insights and trends.
Interactivity and Flexibility:

8) The use of slicers for date, brand, model name, and department enabled dynamic exploration, making the dashboard highly interactive and user-friendly.

## Conclusion:

This Power BI report showcases how data analysis can help uncover important patterns and trends in car purchases and employee details. By cleaning the data and using DAX to create new tables and columns, I was able to generate meaningful insights, like identifying the most popular car brands by gender, average salaries across countries, and the make year with the highest average price.

The interactive slicers and visuals make it easy to filter and explore the data, allowing for deeper understanding and better decision-making. For example, the 1980 make year stood out for its high average price, and gender-based brand preferences highlight opportunities for targeted strategies.

Overall, this report demonstrates how well-organized data and simple visualizations can provide valuable insights for smarter business decisions.

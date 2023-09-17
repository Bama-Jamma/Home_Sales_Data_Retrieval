# Home_Sales_Data_Retrieval

# Home Sales Data Analysis with SparkSQL

This project demonstrates data analysis tasks using PySpark and SparkSQL on a dataset of home sales data. The code provides answers to various questions related to home sales, such as average prices for different types of homes and runtime comparisons between different data processing techniques.

## Getting Started

To run this project, you need to use Google Colab. Follow these steps to set up and execute the code:

1. **Open Google Colab**: Go to [Google Colab](https://colab.research.google.com/).

2. **Create a new notebook**: Click on "File" in the top left corner and select "New Notebook."

3. **Import Dependencies**: Copy and paste the code from this repository into the notebook.

4. **Run the Code**: Execute each code cell one by one by clicking the play button or using the Shift + Enter keyboard shortcut.

## Dependencies

The code requires the following dependencies:

- Java 11
- Spark 3.4.1
- PySpark

These dependencies will be automatically installed when you run the code in Google Colab.

## Project Structure

Here's a brief overview of the main components of this project:

1. **Import Dependencies**: This section installs Java, Spark, and other required libraries.

2. **Create a SparkSession**: Initializes a SparkSession for data processing.

3. **Data Loading**: Loads the home sales data from an AWS S3 bucket into a DataFrame and creates a temporary view.

4. **Data Analysis**: The code answers the following questions using SparkSQL queries:
    - Average price for a four-bedroom house sold in each year.
    - Average price of a home for each year the home was built that have 3 bedrooms and 3 bathrooms.
    - Average price of a home for each year built with specific criteria (3 bedrooms, 3 bathrooms, 2 floors, and >= 2,000 square feet).
    - Average price of a home with a specific price range and its associated "view" rating.

5. **Caching Data**: Demonstrates how to cache and use cached data for improved query performance.

6. **Parquet Data**: Compares query performance between using cached data and reading from Parquet formatted data.

7. **Uncaching Data**: Shows how to uncache data when it's no longer needed.

## Running Queries

You can execute each query cell individually to analyze the home sales data. Results will be displayed after each query.

## Performance Comparison

This project also demonstrates the performance difference between cached data and Parquet formatted data. Cached data retrieval is faster as it's retrieved from memory, while Parquet data involves disk I/O.

## Data Source

The home sales data is retrieved from the following S3 bucket:

- [Home Sales Data](https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv)

## Conclusion

This project showcases the power of SparkSQL for analyzing large datasets and how caching and optimized data formats like Parquet can significantly impact query performance.

Feel free to modify and extend this code to suit your specific data analysis needs.

## Collaboration:

Worked with and helped multiple peers for this project, a specic thank you to Adam Glantz for helping me bounce idea around.

## This code has been brough to you by:

Sleepless Nights
Drink: Zero Sugar Sweet Tea
Music: [Oliver Anthony](https://open.spotify.com/artist/6IkfE2JyVoKwBZXvuytKX3?si=c660d0c76c6b4b67)



## Questions and Answers

*Question 1:** What is the average price for a four-bedroom house sold for each year? Round off your answer to two decimal places.

```sql
SELECT YEAR(date) AS year,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE bedrooms = 4
GROUP BY YEAR(date)
ORDER BY year;
The average price for a four-bedroom house sold for each year is as follows:

year	average_price
2019	300263.70
2020	298353.78
2021	301819.44
2022	296363.88
vbnet


#### Average Price of Homes Built with Three Bedrooms and Three Bathrooms Each Year

To calculate the average price of a home for each year it was built that has three bedrooms and three bathrooms, we can use SparkSQL. The result will be rounded to two decimal places.


Question 2:** What is the average price of a home for each year it was built that has three bedrooms and three bathrooms? Round off your answer to two decimal places.

```sql
SELECT date_built,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE bedrooms = 3
  AND bathrooms = 3
GROUP BY date_built
ORDER BY date_built;
The average price of a home for each year it was built that has three bedrooms and three bathrooms is as follows:

date_built	average_price
2010	292859.62
2011	291117.47
2012	293683.19
2013	295962.27
2014	290852.27
2015	288770.30
2016	290555.07
2017	292676.79

#### Average Price of Homes with Specific Criteria Each Year

To find the average price of a home for each year that has three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet, we can use SparkSQL. The result will be rounded to two decimal places.


**Question 3:** What is the average price of a home for each year that has three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet? Round off your answer to two decimal places.

```sql
SELECT date_built,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE bedrooms = 3
  AND bathrooms = 3
  AND floors = 2
  AND sqft_living >= 2000
GROUP BY date_built
ORDER BY date_built;
The average price of a home for each year that meets the specified criteria is as follows:

date_built	average_price
2010	285010.22
2011	276553.81
2012	307539.97
2013	303676.79
2014	298264.72
2015	297609.97
2016	293965.10
2017	280317.58
vbnet


#### "View" Rating for Homes Costing More Than or Equal to $350,000

To determine the "view" rating for homes costing more than or equal to $350,000, we can use SparkSQL. The result will be rounded to two decimal places, and the query runtime will also be provided.


**Question 4:** What is the "view" rating for homes costing more than or equal to $350,000? Determine the run time for this query, and round off your answer to two decimal places.
sql
SELECT view,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE price >= 350000



User
Can you please put everything in the markdown language?
ChatGPT
Certainly! Here are the questions and answers in Markdown format:

Question 1: Average Price for Four-Bedroom Houses Sold Each Year
What is the average price for a four-bedroom house sold for each year? Round off your answer to two decimal places.

sql

SELECT YEAR(date) AS year,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE bedrooms = 4
GROUP BY YEAR(date)
ORDER BY year;
The average price for a four-bedroom house sold for each year is as follows:

year	average_price
2019	300263.70
2020	298353.78
2021	301819.44
2022	296363.88
Question 2: Average Price of Homes Built with Three Bedrooms and Three Bathrooms Each Year
What is the average price of a home for each year it was built that has three bedrooms and three bathrooms? Round off your answer to two decimal places.

sql

SELECT date_built,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE bedrooms = 3
  AND bathrooms = 3
GROUP BY date_built
ORDER BY date_built;
The average price of a home for each year it was built that has three bedrooms and three bathrooms is as follows:

date_built	average_price
2010	292859.62
2011	291117.47
2012	293683.19
2013	295962.27
2014	290852.27
2015	288770.30
2016	290555.07
2017	292676.79
Question 3: Average Price of Homes with Specific Criteria Each Year
What is the average price of a home for each year that has three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet? Round off your answer to two decimal places.

sql

SELECT date_built,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE bedrooms = 3
  AND bathrooms = 3
  AND floors = 2
  AND sqft_living >= 2000
GROUP BY date_built
ORDER BY date_built;
The average price of a home for each year that meets the specified criteria is as follows:

date_built	average_price
2010	285010.22
2011	276553.81
2012	307539.97
2013	303676.79
2014	298264.72
2015	297609.97
2016	293965.10
2017	280317.58
Question 4: "View" Rating for Homes Costing More Than or Equal to $350,000
What is the "view" rating for homes costing more than or equal to $350,000? Determine the run time for this query, and round off your answer to two decimal places.

sql

SELECT view,
       ROUND(AVG(price), 2) AS average_price
FROM home_sales
WHERE price >= 350000
GROUP BY view
ORDER BY average_price DESC
LIMIT 1;
The "view" rating for homes costing more than or equal to $350,000 is as follows:

view	average_price
91	1137372.73

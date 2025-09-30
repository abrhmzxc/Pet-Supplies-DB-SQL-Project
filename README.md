# Pet Supplies By PetMind
Data Analyst Associate Practical Sample Exam using PostgreSQL
- Data Cleaning
- Exploratory Data Analysis
## Introduction
PetMind, a United States(U.S) based company, a retailer of products for pets. They sells product that are a mix of luxury items and everyday items which include toys and food. The company wants to increase sales by selling more products for some animals repeatedly and they have been testing this approach for the last past year.
## Data
The data table is named `pet_supplies`.

The dataset contains the sales records in the stores last year. 

##### The pet supplies

| Column Name | Criteria                                                |
|-------------|---------------------------------------------------------|
|product_id | Nominal. The unique identifier of the product. </br>**Missing values are not possible due to the database structure.**|
| category | Nominal. The category of the product, one of 6 values (Housing, Food, Toys, Equipment, Medicine, Accessory). </br>**Missing values should be replaced with “Unknown”.** |
| animal | Nominal. The type of animal the product is for. One of Dog, Cat, Fish, Bird. </br>**Missing values should be replaced with “Unknown”.** |
| size | Ordinal. The size of animal the product is for. Small, Medium, Large. </br>**Missing values should be replaced with “Unknown”.**|
| price | Continuous. The price the product is sold at. Can be any positive value, round to 2 decimal places. </br>**Missing values should be replaced with 0.** |
| sales | Continuous. The value of all sales of the product in the last year. This can be any positive value, rounded to 2 decimal places. </br>**Missing values should be replaced with the overall median sales.**|
| rating | Discrete. Customer rating of the product from 1 to 10. </br>**Missing values should be replaced with 0.** |
| repeat_purchase | Nominal. Whether customers repeatedly buy the product (1) or not (0). </br>**Missing values should be removed.** |

### This is the sample data set.
![pet_supplies_sample_data](https://github.com/user-attachments/assets/683380c5-05e2-4c14-aa0b-d0d5523fb9dd) 
## Objective

The company PetMind want a report on how repeat purchases impact sales.

**1.) Write a query to return a table that matches the description provided.**

-- make sure all of the data is clean before you start your analysis. The [table](#the-pet-supplies) shows what the data should look like.

**2.) Return the `animal`, `repeat_purchase` indicator and the `avg_sales`, along with the `min_sales` and `max_sales`. All values should be rounded to whole numbers.**

-- Show whether sales are higher for repeat purchases for different animals. You also want to give a range for the sales

**3.) Write a query to return the `product_id`, `sales` and `rating` for the relevant products.**

-- The management team want to focus on efforts in the next year on the most popular pets - cats and dogs - for products that are bought repeatedly. 

----------- 

## Process
> Note: In a real workplace, you want to avoid mistakes specially with data that in just one wrong code/query the raw data will be destroyed. So if you are in real workplace, creating a new table, duplicating the real raw data to a new data table and working on that 
duplicated table will let you do all kind of things, experiment, and assess every possible query that may lead you to the best results that you need without the pressure of destroying or deleting the whole raw data as you work.

Taking a quick look at the data, we're all sure that it is not the best data to report on too. Important to note in assessing the data are:

1. Nulls
2. Not standardized categorical data. Some are all capital letters
3. ' ','-', 'unlisted' unwanted values.
4. Duplicated data

With that in mind, cleaning the data is the first priority.

- Identify and Replace missing Values
- Convert values between data types
- Clean categorical and text data by manipulating strings

__Step 1:__ 
</br>
Checking for duplicated data: 

<img width="813" height="307" alt="image" src="https://github.com/user-attachments/assets/62fe4a47-9acf-4380-9080-7e40b3b96515" />

> 'Your query ran successfully but returned no results.' meaning there are no duplicated data in the data set that needs to be remove
>> The 'PARTITION BY' clause divides the result set into partitions and assigns a unique number to each row within each partition.
>>> to be sure that no duplicate data are in the data set, querying it is the best way.

Querying what is asked in the [table](#the-pet-supplies)


<img width="751" height="597" alt="image" src="https://github.com/user-attachments/assets/a2cca375-37e9-4e07-a965-6a56f74a7496" />







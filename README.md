# Pet Supplies By PetMind
Data Analyst Associate Practical Sample Exam using PostgreSQL
- Data Cleaning
- Exploratory Data Analysis
## Introduction
PetMind, a United States(U.S) based company, a retailer of products for pets. They sells product that are a mix of luxury items and everyday items which include toys and food. The company wants to increase sales by selling more products for some animals repeatedly and they have been testing this approach for the last past year.
## Data
The data table is named `pet_supplies`.

The dataset contains the sales records in the stores last year. 


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
**1.) Write a query to return a table that matches the description provided.**

-- make sure all of the data is clean before you start your analysis. The [table](#the-pet-supplies) shows what the data should look like.

**2.) Return the `animal`, `repeat_purchase` indicator and the `avg_sales`, along with the `min_sales` and `max_sales`. All values should be rounded to whole numbers.**

-- Show whether sales are higher for repeat purchases for different animals. You also want to give a range for the sales

**3.) Write a query to return the `product_id`, `sales` and `rating` for the relevant products.**

-- The management team want to focus on efforts in the next year on the most popular pets - cats and dogs - for products that are bought repeatedly. 

----------- 
__TASK 1:__ 
</br>Query to return a table that matches the date description provided.
Taking a quick look at the data , we're all sure that it is not the best data to report on too. 

##### The pet supplies

1. Nulls
2. Not standardized categorical data. Some are all capital letters
3. ' ','-', 'unlisted' unwanted values.

- Identify and Replace missing Values
- Convert values between data types
- Clean categorical and text data by manipulating strings



__TASK 2:__
- Aggregate numeric, categorical variables and dates by group




[Jump to a section with custom ID](#some-id)

...















<a name="some-id" />



##### Section with some ID







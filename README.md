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
> Note: </br>
In a real workplace, you want to avoid mistakes specially with data that in just one wrong code/query the raw data will be destroyed. So if you are in real workplace, creating a new table, duplicating the real raw data to a new data table and working on that 
duplicated table will let you do all kind of things, experiment, and assess every possible query that may lead you to the best results that you need without the pressure of destroying or deleting the whole raw data as you work.


__Step 1:__ 
</br>

__Cleaning the data__</br>
Taking a quick look at the data, we're all sure that it is not the best data to report on too. Important to note in assessing the data are:

1. Nulls
2. Not standardized categorical data. Some are all capital letters
3. ' ','-', 'unlisted' unwanted values.
4. Duplicated data

With that in mind, cleaning the data is the first priority.

- Identify and Replace missing Values
- Convert values between data types
- Clean categorical and text data by manipulating strings


To check for duplicated data: 

<img width="813" height="307" alt="image" src="https://github.com/user-attachments/assets/62fe4a47-9acf-4380-9080-7e40b3b96515" />

> 'Your query ran successfully but returned no results.' meaning there are no duplicated data in the data set that needs to be remove
>> The 'PARTITION BY' clause divides the result set into partitions and assigns a unique number to each row within each partition.
>>> to be sure that no duplicate data are in the data set, querying it is the best way.

Querying to return a table that matches the [table](#the-pet-supplies) description:

<img width="877" height="784" alt="image" src="https://github.com/user-attachments/assets/5bd191f5-4509-4bbb-ab34-a011b8285c87" />

![cleaned_per_supplies](https://github.com/user-attachments/assets/d2653bc8-0b55-4fcd-88bf-cf28332ff893)


- Any missing values in columns category, animal and size are replaced with 'Unknown'
  > To ensure there are no unexpected values, the 'Unknown' in else should suffice and it also catches the nulls
- Standardizing values
  > Using LOWER function to ensure case-Insensitive comparison and then INITCAP for standardizing
- Any missing values in columns price and rating replaced with '0'
- any missing values in column sales are replaced with the overall median sales.
  > by using common table expression (CTE) to query the median of the sales so it can be used to replace missing values in column sales

__Step 2:__ 
</br>
To show whether the sales are higher for repeat purchases for different animals. Return the table 'animal', 'repeat_purchase' for indicator, 'avg_sales' and with 'min_sales' and 'max_sales'.

<img width="418" height="244" alt="image" src="https://github.com/user-attachments/assets/740a4333-8aa6-4439-b165-3417289ba912" />

> I did not put the query for the cleaned data in the FROM yet, to visualize and not to be confused with the code.
>> I replaced the repeat_purchases (1= Yes, and 0 =No to visually tell and determine if it is a repeated purchases, instead of binary number (0,1)
>>> average the sales to recognize the difference of non-repeated purchase to repeated.
>>> GROUP BY the animal and repeat_purchace and ORDER BY average sale to tell whether the repeated purchases have a higher sales than the other

#### With the clean data

<img width="630" height="771" alt="image" src="https://github.com/user-attachments/assets/4e0d6659-4d6a-4c4c-a813-5692fd38b54f" />

<img width="956" height="286" alt="image" src="https://github.com/user-attachments/assets/4544b139-4848-4ad9-bbc9-617d1d708545" />

__Observation__
</br>

- Bird are the highest sales in both non-repeated purchase and repeated purchase, next to dog and cat.
- Bird in repeated purchase with the value '1408' appeared to be the highest sale compare to bird not repeated purchase with the value '1380'
- It appears to be depending on the different kind of animal impacted the repeated purchase and the avg sales.
- The results tells us that the products for the birds are the highest sales which tells us that the management should always stock their bird products as they can because many people buy bird supplies.
  

__Step 3:__ 

The management team want to focus on efforts in the next year on the most popular pets - cats and dogs - for products that are bought repeatedly.
return the product_id, sales and rating for the relevant products.

- the columns should be product_id, sales, and rating
- for the relevant products that is dogs and cats where they are bought repeatedly

<img width="387" height="143" alt="image" src="https://github.com/user-attachments/assets/c176ee03-a048-4965-84e3-134f84555591" />

#### With the clean data

<img width="737" height="759" alt="image" src="https://github.com/user-attachments/assets/888097d9-c054-4176-b591-2623035d684c" />

<img width="956" height="505" alt="image" src="https://github.com/user-attachments/assets/8609a807-c404-4259-b1c7-023c6007ee21" /> 

> I did put animal also, so I can tell whether the product is for cat or dog
> The result is filtered for cats and dogs only with the repeated purchases.

__Observation__

- Product 518, for dogs, have the highest sales compared to cats. With a value of 1797.02 sales
- Product 280 has the second highest sales but has lower rating than the 1st highest sale product which will need more checking and investigation on the actual product to test and see whether why the ratings is low but at the same time has the high sale purchaces.
- By getting the highest sales by rank, the management should always check the stock of these products so the sales will still go up.

### Conclusion

- Given that the company wants to know if the repeated purchases impact sales, the results shows that


<img width="671" height="108" alt="image" src="https://github.com/user-attachments/assets/bd21d877-a9f0-4e49-8cc1-58f034d0693f" />

<img width="814" height="87" alt="image" src="https://github.com/user-attachments/assets/c3985363-865d-451d-9773-4c47600587ad" />







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
Taking a quick look at the data using __basic query__ to analyze every column, to look for inconsistency, we're all sure that it is not the best data to report on too. Important to note in assessing the data are:

1. Nulls
2. Not standardized categorical data. Some are all capital letters
3. ' ','-', 'unlisted' unwanted values.
4. Checking for Duplicated data

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

<img width="984" height="741" alt="image" src="https://github.com/user-attachments/assets/c463f8d4-5156-4726-9cbf-15e6b7c18e56" />


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

<img width="726" height="847" alt="image" src="https://github.com/user-attachments/assets/44aeb815-860e-44c9-b920-7f3639a18c6a" />



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

<img width="826" height="804" alt="image" src="https://github.com/user-attachments/assets/07ca6ffc-fb0c-4385-a5bf-4b04a7983334" />


<img width="956" height="505" alt="image" src="https://github.com/user-attachments/assets/8609a807-c404-4259-b1c7-023c6007ee21" /> 

> I did put animal also, so I can tell whether the product is for cat or dog
> The result is filtered for cats and dogs only with the repeated purchases.

__Observation__

- Product 518, for dogs, have the highest sales compared to cats. With a value of 1797.02 sales
- Product 280 has the second highest sales but has lower rating than the 1st highest sale product which will need more checking and investigation on the actual product to test and see whether why the ratings is low but at the same time has the high sale purchaces.
- By getting the highest sales by rank, the management should always check the stock of these products so the sales will still go up.

## Conclusion

> Using the function GROUP BY ROLLUP to easily show the sub total and total per aggregated values, to easily compare the repeated and non-repeated purchase and also their average anf total sales.
- Given that the company wants to know if the repeated purchases impact sales, the answer is yes and no. the results shows that


<img width="1107" height="112" alt="image" src="https://github.com/user-attachments/assets/25af85ed-52f8-4fe6-b144-6eb31acae3bd" />

- High Average Sales but low total sales </br>
  Meaning each transaction or order of product brings in a __large amount of sales__, but the product is s old __infrequently__ or in __low volume__.
- The birds product is __High-value but niche__. This could indicate a luxury item, or a special product or can be rare purchase.
- It is a __premium/low frequency products__, the management established a pricing power but for targeted consumer only promotion.

<img width="1108" height="85" alt="image" src="https://github.com/user-attachments/assets/9a301840-58f2-41a9-aff8-614de25c17c9" />


<img width="1108" height="86" alt="image" src="https://github.com/user-attachments/assets/c8b506e3-73f8-432e-83e5-30da640fea22" />

- Low Average Sales, Hight Total Sales </>
  Meaning each transaction generates __smaller sales amount__, but the product is sold frequently or in __large volume__
- Both for Cats and Dogs is __popular, everyday, or mass-market item__. Revenue coms not from big order size, but from __scale and consistency.
- It is a __Mass-market/high frequenct products__, the management strategy is efficieny & distribution.

<img width="1110" height="86" alt="image" src="https://github.com/user-attachments/assets/65734f39-d18d-404e-87f1-ed34e092f164" />

- Meaning the repeated purchases will impact the sales mainly depends of the kind of product to sell, luxury or not, for everyday  or for monthly/yearly.

### So for the real business question is, "Does the company want to focus on margin per sale or overall revenue through scale?"

----


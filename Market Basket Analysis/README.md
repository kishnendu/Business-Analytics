# [Python] Market Basket Analysis: Data Pre-processing, Data Exploration and Visualizations and Association Rules Mining

## I. Introduction

### 1. Market Basket Analysis

**What is Market Basket Analysis?**

**Market Basket Analysis** is one of the key techniques used to uncover associations between items. It works by looking for combinations of items that occur together frequently in transactions


**Major types of Market Basket Analysis**

- **Association Rule Mining**: identifies frequent item sets and generating association rules that express the likelihood of one item being purchased with the purchase of another item.
- **Sequence Analysis**: identifies frequent item sequences and generates sequential association rules describing the likelihood of one item sequence being followed by another.
- **Cluster Analysis**: groups similar items or transactions into clusters or segments based on their attributes to identify customer segments with similar purchasing behaviors

**What is the objective of market basket analysis?**

Market basket analysis aims to understand customer behavior and preferences by identifying which products are often purchased together. This information can be used for various purposes, such as product recommendations, store layout optimization, and targeted marketing campaigns.


### 2. Business Questions

Find the significant trends and patterns in customers shopping habits. Answer the primary question: **"Which items are frequently bought together by customers?"** to identify frequently purchased product combinations, then suggest promotions and cross-selling strategies.

### 3. About the Dataset

The dataset belongs to "The Bread Basket" a bakery located in Edinburgh *(publicly available on [Kaggle](https://www.kaggle.com/datasets/ytgangster/online-sales-in-usa))*. This dataset includes 20507 entries and 4 columns, recording over 9000 transactions of customers who ordered different items from this bakery online from 2016-01-11 to 2017-12-03.

Overview of the dataset:

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-1.png)

### 4. About this Project

As this project aims to identify the associations between itemsets, **Association Rule Mining** approach is adopted. 

There are several algorithms used in Market Basket Analysis. This project will use **Apriori Algorithm**, one of the most widely-used and well-known algorithms used in Market Basket Analysis. It helps to find frequent itemsets in transactions and identifies association rules between these items. 

**Apriori Algorithm**

Some important metrics in Apriori Algorithm:

- **Support:** indicates **how frequently** the item set appears in the data set.

    `support{A} = (Number of transactions containing A) / (Total number of transactions)`

- **Confidence:** measures the percentage of times that item B is purchased, given that item A was purchased. It’s an indication of **how often** the rule has been found to be **true.**
 
    `confidence{A->B} = support{A,B} / support{A}`

- **Lift**: indicates how many more times A and B actually appear in the same order, compared to if there was no relationship between them.

    `lift{A,B} = lift{B,A} = support{A,B} / (support{A} * support{B})`

In this project, **the minimum support threshold that an itemset must meet to be considered frequent is identified at 1%** in total number of transactions (1% of 9465, which is approx. 95). 

Just because an item or itemset is common does not mean that there is a strong association between them. For example, the item "coffee" may have a high support value, but that does not mean there is a strong association between coffee and any other particular item. 

Therefore, we should also consider the lift metric when assessing the associations between items, as it takes into account the support of each item to measure the strength of the association between them. 
- `lift{A,B} = 1`: no relationship between A and B (A and B occur together only by chance).
- `lift{A,B} > 1`: positive relationship between A and B ( A and B occur together more often than random).

This project will set the **minimum threshold for lift metric to 1.2** to return the association rules that occur at least 20% more often than we would expect if they were random.

The association rules results will be sorted and ranked in descending order based on confidence values.

**Project Layout**

The project will follow these steps:

1. Install the environment
2. Import and clean the dataset
3. Conduct simple EDA and Visualizations
4. Apply Apriori Algorithm to implement Market Basket Analysis

## II. Data Exploration and Visualizations

### 1. Top 20 best selling items

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-2.png)

### 2. Number of items per transaction

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-3.png)

 Number of items per transaction ranges from 1 to 11 items, in which transactions with two or more items account for nearly 60%. As this project mainly focuses the frequency and quantity sold of each item, all sales trends and patterns will be calculated at item-level (the quantity of items sold), not at transaction-level. 

### 3. Quantity Sold by Month

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-4.png)

### 4. Quantity Sold by Days of Week

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-5.png)

### 5. Quantity Sold by Hours of Day

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-6.png)

## III. Market Basket Analysis

### 1. Associations Rules Results

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-7.png)

### 2. Parallel coordinates plot

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-8.png)

### 3. Itemsets Lift

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-9.png)

### 3. Itemsets Confidence

![image](https://github.com/kishnendu/Business-Analytics/blob/main/Market%20Basket%20Analysis/Images/Img-10.png)

## IV. Insights 

### Data Exploration

- **Best selling items**: Coffee is by far the most popular items sold, accounting for 26.7% of total number of items sold. Bread ranks second at 16,2%. Over 80% of total items (77/94) have low frequency of below 1% of total quantity sold. 
- **Number of items per transaction**: Over 38% of transactions consist of only one item. Most of transactions (approx. 95%) have equal to or less than 5 items. 
- **Sales Trends and Patterns**: 

**By month**: In general, each month typically sold round 500 items per month. However, Nov 2016 to Mar 2017 witness exceptional high numbers of items sold of 2300-2800 items per month, 5 times higher than usual. This may result from the maketing compaigns in association with holiday seasons, when demand for bakery products is highest over the year. Note that data is recorded from 2016-01-11 to 2017-12-03, so that the value of 2016-01 bar contains quantity of 20 days, 2017-12 bar contains quantity for 3 days only (that maybe partly the reason why the number of items sold was low regardless of holidays). 

**By days of week**: It's quite obvious that we sold more items on weekends, especially Saturday, with 20% more than average. Wednesday has lowest sales quantity with 30% less than average.

**By hours of day**: Most items were ordered from 9AM-2PM, with proportion of 78% of total sales quantity. 

### Market Basket Analysis

- There are 15 association rules found with min_support=0.01 and min_lift=1.2.
- Coffee has very high support, it appears in 47.8% of total orders. 
- Among 15 association rules above, coffee appears in 10/15 rules (67.7%). Although bread is the second most sold items (support=32.7%), it is not strongly associated with any other items. 
- When customers order toast (support=3.3%), more than 70% of them will also buy coffee. It's 1.47 times more than random. 
- Similarly, nearly 60% of customers who buy spanish brunch will buy coffee, it happens 1.25 times more than random. 
- Associations rules that have around 20% to be true are found between: {cake -> tea}, {coffee, tea -> cake}, {sandwich -> tea}, {hot chocolate -> cake}.
- There are some itemsets that have pretty strong positive relationships (lift values are close to 2): {coffee, tea -> cake} and {hot chocolate -> cake}.

## V. Recommendations

- Consider suspending the sales of some extremely low-sales items, with only several items sold over the 2 years (e.g polenta, raw bars, olum & polenta, bacon, etc. ) to save storage costs and prevent out-of-date.
- Allocate and reinforce shipping resources during peak hours from 9AM-2PM to ensure that we meet high demand. Offer promotions for orders placed after 6 PM.
- Offer Promotions/Freeship/Discount/Gift for orders taken on weekdays to increase sales, especially on Wednesday: e.g Happy Wednesday - Happy Combo
- We need to consider other factors such as item costs, item profit margins, preservation, transportation, etc. to determine the most effective itemsets/ combo/ recommendations. For example, we can combine more frequent items with less frequent ones to boost overall sales: cake & juice, bread & jam, cookies & smoothies, sandwich & coke, etc.
- Create combo of some items that have pretty high confidence levels and not-too-low support levels (as they are not significant), such as: cake & tea, sandwich & tea, pastry & coffee & toast, etc.
- **Future Analysis**: Investigate why there are exceptional high numbers of transactions from Nov 2016 to Mar 2017, take sales amount, marketing costs and overall performance into consideration. Is it results from (a) marketing compaign(s) or any internal/external factors? How to optimize conditions that may improve overall performance?

# Escotech Data Analysis Project

## Structure of the dataset

1. model_sales table:
   Data columns -
   
   ```
   1. Date - date
   2. City - varchar(50)
   3. Model - varchar(50)
   4. Units Sold - int(11)
   5. Price - int(11)
   ```

2. accessory_sales table:
   Data columns -
   
   ```
   1. Date - date
   2. City - varchar(50)
   3. Model - varchar(50)
   4. Accessory - varchar(50)
   5. Version - varchar(50)
   6. Units Sold - int(11)
   7. Price - int(11)
   ```

## Company description

#### _Company Overview: Escotech Automobile Ltd._

***Introduction:***

Escotech Automobile Ltd. is a leading manufacturer of electric vehicles (e-vehicles) specializing in high-performance e-scooters. Known for innovation and quality, Escotech has established itself as a key player in the sustainable transportation sector.

***Product Line:***
Escotech manufactures four distinct e-scooter models, each designed to cater to different customer needs:

1. **Escotech Mk 1**: Priced at ₹1,25,000, this model is known for its reliability and robust performance.
2. **Escotech Mk 1 plus**: An enhanced version of Mk 1, priced at ₹1,50,000, offering advanced features and improved performance.
3. **Escotech mini**: A compact and affordable model priced at ₹90,000, ideal for city commuting.
4. **Escotech LBR 2**: The premium model priced at ₹2,00,000, featuring cutting-edge technology and superior performance.

***Market Presence:***
Escotech operates sales units in the top 10 major cities in India:

1. Mumbai
2. Delhi
3. Bangalore
4. Hyderabad
5. Ahmedabad
6. Chennai
7. Kolkata
8. Pune
9. Jaipur
10. Surat

***Sales Performance:***
For the first quarter of 2024, Escotech has recorded daily sales data for each model across these cities. This data helps in understanding market trends and guiding production planning.

***Accessories:***
Escotech also offers a range of accessories for its e-scooters:

1. Body Cover: Available in three qualities (Mk1, Mk2, Mk3) with prices starting from ₹300.
2. Original Floor Mat: A universal accessory priced at ₹350.
3. Motor Controller: Available in two versions (CR01 and DR01), priced at ₹7,500 and ₹12,500 respectively, specific to each scooter model.

***Strategic Focus:***
Escotech is committed to sustainability and innovation, continuously improving its product offerings to meet the evolving needs of the market. The company places a strong emphasis on quality and customer satisfaction, ensuring its e-scooters and accessories are of the highest standards.

***Future Outlook:***
With a robust market presence and a diverse product lineup, Escotech Automobile Ltd. is poised for significant growth. The company aims to expand its footprint further and continue leading the transition towards eco-friendly transportation solutions.

## Questions needed to be answered

Based on the available dataset, here are some specific questions that the production head can ask the sales director, which can be directly answered using the data:

1. ***Overall Sales Performance:***
   
   1. What are the total units sold for each e-scooter model (Escotech Mk 1, Mk 1 plus, mini, LBR 2) across all cities in Q1 2024?
   2. What is the total revenue generated for each e-scooter model across all cities in Q1 2024?

2. ***City-wise Performance:***
   
   1. Which city had the highest sales volume for the Escotech Mk 1 in Q1 2024, and how many units were sold?
   2. What are the total units sold and total revenue generated for each e-scooter model in each city for Q1 2024?

3. ***Model-specific Insights:***
   
   1. How do the sales figures for the Escotech Mk 1 compare to the Mk 1 plus in each city?
   2. What are the month-by-month sales figures for each e-scooter model across all cities in Q1 2024?

4. ***Accessories Sales:***
   
   1. What are the total units sold and revenue generated for each accessory (Body Cover Mk1, Mk2, Mk3, Original Floor Mat, Motor Controller CR01, DR01) across all cities in Q1 2024?
   2. Which accessory had the highest sales volume, and which model is it most commonly associated with?

5. ***Monthly Sales Trends:***
   
   1. What are the sales trends for each e-scooter model and accessory over the three months (January, February, March) of Q1 2024?
   2. Are there any noticeable peaks or troughs in sales for specific models or accessories during Q1 2024?

6. ***Comparison of Sales Performance:***
   
   1. How does the sales performance of the Escotech mini compare to the other models in each city?
   2. Which city has the highest overall revenue from accessory sales, and which accessory contributed the most?

7. ***Inventory and Supply Chain Insights***:
   
   1. Are there any models or accessories that consistently had low sales volumes in certain cities?
   2. Based on current sales trends, which models or accessories should we prioritize in production to meet projected demand?

## Answers

#### ***Overall Sales Performance:***

**What are the total units sold for each e-scooter model (Escotech Mk 1, Mk 1 plus, mini, LBR 2) across all cities in Q1 2024?**

*Code*

```sql
# Overall Sales Performance - Number of scooters sold in all cities
select distinct Model as Model_Name, count(`Units Sold`) as Total_Sales from model_sales ms
group by Model
order by Total_Sales desc;
```

*Output*

| Model_Name         | Total_Sales |
|:------------------:|:-----------:|
| Escotech mini      | 803         |
| Escotech Mk 1 plus | 796         |
| Escotech Mk 1      | 778         |
| Escotech LBR 2     | 764         |

*Plot*

<img src="assets/2024-08-14-17-17-07-Final%20Report-14.png" title="" alt="loading-ag-12374" data-align="center">

**What is the total revenue generated for each e-scooter model across all cities in Q1 2024?**

*Code*

```sql
# Overall Sales Performance - Revenue of scooters sold in all cities
select distinct Model as Model_Name, sum(`Units Sold` * Price) as Total_Revenue from model_sales ms
group by Model
order by Total_Revenue desc;
```

*Output*

| Model_Name         | Total_Revenue |
|:------------------:|:-------------:|
| Escotech LBR 2     | 343200000     |
| Escotech Mk 1 plus | 271650000     |
| Escotech Mk 1      | 229000000     |
| Escotech mini      | 166050000     |

*Plot*

<img title="Total Revenue" src="assets/2024-08-14-17-17-56-Final%20Report-0.png" alt="loading-ag-12375" data-align="center">

#### ***City-wise Performance:***

**Which city had the highest sales volume for the Escotech Mk 1 in Q1 2024, and how many units were sold?**

*Code*

```sql
# City-wise Performance - Highest sales volume of Escotech Mk 1 - city
select distinct City, count(`Units Sold`) as Total_Sales from model_sales ms
where Model = 'Escotech Mk 1'
group by City
order by Total_Sales desc
limit 1
```

*Output*

| City   | Total_Sales |
|:------:|:-----------:|
| Mumbai | 81          |

**What are the total units sold and total revenue generated for each e-scooter model in each city for Q1 2024?**

*Code*

```sql
# City-wise Performance - Total revenue sheet
select distinct City, Model, sum(`Units Sold`) as Total_Sales, sum(`Units Sold` * Price) as Total_Revenue from model_sales ms 
group by City, Model
order by City
```

*Output*

| City      | Model              | Total_Sales | Total_Revenue |
|:---------:|:------------------:|:-----------:|:-------------:|
| Ahmedabad | Escotech LBR 2     | 157         | 31400000      |
| Ahmedabad | Escotech mini      | 181         | 16290000      |
| Ahmedabad | Escotech Mk 1      | 202         | 25250000      |
| Ahmedabad | Escotech Mk 1 plus | 197         | 29550000      |
| Bangalore | Escotech LBR 2     | 165         | 33000000      |
| Bangalore | Escotech mini      | 203         | 18270000      |
| Bangalore | Escotech Mk 1      | 185         | 23125000      |
| Bangalore | Escotech Mk 1 plus | 184         | 27600000      |
| Chennai   | Escotech LBR 2     | 177         | 35400000      |
| Chennai   | Escotech mini      | 174         | 15660000      |
| Chennai   | Escotech Mk 1      | 186         | 23250000      |
| Chennai   | Escotech Mk 1 plus | 185         | 27750000      |
| Delhi     | Escotech LBR 2     | 171         | 34200000      |
| Delhi     | Escotech mini      | 184         | 16560000      |
| Delhi     | Escotech Mk 1      | 173         | 21625000      |
| Delhi     | Escotech Mk 1 plus | 163         | 24450000      |
| Hyderabad | Escotech LBR 2     | 162         | 32400000      |
| Hyderabad | Escotech mini      | 179         | 16110000      |
| Hyderabad | Escotech Mk 1      | 195         | 24375000      |
| Hyderabad | Escotech Mk 1 plus | 166         | 24900000      |
| Jaipur    | Escotech LBR 2     | 182         | 36400000      |
| Jaipur    | Escotech mini      | 177         | 15930000      |
| Jaipur    | Escotech Mk 1      | 169         | 21125000      |
| Jaipur    | Escotech Mk 1 plus | 179         | 26850000      |
| Kolkata   | Escotech LBR 2     | 173         | 34600000      |
| Kolkata   | Escotech mini      | 195         | 17550000      |
| Kolkata   | Escotech Mk 1      | 166         | 20750000      |
| Kolkata   | Escotech Mk 1 plus | 196         | 29400000      |
| Mumbai    | Escotech LBR 2     | 177         | 35400000      |
| Mumbai    | Escotech mini      | 198         | 17820000      |
| Mumbai    | Escotech Mk 1      | 167         | 20875000      |
| Mumbai    | Escotech Mk 1 plus | 185         | 27750000      |
| Pune      | Escotech LBR 2     | 185         | 37000000      |
| Pune      | Escotech mini      | 175         | 15750000      |
| Pune      | Escotech Mk 1      | 199         | 24875000      |
| Pune      | Escotech Mk 1 plus | 199         | 29850000      |
| Surat     | Escotech LBR 2     | 167         | 33400000      |
| Surat     | Escotech mini      | 179         | 16110000      |
| Surat     | Escotech Mk 1      | 190         | 23750000      |
| Surat     | Escotech Mk 1 plus | 157         | 23550000      |

 *Plots*

<img title="" src="assets/2024-08-14-17-22-13-Final Report-1.png" alt="" data-align="center">

Ahmedabad

<img title="" src="assets/2024-08-14-17-22-31-Final Report-2.png" alt="" data-align="center">

Bangalore

<img src="assets/2024-08-14-17-45-03-2024-08-14-17-23-10-Final%20Report-3.png" title="" alt="" data-align="center">

Chennai

<img src="assets/2024-08-14-17-23-46-Final%20Report-4.png" title="" alt="" data-align="center">

Delhi

<img title="" src="assets/2024-08-14-17-24-29-Final Report-5.png" alt="" data-align="center">

Hyderabad

<img title="" src="assets/2024-08-14-17-24-45-Final Report-6.png" alt="" data-align="center">

Jaipur

<img title="" src="assets/2024-08-14-17-25-09-Final Report-7.png" alt="" data-align="center">

Kolkata

<img title="" src="assets/2024-08-14-17-25-20-Final Report-8.png" alt="" data-align="center">

Mumbai

<img title="" src="assets/2024-08-14-17-26-11-Final Report-9.png" alt="" data-align="center">

Pune

<img title="" src="assets/2024-08-14-17-26-23-Final Report-10.png" alt="" data-align="center">

Surat

#### ***Model-specific Insights:***

**How do the sales figures for the Escotech Mk 1 compare to the Mk 1 plus in each city?**

*Code*

```sql
# Model-specific Insights - Escotech Mk 1 vs Escotech Mk 1 plus in each city
select t1.City, t1.Mk1_Total_Sales, t2.Mk1_plus_Total_Sales from
(select distinct City, sum(`Units Sold`) as Mk1_Total_Sales from model_sales ms
where Model = 'Escotech Mk 1'
group by City) t1
join 
(select distinct City, sum(`Units Sold`) as Mk1_plus_Total_Sales from model_sales ms
where Model = 'Escotech Mk 1 plus' 
group by City) t2
on t1.City = t2.City
```

*Output*

| City      | Mk1_Total_Sales | Mk1_plus_Total_Sales |
|:---------:|:---------------:|:--------------------:|
| Ahmedabad | 202             | 197                  |
| Bangalore | 185             | 184                  |
| Chennai   | 186             | 185                  |
| Delhi     | 173             | 163                  |
| Hyderabad | 195             | 166                  |
| Jaipur    | 169             | 179                  |
| Kolkata   | 166             | 196                  |
| Mumbai    | 167             | 185                  |
| Pune      | 199             | 199                  |
| Surat     | 190             | 157                  |

*Plot*

<img title="" src="assets/2024-08-14-17-26-42-Final Report-11.png" alt="" data-align="center">

**What are the month-by-month sales figures for each e-scooter model across all cities in Q1 2024?**

*Code*

```sql
# Model-specific Insights - Month by month
select c1.Model, c1.Month_1_Sales, c2.Month_2_Sales, c3.Month_3_Sales from
(select distinct Model, sum(`Units Sold`) as Month_1_Sales from model_sales ms
where month(`Date`) = 1
group by Model) c1
join
(select distinct Model, sum(`Units Sold`) as Month_2_Sales from model_sales ms
where month(`Date`) = 2
group by Model) c2
on c1.Model = c2.Model
join
(select distinct Model, sum(`Units Sold`) as Month_3_Sales from model_sales ms
where month(`Date`) = 3
group by Model) c3
on c2.Model = c3.Model
```

*Output*

| Model              | Month_1_Sales | Month_2_Sales | Month_3_Sales |
|:------------------:|:-------------:|:-------------:|:-------------:|
| Escotech LBR 2     | 589           | 578           | 549           |
| Escotech mini      | 623           | 571           | 651           |
| Escotech Mk 1      | 658           | 570           | 604           |
| Escotech Mk 1 plus | 608           | 569           | 634           |

*Plot*

<img title="" src="assets/2024-08-14-17-26-55-Final Report-12.png" alt="" data-align="center">

#### ***Accessories Sales:***

**What are the total units sold and revenue generated for each accessory (Body Cover Mk1, Mk2, Mk3, Original Floor Mat, Motor Controller CR01, DR01) across all cities in Q1 2024?**

*Code*

```sql
# Accessory Sales - All accessories total revenue
select Accessory, Version, sum(`Units Sold`) as Total_Sales, sum(`Units Sold` * Price) as Total_Revenue from accessory_sales as2 
group by Accessory, Version
order by Total_Revenue desc
```

*Output*

| Accessory          | Version | Total_Sales | Total_Revenue |
|:------------------:|:-------:|:-----------:|:-------------:|
| Motor Controller   | DR01    | 1852        | 23150000      |
| Motor Controller   | CR01    | 1841        | 13807500      |
| Body Cover         | Mk3     | 7278        | 2911200       |
| Body Cover         | Mk2     | 7305        | 2556750       |
| Original Floor Mat |         | 7138        | 2498300       |
| Body Cover         | Mk1     | 7290        | 2187000       |

*Plot*

<img title="" src="assets/2024-08-14-17-27-07-Final Report-13.png" alt="" data-align="center">

**Which accessory had the highest sales volume, and which model is it most commonly associated with?**

*Code*

```sql
# Accessory Sales - Top sold accessory and associated model
select Accessory, Model, count(`Units Sold`) as Total_Sales from accessory_sales as2 
group by Accessory, Model 
order by Total_Sales desc 
limit 1
```

*Output*

| Accessory  | Model         | Total_Sales |
|:----------:|:-------------:|:-----------:|
| Body Cover | Escotech Mk 1 | 2376        |

#### ***Monthly Sales Trends:***

**What are the sales trends for each e-scooter model and accessory over the three months (January, February, March) of Q1 2024?**

*Code*

```sql
# MOM Model Sales - Query 1
with MOM_Model_Sales1 as
(
    select 
        Model, 
        month(`Date`) as `Month`, 
        sum(`Units Sold` * price) as Total_Revenue 
    from model_sales ms
    where Model = 'Escotech LBR 2'
    group by Model, month(`Date`)
),
MOM_Model_Sales2 as
(
    select 
        Model, 
        month(`Date`) as `Month`, 
        SUM(`Units Sold` * price) as Total_Revenue 
    from model_sales ms
    where Model = 'Escotech mini'
    group by Model, month(`Date`)
),
MOM_Model_Sales3 as
(
    select 
        Model, 
        month(`Date`) as `Month`, 
        SUM(`Units Sold` * price) as Total_Revenue 
    from model_sales ms
    where Model = 'Escotech Mk 1'
    group by Model, month(`Date`)
),
MOM_Model_Sales4 as
(
    select 
        Model, 
        month(`Date`) as `Month`, 
        SUM(`Units Sold` * price) as Total_Revenue 
    from model_sales ms
    where Model = 'Escotech Mk 1 plus'
    group by Model, month(`Date`)
)
select *,
    LAG(Total_Revenue, 1) over (order by `Month`) as Previous_Month,
    (Total_Revenue - (LAG(Total_Revenue, 1) over (order by `Month`)))/Total_Revenue * 100 as Percentage_Change
from MOM_Model_Sales1
union
select *,
    LAG(Total_Revenue, 1) over (order by `Month`) as Previous_Month,
    (Total_Revenue - (LAG(Total_Revenue, 1) over (order by `Month`)))/Total_Revenue * 100 as Percentage_Change
from MOM_Model_Sales2
union
select *,
    LAG(Total_Revenue, 1) over (order by `Month`) as Previous_Month,
    (Total_Revenue - (LAG(Total_Revenue, 1) over (order by `Month`)))/Total_Revenue * 100 as Percentage_Change
from MOM_Model_Sales3
union
select *,
    LAG(Total_Revenue, 1) over (order by `Month`) as Previous_Month,
    (Total_Revenue - (LAG(Total_Revenue, 1) over (order by `Month`)))/Total_Revenue * 100 as Percentage_Change
from MOM_Model_Sales4
order by Model,`Month`


# MOM Accessory Sales - Query 2
WITH MOM_Acc_Sales1 as
(
    select 
        Accessory, `Version`, 
        month(`Date`) as `Month`, 
        SUM(`Units Sold` * price) as Total_Revenue 
    from accessory_sales a
    where Accessory = 'Body Cover'
    group by Accessory,`Version`, month(`Date`)
),MOM_Acc_Sales2 as
(
    select 
        Accessory, `Version`, 
        month(`Date`) as `Month`, 
        SUM(`Units Sold` * price) as Total_Revenue 
    from accessory_sales a
    where Accessory = 'Original Floor Mat'
    group by Accessory,`Version`, month(`Date`)
),
MOM_Acc_Sales3 as
(
    select 
        Accessory, `Version`, 
        month(`Date`) as `Month`, 
        SUM(`Units Sold` * price) as Total_Revenue 
    from accessory_sales a
    where Accessory = 'Motor Controller'
    group by Accessory,`Version`, month(`Date`)
)
select *,
    LAG(Total_Revenue, 1) over (partition by `Version` order by `Month`) as Previous_Month,
    (Total_Revenue - (LAG(Total_Revenue, 1) over (partition by `Version` order by `Month`)))/Total_Revenue * 100 as Percentage_Change
from MOM_Acc_Sales1
union
select *,
    LAG(Total_Revenue, 1) over (partition by `Version` order by `Month`) as Previous_Month,
    (Total_Revenue - (LAG(Total_Revenue, 1) over (partition by `Version` order by `Month`)))/Total_Revenue * 100 as Percentage_Change
from MOM_Acc_Sales2
union
select *,
    LAG(Total_Revenue, 1) over (partition by `Version` order by `Month`) as Previous_Month,
    (Total_Revenue - (LAG(Total_Revenue, 1) over (partition by `Version` order by `Month`)))/Total_Revenue * 100 as Percentage_Change
from MOM_Acc_Sales3
order by Accessory,`Version`,`Month`
```

*Output*

Model Table - Query 1

| Model                           | Month | Total_Revenue | Previous_Month | Percentage_Change     |
|:-------------------------------:|:-----:|:-------------:|:--------------:|:---------------------:|
| Escotech LBR 2                  | 1     | 117800000     |                |                       |
| Escotech LBR 2                  | 2     | 115600000     | 117800000      | -1.9031               |
| Escotech LBR 2                  | 3     | 109800000     | 115600000      | -5.2823               |
| Escotech mini                   | 1     | 56070000      |                |                       |
| <mark>Escotech mini</mark>      | 2     | 51390000      | 56070000       | <mark>-9.1068</mark>  |
| <mark>Escotech mini</mark>      | 3     | 58590000      | 51390000       | <mark>12.2888</mark>  |
| Escotech Mk 1                   | 1     | 82250000      |                |                       |
| <mark>Escotech Mk 1</mark>      | 2     | 71250000      | 82250000       | <mark>-15.4386</mark> |
| Escotech Mk 1                   | 3     | 75500000      | 71250000       | 5.6291                |
| Escotech Mk 1 plus              | 1     | 91200000      |                |                       |
| Escotech Mk 1 plus              | 2     | 85350000      | 91200000       | -6.8541               |
| <mark>Escotech Mk 1 plus</mark> | 3     | 95100000      | 85350000       | <mark>10.2524</mark>  |

Accessory Table - Query 2

| Accessory                     | Version           | Month | Total_Revenue | Previous_Month | Percentage_Change     |
| ----------------------------- | ----------------- | ----- | ------------- | -------------- | --------------------- |
| Body Cover                    | Mk1               | 1     | 733500        |                |                       |
| Body Cover                    | Mk1               | 2     | 721800        | 733500         | -1.6209               |
| Body Cover                    | Mk1               | 3     | 731700        | 721800         | 1.3530                |
| Body Cover                    | Mk2               | 1     | 863100        |                |                       |
| Body Cover                    | Mk2               | 2     | 791350        | 863100         | -9.0668               |
| <mark>Body Cover</mark>       | <mark>Mk2</mark>  | 3     | 902300        | 791350         | <mark>12.2964</mark>  |
| Body Cover                    | Mk3               | 1     | 984000        |                |                       |
| Body Cover                    | Mk3               | 2     | 932000        | 984000         | -5.5794               |
| Body Cover                    | Mk3               | 3     | 995200        | 932000         | 6.3505                |
| Motor Controller              | CR01              | 1     | 4920000       |                |                       |
| <mark>Motor Controller</mark> | <mark>CR01</mark> | 2     | 4320000       | 4920000        | <mark>-13.8889</mark> |
| Motor Controller              | CR01              | 3     | 4567500       | 4320000        | 5.4187                |
| Motor Controller              | DR01              | 1     | 8125000       |                |                       |
| <mark>Motor Controller</mark> | <mark>DR01</mark> | 2     | 7700000       | 8125000        | <mark>-5.5195</mark>  |
| <mark>Motor Controller</mark> | <mark>DR01</mark> | 3     | 7325000       | 7700000        | <mark>-5.1195</mark>  |
| Original Floor Mat            |                   | 1     | 864850        |                |                       |
| Original Floor Mat            |                   | 2     | 792400        | 864850         | -9.1431               |
| Original Floor Mat            |                   | 3     | 841050        | 792400         | 5.7844                |

**Are there any noticeable peaks or troughs in sales for specific models or accessories during Q1 2024?**

According to the tables in previous outputs, we can see the highlighted figures of peaks or troughs -

1. Escotech mini had a sharp decline in sales figures in second month immediately followed by a growth in last month of the quarter.

2. Escotech Mk 1 had a sheer drop in sales in the second month.

3. Escotech Mk 1 plus performed better in the market in the last month.

4. Body Cover Mk 2 version had a good market performance comparing to all other accessories.

5. Motor Controller CR01 had bad figures in the second month, but gradually improved.

6. On the other hand controller version DR01 had decline all over the quarter. One reason may be its high cost.

#### ***Comparison of Sales Performance:***

**How does the sales performance of the Escotech mini compare to the other models in each city?**

*Code*

```sql
# Sales Performance Comparison - Model Escotech mini
select t1.City,
(t1.`Escotech LBR 2`-t2.`Escotech mini`)/t2.`Escotech mini` * 100 as 'w.r.t_Escotech_LBR_2',
(t3.`Escotech Mk 1`-t2.`Escotech mini`)/t2.`Escotech mini` * 100 as 'w.r.t_Escotech_Mk_1',
(t4.`Escotech Mk 1 plus`-t2.`Escotech mini`)/t2.`Escotech mini` * 100 as 'w.r.t_Escotech_Mk_1_plus'
from
(select
    distinct City, 
    sum(`Units Sold`) as 'Escotech LBR 2'
from model_sales ms
where Model = 'Escotech LBR 2'
group by City) t1
join
(select
    distinct City, 
    sum(`Units Sold`) as 'Escotech mini'
from model_sales ms
where Model = 'Escotech mini'
group by City) t2
on t1.City = t2.City
join
(select
    distinct City, 
    sum(`Units Sold`) as 'Escotech Mk 1'
from model_sales ms
where Model = 'Escotech Mk 1'
group by City) t3
on t2.City = t3.City
join
(select
    distinct City, 
    sum(`Units Sold`) as 'Escotech Mk 1 plus'
from model_sales ms
where Model = 'Escotech Mk 1 plus'
group by City) t4
on t3.City = t4.City
```

*Output*

The table shows where Escotech mini sales are relative to other models. That means, in Ahmedabad, Escotech mini had 13.2597% less sales than LBR 2.

| City      | w.r.t_Escotech_LBR_2 | w.r.t_Escotech_Mk_1 | w.r.t_Escotech_Mk_1_plus |
|:---------:|:--------------------:|:-------------------:|:------------------------:|
| Ahmedabad | -13.2597             | 11.6022             | 8.8398                   |
| Bangalore | -18.7192             | -8.8670             | -9.3596                  |
| Chennai   | 1.7241               | 6.8966              | 6.3218                   |
| Delhi     | -7.0652              | -5.9783             | -11.4130                 |
| Hyderabad | -9.4972              | 8.9385              | -7.2626                  |
| Jaipur    | 2.8249               | -4.5198             | 1.1299                   |
| Kolkata   | -11.2821             | -14.8718            | 0.5128                   |
| Mumbai    | -10.6061             | -15.6566            | -6.5657                  |
| Pune      | 5.7143               | 13.7143             | 13.7143                  |
| Surat     | -6.7039              | 6.1453              | -12.2905                 |

**Which city has the highest overall revenue from accessory sales, and which accessory contributed the most?**

*Code*

```sql
# Revenue Perfromance of Accessories
select t1.City, t1.Body_Cover, t2.Original_Floor_Mat, t3.Motor_Controller, (t1.Body_Cover + t2.Original_Floor_Mat + t3.Motor_Controller) as Total from
(select
    distinct City,
    sum((`Units Sold` * Price)) as Body_Cover
from accessory_sales
where Accessory = 'Body Cover'
group by City) t1
join
(select
    distinct City,
    sum((`Units Sold` * Price)) as Original_Floor_Mat
from accessory_sales
where Accessory = 'Original Floor Mat'
group by City) t2
on t1.City = t2.City
join
(select
    distinct City,
    sum((`Units Sold` * Price)) as Motor_Controller
from accessory_sales
where Accessory = 'Motor Controller'
group by City) t3
on t2.City = t3.City
```

*Output*

City with highest overall revenue and the contributing accessory is highlighted.

| City                   | Body_Cover | Original_Floor_Mat | <mark>Motor_Controller</mark> | Total   |
|:----------------------:|:----------:|:------------------:|:-----------------------------:|:-------:|
| <mark>Ahmedabad</mark> | 773550     | 245350             | <mark>4072500</mark>          | 5091400 |
| Bangalore              | 751300     | 262150             | 3442500                       | 4455950 |
| Chennai                | 766600     | 240450             | 3757500                       | 4764550 |
| Delhi                  | 750500     | 243950             | 3500000                       | 4494450 |
| Hyderabad              | 766700     | 238000             | 3497500                       | 4502200 |
| Jaipur                 | 770600     | 256550             | 3610000                       | 4637150 |
| Kolkata                | 771200     | 242550             | 3845000                       | 4858750 |
| Mumbai                 | 770150     | 252350             | 3632500                       | 4655000 |
| Pune                   | 761050     | 262150             | 3742500                       | 4765700 |
| Surat                  | 773300     | 254800             | 3857500                       | 4885600 |

#### ***Inventory and Supply Chain Insights***:

**Are there any models or accessories that consistently had low sales volumes in certain cities?**

*Code*

```sql
# Inventory Analysis - Models
WITH MOM_Model_Sales as
(
    select 
        City,
        Model, 
        month(`Date`) as `Month`, 
        SUM(`Units Sold`) as Total_Sales
    from model_sales ms
    group by City, Model, `Month`
)
select *,
    LAG(Total_Sales,1) over (partition by City, Model order by `Month`) as Previous_Month,
    (Total_Sales - (LAG(Total_Sales,1) over (partition by City, Model order by `Month`)))/Total_Sales * 100 as Percentage_Change
from MOM_Model_Sales
order by City, Model, `Month`


# Inventory Analysis - Accessories
WITH MOM_Accessory_Sales as
(
    select 
        City,
        Accessory,
        `Version`,
        month(`Date`) as `Month`, 
        SUM(`Units Sold`) as Total_Sales
    from accessory_sales ms
    group by City, Accessory, `Version`, `Month`
)
select *,
    LAG(Total_Sales,1) over (partition by City, Accessory,`Version` order by `Month`) as Previous_Month,
    (Total_Sales - (LAG(Total_Sales,1) over (partition by City, Accessory,`Version` order by `Accessory`, `Month`)))/Total_Sales * 100 as Percentage_Change
from MOM_Accessory_Sales
order by City, Accessory, `Version`, `Month`
```

*Output*

Model Table - Consistent falling trend is highlighted.

| City                   | Model                       | Month | Total_Sales | Previous_Month | Percentage_Change     |
|:----------------------:|:---------------------------:|:-----:|:-----------:|:--------------:|:---------------------:|
| Ahmedabad              | Escotech LBR 2              | 1     | 52          |                |                       |
| Ahmedabad              | Escotech LBR 2              | 2     | 47          | 52             | -10.6383              |
| Ahmedabad              | Escotech LBR 2              | 3     | 58          | 47             | 18.9655               |
| Ahmedabad              | Escotech mini               | 1     | 57          |                |                       |
| Ahmedabad              | Escotech mini               | 2     | 52          | 57             | -9.6154               |
| Ahmedabad              | Escotech mini               | 3     | 72          | 52             | 27.7778               |
| Ahmedabad              | Escotech Mk 1               | 1     | 66          |                |                       |
| Ahmedabad              | Escotech Mk 1               | 2     | 65          | 66             | -1.5385               |
| Ahmedabad              | Escotech Mk 1               | 3     | 71          | 65             | 8.4507                |
| Ahmedabad              | Escotech Mk 1 plus          | 1     | 60          |                |                       |
| Ahmedabad              | Escotech Mk 1 plus          | 2     | 61          | 60             | 1.6393                |
| Ahmedabad              | Escotech Mk 1 plus          | 3     | 76          | 61             | 19.7368               |
| Bangalore              | Escotech LBR 2              | 1     | 47          |                |                       |
| Bangalore              | Escotech LBR 2              | 2     | 72          | 47             | 34.7222               |
| Bangalore              | Escotech LBR 2              | 3     | 46          | 72             | -56.5217              |
| Bangalore              | Escotech mini               | 1     | 55          |                |                       |
| Bangalore              | Escotech mini               | 2     | 68          | 55             | 19.1176               |
| Bangalore              | Escotech mini               | 3     | 80          | 68             | 15.0000               |
| Bangalore              | Escotech Mk 1               | 1     | 68          |                |                       |
| Bangalore              | Escotech Mk 1               | 2     | 57          | 68             | -19.2982              |
| Bangalore              | Escotech Mk 1               | 3     | 60          | 57             | 5.0000                |
| Bangalore              | Escotech Mk 1 plus          | 1     | 62          |                |                       |
| Bangalore              | Escotech Mk 1 plus          | 2     | 64          | 62             | 3.1250                |
| Bangalore              | Escotech Mk 1 plus          | 3     | 58          | 64             | -10.3448              |
| Chennai                | Escotech LBR 2              | 1     | 57          |                |                       |
| Chennai                | Escotech LBR 2              | 2     | 61          | 57             | 6.5574                |
| Chennai                | Escotech LBR 2              | 3     | 59          | 61             | -3.3898               |
| Chennai                | Escotech mini               | 1     | 47          |                |                       |
| Chennai                | Escotech mini               | 2     | 64          | 47             | 26.5625               |
| Chennai                | Escotech mini               | 3     | 63          | 64             | -1.5873               |
| Chennai                | Escotech Mk 1               | 1     | 63          |                |                       |
| Chennai                | Escotech Mk 1               | 2     | 59          | 63             | -6.7797               |
| Chennai                | Escotech Mk 1               | 3     | 64          | 59             | 7.8125                |
| Chennai                | Escotech Mk 1 plus          | 1     | 69          |                |                       |
| Chennai                | Escotech Mk 1 plus          | 2     | 50          | 69             | -38.0000              |
| Chennai                | Escotech Mk 1 plus          | 3     | 66          | 50             | 24.2424               |
| Delhi                  | Escotech LBR 2              | 1     | 54          |                |                       |
| Delhi                  | Escotech LBR 2              | 2     | 63          | 54             | 14.2857               |
| Delhi                  | Escotech LBR 2              | 3     | 54          | 63             | -16.6667              |
| Delhi                  | Escotech mini               | 1     | 68          |                |                       |
| Delhi                  | Escotech mini               | 2     | 54          | 68             | -25.9259              |
| Delhi                  | Escotech mini               | 3     | 62          | 54             | 12.9032               |
| Delhi                  | Escotech Mk 1               | 1     | 71          |                |                       |
| <mark>Delhi</mark>     | <mark>Escotech Mk 1</mark>  | 2     | 52          | 71             | <mark>-36.5385</mark> |
| <mark>Delhi</mark>     | <mark>Escotech Mk 1</mark>  | 3     | 50          | 52             | <mark>-4.0000</mark>  |
| Delhi                  | Escotech Mk 1 plus          | 1     | 50          |                |                       |
| Delhi                  | Escotech Mk 1 plus          | 2     | 54          | 50             | 7.4074                |
| Delhi                  | Escotech Mk 1 plus          | 3     | 59          | 54             | 8.4746                |
| Hyderabad              | Escotech LBR 2              | 1     | 49          |                |                       |
| Hyderabad              | Escotech LBR 2              | 2     | 54          | 49             | 9.2593                |
| Hyderabad              | Escotech LBR 2              | 3     | 59          | 54             | 8.4746                |
| Hyderabad              | Escotech mini               | 1     | 71          |                |                       |
| <mark>Hyderabad</mark> | <mark>Escotech mini</mark>  | 2     | 58          | 71             | <mark>-22.4138</mark> |
| <mark>Hyderabad</mark> | <mark>Escotech mini</mark>  | 3     | 50          | 58             | <mark>-16.0000</mark> |
| Hyderabad              | Escotech Mk 1               | 1     | 72          |                |                       |
| Hyderabad              | Escotech Mk 1               | 2     | 56          | 72             | -28.5714              |
| Hyderabad              | Escotech Mk 1               | 3     | 67          | 56             | 16.4179               |
| Hyderabad              | Escotech Mk 1 plus          | 1     | 59          |                |                       |
| Hyderabad              | Escotech Mk 1 plus          | 2     | 46          | 59             | -28.2609              |
| Hyderabad              | Escotech Mk 1 plus          | 3     | 61          | 46             | 24.5902               |
| Jaipur                 | Escotech LBR 2              | 1     | 69          |                |                       |
| Jaipur                 | Escotech LBR 2              | 2     | 56          | 69             | -23.2143              |
| Jaipur                 | Escotech LBR 2              | 3     | 57          | 56             | 1.7544                |
| Jaipur                 | Escotech mini               | 1     | 72          |                |                       |
| Jaipur                 | Escotech mini               | 2     | 46          | 72             | -56.5217              |
| Jaipur                 | Escotech mini               | 3     | 59          | 46             | 22.0339               |
| Jaipur                 | Escotech Mk 1               | 1     | 59          |                |                       |
| Jaipur                 | Escotech Mk 1               | 2     | 54          | 59             | -9.2593               |
| Jaipur                 | Escotech Mk 1               | 3     | 56          | 54             | 3.5714                |
| Jaipur                 | Escotech Mk 1 plus          | 1     | 54          |                |                       |
| Jaipur                 | Escotech Mk 1 plus          | 2     | 65          | 54             | 16.9231               |
| Jaipur                 | Escotech Mk 1 plus          | 3     | 60          | 65             | -8.3333               |
| Kolkata                | Escotech LBR 2              | 1     | 72          |                |                       |
| Kolkata                | Escotech LBR 2              | 2     | 46          | 72             | -56.5217              |
| Kolkata                | Escotech LBR 2              | 3     | 55          | 46             | 16.3636               |
| Kolkata                | Escotech mini               | 1     | 68          |                |                       |
| Kolkata                | Escotech mini               | 2     | 62          | 68             | -9.6774               |
| Kolkata                | Escotech mini               | 3     | 65          | 62             | 4.6154                |
| Kolkata                | Escotech Mk 1               | 1     | 60          |                |                       |
| <mark>Kolkata</mark>   | <mark>Escotech Mk 1</mark>  | 2     | 54          | 60             | <mark>-11.1111</mark> |
| <mark>Kolkata</mark>   | <mark>Escotech Mk 1</mark>  | 3     | 52          | 54             | <mark>-3.8462</mark>  |
| Kolkata                | Escotech Mk 1 plus          | 1     | 66          |                |                       |
| Kolkata                | Escotech Mk 1 plus          | 2     | 58          | 66             | -13.7931              |
| Kolkata                | Escotech Mk 1 plus          | 3     | 72          | 58             | 19.4444               |
| Mumbai                 | Escotech LBR 2              | 1     | 67          |                |                       |
| <mark>Mumbai</mark>    | <mark>Escotech LBR 2</mark> | 2     | 61          | 67             | <mark>-9.8361</mark>  |
| <mark>Mumbai</mark>    | <mark>Escotech LBR 2</mark> | 3     | 49          | 61             | <mark>-24.4898</mark> |
| Mumbai                 | Escotech mini               | 1     | 67          |                |                       |
| Mumbai                 | Escotech mini               | 2     | 65          | 67             | -3.0769               |
| Mumbai                 | Escotech mini               | 3     | 66          | 65             | 1.5152                |
| Mumbai                 | Escotech Mk 1               | 1     | 72          |                |                       |
| Mumbai                 | Escotech Mk 1               | 2     | 44          | 72             | -63.6364              |
| Mumbai                 | Escotech Mk 1               | 3     | 51          | 44             | 13.7255               |
| Mumbai                 | Escotech Mk 1 plus          | 1     | 57          |                |                       |
| Mumbai                 | Escotech Mk 1 plus          | 2     | 62          | 57             | 8.0645                |
| Mumbai                 | Escotech Mk 1 plus          | 3     | 66          | 62             | 6.0606                |
| Pune                   | Escotech LBR 2              | 1     | 64          |                |                       |
| Pune                   | Escotech LBR 2              | 2     | 64          | 64             | 0.0000                |
| Pune                   | Escotech LBR 2              | 3     | 57          | 64             | -12.2807              |
| Pune                   | Escotech mini               | 1     | 64          |                |                       |
| Pune                   | Escotech mini               | 2     | 48          | 64             | -33.3333              |
| Pune                   | Escotech mini               | 3     | 63          | 48             | 23.8095               |
| Pune                   | Escotech Mk 1               | 1     | 70          |                |                       |
| <mark>Pune</mark>      | <mark>Escotech Mk 1</mark>  | 2     | 67          | 70             | <mark>-4.4776</mark>  |
| <mark>Pune</mark>      | <mark>Escotech Mk 1</mark>  | 3     | 62          | 67             | <mark>-8.0645</mark>  |
| Pune                   | Escotech Mk 1 plus          | 1     | 66          |                |                       |
| Pune                   | Escotech Mk 1 plus          | 2     | 63          | 66             | -4.7619               |
| Pune                   | Escotech Mk 1 plus          | 3     | 70          | 63             | 10.0000               |
| Surat                  | Escotech LBR 2              | 1     | 58          |                |                       |
| Surat                  | Escotech LBR 2              | 2     | 54          | 58             | -7.4074               |
| Surat                  | Escotech LBR 2              | 3     | 55          | 54             | 1.8182                |
| Surat                  | Escotech mini               | 1     | 54          |                |                       |
| Surat                  | Escotech mini               | 2     | 54          | 54             | 0.0000                |
| Surat                  | Escotech mini               | 3     | 71          | 54             | 23.9437               |
| Surat                  | Escotech Mk 1               | 1     | 57          |                |                       |
| Surat                  | Escotech Mk 1               | 2     | 62          | 57             | 8.0645                |
| Surat                  | Escotech Mk 1               | 3     | 71          | 62             | 12.6761               |
| Surat                  | Escotech Mk 1 plus          | 1     | 65          |                |                       |
| Surat                  | Escotech Mk 1 plus          | 2     | 46          | 65             | -41.3043              |
| Surat                  | Escotech Mk 1 plus          | 3     | 46          | 46             | 0.0000                |

Accessory Table - Consistent falling trend is highlighted.

| City                   | Accessory                       | Version           | Month | Total_Sales | Previous_Month | Percentage_Change     |
|:----------------------:|:-------------------------------:|:-----------------:|:-----:|:-----------:|:--------------:|:---------------------:|
| Ahmedabad              | Body Cover                      | Mk1               | 1     | 260         |                |                       |
| Ahmedabad              | Body Cover                      | Mk1               | 2     | 240         | 260            | -8.3333               |
| Ahmedabad              | Body Cover                      | Mk1               | 3     | 239         | 240            | -0.4184               |
| Ahmedabad              | Body Cover                      | Mk2               | 1     | 237         |                |                       |
| Ahmedabad              | Body Cover                      | Mk2               | 2     | 225         | 237            | -5.3333               |
| Ahmedabad              | Body Cover                      | Mk2               | 3     | 285         | 225            | 21.0526               |
| Ahmedabad              | Body Cover                      | Mk3               | 1     | 244         |                |                       |
| Ahmedabad              | Body Cover                      | Mk3               | 2     | 240         | 244            | -1.6667               |
| Ahmedabad              | Body Cover                      | Mk3               | 3     | 242         | 240            | 0.8264                |
| Ahmedabad              | Motor Controller                | CR01              | 1     | 74          |                |                       |
| Ahmedabad              | Motor Controller                | CR01              | 2     | 59          | 74             | -25.4237              |
| Ahmedabad              | Motor Controller                | CR01              | 3     | 60          | 59             | 1.6667                |
| Ahmedabad              | Motor Controller                | DR01              | 1     | 69          |                |                       |
| Ahmedabad              | Motor Controller                | DR01              | 2     | 79          | 69             | 12.6582               |
| Ahmedabad              | Motor Controller                | DR01              | 3     | 62          | 79             | -27.4194              |
| Ahmedabad              | Original Floor Mat              |                   | 1     | 244         |                |                       |
| Ahmedabad              | Original Floor Mat              |                   | 2     | 218         | 244            | -11.9266              |
| Ahmedabad              | Original Floor Mat              |                   | 3     | 239         | 218            | 8.7866                |
| Bangalore              | Body Cover                      | Mk1               | 1     | 230         |                |                       |
| Bangalore              | Body Cover                      | Mk1               | 2     | 227         | 230            | -1.3216               |
| Bangalore              | Body Cover                      | Mk1               | 3     | 244         | 227            | 6.9672                |
| Bangalore              | Body Cover                      | Mk2               | 1     | 260         |                |                       |
| Bangalore              | Body Cover                      | Mk2               | 2     | 224         | 260            | -16.0714              |
| Bangalore              | Body Cover                      | Mk2               | 3     | 248         | 224            | 9.6774                |
| Bangalore              | Body Cover                      | Mk3               | 1     | 242         |                |                       |
| Bangalore              | Body Cover                      | Mk3               | 2     | 221         | 242            | -9.5023               |
| Bangalore              | Body Cover                      | Mk3               | 3     | 249         | 221            | 11.2450               |
| Bangalore              | Motor Controller                | CR01              | 1     | 50          |                |                       |
| Bangalore              | Motor Controller                | CR01              | 2     | 59          | 50             | 15.2542               |
| Bangalore              | Motor Controller                | CR01              | 3     | 60          | 59             | 1.6667                |
| Bangalore              | Motor Controller                | DR01              | 1     | 59          |                |                       |
| Bangalore              | Motor Controller                | DR01              | 2     | 65          | 59             | 9.2308                |
| Bangalore              | Motor Controller                | DR01              | 3     | 50          | 65             | -30.0000              |
| Bangalore              | Original Floor Mat              |                   | 1     | 241         |                |                       |
| Bangalore              | Original Floor Mat              |                   | 2     | 251         | 241            | 3.9841                |
| Bangalore              | Original Floor Mat              |                   | 3     | 257         | 251            | 2.3346                |
| Chennai                | Body Cover                      | Mk1               | 1     | 256         |                |                       |
| Chennai                | Body Cover                      | Mk1               | 2     | 254         | 256            | -0.7874               |
| Chennai                | Body Cover                      | Mk1               | 3     | 250         | 254            | -1.6000               |
| Chennai                | Body Cover                      | Mk2               | 1     | 221         |                |                       |
| Chennai                | Body Cover                      | Mk2               | 2     | 244         | 221            | 9.4262                |
| Chennai                | Body Cover                      | Mk2               | 3     | 243         | 244            | -0.4115               |
| Chennai                | Body Cover                      | Mk3               | 1     | 238         |                |                       |
| Chennai                | Body Cover                      | Mk3               | 2     | 229         | 238            | -3.9301               |
| Chennai                | Body Cover                      | Mk3               | 3     | 260         | 229            | 11.9231               |
| Chennai                | Motor Controller                | CR01              | 1     | 68          |                |                       |
| <mark>Chennai</mark>   | <mark>Motor Controller</mark>   | <mark>CR01</mark> | 2     | 57          | 68             | <mark>-19.2982</mark> |
| <mark>Chennai</mark>   | <mark>Motor Controller</mark>   | <mark>CR01</mark> | 3     | 51          | 57             | <mark>-11.7647</mark> |
| Chennai                | Motor Controller                | DR01              | 1     | 76          |                |                       |
| <mark>Chennai</mark>   | <mark>Motor Controller</mark>   | <mark>DR01</mark> | 2     | 68          | 76             | <mark>-11.7647</mark> |
| <mark>Chennai</mark>   | <mark>Motor Controller</mark>   | <mark>DR01</mark> | 3     | 51          | 68             | <mark>-33.3333</mark> |
| Chennai                | Original Floor Mat              |                   | 1     | 235         |                |                       |
| Chennai                | Original Floor Mat              |                   | 2     | 217         | 235            | -8.2949               |
| Chennai                | Original Floor Mat              |                   | 3     | 235         | 217            | 7.6596                |
| Delhi                  | Body Cover                      | Mk1               | 1     | 250         |                |                       |
| <mark>Delhi</mark>     | <mark>Body Cover</mark>         | <mark>Mk1</mark>  | 2     | 229         | 250            | <mark>-9.1703</mark>  |
| <mark>Delhi</mark>     | <mark>Body Cover</mark>         | <mark>Mk1</mark>  | 3     | 225         | 229            | <mark>-1.7778</mark>  |
| Delhi                  | Body Cover                      | Mk2               | 1     | 249         |                |                       |
| Delhi                  | Body Cover                      | Mk2               | 2     | 215         | 249            | -15.8140              |
| Delhi                  | Body Cover                      | Mk2               | 3     | 270         | 215            | 20.3704               |
| Delhi                  | Body Cover                      | Mk3               | 1     | 233         |                |                       |
| Delhi                  | Body Cover                      | Mk3               | 2     | 246         | 233            | 5.2846                |
| Delhi                  | Body Cover                      | Mk3               | 3     | 227         | 246            | -8.3700               |
| Delhi                  | Motor Controller                | CR01              | 1     | 64          |                |                       |
| Delhi                  | Motor Controller                | CR01              | 2     | 64          | 64             | 0.0000                |
| Delhi                  | Motor Controller                | CR01              | 3     | 57          | 64             | -12.2807              |
| Delhi                  | Motor Controller                | DR01              | 1     | 65          |                |                       |
| Delhi                  | Motor Controller                | DR01              | 2     | 51          | 65             | -27.4510              |
| Delhi                  | Motor Controller                | DR01              | 3     | 53          | 51             | 3.7736                |
| Delhi                  | Original Floor Mat              |                   | 1     | 266         |                |                       |
| Delhi                  | Original Floor Mat              |                   | 2     | 210         | 266            | -26.6667              |
| Delhi                  | Original Floor Mat              |                   | 3     | 221         | 210            | 4.9774                |
| Hyderabad              | Body Cover                      | Mk1               | 1     | 213         |                |                       |
| Hyderabad              | Body Cover                      | Mk1               | 2     | 234         | 213            | 8.9744                |
| Hyderabad              | Body Cover                      | Mk1               | 3     | 241         | 234            | 2.9046                |
| Hyderabad              | Body Cover                      | Mk2               | 1     | 249         |                |                       |
| Hyderabad              | Body Cover                      | Mk2               | 2     | 231         | 249            | -7.7922               |
| Hyderabad              | Body Cover                      | Mk2               | 3     | 266         | 231            | 13.1579               |
| Hyderabad              | Body Cover                      | Mk3               | 1     | 247         |                |                       |
| Hyderabad              | Body Cover                      | Mk3               | 2     | 243         | 247            | -1.6461               |
| Hyderabad              | Body Cover                      | Mk3               | 3     | 258         | 243            | 5.8140                |
| Hyderabad              | Motor Controller                | CR01              | 1     | 75          |                |                       |
| Hyderabad              | Motor Controller                | CR01              | 2     | 41          | 75             | -82.9268              |
| Hyderabad              | Motor Controller                | CR01              | 3     | 72          | 41             | 43.0556               |
| Hyderabad              | Motor Controller                | DR01              | 1     | 61          |                |                       |
| Hyderabad              | Motor Controller                | DR01              | 2     | 57          | 61             | -7.0175               |
| Hyderabad              | Motor Controller                | DR01              | 3     | 49          | 57             | -16.3265              |
| Hyderabad              | Original Floor Mat              |                   | 1     | 231         |                |                       |
| <mark>Hyderabad</mark> | <mark>Original Floor Mat</mark> |                   | 2     | 228         | 231            | <mark>-1.3158</mark>  |
| <mark>Hyderabad</mark> | <mark>Original Floor Mat</mark> |                   | 3     | 221         | 228            | <mark>-3.1674</mark>  |
| Jaipur                 | Body Cover                      | Mk1               | 1     | 259         |                |                       |
| Jaipur                 | Body Cover                      | Mk1               | 2     | 223         | 259            | -16.1435              |
| Jaipur                 | Body Cover                      | Mk1               | 3     | 250         | 223            | 10.8000               |
| Jaipur                 | Body Cover                      | Mk2               | 1     | 239         |                |                       |
| Jaipur                 | Body Cover                      | Mk2               | 2     | 207         | 239            | -15.4589              |
| Jaipur                 | Body Cover                      | Mk2               | 3     | 262         | 207            | 20.9924               |
| Jaipur                 | Body Cover                      | Mk3               | 1     | 269         |                |                       |
| Jaipur                 | Body Cover                      | Mk3               | 2     | 224         | 269            | -20.0893              |
| Jaipur                 | Body Cover                      | Mk3               | 3     | 265         | 224            | 15.4717               |
| Jaipur                 | Motor Controller                | CR01              | 1     | 67          |                |                       |
| Jaipur                 | Motor Controller                | CR01              | 2     | 52          | 67             | -28.8462              |
| Jaipur                 | Motor Controller                | CR01              | 3     | 64          | 52             | 18.7500               |
| Jaipur                 | Motor Controller                | DR01              | 1     | 55          |                |                       |
| Jaipur                 | Motor Controller                | DR01              | 2     | 57          | 55             | 3.5088                |
| Jaipur                 | Motor Controller                | DR01              | 3     | 67          | 57             | 14.9254               |
| Jaipur                 | Original Floor Mat              |                   | 1     | 274         |                |                       |
| Jaipur                 | Original Floor Mat              |                   | 2     | 201         | 274            | -36.3184              |
| Jaipur                 | Original Floor Mat              |                   | 3     | 258         | 201            | 22.0930               |
| Kolkata                | Body Cover                      | Mk1               | 1     | 263         |                |                       |
| Kolkata                | Body Cover                      | Mk1               | 2     | 220         | 263            | -19.5455              |
| Kolkata                | Body Cover                      | Mk1               | 3     | 247         | 220            | 10.9312               |
| Kolkata                | Body Cover                      | Mk2               | 1     | 274         |                |                       |
| Kolkata                | Body Cover                      | Mk2               | 2     | 228         | 274            | -20.1754              |
| Kolkata                | Body Cover                      | Mk2               | 3     | 254         | 228            | 10.2362               |
| Kolkata                | Body Cover                      | Mk3               | 1     | 249         |                |                       |
| <mark>Kolkata</mark>   | <mark>Body Cover</mark>         | <mark>Mk3</mark>  | 2     | 238         | 249            | <mark>-4.6218</mark>  |
| <mark>Kolkata</mark>   | <mark>Body Cover</mark>         | <mark>Mk3</mark>  | 3     | 232         | 238            | <mark>-2.5862</mark>  |
| Kolkata                | Motor Controller                | CR01              | 1     | 68          |                |                       |
| Kolkata                | Motor Controller                | CR01              | 2     | 70          | 68             | 2.8571                |
| Kolkata                | Motor Controller                | CR01              | 3     | 63          | 70             | -11.1111              |
| Kolkata                | Motor Controller                | DR01              | 1     | 62          |                |                       |
| Kolkata                | Motor Controller                | DR01              | 2     | 57          | 62             | -8.7719               |
| Kolkata                | Motor Controller                | DR01              | 3     | 68          | 57             | 16.1765               |
| Kolkata                | Original Floor Mat              |                   | 1     | 231         |                |                       |
| Kolkata                | Original Floor Mat              |                   | 2     | 229         | 231            | -0.8734               |
| Kolkata                | Original Floor Mat              |                   | 3     | 233         | 229            | 1.7167                |
| Mumbai                 | Body Cover                      | Mk1               | 1     | 248         |                |                       |
| Mumbai                 | Body Cover                      | Mk1               | 2     | 263         | 248            | 5.7034                |
| Mumbai                 | Body Cover                      | Mk1               | 3     | 252         | 263            | -4.3651               |
| Mumbai                 | Body Cover                      | Mk2               | 1     | 223         |                |                       |
| Mumbai                 | Body Cover                      | Mk2               | 2     | 227         | 223            | 1.7621                |
| Mumbai                 | Body Cover                      | Mk2               | 3     | 269         | 227            | 15.6134               |
| Mumbai                 | Body Cover                      | Mk3               | 1     | 227         |                |                       |
| Mumbai                 | Body Cover                      | Mk3               | 2     | 230         | 227            | 1.3043                |
| Mumbai                 | Body Cover                      | Mk3               | 3     | 267         | 230            | 13.8577               |
| Mumbai                 | Motor Controller                | CR01              | 1     | 70          |                |                       |
| <mark>Mumbai</mark>    | <mark>Motor Controller</mark>   | <mark>CR01</mark> | 2     | 54          | 70             | <mark>-29.6296</mark> |
| <mark>Mumbai</mark>    | <mark>Motor Controller</mark>   | <mark>CR01</mark> | 3     | 52          | 54             | <mark>-3.8462</mark>  |
| Mumbai                 | Motor Controller                | DR01              | 1     | 67          |                |                       |
| <mark>Mumbai</mark>    | <mark>Motor Controller</mark>   | <mark>DR01</mark> | 2     | 63          | 67             | <mark>-6.3492</mark>  |
| <mark>Mumbai</mark>    | <mark>Motor Controller</mark>   | <mark>DR01</mark> | 3     | 55          | 63             | <mark>-14.5455</mark> |
| Mumbai                 | Original Floor Mat              |                   | 1     | 241         |                |                       |
| Mumbai                 | Original Floor Mat              |                   | 2     | 224         | 241            | -7.5893               |
| Mumbai                 | Original Floor Mat              |                   | 3     | 256         | 224            | 12.5000               |
| Pune                   | Body Cover                      | Mk1               | 1     | 246         |                |                       |
| Pune                   | Body Cover                      | Mk1               | 2     | 245         | 246            | -0.4082               |
| Pune                   | Body Cover                      | Mk1               | 3     | 261         | 245            | 6.1303                |
| Pune                   | Body Cover                      | Mk2               | 1     | 249         |                |                       |
| <mark>Pune</mark>      | <mark>Body Cover</mark>         | <mark>Mk2</mark>  | 2     | 226         | 249            | <mark>-10.1770</mark> |
| <mark>Pune</mark>      | <mark>Body Cover</mark>         | <mark>Mk2</mark>  | 3     | 224         | 226            | <mark>-0.8929</mark>  |
| Pune                   | Body Cover                      | Mk3               | 1     | 246         |                |                       |
| Pune                   | Body Cover                      | Mk3               | 2     | 235         | 246            | -4.6809               |
| Pune                   | Body Cover                      | Mk3               | 3     | 246         | 235            | 4.4715                |
| Pune                   | Motor Controller                | CR01              | 1     | 53          |                |                       |
| Pune                   | Motor Controller                | CR01              | 2     | 58          | 53             | 8.6207                |
| Pune                   | Motor Controller                | CR01              | 3     | 63          | 58             | 7.9365                |
| Pune                   | Motor Controller                | DR01              | 1     | 72          |                |                       |
| Pune                   | Motor Controller                | DR01              | 2     | 61          | 72             | -18.0328              |
| Pune                   | Motor Controller                | DR01              | 3     | 62          | 61             | 1.6129                |
| Pune                   | Original Floor Mat              |                   | 1     | 272         |                |                       |
| <mark>Pune</mark>      | <mark>Original Floor Mat</mark> |                   | 2     | 245         | 272            | <mark>-11.0204</mark> |
| <mark>Pune</mark>      | <mark>Original Floor Mat</mark> |                   | 3     | 232         | 245            | <mark>-5.6034</mark>  |
| Surat                  | Body Cover                      | Mk1               | 1     | 220         |                |                       |
| Surat                  | Body Cover                      | Mk1               | 2     | 271         | 220            | 18.8192               |
| Surat                  | Body Cover                      | Mk1               | 3     | 230         | 271            | -17.8261              |
| Surat                  | Body Cover                      | Mk2               | 1     | 265         |                |                       |
| Surat                  | Body Cover                      | Mk2               | 2     | 234         | 265            | -13.2479              |
| Surat                  | Body Cover                      | Mk2               | 3     | 257         | 234            | 8.9494                |
| Surat                  | Body Cover                      | Mk3               | 1     | 265         |                |                       |
| Surat                  | Body Cover                      | Mk3               | 2     | 224         | 265            | -18.3036              |
| Surat                  | Body Cover                      | Mk3               | 3     | 242         | 224            | 7.4380                |
| Surat                  | Motor Controller                | CR01              | 1     | 67          |                |                       |
| Surat                  | Motor Controller                | CR01              | 2     | 62          | 67             | -8.0645               |
| Surat                  | Motor Controller                | CR01              | 3     | 67          | 62             | 7.4627                |
| Surat                  | Motor Controller                | DR01              | 1     | 64          |                |                       |
| Surat                  | Motor Controller                | DR01              | 2     | 58          | 64             | -10.3448              |
| Surat                  | Motor Controller                | DR01              | 3     | 69          | 58             | 15.9420               |
| Surat                  | Original Floor Mat              |                   | 1     | 236         |                |                       |
| Surat                  | Original Floor Mat              |                   | 2     | 241         | 236            | 2.0747                |
| Surat                  | Original Floor Mat              |                   | 3     | 251         | 241            | 3.9841                |

**Based on current sales trends, which models or accessories should we prioritize in production to meet projected demand?**

*Code*

```sql
# Trend - Models
select Model, sum(Percentage_Change) as Overall_Trend from
(WITH MOM_Model_Sales AS
(
    SELECT 
        City,
        Model, 
        MONTH(`Date`) AS `Month`, 
        SUM(`Units Sold`) AS Total_Sales
    FROM model_sales ms
    GROUP BY City, Model, `Month`
)
SELECT Model, `Month`, Sum(Total_Sales) as Total_Sales,
    LAG(sum(Total_Sales),1) OVER (partition by Model order by `Month`) AS Previous_Month,
    (sum(Total_Sales) - (LAG(sum(Total_Sales),1) OVER (partition by Model order by `Month`)))/sum(Total_Sales) * 100 as Percentage_Change
FROM MOM_Model_Sales
group by Model, `Month`) t1
group by Model

# Trend - Accessories
select Accessory,`Version`, sum(Percentage_Change) as Overall_Trend from
(WITH MOM_Accessory_Sales AS
(
    SELECT 
        City,
        Accessory,
        `Version`,
        MONTH(`Date`) AS `Month`, 
        SUM(`Units Sold`) AS Total_Sales
    FROM accessory_sales ms
    GROUP BY City, Accessory, `Version`, `Month`
)
SELECT Accessory, `Version`, `Month`, sum(Total_Sales) as Total_Sales,
    LAG(sum(Total_Sales),1) OVER (partition by Accessory, `Version` order by `Month`) AS Previous_Month,
    (sum(Total_Sales) - (LAG(sum(Total_Sales),1) OVER (partition by Accessory, `Version` order by `Month`)))/sum(Total_Sales) * 100 as Percentage_Change
FROM MOM_Accessory_Sales
group by Accessory, `Version`, `Month`) t2
group by Accessory, `Version`
```

*Output*

We should prioritize the production of highlighted Models (Overall_Trend in %)

| Model                           | Overall_Trend       |
|:-------------------------------:|:-------------------:|
| Escotech LBR 2                  | -7.1854             |
| <mark>Escotech mini</mark>      | <mark>3.1820</mark> |
| Escotech Mk 1                   | -9.8095             |
| <mark>Escotech Mk 1 plus</mark> | <mark>3.3983</mark> |

We should prioritize the production of highlighted Accessories (Overall_Trend in %)

| Accessory               | Version          | Overall_Trend        |
|:-----------------------:|:----------------:|:--------------------:|
| <mark>Body Cover</mark> | <mark>Mk1</mark> | <mark>-0.2679</mark> |
| <mark>Body Cover</mark> | <mark>Mk2</mark> | <mark>3.2296</mark>  |
| <mark>Body Cover</mark> | <mark>Mk3</mark> | <mark>0.7711</mark>  |
| Motor Controller        | CR01             | -8.4702              |
| Motor Controller        | DR01             | -10.6390             |
| Original Floor Mat      |                  | -3.3587              |

## Conclusions

From all the above analysis, we can conclude that -

1. In order to decide new production plan, the production head must prioritize -
   
   1. Increasing the production of Escotech mini and Mk 1 plus models as they have consistent growth in sales figures.
   
   2. Increasing the production of Body Covers, for all versions, as they have consistently rising sales.
   
   3. Reducing the production of both Motor Controller Versions and Original Floor Mat
   
   4. Reducing the production of remaining two models - LBR 2 and Mk 1.

2. In terms of overall sales figures, Escotech mini performed well, and LBR 2 performed worst. Although difference between their sales figures is not high.

3. In terms of overall sales figures, Motor Controller DR01 performed well, and Body Cover Mk1 performed worst.

4. In models, Escotech LBR 2 was responsible for high revenue gain with less sales because of high price, while mini gained less revenue, although it's sales figures are not very less.

5. In accessories, both the Motor Controllers, although providing more sophisticated features, were overall less popular.

## License

This project and the dataset is made available under [CC BY-NC-SA 4.0.](https://creativecommons.org/licenses/by-nc-sa/4.0/)

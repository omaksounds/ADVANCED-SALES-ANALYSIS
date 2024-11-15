## Project Overview
This project provides an in-depth analysis of Adventure Works’ sales data, focusing on identifying key revenue streams, customer demographics, and product performance. The dashboard is designed to support data-driven decision-making by offering interactive insights on time trends, product categories, and regional performance.

## Features
The dashboard comprises of the following features;
- **Custom-Built Charts**

  These are visually tailored charts that go beyond standard charting options, designed to highlight specific aspects of the data and provide clearer insights. Each chart is customized in terms of color scheme, labels, and formatting to make the data more intuitive and accessible for end-users.

- **Interactive Dashboard Design**
  
  The dashboard is designed with interactive elements, allowing users to drill down into data, filter by specific parameters, and get dynamic updates based on their selections. This interaction enables users to explore the data from various angles without needing technical skills.

- **Macro-Enabled Filter Reset**
  
  This feature uses a macro that allows users to reset all filters on the dashboard to their default state with a single click. It’s particularly useful for large, complex dashboards where multiple filters are in place.

 ## Backend Process (Data Importation,Cleaning and Transformation)
The dataset is an Excel workbook containing six worksheets. Data import, cleaning, and transformation were conducted using Microsoft Excel’s Power Query.

After importing the data into Power Query, I selected all six worksheets and clicked on “Transform Data” to initiate the data cleaning and transformation process.

I began with a thorough data exploration to understand the dataset fully before proceeding.

Starting with the Facts table, I found it contained 26 columns, some of which were unnecessary for answering the business questions. Instead of deleting columns, I opted to deselect those not needed, retaining only the relevant columns for analysis.

![Screenshot2](https://github.com/user-attachments/assets/26671910-c25f-4709-9304-e422414390a4)
![Screenshot1](https://github.com/user-attachments/assets/55cd2880-0993-4de6-8ca5-2e68c95b1ce4)


During data profiling, I noticed that several columns were not assigned the correct data types. To address this, I used the “Detect Data Type” feature to automatically adjust the columns to their appropriate data types.

![Screenshot3](https://github.com/user-attachments/assets/e70d7b00-79ff-4afc-9832-5a999861526e)

I created a custom column named “Total Revenue” by multiplying the “Order Quantity” by the “Unit Price.”

![Screenshot4](https://github.com/user-attachments/assets/435f3877-10f5-435b-a4d3-d930f6b4b8b9)
![Screenshot5](https://github.com/user-attachments/assets/bae1d8e8-85b8-45f3-9526-6c035950742f)


I added another custom column named “COGS (Cost of Goods Sold)” by multiplying the “Order Quantity” by the “Cost.”

![Screenshot6](https://github.com/user-attachments/assets/7a5ad434-c40c-4576-9a3d-35e9d5238d69)
![Screenshot7](https://github.com/user-attachments/assets/aee10e7e-0c71-46d5-bada-98473b7fd873)


I added a custom column named “Total Profit” by subtracting the COGS from the Total Revenue.

![Screenshot8](https://github.com/user-attachments/assets/24e8d14c-d893-4ffa-8d12-aef6f2b6d58a)
![Screenshot9](https://github.com/user-attachments/assets/2bf6e23c-47c0-4051-81a5-fd2491ca0f49)


To segment the prices into “Expensive” and “Less Expensive,” I created a conditional column named “Product Price Type.” This column categorizes any price of $150 or less as “Less Expensive,” and anything above $150 as “Expensive.”

![Screenshot10](https://github.com/user-attachments/assets/90b502dd-5749-4652-b986-7ba7b3e3b1bf)
![Screenshot11](https://github.com/user-attachments/assets/6cf989ee-eefe-4a27-bf5f-0fcb97c21d67)


In the dimensional tables, I began with the “Sales Territory” table, where I found an empty row across multiple columns and a column filled entirely with “null” values. I removed these to ensure a clean dataset.

Next, I reviewed the “Product” table, selecting only the relevant columns and removing the rest. In one of the columns, I noticed values marked as “N/A,” which I replaced with “Unspecified” for consistency

![Screenshot12](https://github.com/user-attachments/assets/1140a5d1-666c-40c4-ab32-1046c1eb1ac3)
![Screenshot13](https://github.com/user-attachments/assets/fa53c777-b0b7-4b2d-a50c-18ab30b9e015)


I applied the same approach to the “Geography” dimensional table, selecting only the columns relevant to answering the business questions.

For the “Date” table, I retained only the date column and removed the others to create a custom calendar. I first extracted the “Year” from the date column; however, the extracted years ranged from 2005 to 2010. Since the business requirements specified a timeframe from 2005 to 2008, I filtered out the years 2009 and 2010 from the dataset.

![Screenshot14](https://github.com/user-attachments/assets/50e0b785-62c2-48bd-ba05-59bd3f1972f5)


I inserted the month number to enable sorting from January to December instead of alphabetically. I then extracted the month name but, due to space constraints, limited it to the first three characters.

I applied a similar approach to the day of the week, extracting the abbreviated day names. I also added a conditional column to indicate whether each date fell on a weekend or a weekday.

![Screenshot15](https://github.com/user-attachments/assets/20c7c27a-1b56-45e6-8405-92457244f078)
![Screenshot16](https://github.com/user-attachments/assets/7bc57a1e-ce66-4831-8d6d-b711187ab950)


I extracted the quarter, but it initially displayed as numbers. To make it more descriptive, I added the prefix “Qtr,” resulting in labels such as “Qtr 1,” applied automatically across the entire column.

![Screenshot17](https://github.com/user-attachments/assets/dd79f287-c428-4cca-a3e9-e9ebf934d18b)
![Screenshot18](https://github.com/user-attachments/assets/9e2d263a-123f-47a7-b946-bd1bcff898bb)
![Screenshot19](https://github.com/user-attachments/assets/d245d91a-3b8b-4f83-93ef-06b8123097d2)


Lastly, in the “Customer” table, I observed that names were split across different columns. I merged the first and last name columns to create a full name column, then removed any columns not needed for the analysis.

![Screenshot20](https://github.com/user-attachments/assets/ff7ee343-3caa-4db4-af9a-d7928f04be29)


To extract the customers’ ages from the date of birth column, I used the following M code, as shown in the image below. This allowed me to calculate each customer’s age accurately.

![Screenshot21](https://github.com/user-attachments/assets/314b7907-94d4-4c9d-9914-8d46bd690044)


After calculating each customer’s age, I added a conditional column to categorize them into age groups, creating age bins to simplify the analysis process.

![Screenshot22](https://github.com/user-attachments/assets/eddab75e-1e37-40de-bd78-b1741451e5c2)


After completing the data cleaning process, I closed and loaded the data into the data model (Power Pivot) to begin modeling by linking the dimension tables to the facts table.

During modeling, I noticed that the geography table could not be directly linked to the facts table, as there was no geography key in the facts table. However, a geography key was available in the customer table. Therefore, I linked the geography table to the customer table, and then linked the customer table to the facts table.

![Screenshot23](https://github.com/user-attachments/assets/b55d359e-a806-42b1-b893-bfd72b777104)


After linking the tables, I created a new table in Power Pivot named “Measures” to store all my DAX calculations for easy access.

Once that was set up, I closed Power Pivot and returned to the workbook.

## Dashboard Design Process
The dashboard’s color scheme was selected to highlight key areas related to the business questions being addressed.

This project includes two distinct dashboards. The first dashboard provides an overview of key sales metrics, displaying KPIs alongside time-based analysis, enabling users to track sales trends monthly, quarterly, and even daily. This setup offers a high-level view of sales, allowing users to quickly assess overall performance and identify areas that may warrant further analysis.

![dashboard1](https://github.com/user-attachments/assets/b41ec323-1539-4711-949d-e41447dcec18)



The second dashboard on the other hand focuses on detailed insights into product and customer data.


![dashboard2](https://github.com/user-attachments/assets/70e09715-3ddc-4d17-90e6-5774148eb2a2)



To enhance the user experience, I linked both dashboards, enabling easy navigation between them with a single click. Additionally, I included a macro-enabled reset button, allowing users to clear all filters and slicers with one click.

## Key insights from the first Dashboard
To provide clarity on the goals of the first dashboard, here are the key business questions it addresses:

![screenshot25](https://github.com/user-attachments/assets/7578c427-c534-4151-8f6d-a934007b68fb)



To address the business questions outlined above, here are key insights from the dashboard:

#### 1. *KPI Comparison to Previous Year:*
![kpis](https://github.com/user-attachments/assets/7bbef926-2b33-42c5-93eb-a7e7f9f2f227)



The dashboard highlights year-over-year changes in critical metrics, including Total Quantity (631.92K), COGS ($180.80M), Revenue ($307.09M), Profit ($126.29M), Profit Margin (41.1%), and Total Transactions (60.40K). This comparison aids in identifying growth patterns and areas for improvement.

#### 2. *Yearly Performance Metrics (Above Average Years):*
![Screenshot26](https://github.com/user-attachments/assets/7ecaad73-f6e6-4c03-afa0-66d26182589d)

The years 2007 and 2008 show above-average profit contributions, collectively accounting for 67.1% of total profit. These high-performance periods serve as potential benchmarks for future strategic planning.

#### 3. *Monthly Profit Trends:*
![Screenshot27](https://github.com/user-attachments/assets/764d0524-4f7c-42cd-9893-ed85b7c68d37)


The line chart provides monthly insights, showing peaks and declines. For instance, June, May and April had higher profits in 2008, indicating possible seasonal demand.

#### 4. *Profit by Week Type:*
![Screenshot29](https://github.com/user-attachments/assets/900e21a2-0e47-43b3-8611-34cc2beaef78)

Weekdays generated 72% of the total profit ($90.94M), compared to 28% from weekends. This insight underscores the profitability of weekday operations, providing a basis for resource allocation during peak periods.

#### 5. *Quarterly Profit Analysis:*
![qtr](https://github.com/user-attachments/assets/50a004df-203c-44be-a412-3be5659ef607)


Analysis by quarter reveals Q2 and Q1 as the most profitable periods, with Q2 contributing $39.02M and Q1 $32.30M. This finding could inform efforts to sustain or increase profitability in these quarters.

#### 6. *Profit by Weekday:*
![Screenshot28](https://github.com/user-attachments/assets/119deaed-19ba-4d79-9062-02ff700904a8)

Mid-week days, specifically Wednesday, Thursday, and Friday, consistently deliver higher profits, with respective contributions of $18.22M, $18.81M, and $18.28M. This trend indicates that these days are optimal for targeted campaigns and promotional activities.

These insights directly address the business questions, providing actionable data to support decision-making and performance monitoring.





## Key insights from the Second Dashboard
For the second dashboard, the following business questions are addressed:

![screenshot260](https://github.com/user-attachments/assets/0811e966-293e-4942-8715-580c845c8903)


To address the business questions outlined above, here are key insights from the second dashboard:

#### 1. *Top 5 Profitable Products:*
![Screenshot31](https://github.com/user-attachments/assets/255d88de-9c66-440d-896e-9490f2fe97b6)

These top 5 product variations dominate profitability, contributing significantly to the company’s revenue. The top 5 products make up 24.8% of the profit, indicating their high market demand and strong sales performance relative to other products.

#### 2. *Top 5 Profitable Customers:*
![top5customers](https://github.com/user-attachments/assets/8ac7866e-364d-468f-9141-02672430f093)

These High-value customers, generate significant profits, though they represent only 0.3% of total customers. This small customer segment plays a crucial role in profit, suggesting a targeted approach toward these top clients could be beneficial.

#### 3. *Profit by Gender:*
![Screenshot33](https://github.com/user-attachments/assets/e46a45cc-f1f6-4d2f-8c88-37545d90d4bc)

Profits are almost evenly split between male and female customers, with females contributing slightly more (50.4%). This balanced gender distribution implies no strong gender-based skew in purchasing behavior, indicating broad product appeal.

#### 4. *Profit by Product Color:*
![color](https://github.com/user-attachments/assets/1a6809f9-837b-442d-a1af-a027fe50d62a)


Black, Red and Silver products lead in profitability. Emphasizing these colors in future product releases or marketing could align with customer preferences and boost sales further.

#### 5. *Profit by Pricing Types:*
![Screenshot35](https://github.com/user-attachments/assets/faaf0019-0bef-463e-a876-7a1831b0e0f6)

Higher-priced items (above $150) account for 95.4% of total profits, highlighting the company’s strength in the premium segment. This suggests that focusing on high-end products could be more profitable than expanding low-cost options.

#### 6. *Country-wise Profit Distribution:*
![country](https://github.com/user-attachments/assets/b5685f9e-04e6-4391-b93d-8901403556c5)


The United States and Australia are key markets, contributing 62.7% of the total profit. This strong geographic concentration suggests these countries should remain the focus for targeted marketing and resource allocation.

#### 7. *Profit by Age Groups:*
![age](https://github.com/user-attachments/assets/b3f285cf-79ac-4349-83bb-4871faeeb4fb)


Customers above 50 years of age contribute the most to profits (36.2%), making this age group a valuable demographic. Marketing efforts tailored towards this age group might enhance profitability by aligning more closely with their purchasing patterns.

These insights provide clear direction for strategic decisions, from targeted marketing and product focus to geographic prioritization, helping the company maximize profitability based on data-driven findings.




These questions guide the dashboard’s layout and metrics, helping users gain insights into sales performance.







# Practical_Application_2
Jupytor Notebook created for Practical Application Assignment for Module 11 of AI/ML Certification Course

September 3rd, 2024
Professional Certificate in ML/AI
Practical Application II
Kimberly Tulga




Read ME: What drives the price of car?


Overview

The dataset provides information about a sample of 426K vehicles that were sold in the USA and were manufactured between 1900-2022. The dataset offers 16 factors of the vehicle along with their listed prices. Our client is a used car dealership that wants to use our analysis model to price its inventory. The model needs to provide the most important factors of a car when determining its price.
Summary

The initial dataset included 16 factors and the price. The info() function showed a large number of NaN values across many of the factors. I wanted to keep as many values as possible by utilizing the LabelEncoder() function on all missing values. I noticed that the Year, Price, and Odometer columns had a large number of outliers and trimmed the data where the price was between $500 - $200k. I ran my model using 5 different prediction models: Sequential Selector, Ridge, Lasso, Sequential Selector using Lasso, and Recursive Feature Elimination with Lasso. The results from the initial run are shown in Figure 1.



<img width="549" alt="Screen Shot 2024-09-10 at 1 23 23 PM" src="https://github.com/user-attachments/assets/16ddb089-912c-42e1-8005-37cc9a2049ff">
 
Figure 1: Results from Initial Run




Since the R^2 scores were so low at 18%, further refining the initial dataset was required. Furthermore, I noticed both the ‘Year’ and the ‘Odometer’ might be telling the same story since their correlation coefficients were inverse of one another after using the corr() function.


Round 2 – No Outliers

I wanted to refine the model by eliminating most of the outlier values and columns that had large NaN values. I dropped the ‘VIN’, ‘size’, ‘cylinders’, and ‘condition’ columns. I also dropped the ‘odometer’ column to eliminate overfitting. Furthermore, I trimmed the dataset by setting the ‘title_status’ column equal to 'clean', applied the same price filter of $500 - $58,000, and adjusted the 'Year' of the vehicle to newer than 2005. With those filters, I was able to get rid of outliers in the ‘Price’ and ‘Year’ columns. My dataset went from 426K records down to 307K records. With this smaller dataset, I repeated the prediction models I used previously and got the following results shown in Figure 2.


<img width="800" alt="Screen Shot 2024-09-10 at 1 40 27 PM" src="https://github.com/user-attachments/assets/091a171a-6344-4242-85c7-1f8fa2503216">

Figure 2: Results from Round 2

Round 3 – Cleaner Dataset

I wondered if a cleaner dataset would be able to improve the R-score of the models even further. Using Excel software, I wanted to see the exact quality of the data. I quickly noticed that the ‘model’ column was more of the description of each vehicle as many of them contained information regarding each vehicle’s model, trim, drive info, body style, and year.  For example: the most popular vehicle in the list Ford F-150 would have over 700 different names in the ‘model’ column ( i.e. "ford f150 super cab xl pickup 4d"). I decided to clean the dataset for the 35 most popular vehicle models by renaming the existing ‘model’ column to ‘description’, and creating a new ‘model’ column that would contain only the model information of each vehicle. Cleaning up the dataset for the top 35 most popular vehicles yielded about 111.6K records. While cleaning those datasets, I quickly realized many vehicles were duplicates of each other, and some vehicles were duplicated at least 5 times. However, getting rid of those duplicates was not in the scope of this round. I re-run the models as I did in Round 2 with the smaller, yet cleaner dataset. The results of the Round 3 are shown in Figure 3.

<img width="753" alt="Screen Shot 2024-09-10 at 2 00 07 PM" src="https://github.com/user-attachments/assets/fa3b7d05-f3b3-4896-bb98-47a2ce4e95e1">
 
Figure 3: Results from Round 3 - Cleaner Dataset

Key findings

The latest model yielded that 'Year' followed by the 'Model' were the most important factors when determining car price. The 'Drive' and th 'Manufacturer' were the next important factors, followed by the 'Fuel'. Figure 4 shows each feature and their prediction coefficients for the Sequential Selector with the Lasso model.

<img width="224" alt="Screen Shot 2024-09-10 at 2 07 42 PM" src="https://github.com/user-attachments/assets/b9e86d6b-37e7-4b6c-ab24-614e0dd0a140">
 
Figure 4: Sequential Selector with Lasso Model Features and Coefficients for Round 3


Recommendation

I believe that the prediction could be further improved if more data cleaning could be conducted. The initial dataset would not have so many NaN values if information could be extracted from the ‘model’ column. The model column has very few NaN values and it contains information for manufacturer, model, trim, drive, gas, and body type. The dataset also needs to be trimmed to get rid of duplicate values. This type of deep data cleaning may take excessive manpower. However, it will substantially improve the R-score of the prediction models.

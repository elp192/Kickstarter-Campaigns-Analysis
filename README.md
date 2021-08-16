
# Kickstarter Campaigns Analysis
## Overview of Project
### Background
The Excel sheet includes Kickstarter project data of previous campaigns from 2009 to 2017, which provide information for those who plan to start crowdfunding campaigns. By analyzing previous crowdfunding data, hidden trends are discovered, and it can be determined which factors contribute to the success or failure of a new campaign.<br>
The dataset consists of about 4000 rows and several columns. Each row represents a campaign, and the columns show some attributes related to the project, such as the name of the projects, short descriptions of the projects, amount of money considered as goals and pledges, etc.
### Purpose
In this project, we want to provide insights for our client, Louise, who wants to be successful in starting a campaign located in the United States (US) and categorized and subcategorized as "Play" and "Theater" market, respectively. The estimated budget for her project is about $10,000, and the estimated cost is approximately $12,000. Also, she is interested in gaining an overview of the "musicals" market in Great Britain (GB) for future projects considering her budget of £4,000. In this regard, the main goal of this project is to predict the percentage of Louise's success in starting new campaigns by analyzing data related to the previous campaigns with similar factors that Louise has.<br>
To measure and observe new trends and easily interpret the data, various columns and worksheets are created, and organizing tools such as filters, formatting, pivot tables, and charts are utilized. The analyses are presented next.
## Analysis and Challenges
### Data Preparation for Analysis
#### Created columns
The created columns in the Kickstarter sheet are as follows:<br>
1. **Percentage Funded** (column O)<br>
     Pledged (column E) and Goal (column D) columns determining the amount of money each campaign made and the amount of money campaign needs to be successful, respectively, are utilized to create a percentage funded column. This column determines the percentage of goal that was satisfied by each champaign.<br>
An example of the formula to create column O for row 2 is as follows:

         =ROUND(E2/D2*100,0)

2. **Average Donations** (column P)<br>
     Pledged (column E) and Backers (column L) columns, determining the amount of money each campaign made and the number of backers in each campaign, respectively, are utilized to create the Average Donations column. This column determines historical information about the average money that each people provide to a campaign.<br>
An example of the formula to create column P for row 2 is as follows:

         =ROUND(E2/L2,2)
    
   :exclamation: In column P, few cells may represent #DIV/0! error as campaigns related to these cells may not have backers. To avoid this error, the following formula (an example for row 2) is used:

        =IFERROR(ROUND(E2/L2,2),0)
    
3. **Parent Category and Subcategory** (column N)<br>
     The Category and Subcategory column groups category (e.g., film and video) and subcategory (e.g., television), separated by a backslash. This column is divided into Parent Category (column Q) and Subcategory (column R) columns using the “Data” tab, “Text,” and “Columns” button.

4. **Date Created Conversion and Ended Conversion** (columns S and T)<br>
   There are two columns in the Kickstarter sheet representing deadline (column I) and launch date (column J) of projects. With information from these columns, the opening length of a campaign in which it reaches to its outcome (column F) can be determined. <br>
It isn't easy to interpret date formats using these columns because they include Unix timestamps. In this regard, a formula is used to convert data to a readable date format. The columns named Date Created Conversion (column S) and Date Ended Conversion (column T) are created to represent the readable date related to columns I and J.<br>
As an example, the following formula is used to convert the deadline for row 2:

        =(((J2/60)/60)/24)+DATE(1970,1,1)

5. **Years** (column U)<br>
   This column selects a year related to each campaign from the Date Created Conversion column using Year() function.

It is worth mentioning that to customize the worksheet **conditional formatting**, highlighting the cells with specific colors based on defined conditions, is applied on two Kickstarter columns, named outcomes (F) and Percentage Funded (O). <br>
The outcomes column determines whether the project is successful, failed, canceled, or lived. Also, as mentioned earlier, the Percentage Funded column shows the percentage of goal satisfied by each campaign. Thus, conditional formatting enables us to visually get information about outcomes and percentage funded.<br>
The created columns in Kickstarter sheet and conditional formation of columns are shown in Figure 1 and Figure 2, respectively:

<p align="center">
   <img width="752" alt="Created Columns" src="https://user-images.githubusercontent.com/85843401/124200105-853f3000-daa2-11eb-86b4-321a191b6095.png"><figcaption>Figure 1: Representation of created columns.</figcaption></figure>
</p> 

<p align="center">
   <img width="834" alt="Conditional Formatting" src="https://user-images.githubusercontent.com/85843401/124200125-8d976b00-daa2-11eb-9412-7d4d5f47e47c.png"><figcaption>Figure 2: An illustration of conditional formatting.</figcaption></figure>
</p> 

### Created New Worksheets and Analysis
The additional Excel sheets are created to statistically analyze the data, create the pivot tables, charts and use the VLOOKUP function. In this section, the process of creating new sheets and related analysis to the data are presented.<br>
1. **Analysis of Category Statistics Sheet**<br>
   In this sheet, the pivot table is created in which rows and columns demonstrate Category and Outcomes (columns of Kickstarter sheet); respectively, Outcomes are counted in the Values field, and data are filtered by Country. From this table, it can be observed that the total number of Outcomes in all categories and countries is 4114. In addition, 349, 1530, 50, and 2185 of Outcomes are canceled, failed, lived, and successful (Figure 3).

<p align="center">
<img width="666" alt="Category Statistics" src="https://user-images.githubusercontent.com/85843401/124200584-b8ce8a00-daa3-11eb-83bc-653be2c7ea56.png"><figcaption>Figure 3: Comparison of outcomes of campaigns in various categories.</figcaption></figure>
</p> 

   As Louise is interested in United States (US), the data are filtered by the US. As can be observed, the total number of Outcomes is 3038. This information shows that a large number of campaigns belong to the US. From Figure 4, it can be observed that out of 912 campaigns in the theatre category, about 57.5% of them are successful.

<p align="center">
   <img width="670" alt="Category Statistics_US" src="https://user-images.githubusercontent.com/85843401/124200727-0ea33200-daa4-11eb-9e7b-e01c3c58b2dd.png">
<figcaption>Figure 4: Comparing outcomes of campaigns in various categories and United States.
.</figcaption></figure>
</p> 

2. **Analysis of Subcategory Statistics Sheet**<br>
   In this sheet, rows and columns represent Subcategories and Outcomes (columns of Kickstarter sheet), respectively, and Outcomes are counted. The data are filtered by Country and Parent Category (columns of Kickstarter sheet).<br>
   There are 604 campaigns in Great Britain (GB), and 59% of them belong to theater. Musical, plays, and spaces markets are the subcategories of the theater field.
The musical market is the future target for Louise in GB. As shown in Figure 5, among other successful markets in the theater field, only 3.78% of successful campaigns are allocated to musical market. However, the play is the most successful market in this category by about 92%.

<p align="center">
   <img width="676" alt="Subcategory Statistics" src="https://user-images.githubusercontent.com/85843401/124202938-92135200-daa9-11eb-86f1-16f1b0973cea.png">
<figcaption>Figure 5: Comparing outcomes of campaigns in the subcategory of theater (i.e., musical, plays and spaces) and GB.</figcaption></figure>
</p> 

3. **Analysis of Edinburg Research Sheet**<br>
   As Louise is interested in five plays called be Prepared, Checkpoint 22, Cutting Off Kate Bush, Jestia and Raedon, and The Hitchhiker's Guide to the Family, at the Edinburgh Festival Fringe, the new sheet is created. In this sheet, each column represents name of the play, short description, goals, pledges, average donation, and number of backers. This information is obtained using the VLOOKUP function.<br>
As an example, the following formula is used to obtained information about be Prepared play:

       =VLOOKUP(A2, Kickstarter!$B:$C, 2, FALSE)

Table 1 shows that goals and pledges amount related to the plays that Louise is interested in are less than £4,200. In addition, the average donations for these plays are in the range of £33-52.

<p align="center">
   <img width="1091" alt="Endinburgh Research" src="https://user-images.githubusercontent.com/85843401/124203154-106ff400-daaa-11eb-9fda-81d8b31abd74.png"><figcaption>Table 1: Representing goals, pledges, average donation, and the number of backers related to the plays that Louise is interested in.</figcaption></figure>
</p> 

4. **Analysis of Musical Market in GB**<br>
   For further analysis, whiskers and box plot related to musicals market in GB that Louise specifically plans to start a campaign in this market, is shown in Figure 6. In this plot, the campaign goals and pledges are compared. The median of goals and pledges are £2000 and less than £500, respectively. Also, the median of goals is higher than the third quantile of pledges. In addition, the amount of pledges for 25% of campaigns is close to £0 and this criteria for 75% of campaigns is less than £1500.<br>
   According to these results we can conclude that Louise needs to decrease her goals amount to gain a better opportunity for success.
   
<p align="center">
   <img width="364" alt="Comparison of Goal and Pledged in GB and Musical Subcategory" src="https://user-images.githubusercontent.com/85843401/124203758-6ee9a200-daab-11eb-8ca3-5200efeb4537.png"><figcaption>Figure 6: Comparing amount of goals and pledges in GB and musical Subcategory.</figcaption></figure>
</p> 

5. **Analysis of Successful US Kickstarters and Failed US Kickstarters using Descriptive Statistics**<br>
To measure and compare the statistics (i.e., central tendency, spread, ...) of successful and failed Kickstarters in the plays category, two sheets are created. These two sheets are the results of filtering in US country (US and plays respectively are country and category for Louise that she is interested in) based on success or failure of a campaign.<br>
Using data from Successful US Kickstarters and Failed US Kickstarters sheets, in another sheet (i.e., Descriptive Statistic), mean, median, standard deviations, lower quantile, upper quantile, and IQR for both goals and pledges data when Kickstarters are successful and failed are calculated.<br>
The examples of formulas for goal and successful Kickstarters are as follows:

       =AVERAGE('Successful US Kickstarters'!D:D)
       =MEDIAN('Successful US Kickstarters'!D:D)
       =STDEV.P('Successful US Kickstarters'!D:D)
       =QUARTILE.EXC('Successful US Kickstarters'!D:D, 3)
       =QUARTILE.EXC('Successful US Kickstarters'!D:D, 1)

From Table 2, some conclusions can be conducted.<br>
- As means of goals and pledges are greater than their medians, the distributions are positively skewed (right-skewed).<br>
- The mean of goals in failed campaigns is twice as successful campaigns. Also, the mean of pledges is 15 times lower than the goals. Considering the significantly higher goal of unsuccessful campaigns, we conclude that setting a goal with a lower amount can be a factor in a success of a campaign.<br>
- The standard deviations of goals and pledges are significantly higher than the IQR of goals and pledges (more than two times). This means that in related data, it should be outliers that considerably impact standard deviations. So, IQR can be a better criterion for analyzing the dispersion in our data.

<p align="center">
   <img width="278" alt="Descriptive Statistics" src="https://user-images.githubusercontent.com/85843401/124204281-b9b7e980-daac-11eb-9c49-c68242100cb9.png"><figcaption>Table 2: Representation of statistics related to goals and pledges in successful and failed campaigns.</figcaption></figure>
</p> 

6. **Analysis of Outcomes Based on Launch Date**<br>
In the Outcomes Based on the Launch Date sheet, the pivot table is created. In this table, rows and columns are constructed from Outcomes and Date Created Conversion (months of the year) columns of the Kickstarter sheet, respectively. Also, data are filtered by Parent Category and Years (columns of Kickstarter sheet).<br>
Obtained data shows that the most successful campaigns are organized in May, and the least of them are in December. This trend is the same while the table is filtered by a Category called theater. As can be seen in a line chart (Figure 7), the number of successful campaigns is decreased from 111 (about 13% of successful campaigns) in May to 37 (about 4.5% of successful campaigns) in December. Furthermore, out of 1369 campaigns, about 61%, 36%, 3% of them are successful, failed, and canceled, respectively.<br>
The observed results help Louise to make the right decision to start her new campaign at an appropriate month of a year.

<p align="center">
  <img width="696" alt="Theater Outcomes  by Launch Date" src="https://user-images.githubusercontent.com/85843401/124204725-a6594e00-daad-11eb-93fa-2dc99192a465.png">
<figcaption>Figure 7: Comparing theater outcome based on month of the year.</figcaption></figure>
</p> 

7. **Analysis of Outcomes Based on Goals**<br>
   Eight columns named Goal, Number Successful, Number Failed, Number Canceled, Total Projects, Percentage Successful, Percentage Failed, and Percentage Canceled are created in Outcomes Based on Goals sheet. In the Goal column (column A), champaigns are grouped according to their goals, which results in 12 rows. The number of successful, failed, and canceled campaigns (columns B to D) are calculated using COUNTIFs in the Plays Subcategory. An example of this calculation for the number of successful projects in the range of 1000 to 4999 is as follows:

         =COUNTIFS(Kickstarter!$D:$D,">=1000",Kickstarter!$D:$D,"<=4999",Kickstarter!$F:$F,"successful",Kickstarter!$R:$R,"plays")

   where D, F, and R columns named Goal, Outcomes, Subcategory in the Kickstarter sheet, respectively.<br>
   In the Total Projects column (column E) and Percentage columns (column F-H), the summation (using SUM function) and percentage of successful, failed, and canceled campaigns are calculated.<br>
   The line chart (Figure 8) represents percentage of successful, failed, and canceled champaigns versus goal range. Results show that 76% and 73% of campaigns in the goal range of less than $1,000 and $1,000-$4,999 are successful. In the goal range of $45,000-$49,999 and greater than $50,000 least number of campaigns (about 0% and 13%) achieve their goals. Therefore, we can conclude that overall, when the goal is set to a higher amount, the rate of success of campaigns is declined. However, it can be observed that this trend for campaigns with a fundraising goal range of $35,000-$45,000 is different, and they were able to reach their goal (67% of campaigns in this range).<br>
The Louise cost is in the range of $10,000-$14,999. From the table, it can be seen that there are not a significant number of campaigns in this range (6.8%); however, among this number 54% of them are successful.

<p align="center">
<img width="641" alt="Outcome Based on Goal" src="https://user-images.githubusercontent.com/85843401/124205002-4fa04400-daae-11eb-8146-55c903cc4138.png">
<figcaption>Figure 8: Comparing theater outcome based on month of the year.</figcaption></figure>
</p> 

### Challenges and Difficulties Encountered
One of the important challenges can be analyzing and organizing the results obtained from pivot tables and charts. The first important step to solve this difficulty is to understand the problem that what kind of information a customer exactly needs to know. The next step is to read different papers and reports to learn how others in different fields present and conclude results based on their goals. In this work, the presented results should provide suitable information for Louise to enable her to make a correct decision for opening the campaign at an appropriate location and at a good time based on her costs and budget.<br>
Other challenges can be using Excel functions correctly and selecting the proper variable for each field of pivot tables. These issues are solved by watching different learning videos, studying books, and online searches.

## Results
### Conclusions about the Outcomes based on Launch Date
:white_medium_small_square: The highest number of successful campaigns is 111 (about 13% of successful campaigns) in May.<br>
:white_medium_small_square:	The lowest number of successful campaigns is 37 (about 4.5% of successful campaigns) in December.<br>
:white_medium_small_square:	The total number of campaigns in May and June (166 and 153 out of 1369 campaigns) are more than other months of the year.<br>
:white_medium_small_square: 62%, 36%, 2.7% of campaigns are successful, failed, and canceled, respectively.<br>

:white_check_mark: The month of the year that the campaign launched at is an important factor for success of campaigns. May and June are the best months of the year for campaigns to be successful, while December is the worst. 

### Conclusions about the Outcomes based on Goals
:white_medium_small_square:	76% of campaigns with the goal range of less than $1,000 are successful.<br>
:white_medium_small_square: 73% of campaigns with the goal range of $1,000 to $4,999 are successful.<br>
:white_medium_small_square: 45%-55% of campaigns with the goal range of $5,000 to $24,999 are successful.<br>
:white_medium_small_square: Less than 27% of campaigns with the goal range of $25,000 to $34,999 are successful.<br>
:white_medium_small_square: 67% of campaigns with the goal range of $35,000 to $44,999 are successful.<br>
:white_medium_small_square: Less than 13% of campaigns with the goal range of more than $45,000 are successful.

:white_check_mark: The success chance of campaigns with goal range more than $45000, is reduced compared to those with lower goal range.

 ### some limitations of this dataset
There are some limitations that one may encounter while analyzing this dataset.<br>
:warning: The dataset is limited to a specific period (i.e., 2009-2017). This means that the sample size is not large enough to provide accurate insight for Kickstarter campaigns that plan to open the campaigns in the current year.<br>
:warning:	The number of countries included in the dataset is limited.<br>
:warning:	Other factors may influence the success or failure of campaigns ignored during analysis or/and are unavailable in the dataset. As an example, how much advertising can influence the chance of success or failure of projects.

### Other possible tables/graphs 
:black_small_square: Pivot tables can be created to compare the differences among countries in terms of receiving funds from backers, length of campaigns, and so on and analyze whether there is any relationship between these factors and Outcomes (success or failure of campaigns).<br>
:black_small_square: A pivot table can be created to determine which campaigns and at which months of the year receive more funding from backers on average.<br>
<br>
<br>
\*This project was done as part of the University of Toronto Data Analytics program.

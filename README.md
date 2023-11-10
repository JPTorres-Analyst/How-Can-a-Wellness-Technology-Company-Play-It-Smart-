# How-Can-a-Wellness-Technology-Company-Play-It-Smart-


<h2>Description</h2>
This project consists in the cleaning, processing and analysis of fitness tracking information from a dataset available in Kaggle (https://www.kaggle.com/datasets/arashnic/fitbit) to draw insights and trends shown by the users in order to help the company make data-driven decisions to improve their service.
<br />


<h2>Tools Used</h2>

- <b>R Programming</b> 
- <b>Speadsheets</b>

<p>
 
<h2> ASK PHASE: </h2>
<b>What is the question we are trying to solve?</b>

What are meaningful insights for the company by analyzing existing fitness tracking in order to improve their service to customers.


<b>How can your insights drive business decisions?</b>

By pointing out trends and existing aspects that users already show with their data. By doing this the company has a ground to either improve their products or use it as a guide to better assist their customers.


<b>Business task</b>

Provide insights from existing fitness tracking devices data in order to improve Bellabeats products.

<b>Key stakeholders</b>

-Urska Srsen, cofounder and Chief Officer
-Sando Mur, mathematician and Bellabeat’s cofounder.



<FONT COLOR="RED">Moving on to the next phase:</FONT>

<h2> PREPARE PHASE: </h2>

Since we are going to be working in R studio, we need to import the data, to do this we do the following: go to the files pane located in the right bottom corner

////INSERT IMAGE///


Before we start to make changes to the data, we are going to call some libraries that will help us with the process phase:

```
library(tidyverse)
library(readr)
library(dplyr)
library(tidyr)
library(lubridate)
library(ggplot2)
library(skimr)
library(janitor)
```
After taking a look at the different datasets, I choose to work with "dailyActivity_merged" since it was the dataset with the most relevant data for each user, some of the other datasets were just repetive and were not to the point like the one mentioned above. If necesary any other important information from the other datasets can be merged to our dataframe later.

Now, we take a look of the structure of our code, so we have an idea of the data we are going to be working with:

```
head(dailyActivity_merged)
str(dailyActivity_merged)
colnames(dailyActivity_merged)
```
Those are some functions that gives us a glimpse of the structure of the data, the column names and a snippet of the entire dataset.

To ensure the integrity of the data, we are going to use the following functions to determine whether we have duplicated entries or NULL values that we need to correct.

```
sum(duplicated(mutated_dailyActivity))
sum(is.null(mutated_dailyActivity))
```
Since both code lines returned a value of 0, that means that we do not have either duplicates or NULL values in our dataset.

To conclude with this phase we are going to check how many total users are, to do this we use the following code

`dailyActivity_merged %>% group_by(Id) %>% summarize()`

Which gave us a total of 33. This does not match with the initail information given to us in the problem, since they said that there was a total of 30 users, this means that more users input information in this dataset. The reason could be more people entering data or one user using multiple IDs.
 
<h2> PROCESS PHASE: </h2>

Now, we are going to start to process the data. First of all I will include any modifications to a new dataframe, so in case I need to go back to the original information, I will always have that option.

```
mutated_dailyActivity<- dailyActivity_merged
```
I noticed earlier when examining the structure of the data, that the date format was 'chr' which doesn't correspond with the proper Date format, so we will start by correcting that.
```
mutated_dailyActivity<- dailyActivity_merged %>% mutate(Date=mdy(ActivityDate))
```
Then, I proceeded to clean the data a little bit more, by ommiting not relevant information, like the differt messurements for the distance in the same day, I will only keep the total distance, since this is a more relevant stat for the analysis.

```
mutated_dailyActivity<-mutated_dailyActivity %>% subset(select=-c(TrackerDistance))
```

Now, using the "Date" column, I'm going to create a new column that assigns the repective day of the week for that date, so when filtering and creating visualizations, we can have a better understanding of the results.

```
mutated_dailyActivity<-mutated_dailyActivity %>% mutate(Day_of_Week=wday(Date,label=TRUE))
````
Then, we are going to calculate the total ammount of days that this dataset covers.

````
 Start_and_FinishDate<-mutated_dailyActivity %>% group_by(Id) %>% summarize(Start=min(Date),Finish=max(Date),Duration=Finish-Start)
````
Then we calculate the average of all the durations of the tracking of the different users

````
Start_and_FinishDate %>% summarize(mean(Duration_Days))
````
Obatining an average of 28.25 days tracked.


Moving on now to the process step:


<h2> ANALYSIS PHASE: </h2>

<b>What tools are you choosing and why?</b>


I opted for R and spreadsheets to solve this case study, I liked the versatility of R because you can import data, clean it, process it and make your visualizations so I pretty much had anything that I needed. I also used spreadsheets because when I would summarize data in smaller tables I would move them there for ease of view and also to do some of the charts.


<b>Have you ensured data integrity?</b>


Yes, I used the common procedures to ensure integrity, like checking for null values and duplicated information.


<b>What steps have you taken to ensure that the data is clean?</b>


I made sure that each format of the dataset values would match their purpose, for example having “Double” variables for number of calories or steps taken, and having “date” variables for different dates.
Also I made sure that the daily entries were in fact daily and not repeated in the same day. I decided not to consider data that wasn’t meaningful, for example there was an user that only participated for days of the 1st week, which is not even a 25% of the total period.
I also compared the merged dataset with their particular tables to see if the information matched.
To summarize, I made sure that there was one entry per day per user, were all the different data entries were not repeated and did not contain null values.
Furthermore, I changed the respective data set structure to match the proper variable type. For example data type to “date” instead of “chr”, where one is a string of character value and the other is a date type meaning that indicates  a specific time in a year.


<b>How can you verify that your data is clean and ready to analyze?</b>


By using certain functions that allow me to do just that in R.


<b>Have you documented your cleaning process so you can review and share those results?</b>


Yes, for every chunk of code I wrote, I commented what was the purpose for it.


<b>Key tasks accomplished</b>


-Checked data for errors.
-Chose the tools.
-Transformed the data so I could work with it effectively. 
-Documented the cleaning process.




Onto to the analyze phase:

<h2> SHARE PHASE: </h2>

<b>How should you organize your data to perform analysis on it?</b>
In my case, I used the dailyActivity_merged file, created my own dataset over it and added the columns for my summary.


<b>Has your data been properly formatted?</b>
Yes, I made sure to use R functions to clean and format the data, all of this has been detailed in the code. 




<b>How will these insights help answer your business questions?</b>
By showing the trends on the users fitness data, so we can make data driven decisions for the next trackers or the mobile app.


<b>Key tasks</b>
-Aggregated the data so it’s useful and accessible
-Organized and formatted the data.
-Performed calculations.
-Identified trends and relationships.




-SHARE PHASE-




Now that the cleaning, formatting, processing and analysis of the data has been completed, we proceed to create data visualizations that will help me explain the insights and recommendations to stakeholders.

</p>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

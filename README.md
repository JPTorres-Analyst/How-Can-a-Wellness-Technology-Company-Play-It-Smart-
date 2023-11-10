# How-Can-a-Wellness-Technology-Company-Play-It-Smart-


<h2>Description</h2>
This project consists in the cleaning, processing and analysis of fitness tracking information from a dataset available in Kaggle (https://www.kaggle.com/datasets/arashnic/fitbit) to draw insights and trends shown by the users in order to help the company make data-driven decisions to improve their service.
<br/>
The dataset includes 18 different tables with data of their physical activity, their steps, the intensities, etc. That will need to be managed in order to summarize the information of the different users.
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

Since we are going to be working in R studio, we need to import the data, to do this we do the following: go to the files pane located in the right bottom corner. "3" as shown in the following image, where we can browse through our files and choose our datasets.

<img src=https://i.stack.imgur.com/bADSk.png/>

Before we start to make changes to the data, we are going to import some libraries that will help us with the process phase:

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

Which gave us a total of 33. This does not match with the initial information given to us in the problem, since they said that there was a total of 30 users, this means that more users input information in this dataset. The reason could be more people entering data or one user using multiple IDs.
 
<h2> PROCESS, ANALYZE AND SHARE PHASE: </h2>

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

Then, I will plot some of the information summarized so far to see if it is displaying in a understandable way and also to get a glance of the data.

````
ggplot(data = mutated_dailyActivity,ylim=(0:15000))+geom_col(mapping = aes(x=Day_of_Week,y=Calories,fill=fct_rev(Number_of_Week)))+facet_wrap(~Id)+scale_y_continuous(name="Calories Burned",breaks=seq(0,15000,3000),limits=c(0,15000))+labs(title="Daily Calories Burned by Every User",x="Day of Week",
+       fill="Number of Week",caption = "Data source: Fitness Tracking, Bellafit",subtitle = "In a month of use")
````

<img src=https://i.imgur.com/KOPc5EZ.png/>

As we can see in the previous image, one of the users only tracked 4 days of the first week, so I opted to discard this information since we have a total average duration of 28 days, 4 days of tracking is not representative at all. 

To drop the information of that user we use the following code:

````
mutated_dailyActivity<- mutated_dailyActivity[-c(378,379,380,381), ]
````
Now that we have all the data that we need, with no missing information and that is consistent, we proceed to summarize it to obtain meaninful trends shown by the users.

````
mutated_dailyActivity %>% group_by(Id) %>% summarize(mean(Calories), mean(TotalSteps), mean(Total_Active_Minutes))
````
This allows us to summarize the average calories burned, steps taken and total minutes of exercise per user

<img src=https://i.imgur.com/6yuGcZE.png/>

````
mutated_dailyActivity %>% group_by(Day_of_Week) %>% summarize(mean(TotalSteps))
````
The chunk above summarizes the average steps taken for each user in each day of the week. Which when plotted looks like this:

<img src=https://i.imgur.com/jttrTta.png/>


Now, another interesting trend is to see what's the day of the week when the users burn the most ammount of calories, to do this we use the following code:
````
mutated_dailyActivity %>% group_by(Day_of_Week) %>% summarize(mean(Calories))
````

When plotted it looks like this:

<img src=https://i.imgur.com/YUI1jqQ.png/>

Acconding to the charts we can say that users tend to walk more and burn the most ammount of calories on twesdays and saturdays. Then it would be interesting the correlation between these two variables. We will now plot a scatterplot that shows the correlation between the two mentioned variable:

````
ggplot(data=mutated_dailyActivity,mapping=aes(x=TotalSteps,y=Calories))+geom_point()+geom_smooth()+labs(title = "Calories Burned vs. Steps Taken ", y="Calories Burned",x="Steps Taken")
````

<img src=https://i.imgur.com/j0ZOPM3.png/>

Obtaining a possitive correlation, that means, the more steps taken then the more calories that are burned by the users.

The same can be seen when comparing the average Caloris Burned per user with the Total Active minutes of exercise:

<img src=https://i.imgur.com/4W45GON.png/>

Finally, one more important observartion in the data of all users, is to see how much of their awake time per day they spent in each phase of intensity. To do this, we are going to summarize the total active time per day and see how much percent in average each intensity contributes to the total.

To summarize all this information, we use the following code:

````
mutated_dailyActivity %>% summarize(Total_Time_of_Exercise=mean(Total_Active_Minutes),mean(VeryActive_Minutes_P100),mean(FairlyActive_Minutes_P100),mean(Lightly_Minutes_P100),mean(Sedentary_Minutes_P100))

````
If we plot this information we obtain the following chart


<img src=https://i.imgur.com/mTL6nck.png/>


<h2>Recomendations and Conclusions</h2>

It is important to mention that the population in this dataset (33 users) is not a reliable source to make meaninful asumptions or take important decisions, with a sample this small the information could be bias and not accurate to describe the entire population of costumers that use fitness devices to track their data.

Keeping this in mind and considering the worked we have done we can make the following recomendations:

1- Since we know that users tend to do more physical activity on twesdays and saturdays, it would be a great strategy to remind users the very next day (wednesdays and sundays) of the amount of activity the did the day before in order to motivate them to "keep their record" or "Keep a strike", since by doing this they can use psycology to push customers to be more active and at the same time use their fitness tracker more.

2- As we saw in the pie chart, most of their active minutes, they spend it being sedentary, so the application could have reminders that warn the users how long they have spent without exercising, or how beneficial doing some kind of exercise could be.

3- Distinguish phsycial activity not only by intensity but by type of, that is, labeling the type of training thy are doing, since by having information like this can take us to further analysis and more valuable and accurate insights.

4-Increase the dataset by requesting their existing users to track their fitness information, as we mentioned before, 33 users is not enough to entablish trends that describe the entire population of potential customers.




</p>
</p>

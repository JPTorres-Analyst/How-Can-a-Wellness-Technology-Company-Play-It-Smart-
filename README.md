# How-Can-a-Wellness-Technology-Company-Play-It-Smart-


<h2>Description</h2>
This project consists in the cleaning, processing and analysis of fitness tracking information from a dataset available in Kaggle (https://www.kaggle.com/datasets/arashnic/fitbit) to draw insights and trends shown by the users in order to help the company make data-driven decisions.
<br />


<h2>Tools Used</h2>

- <b>R Programming</b> 
- <b>Speadsheets</b>

<p>
 
<h2> ASK PHASE: </h2>
<b>What is the question we are trying to solve?</b>

What are meaningful insights for the company by analyzing existing fitness tracking in order to improve their service to customers.


<b>How can your insights drive business decisions?</b>

By pointing at trends and existing aspects that users already show with their data. By doing this the company has a ground to either improve their products or use it as a guide to better assist their customers.


<b>Business task</b>

Provide insights from existing fitness tracking devices data in order to improve Bellabeats products.

<b>Key stakeholders</b>

-Urska Srsen, cofounder and Chief Officer
-Sando Mur, mathematician and Bellabeat’s cofounder.



<FONT COLOR="RED">Moving on to the next phase:</FONT>

<h2> PREPARE PHASE: </h2>

<b>Where is the data stored?</b>

The data is stored in a dataset available in the platform Kaggle.

<b>How is the data organized? Is it long or wide format?</b>

The data is divided in many tables where you find both formats, wide and long.

<b>Are there issues with bias or credibility in this data?</b>

Yes, there are many factors we can worry about here, in the following images I’ll show some of the concerns.
By the way, I’ll be using ROCCC system to verify its bias and credibility.

R: Reliable
O: Original
C: Comprehensive
C: Current
C: Cited

In terms of reliability, I would say it is medium, because some of the information provided does not match the data, for example it said that the data belong to 30 different users, and when it’s verified we encounter 33 different users in the list.

Furthermore I don’t consider 30 or 33 to be a meaningful number of users to gather information from and then build a new product or make changes to existing products, I think the sample is just way too small.



As we can see in the picture, when we use R, to count all the different IDs, belonging to the different users we obtain a total of 33 different IDs. meaning that there may be repeated users with different IDs.

When it comes to originality, I would score it medium, because it was obtained from a fitness tracking website, so it is not first party but still is understandable, a lot of times companies need to do this before they launch a product.

In terms of how comprehensive it is, I would say it was moderately organized, since some of the tables were properly merged and the data in it was easy to pick up, but there were some other tables where you would take a while to interpret it.










When it comes to how updated the data is, then it gets a very low score, because it is not current at all, we are working with data from 2016.





And finally the data was cited, is is from the a tracking database named….


		 	 	 		
<h2> PROCESS PHASE: </h2>
				
<b>How are you addressing licensing, privacy, security, and accessibility? </b>


This is not something I really paid too much attention too because the source of the information is public dataset, so anybody can access it, besides there is not sensitive information that can be displayed. 


<b>How did you verify the data’s integrity?</b>


By making sure there were no null values or repeated values in the datasets I was working with.


<b>How does it help answer you question? </b>


By taking me to the right results, since if the data was duplicated the results would be inaccurate and wouldn’t represent in a proper way the population that I’m studying.
This is a really important step before starting to process the data.


<b>Are there any problems with the data?</b>


I have found some problems regarding the structure of the data, for example I couldn’t obtain the day of the week with the date columns of the datasets, and this was because it was stored as a character instead of a “date value”. Also the problem that I mentioned earlier, when I specify that the total users were 33 instead or 30 and lastly there were some users that didn’t track enough data for it to be meaningful for the study, so I decided to erase those records to have a more accurate result.


Key tasks accomplished


Download data and store it appropriately.
Identify how it’s organized.
Sort and filter data.
Determine the credibility of data.




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

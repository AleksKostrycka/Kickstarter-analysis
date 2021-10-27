# Kickstarting with Excel - Campaign Outcomes 

## Overview of Project
This project is designed to illustrate historical performance of theatrical fundraising campaings, as it relates to the timing of the launch of the campaign and the size of the fundraising goal, in order to more accurately make decisions and design future theatrical campaings. The below sections will explain the purpose, analysis and challanges, as well as the results of the project performed.
### Purpose
There are ultimetly two questions this analysis is trying to answer. First, identify the correlation between the time of the year that a theater campain is launched and the success of that campain. This will illustrate what is the best month to create a theater campaign to unlock the greatest level of success. Second, identify the correlation between the size of the campaign's fundraising goal and its success. This will enable the creator to design a theatrical perfomace with a realistic goal to make it successful.
## Analysis and Challenges
In this section we will describe how the analysis was performed and any challanges that we encountered and overcame to complete the project.
### Analysis of Outcomes Based on Launch Date
The purpose of this analysis is to create a correlation between the month the theater campaign is launched and its success. First, we needed to create a new column within the dataset that extracted the year from the date (mm/dd/yy) of the campaign launch. This was completed by using the function `YEAR()` with a reference to the Date Created Conversion column. Then a Pivot table was created using the Insert Pivot Table option in a new worksheet, titled Theater Outomes by Launch Date. This pivot was then designed to illustrate the MONTHS that the campaign was launched using the ROW section of the Pivot, the COUNT of successful, failed, and canceled campaigns using the columns and values sections of the Pivot, and adding filters to isolate the Parent Category, theater, and year. The pivot table shown below: 

![This is an image](https://github.com/AleksKostrycka/Kickstarter-analysis/blob/main/Theater%20Outcomes%20by%20Launch%20Date.png?raw=true)

In the Pivot table you can see how many total theatrical campaings were started in a given month, regardless of year of the campaign. Further you can see the count of successful, failed and canceled campaings that were launched in a given month. Just from looking at the data table above you can already see that by far the most successful campaigns were launched in May and June. However, looking at numbers on a pivot able can prove to be diffucult as this can be overwhelming and confusing. Therefore visualizing this information in a graph format proved to be a much easier way to digest the information and come up with conclusions. The graph was created by hilighting the pivot table data, using the Insert tab and choosing the Line graph option in Excel. This created the visualization below:

![This is an image](https://github.com/AleksKostrycka/Kickstarter-analysis/blob/main/Theater_Outcomes_vs_Launch.png?raw=true)

After creating this visualization that has MONTHS on the x-axis, and the number of campaings on the y-axis we are able to graph 3 individual lines to represent the number of successful, failed and canceled theater campaings launched in a given month. This is designed to tell us which month a campaing can be launched that will have the greatest chance of success based on the historical data presented. From looking at the graph the greatest number of successful campaings were launched between April - August. 

### Analysis of Outcomes Based on Goals
The purpose of the second analysis was to create a correlation between the size of the fundraising goal and campaign's success, specifically focusing on theatrical play campaings. First we created a new table in a new sheet that was titled Outcomes Based on Goals. This table was designed to group fundraising goals on a scale to organize the number of successful, failed and canceled campaings on the goal scale. See table below for the outcome of the exercise. 

![This is an image](https://github.com/AleksKostrycka/Kickstarter-analysis/blob/main/Outcomes%20based%20on%20Goals%20Table%20.png?raw=true)

This table was completed largely by using the `COUNTIFS` function in Excel. This function allows the user to count the number of outcomes based on ranges and a specific critetria. We are able to connect this table to the original Kickstarter dataset to summarize the data in a specific way. In the next section we will explain the details of how the formula was written to perform this analysis and create this table. 

#### Formulas Used
The `COUNTIFS` function in excel enables us to perform this anlysis by creating formulas to count the number of successful, failed and canceled outcomes within a specific fundraising goal range focusing only on theatrical plays. 

First we needed to COUNT how many successful outcomes are there in the data set 

`COUNTIFS(KICKSTARTER!$F:$F,"successful")`

The above will give you the total number of successful campaigns in the data set, we needed to add additional range and criteria to further filter the outcomes. To be able to group the outcomes to only focus on a specific range of the fundrasing goal we added the follwing: 

`COUNTIFS(KICKSTARTER!$D:$D,"<1000"`)

Now we are able to identify the count of successful campaigns for a specific fundraising goal range, in this case less than 1,000. Still we are showing the number of total successful campaings which have fundraising goals of less than $1,000. We need to further filter the data to determine the number of successful campaings with a fundraising goal of less than $1,000 that are only theatrical plays.

`COUNTIFS(KICKSTARTED!$R:$R, "plays"` 

This will result in the outcome that focused on theatrical play campagins in the data set.

The entire function will be displayed as: 

`COUNTIFS(Kickstarter!$F:$F,"successful",Kickstarter!$D:$D,"<1000",Kickstarter!$R:$R,"plays")`

This is then applied to all other types of outcomes such as "failed" and "canceled". While this formula worked for the less than $1,000 fundraising goal and greater then $50,000 goal, we needed to adjust the formula slightly to caputre the ranges of the other goals outlined. Below we will ilustrate how to write the `COUNTIFS` function that satisfys all the filters above and the fundraising goal as a range of numbers such as equal to or greater than $1,000 and equal to or less then $4,999. 

The begining and end of the `COUNTIFS` forumla described above does not change for this range, the only part of the formula that will change is the `COUNTIFS(KICKSTARTER!$D:$D,"<1000"`). Fore Excel to be ablle to count the number of outcomes with goals between a specific range the forumala must include the following:

`COUNTFS(Kickstarter!$D:$D,">=1000",Kickstarter!$D:$D,"<=4999"`

The above tells Excel to only look for outcomes that have a fundraising goal of greater or equal to $1,000 and less than of equal to $4,999. The final formula to count the number theatrical plays with a successful outcome within a fundraising goal of greater than or equal to $1000 and less than of equal to $4,999 is:

`COUNTIFS(Kickstarter!$F:$F,"successful",Kickstarter!$D:$D,">=1000",Kickstarter!$D:$D,"<=4999",Kickstarter!$R:$R,"plays")`

This formula can now be manipulated to filter for failed and canceled campaigns as well as the different ranges outlined in the data table above. 

Total Number of Projects was derived from the use of the `SUM` function across the different outcomes (successful, failed and canceled) for reach goal range:

`SUM(B2:D2)`

The Percentage of Successful, Failed and Canceled outcomes was created by using the below function to divide the number of successful (failed or canceled) campaings by the total number of campaings in the specific goal range. This could answer the question: "What is the percetange of successful campaings that had a goal of less than $1,000?"

`ROUND(B2/E2,2)`

The answer to the question above is 76%. Meaning that 76% of theatrical play campaings with a fundraisng goal of less than $1,000 were successful. This is repeated by using the number of failed and canceled campaings over the total capmaings within the goal range. `ROUND` helps to specify how exact do we want the answer to be - with 2 decimal points .76 translates to 76%.

#### Analysis of Outcomes Based on Goals Visualization
As stated in the first analysis, the table alone can be cumbersome to read and interpert to be able to fully analyze the data. Therefore a visualization must be created to be able to easily identify the trends within this data set. The graph below was created by hilighting the Goal Column (A) as well as the Percentage of Successful, Percetange of Failed, and Percentage of Canceled outcomes, Columns (F, G & H). Then, using the Insert tab within Excel and choosing the line graph function. 

![This is an image](https://ucb.bootcampcontent.com/alekskostrycka-EYIWpz/kickstarter-analysis/-/raw/main/Outcomes_vs_Goals.png)

After creating this visualization we can see the range of fundraising goals on the x-axis and the percentage of outcomes on the y-axis. We can map the percentage of successful  outcomes and percentage of failed outcomes based on the fundraising goal. We can interpert the line graph and determine historically what size fundraising goal campaings were frequently successful in the theatrical play landscape. For the fundraising goal of equal to or greater than $1,000 and less than of equal to $4,999 - 73% were successful and 27% failed. Therfore if we are looking to design a play with the fundraising goal with in that range, we have histrocial data that tells us there is a 73% success rate for that range.

There were no Cancled plays in the dataset. 

### Challenges and Difficulties Encountered
We came across 2 main challanges while preparing this project, both challanges were in the Outcomes based on Goals Analysis section. 

One of the main challanges that we were faced with in this dataset is combining the COUNTIFS formulas to appropirately filter the data to show outcomes that we are interested in. The first goal of ">1,000" was quite simple as this was just added as another criteria to the goal range in the function. However the diffuclty was increased when the goal became a range. This took the function an extra step further to be able to define the range of the goal. The "HINT" within the challange outline was able to illustrate how to write the `COUNIFS` function to be able to caputre the range. We learned that the range and criteria will need to be repeated twice in the forumla with two separate specifications to filter the data for the specific goal range. This was then applied to all the different outcomes and ranges. 

The second challange that we faced in the preparation of this analysis was to be able to caputre the "equal to" portion of each goal range. First time through the `COUNTIFS` function did not specify the "equal to" portion of the ranges and the graph was missing information. This was realized by comparing the result to the expectation in the challange description. This was fixed by adding "=" to each section of the range to include the "equal to" language in the forumla. 

## Results

**- What are two conclusions you can draw about the Outcomes based on Launch Date?**

The first conclusion that can be drawn from the Outcomes based on Launch Data Analysis is that historically the greatest number of sucessful campaigns were launched between April and August. Therefore if someone is designing a theatrical campaign the best launch timeframe to consider should be with in those months. Said another way, out of 839 total sucessful theatrical campaigns 441 were launched between April and August, that is a little over 50%. In conclusion, there is a greater percetange chance to have a successful theatrical campaign if the launch date is within the months of April - August. 
The second conclusion that can be drawn from the analisys is that October is not an ideal month to launch a campaign. While the failed campaign outcomes are significantly lower than the succesful outcomes, the rate of failed outcomes closely follows the rate of successful outcomes relative to the total number of campaigns launched within the month. It stands to reason that because May has the highest total campaign launches it will have the highest rate of successful campaings, and the highest rate of failed campaigns, just purely based on volume. However in October the volume of campaigns launched is significatly lower, the total campaings is 115, the rate is 65 successful and 50 failed. This tells us that in October 57% of campaigns were successful but 47% failed. Comparing to May which has a total of 166 campaings, 67% successful, 31% failed and 2% canceled. Therefore a conclusion that can be made based on histroical data is that October is not an ideal month to launch a campaign. 

**- What can you conclude about the Outcomes based on Goals?**

One conclusion that can be drawn from the Outcomes based on Goals Analysis is that the greatest success rate for theatrical play campaings are those with the smallest fundraising goals. Out of a total of 186 projects which have a fundraising goal of less than $1000 the success rate is 76%. Comparing that with the next range of fundraising goals, between $1000 and $4999 the rate of success on 534 projects is 73%. Therefore while looking purely on the rate of successful projects for a specific fundraising goal, the smaller the goal the greater chance of success. 

**- What are some limitations of this dataset?**

One limitation of this dataset is the relative size of the total projects within a specific fundraising goal. Looking at the percentage of successfull, failed and canceled projects in a vacumm can be misleading while not considering the total number of campaigns within the goal range. For example within the $35,000 to $39,999 range there is a 67% success rate, however there are only 6 total projects in the range. It can be dervied that the $35,000 to $39,999 goal range is more successful than the $5,000 to $9,999 goal range that only has a success rate of 57%. However the number of projects in the higher range is significantly lower, 6 projects and 169 project respectivelly. This is not clear in the visualization created by the line graph.   

**- What are some other possible tables and/or graphs that we could create?**

One solution that can be added to the chart is the Weighted Average of successful, failed and canceled outcomes. This will provide a percenage that is more clear relative to the total number of projects in the range. This will put a significantly higher weight on ranges that have a higher number of projects versus those goal ranges that have only a handful of total projects. This can then be used to create another line graph that will show the Weighted Averege outcomes based on Goals. 
Another solution can be to add a bar graph to the chart that has the total number of projects within the goal range. The user can then quickly identify the goal range and the total number of projects within each goal range and see the percentage of successful and failed  projects relative to the total, which will create a much more inslightful picture of the dataset. 

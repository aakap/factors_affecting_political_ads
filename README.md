# factors_affecting_political_ads
This project looks at how spending, paying organization, and window of air-time affects the number of impressions of political ads in 2018 on Snapchat. 

## Background
Snapchat, a social media platform most popular with [18-24 year olds](https://info.lse.ac.uk/staff/divisions/communications-division/digital-communications-team/assets/documents/guides/A-Guide-To-Social-Media-Platforms-and-Demographics.pdf), first started hosting advertisements in October 2014. With [301 million monthly active users](https://info.lse.ac.uk/staff/divisions/communications-division/digital-communications-team/assets/documents/guides/A-Guide-To-Social-Media-Platforms-and-Demographics.pdf) each spending an average of 30 minutes on the platform per day, Snapchat's platform provides a unique opportunity for advertisers to target this specific younger demographic, especially in North America where the app is used most. In the last few years, there has been a political movement to engage younger voters and turn the tide on voter apathy. Only [43%](https://ourworldindata.org/usa-electoral-turnout) of young voters (aged 30 and younger) voted in the 2016 election. The accesibility of social media platforms with younger user bases such as Snapchat, TikTok, and Instagram, have all played rolls in helping to reverse this trend as [53%](https://www.vox.com/2020/11/7/21552248/youth-vote-2020-georgia-biden-covid-19-racism-climate-change) of young voters cast ballots in the 2020 presidential election. Knowing how to leverage these social media platforms to reach the most people with political advertisements is an increasingly important issue as political campaigns and nonprofits work towards engaging young people in voting. 

## Business Question
Overarching question: **What logistical factors improve number of impressions for political ads on Snapchat?**
Specific question examined: **How does ad spending, length of air-time, and paying organization type effect number of impressions for political ads on Snapchat?**

## Data Exploration
To explore this question, I used data provided by [Snapchat](https://www.snap.com/en-US/political-ads) to find information on impressions, paying organization, spending, and air-time for political ads in 2018. The raw data files are in the repository. After manipulating the raw data (as explained in the Data Analysis section), I ran a simple linear regression between spending and impressions and air-time and impressions, the two variables that appear most obviously related (Figure 1) and then ran a multivariate regression on all three factors with the dependent variable being impressions (Table 1). Paying organization was insignificant, so I re-ran the regression excluding that as shown in Table 2 to generate an equation predicting impressions. 


#### *Figure 1*
![](figure.png)
#### *Table 1*
![](table1.png)
#### *Table 2*
![](table2.png)

## Results and Discussion
Figure 1 shows a positive correlation between spending and number of impressions. However, the R-squared value of 0.75 indicates a weak-medium linear correlation so even though spending can help explain the number of impressions, it is not the only factor. Based on this graph, the predicted equation is impressions = 261.3(_spending_) + 16292. Adding more factors into the picture, Table 1 shows that whether or not the organization is political does not significantly affect impressions as the p-value is greater than 0.05. Excluding this independent variable, the re-run in Table 2 shows both spending and length of duration are signficant (p<0.05) and positively correlate with impressions with a predictor equation of impressions = 259(_spending_) + 3603(_length_) -35076. The F-statistic is also signficant, as reflected in the p-value. 

These results show that spending and length of duration positively correlate with the number of impressions while whether the organization is political does not signficantly impact impressions. This information can be used to help candidates spread out the burden of advertising to non-affiliated organizations who champion their policies. At the same time, the information is helpful is seeing how to fine-tune dollars spent and days advertised to maximize impressions for certain ads. The information is more helpful for the political candidates and ad-organizations, but Snapchat can use the information to decide how long to run ads and what price to charge. It is important to realize that with an R-squared of 0.75, the correlation is not robustly linear and the predicting equations should be used only as rough models. 

However, this model does not consider all the logistical factors involved in political advertisement impressions. Other factors that may improve impressions include length of ad itself, type of ad (sensational, dramatic, etc.), producer, and content based on what age-group is seeing the ad. There are also confounding factors that affect impressions such as virality. Some political ads and videos can go viral on platforms like Snapchat because of algorithms and a human irrationality factor that is difficult to model. Political organizations would benefit from further studies that involve these factors as well as studies that compare the same factors from Snapchat as those from Instagram and Facebook to best see how to leverage each platform to encourage young voter turnout. 


## Data Analysis:
To process the data I used the following steps:
1. Filter currency to only display USD with GUI-based Filter function
2. Use "Find and Replace" GUI to remove "z" from all Date-Time columns and replace with a blank space
3. Use INT(Col, "d") function to convert Date-Time columns into Date only 
4. Take difference between start date and end date after the dates are converted into date only to dislpay number of days the ad ran for
5. Use UNIQUE function on OrganizationName column to get list of individual organizations without repetition
6. From filtered list, manually determine which organizations were directly tied to a political candidate vs which organizations were independent and grassroots 
7. Use IF function to add "1" to Is Org Political column if the OrganizationName column matched any of the organizations pre-determined as political. Else add "0"
8. Generate scatterplot of Impressions vs Spending and add line of best fit (linear) with R-squared value
9. Use Data Analysis ToolPak to generate multivariate regression with Impressions as the y-variable and Length, Spending, and Is Org Political as the x-variables
10. Find which independent variables had p values that were significant (<0.05) and re-run regression on all variables that were signficant 
11. Analyze findings 

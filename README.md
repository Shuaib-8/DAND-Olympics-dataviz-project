### Date created for project and README Files

Created on: `29/10/19`

***
### Project Title

**Olympics Data (1896-2016) Exploration**
***
## Dataset

This is a historical dataset on the modern Olympic Games, including all the Games from Athens 1896 to Rio 2016. These include basic biographical data on athletes (Age, Height, Sex and Weight) and medal results. Both Seasons, Summer and Winter, are included.
There were 271,116 observations (rows) about athletes surrounding the biographical data. Each row corresponds to an individual athlete competing in an individual Olympic event (athlete-events).
The dataset can be found on Kaggle. The data was scraped from [sport-reference](https://www.sports-reference.com) by the user **rgriffin**, which is made available on [kaggle](https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results). There are also kernels with relevant documentation and examples.

Despite prior scraping and wrangling, there were inconsistencies I needed to correct to make this analysis functional. These included:
* Null values - **Age, Weight and Height** information were *not* able to be recorded at times.
For the **Medal** (ordinal) category, missing medals were there to signify standard competitors (None) rather than NAN as not everyone that competed qualified for a medal.
* Misspelled Host City names - instances included Athina to Athens and Sankt Moritz to St. Moritz.
* Data types - Medal (ordinal), Sex and Season (nominal) should have been classed as categories rather than the default strings when imported.
M and F should be fully spelled out to represent Male and Female respectively.
* Missing observations that were related between two tables that anticipated a left join - Athletes information should be preserved while connecting the National Olympic Committee (NOC) - the joining key - table for each Team that also identifies the region. Additionally, this meant additional cleaning to make sure **all** the regions were accounted for. Singapore had 5 different team names under the same NOC, which needed to be updated along with others.

___Data Dictionary___

Taking the cleaned dataset **olympics-master.csv**, these are the columns that were available for analysis. You can see this [here](<https://docs.google.com/spreadsheets/d/1uxtOJlmtZoJeuFNiVbE_RFvUw1tiMeS6f9oUWy_6t8Y/edit?usp=sharing>) based on my evaluations of the most important factors that needed to be clean for data visualisation.

* __ID__ - Unique number for each athlete to be tracked, be it at a single Olympics year or across multiple editions.
* __Name__ - Athlete's name
* __Sex__ - Male and Female
* __Age__ - Integer
* __Height__ - In centimetres (cm)
* __Weight__ - In kilograms (kg)
* __Team__ - Team name
* __NOC__ - National Olympic Committee 3-letter code
* __Games__ - Year and season
* __Year__ - Integer
* __Season__ - Summer or Winter
* __City__ - Host city
* __Sport__ - Sport
* __Event__ - Event
* __Medal__ - Gold, Silver, Bronze and None (standard competitors)


## Summary of Findings

___Univariate Exploration___

Starting from my univariate exploration, the Weight variable took on a large range of values (25-214 kg).

* Weight (kg) - I used a log transformation given that Weight in its original form illustrated a log-normal type of distribution, which appeared more centred and less (positive/right) skewed after transformation while retaining the unimodal shape.
* Most athletes are grouped in the weight range of around 60-75 Kg.
* There were upper limit outliers for Weight, but I had taken this into consideration as not being erroneous, given explosive sports that tended to have athletes weighing well above the average for their respective events. Hence, the log transformation as above was enough to alleviate this issue.

___Bivariate Exploration___

Additionally, through my bivariate exploration, upon visualising a fitted scatter/regression plot (`regplot`), I found that:
* the conventional positive correlation between Weight and Height is also observed among Olympic athletes, with a correlation coefficient of 0.8 that is also made to fit more linearly via a logarithmic scale for Weight.
* Looking further at the distribution through box and violin plots, there was much less variation and higher medians in terms of the personal attributes shown for medalists then for standard competitors, but we have to consider that standard competitors were part of a bigger sample size compared to medalists which part of a subset.
* Uncovering trends between medals and events   
    * Summer Olympics -  Athletics, Swimming and Gymnastics tend to be among the top three sports Athletes compete respectively, regardless of winning a medal or as a standard competitor.
    * Winter events - the top three events undertaken by standard competitors, Cross Country Skiing, Alpine Skiing and Speed Skating respectively, do not correspond to the order that Athletes earn medals in each category, as Ice Hockey, Cross Country Skiing and Speed Skating respectively represent the most medals earned in each Sport. Hence, we cannot infer a correlation of some sorts between the most common sport events that standards Athletes compete and the number of medals Athletes earn from each Sport.
    * The results and the corresponding visualisation were hard to interpret, as the bars were very thinly space that doesn't suit static visualisations. Interactive visualisations (beyond the scope of this project) would've been useful in this case. Hence, I decided as part of my final Bivariate showcase that this would not be included in the explanatory phase/presentation.
* Lastly from my Bivariate exploration, I tried to discern the phenomena of a Host City/Country performing well when its their turn to host once every four years. This is mostly the case for the
    * Summer Olympics - This is mostly the case especially during the early years between 1900-1920. It gradually declined and this significant advantage only appeared sporadically afterwards, during 1956 (Melbourne) and 1988 (Seoul).
    * Winter Olympics - This trend was not as clear for the Winter version (relative to Summer), but had a similar early advantage between 1928-1948 and afterwards tapered off, where only in 1984 (Yugoslavia) was there a close enough significant effect to early years.
    * Hence, there is empirical evidence to support this statement in some cases, but it is not consistent/significant enough to certify a relationship with being a host and excelling at the Olympics for countries.

___Multivariate Exploration___


Finally from my multivariate exploration, extending from the Height and Weight relationship, I utilised a scatter plot to see how Age varies with respect to these two variables.
* Given much variability, it turns out that the only interesting interaction of Age between Height and Weight is that athletes who are are aged less than 20 years are mostly grouped in the lower range of Height and Weight i.e. less than 150 cm and 40 kg. Hence, this wasn't included in the explanatory phase/presentation.
* Examining further on personal attributes among athletes, I utilised the median to estimate further among medalists (with standard competitors) by Sex. The analysis confirms that Males tend to be heavier, taller and *slightly* older than their Female counterparts.


## Key Insights for Presentation

___Univariate Analysis___

I focus mainly on:

* Participation proportions/counts.
* Performance (medals proportions/counts) in the Olympics by medal winners and standard competitors.

I start by introducing the proportion of Male and Female athletes competing at the Olympics, followed by the the proportion of Olympic events by season. I finish off the univariate analysis by finding out the different proportions between standard competitors and medalists and then by the medals earned exclusively through pie charts.

___Bivariate Analysis___

Moving to the bivariate analysis, I then start looking at the relationships between:

* Numeric variables - surrounding personal attributes via Weight on Height through a fitted (linear model) estimated regression with Weight defined by a log scale.  
    * This is further complemented by a `Histogram (Hist2d) Heatmap`, which shows the density of groupings for athletes by Weight (log scale) and Height.
* This is followed by illustrating descriptive statistics and analysis of the distribution of personal attributes athletes exhibited when competing via the `violinplot`, uncovering summary statistics like the median Height, Age and Weight for athletes by each medal group (standard competitors i.e. None or medalists).
* The bivariate analysis is closed via the analysis of average medals earned based on different Host cities for each Season of the Olympics over time. This data set contains Summer Olympic events between Athens 1896 to Rio de Janiero 2016, while the Winter Olympic events are listed from Chamonix 1924 to Sochi 2014. This was visualised to search for the so-called 'Host advantage'.

___Multivariate Analysis___

Finally, the presentation ends through the multivariate analysis, which uncovers the median estimates of personal attributes - Age, Height and Weight - categorised both by medalists and sex.

The visual encodings I considered to use when polishing my plots:
* Titles, x and y labels - use of bold text via `font weight`
- Annotations - used for clarity, especially when illustrating proportions precisely, while quickly showing summary statistics like the correlation coefficient. These also include legends to distinguish by categories and the way quartiles are shown through the violinplot.
- Colour - for significance such as depicting the colours of medals when presenting the pie chart. Also considering the right colour palette in case of colour blind viewers as in the personal attributes analysed among two categories, along with different shadings to determine hotspots among the heatmap.

### Feedback

I would like to thank my peers/mentor for all the observations, commendations and recommendations, mainly what to include and exclude for my explanatory presentation.

### References

Beyond my Udacity mentor, peers and lectures, I consulted a number of resources including:

* [DataCamp - Introduction to Data Visualization with Python](<https://www.datacamp.com/courses/introduction-to-data-visualization-with-python>)
* [DataCamp - Manipulating DataFrames with pandas](<https://www.datacamp.com/courses/manipulating-dataframes-with-pandas>)
    * This tutorial was very useful, as it provided a case study/example to follow and utilise for my analysis by building a host DataFrame for Olympic host cities using a similar Olympics dataset. This allowed me to answer whether there was a host advantage over various editions. See chapter 5.
* [Medium - 5 Quick and Easy Data Visualizations in Python with Code](<https://towardsdatascience.com/5-quick-and-easy-data-visualizations-in-python-with-code-a2284bae952f>)
* [VanderPlas (2016) - Python Data Science Handbook, see chapter 4](<https://jakevdp.github.io/PythonDataScienceHandbook/>)
*  [McKinney (2017) - Python for Data Analysis 2e, see chapter 9](https://wesmckinney.com/pages/book.html)

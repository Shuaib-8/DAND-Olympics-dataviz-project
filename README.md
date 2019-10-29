### Date created for project and README Files

Created on: `29/10/19`

# Olympics Data (1896-2016) Exploration
## By Shuaib Ahmed


## Dataset

This is a Historical dataset on the modern Olympic Games, including all the Games from Athens 1896 to Rio 2016. These include basic biographical data on athletes (Age, Height, Sex and Weight) and medal results. Both Seasons, Summer and Winter, are included.
There were 271,116 observations (rows) about athletes surrounding the biographical data. Each row corresponds to an individual athlete competing in an individual Olympic event (athlete-events).
The dataset can be found on Kaggle. The data was scraped from [sport-reference](https://www.sports-reference.com) by the user **rgriffin**, which is made available on [kaggle](https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results). There are also kernels with relevant documentation and examples.

Despite prior scraping and wrangling, there were inconsistencies I needed to correct to make this analysis functional. These included:
* Null values - **Age, Weight and Height** information were not able to recorded at times.
For the **Medal** (ordinal) category, missing medals were there to signify standard competitors (None) rather than NAN as not everyone that competed qualified for a medal.
* Misspelled Host City names - instances included Athina to Athens and Sankt Moritz to St. Moritz.
* Data types - Medal (ordinal), Sex and Season (nominal) should have been classed as categories rather than the default strings when imported.
M and F should be fully spelled out to represent Male and Female respectively.
* Missing observations that were related between two tables that anticipated a left join - Athletes information should be preserved while connecting the National Olympic Committee (NOC) - the joining key - table for each Team that also identifies the region. Additionally, this meant additional cleaning to make sure **all** the regions were accounted for. Singapore had 5 different team names under the same NOC, which needed to be updated along with others.


## Summary of Findings

Starting from my univariate exploration, the Weight variable took on a large range of values(25-214 kg), to which I used a log transformation for a log-normal type of distribution in its original form, which appeared more centred and less (positive/right) skewed after transformation while retaining the unimodal shape. Most athletes are grouped in the weight range of around 60-75 Kg.
There were upper limit outliers for Weight, but I had to take this into consideration as not being erroneous, given explosive sports that tended to have athletes weighing well above the average for their respective events. Hence, the log transformation as above was enough to alleviate this issue.

Additionally, through my bivariate exploration, upon visualising a fitted scatter/regression plot (`regplot`), I found that the conventional positive correlation between Weight and Height is also observed among Olympic athletes, with a correlation coefficient of 0.8 that is also made to fit more linearly via a logarithmic scale for Weight.
Looking further at the distribution through box and violin plots, there was much less variation and higher medians in terms of the personal attributes shown for medalists then for standard competitors, but we have to consider that standard competitors were part of a bigger sample size compared to medalists which part of a subset.
Uncovering trends between medals and events starting from the Summer Olympics, Athletics, Swimming and Gymnastics tend to be among the top three sports Athletes compete respectively, regardless of winning a medal or as a standard competitor. However, looking at Winter events, the top three events undertaken by standard competitors - Cross Country Skiing, Alpine Skiing and Speed Skating respectively - do not correspond to the order that Athletes earn medals in each category, as Ice Hockey, Cross Country Skiing and Speed Skating respectively represent the most medals earned in each Sport. Hence, we cannot infer a correlation of some sorts between the most common sport events that standards Athletes compete and the number of medals Athletes earn from each Sport. The results and the corresponding visualisation were hard to interpret, as the bars were very thinly space that doesn't suit static visualisations. Interactive visualisations (beyond the scope of this project) would've been useful in this case. Hence, I decided as part of my final Bivariate showcase that this would not be included in the explanatory phase/presentation.
Lastly from my Bivariate exploration, I tried to discern the phenomena of a Host City/Country performing well when its their turn to host once every four years. This is mostly the case for the Summer Olympics, especially during the early years between 1900-1920. It gradually declined and this significant advantage only appeared sporadically afterwards, during 1956 (Melbourne) and 1988 (Seoul). This trend was not too supported in the Winter Olympics (relative to Summer), but had a similar early advantage between 1928-1948 and afterwards tapered off, where only in 1984 (Yugoslavia) was there a close enough significant effect to early years. Hence, there is empirical evidence to support this statement in some cases, but it is not consistent/significant enough to certify a relationship with being a host and excelling at the Olympics for countries.

Finally from my multivariate exploration, extending from the Height and Weight relationship, I utilised a scatter plot to see how Age varies with respect to these two variables. Given much variability, it turns out that the only interesting interaction of Age between Height and Weight is that athletes who are are aged less than 20 years are mostly grouped in the lower range of Height and Weight i.e. less than 150 cm and 40 kg. Hence, this wasn't included in the explanatory phase/presentation.
Dissecting further on attributes groups for athletes, I utilised the median to estimate further among medalists (with standard competitors) by Sex. The analysis confirms that Males tend to be heavier, taller and *slightly* older than their Female counterparts.


## Key Insights for Presentation

For the presentation, I focus mainly on the participation proportions/counts, personal attributes of athletes and performance (medals counts) in the Olympics over time only for host cities/countries - not entirely focussed on the dynamics between athletes by Sex or Season of the events when it comes to medal performance per se.
I start by introducing the proportion of Male and Female athletes competing at the Olympics, followed by the the proportion of Olympic events by season. I finish off the proportion (univariate) analysis by finding out the different proportions between standard competitors and medalists and then by the medals earned exclusively through pie charts.
Moving to the Bivariate analysis, I then start looking at the relationships between the numeric variables surrounding personal attributes via Weight on Height through a fitted (linear model) estimated regression with Weight defined by a log scale. This is further complemented by a `Histogram (Hist2d) Heatmap`, which shows the density of groupings for athletes by Weight (log scale) and Height. This is followed by illustrating descriptive statistics and analysis of the distribution of personal attributes athletes exhibited when competing via the `violinplot`, uncovering summary statistics like the median Height, Age and Weight for athletes by each medal group (standard competitors i.e. None or medalists). The bivariate analysis is closed via the analysis of average medals earned based on different Host cities for each Season of the Olympics. The Summer Olympic events ran from Athens 1896 to Rio de Janiero 2016. The Winter Olympic events ran from Chamonix 1924 to Sochi 2014. This was visualised to search for the so-called 'Host advantage'.
Finally, the presentation ends through the multivariate analysis, which uncovers the median estimates of personal attributes - Age, Height and Weight - categorised both by medalists and sex.

The visual encodings I considered to use when polishing my plots:
* Titles, x and y labels - use of bold text via `font weight`
- Annotations - used for clarity, especially when illustrating proportions precisely, while quickly showing summary statistics like the correlation coefficient. These also include legends to distinguish by categories and the way quartiles are shown through the violinplot
- Colour - for significance such as depicting the colours of medals when presenting the pie chart. Also considering the right colour palette in case of colour blind viewers as in the personal attributes analysed among two categories, along with different shadings to determine hotspots among the Heatmap.

## Feedback

I would like to thank my peers/mentor for all the observations, commendations and recommendations, mainly what to include and exclude for my explanatory presentation.

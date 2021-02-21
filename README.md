# Group-Project-05

**Group Project 5: Michael, Josh, Yunus**

**Software Requirements:**
-Pandas
-Numpy
-Matplotlib
-Seaborn

-Scikit-learn
    -KMeans
    -DBSCAN
    -StandardScaler
    
## Table of Contents:

For our audience, please begin by examining our ReadMe and read the Introduction, Problem Statement, and Background to familiarize yourselves with the design and focus of our project. Then refer to the below ordered notebooks (01-Data-Cleaning-EDA.ipynb &    02-Modeling-DBSCAN-KMeans.ipynb). Then you should be able to proceed with the remaining sections of our Readme detailing our process, and finally our Executive Summary/Recommendations can be found at the bottom of our Readme file.   

Notebooks:
-01-Data-Cleaning-EDA.ipynb
-02-Modeling-DBSCAN-KMeans.ipynb
Executive Summary:
-README.md (found at the end)
Data:
-Socioeconomic Data
    -socioeconomic determinant for state.csv
-csse_covid_19_daily_reports_us
    -12-31-2020.csv
-unemployment_rate
    -unemployment_all_states_2020.csv
    -un_r_mean_distance.csv
    -{states}2020.xlsx
-various created datasets
    -yun_data
Presentation:
-mitigating_pandemic_effects.pptx,.pdf
Assets:
-various jpgs



### Introduction:

Our group will be presenting to a collection of policy makers regarding the response and current effects involving the recent Coivd-19 pandemic. Due to the many unknown factors of the virus, agencies have struggled with developing an adequate approach to combating the virus. That is why our group has been approached to help analyze the current year end data relating to both the virus and the impact it has had across country & statewide socioeconomic factors. The agency was made aware of an article put out by the cdc https://www.cdc.gov/coronavirus/2019-ncov/community/health-equity/race-ethnicity.html which highlights healthcare inequities across different minority groups. They have tasked us with examining if there is data that will help identify different demographics or clusters that may be disproportionately affected by the pandemic so that they can design proper policies that will allocate funding and support accordingly.  

### Problem Statment:

Can we use socioeconomic, demographic, and employment data to identify groups or clusters most adversely affected by the pandemic in order to properly allocate resources to those areas or groups for both current and future disproportionate effect mitigation?

### Background:

In order to properly answer the question we first wanted to establish different metrics we were most interested in in order to determine levels of "concern" or "risk". While we often hear about the total magnitude of number of deaths via news outlets, one thing that gets lost in translation is the different degrees of impacts Covid has had across different groups. Intuitively we can note that states with higher populations will most likely have higher number of deaths so we wanted to avoid simply tackling our recommendations with aggregate death numbers, but wanted to compare most of our data on a per capita basis. This way we will be able to analyze our data in a more standardized format, but also wanted to make sure we combine these with the sheer totals. As mentioned, one of main driving determinants was death per capita, but we also identified Case Fatality Ratio as one of main determinants. Case Fatality Ratio is calculated by taking the number of deaths divided by the number of confirmed cases then multiplied by 100 to give us a percentage. Intuitively we can assume that a higher CFR should generate more concern since that would indicate people who contract the virus are dying at a higher rate than areas with lower CFRs. Additionally, we wanted to examine how states were impacted from an unemployment standpoint. We compared the rolling averages of unemployment over the 2020 timeframe, but made sure to also standardized this data considering some states were already below or above the country averages prior to the pandemic. We performed this by looking at percent changes across the pandemic epoch and aimed to identify states that experienced deviation of 2 stddev units away from the country's average rate. Now with our features of "concern" in mind, we set out to uncover clusters or trends associated with our features and examine any identifying discrepencies that may provide insight into formulating our recommendations. 

### Data Retrieval:

Data we were able to find comprehensive datasets from a handful of sources:

**Unemployment**
Bureau of Labor Statistics: https://www.bls.gov/lau/

**Socioeconomic Determinants**
STCCenter: https://github.com/stccenter/COVID-19-Data

**Covid Related Data**
 Center for Systems Science and Engineering (CSSE) at Johns Hopkins University: https://github.com/CSSEGISandData/COVID-19
 
The CSSE repo also has an extensive of helpful data sources to investigate for anybody hoping to perform further analysis.

### Data Dictionary:

|Feature|Type|Dataset|Description|
|---|---|---|---|
|Name|object|socioeconomic|Name of corresponding state|
|Postal Code|object|socioeconomic|State abbreviations|
|Area size|int|socioeconomic|the state area measurements, in square kilometers|
|Population size|int|socioeconomic|annual estimates of the total population|
|Population density|float|socioeconomic|people per sq. km|
|Senior Population|float|socioeconomic|population age 65+ (% of total)|
|Young Population|float|socioeconomic|population ages 0-14 (% of total)|
|Male Population|float|socioeconomic|population gender male (% of total)|
|White Population|float|socioeconomic|population race white (% of total)|
|Africa-American Population|float|socioeconomic|population race Africa American (% of total)|
|Hispanic population|float|socioeconomic|population ethnic Hispanic of any race (% of total)|
|Internet access|float|socioeconomic|population using internet and computer|
|High school degree|float|socioeconomic|population with high school and equivalent degrees (% of total)|
|Bachelor degrees|float|socioeconomic|population with Bachelor's degree or higher (% of total)|
|Median household income|int|socioeconomic|median household income|
|Poverty rate|float|socioeconomic|Poverty rate household income below poverty line|
|Uninsured|float|socioeconomic|Population without health care coverage in United States (% of total)|
|Household size|float|socioeconomic|Average number of persons in a household|
|House Owner|float|socioeconomic|owner-occupied housing (% of total household)|
|hospital|int|socioeconomic|Number of hospitals|
|hospital bed|int|socioeconomic|Number of hospital beds|
|ICU bed|int|socioeconomic|Number of ICU beds|
|Nurses|int|socioeconomic|Number of nurses per 1000 population|
|Medical Doctors|int|socioeconomic|Number of medical doctors per 1000 population|
|Province_State|object|covid_daily_reports|name of state or province|
|Country_Region|objecct|covid_daily_reports|Region|
|Last_Update|timeseries|covid_daily_reports|The most recent date the file was pushed.|
|Lat, Long|float|covid_daily_reports|Latitude, Longitude respectively|
|Confirmed|int|covid_daily_reports|Aggregated case count for the state|
|Deaths|int|covid_daily_reports|Aggregated death toll for the state|
|Recovered|float|covid_daily_reports|Aggregated Recovered case count for the state|
|Active|float|covid_daily_reports|Aggregated confirmed cases that have not been resolved (Active cases = total cases - total recovered - total deaths)|
|FIPS|float|covid_daily_reports|Federal Information Processing Standards code that uniquely identifies counties within the USA|
|Incident_Rate|float|covid_daily_reports|cases per 100,000 persons|
|Total_Test_Results|float|covid_daily_reports|Total number of people who have been tested|
|Case_Fatality_Ratio|float|covid_daily_reports|Number recorded deaths * 100/ Number confirmed cases|
|UID|float|covid_daily_reports|Unique Identifier for each row entry|
|ISO3|object|covid_daily_reports|Officialy assigned country code identifiers|
|Testing_Rate|float|covid_daily_reports|Total test results per 100,000 persons. The "total test results" are equal to "Total test results (Positive + Negative)"|
|deaths_per_population|float|socieconomic+daily reports merged|deaths per capita (# of deaths / population)|
|recovered_per_population|float|socieconomic+daily reports merged|recovered cases per capita (# of recovered / population)|
|confirmed_per_population|float|socieconomic+daily reports merged|confirmed cases per capita (# of confirmed/ population)|
|active_per_population|float|socieconomic+daily reports merged|active cases per capita (# of recovered / population)|
|Month Columns|float|unemployment_all_states_2020|unemployment rate by month for corresponding state (row)|

### Data Cleaning:

One thing we wanted to do was combine our socieconomic data with our covid aggregates so we could easily compare our targeted metrics, as well as calculate our per capita columns. Luckily both sets had columns for the respective state/province, which meant we would be able to join these sets using these "like" columns. While one set included US territories, we were able to avoid dropping those columns through using a inner join, which would only create a merged df with entries that were present in both columns. For nulls, since a few columns were entirely null we decided to simply drop those as we were not able to reasonably impute values for those columns given our data. But for the recovered column we were able to impute since according to the data dictionary they supplied the formula, so we used that to address the small amount of nulls found in those columns. For unemployment cleaning we were able to find monthly rates by state, but also wanted to calculate the percent changes over the Covid epoch to see how unemployment fluctuated over this period. 

### EDA:

For EDA we set out to discover trends and any correlations between our demographics and our selected metrics of "concern" highlighted earlier. As we described in the background section, for unemployment we wanted to make sure we kept in mind that states may already have poor uneomployment levels, so we made sure to track percentage over time so to make it a more elastic with respect to covid. Once we were able to establish states that experienced the highest fluctation in the "wrong" direction compared to national average during covid, we wanted to then try and identify any underlying factors that were present throughout the states. For this portion we used seaborn catplot to show different demographic trends between "low risk" and "high risk" (from an unemployment risk standpoint). The most interesting finding we uncovered during this portion of EDA was that states that exhibited abnormal unemployment rates during the year 2020 also exhibited a higher average Hispanic population (as a percentage of the population). This lead us to believe that the hispanic population employment was most adversely affected during Covid and should be addressed with our recommendations. We also observed lower rates of African American population for these states, but we also discovered that African American populations were already positively correlated with higher unemployment levels, so while they may not have been as affected as Hispanic counterparts, the underlying issues of unemployment already existed. And as we discovered further in our EDA higher levels of unemployment is positively correlated with deaths per capita, so both these relationships raised concern. 

For identifying trends amongst our demos and communities relating to our CFR and death per capita metrics we utilized both seaborn correlation heatmapping and pairplotting. We first examined by social elements against deaths per capita but also compared those same elements against cases per capita to see if there were any discrepencies in these correlations. Any presence of differences could lead us to speculate that there could possibly be a gap in the way each demographic is treated medically if they trend higher with deaths but lower with cases. We performed the same techniques with economic factors. The last heatmap cut we performed was to take the same social elements but compare them against CFR. If there was any aforementioned issues with deaths per capita versus cases per capita we would most likely see similar trends supported by our CFR EDA. For further visualization purposes we also created a column that clustered our states by CFR into a 25%/75% split that allowed us to set "hued" clusters in our pairplots. This allowed an easier observation of where these potentially high risk states plotted in our different pairplot comparisons.

For a more detailed analysis of our EDA refer to our EDA notebook within the repo, but here is a bulleted summary of our findings:

**deaths per capita, social demo cut:**
-The most alarming area being the correlation with the African-American Population.
-deaths per capita heatmap the African-American population measures the highest correlational value of 0.32, but in respect to confirmed cases, a much lower, almost neutral -0.081.
-white population correlates negatively with deaths per capita at -0.17, but then positively at 0.23

**deaths per capita, economic demo cut:**
-poverty rate correlates at a rate of 0.2 and 0.16
-unemployment rate we see it correlates negatively with confirmed cases (-0.23), but positively with deaths (0.21)

**cfr, social demo cut:**
-African-American population as the highest correlation amongst features, Hispanic as positive but more moderate, but White population again as negatively correlated.

**EDA Takeaways:**

The big takeaways from our EDA process was that there certainly seems to be a disproportionate impact on minority communities in a range of ways. From unemployment we highlighted that the Hispanic population trends poorly with states that were most impacted during the Covid epoch from a percent change, and as briefly noted while African Americans didn't experience a huge percentage change during this period, our EDA showed they were already at a disadvantage in relation to unemployment levels. So combining these findings, and our EDA findings that supported the impact of unemployment levels regarding death per capita, we can conclusde that there should be steps and measures taken to alleviate the harmful impacts of unemployment during covid for these minority demographics. Furthermore, we see from a 'health' standpoint (analyzed by CFR and death per capita) we can gleam that the minority populations are most adversely affected by Covid and there seems to be some gaps in treatment that would cause the minorities to be associated with higher fatality rates (both CFR and deaths per capita) as opposed to the white population counterparts which trend in the opposite directions. 

### Modeling:

For modeling purposes, since we don't necessarily have an output that we are either classifying or predicting, we have elected to utilize unsupervised modeling through clustering. The advantages of using clustering will be to identify groups that exist within our data and try and distinguish any identifying features that supports our conclusions discovered through EDA. Clustering in genreal attempts to group observations (data) with the notion that clusters of the same group are more similar than clusters of a different group. Ideally we would like to create two or three clusters that will allow us to draw comparisons easier and filter out any trends that would influence our recommendations given to the Covid resource agency. For clustering methods we will explore KMeans and DBSCAN.

**DBSCAN Findings:**
Judging by the clusters we have created we can see that there are a couple of notable differences among each pocket. Consistent with our EDA we notice that across each cluster, as CFR rises, so do the minority populations, while inversely the white population percentage decreases. It is also worth pointing out that there is a similar trend with deaths per capita, once again supporting what we saw with the correlational EDA analysis we performed earlier. While the clustering method is far from perfect, this should be enough to let us draw a conclusion that covid, particularly CFR and deaths per capita, disproportionately affect minority communities at a concerning rate. We were also able to map these labels on our original dataset and find a handful of states that should certainly require the attention of the policy makers: Connecticut, Florida, Illinois, Louisiana, Massachusetts, Michigan, Mississippi, New Jersey, Pennsylvania. We will go into a bit more detail with this in our Executive Summary.

**KMeans Findings:**
We elected to separate out into 3 clusters which created clusters containing 26 states, 21 states, and then 4 states. Let's first compare clusters 0 (26 states) and 1 (21 states) since they are the 2 dominant clusters. Do we see similarities to what we discovered through our DBSCAN method? Let's examine the same metrics we've been focusing on previously. We can see that across the clusters we observe increases in both CFR and deaths per capita again, and once more observe the same trend of positively correlation relating to the minority demographics while simultaneously negatively correlated with the white population demographic. Both models arrive at similar conclusions regarding our statement and highlight the utmost importance of recommending to our agency the need for support for the adversely affected minority communities by this pandemic.

**Modeling Takeaways:**
Through clustering modeling we were able to uncover similar findings that we suspected during our EDA process. This leads us to believe that there is data that would indicate that different demographics are indeed adversely affected by this pandemic. But the issues that we discovered during modeling is a shortage in data. Simply looking at 51 observations (50 states + Washington DC) limited us from a true clustering standpoint. DBSCAN struggles with sets that aren't distinctly separated, but we would speculate that if we had the same data on a county level, as opposed to just state levels, we would be able to better find specific areas that are most impacted. So while on a surface level we can provide recommendations of demographics disproportinately affected and offer a handful of states that require an increased focus from policy makers, we struggled to truly pinpoint exact locations. This is most likely a product of states being rather diverse as a whole, whereas on a county level populations are a lot more similar, making them potentially more 'clusterable.'  

### Executive Summary:

**Problem Statement:** Can we use socioeconomic, demographic, and employment data to identify groups or clusters most adversely affected by the pandemic in order to properly allocate resources to those areas or groups for both current and future disproportionate effect mitigation?

**Recommendations:** As we have expressed throughout this notebook, we believe that we are able to answer our question and provide value on a surface level, but would ask our policy makers to provide us with detailed county level data to truly identify the areas most in need. The issue is not with the data itself, merely a lack of depth of data (only on a state level is difficult to create generalizations). Despite this limitation and given the scope of our project, we still believe we are able to address demographics of concerns which will allow our audience to make decisions accordingly when addressing pandemic effect mitigation.

We reccomend that our audience pay extra attention to the minority demographics when providing aid and resources as they have shown through our data to be the most concerning categories. This was highlighted mainly through our EDA notebook and manifested the concerning relationship in various ways: positive correlations with death per capita and CFR, while white population correlated in the opposite direction. Our inklings were then bolstered through our modeling methods and supported our initial suspicions. Although we do recommend county level data for a more complete answer, we do offer these lists of states to our policy makers to focus their attention: Connecticut, Florida, Illinois, Louisiana, Massachusetts, Michigan, Mississippi, New Jersey, Pennsylvania. These states all presented concern in one of form of another most commonly high cfr rates and above average minority populations. 


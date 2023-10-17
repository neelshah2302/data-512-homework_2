
[![GitHub license](https://img.shields.io/github/license/ishank09/data-512-homework_1)](https://github.com/ishank09/data-512-homework_1/blob/main/LICENSE)

# Considering Bias in Data

# Goal of the project:
The goal of this assignment is to explore the concept of bias in data using Wikipedia articles. This assignment will consider articles about cities in different US states. For this assignment, you will combine a dataset of Wikipedia articles with a dataset of state populations, and use a machine learning service called ORES to estimate the quality of the articles about the cities.

We will perform an analysis of the coverage of US cities on Wikipedia and how the quality of articles about cities varies among states. The analysis will consist of a series of tables that show:
1. The states with the greatest and least coverage of cities on Wikipedia compared to their population.
2. The states with the highest and lowest proportion of high-quality articles about cities.
3. A ranking of US geographic regions by articles-per-person and proportion of high-quality articles.

At the end, we have a short reflection on the project that focuses on both your findings from this analysis and the process we went through to reach those findings that help us understand the causes and consequences of biased data in large, complex data science projects.

# Licence: 
https://www.mediawiki.org/wiki/API:REST_API#Terms_and_conditions
https://creativecommons.org/licenses/by/4.0/

# REST API Documentation and other sources: 
https://www.mediawiki.org/wiki/API:Info
https://www.mediawiki.org/wiki/ORES
https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html
https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state

# Implementation:

HW2_Data_Ingestion_and_Analysis.ipynb - This notebook will cover and run 3 high-level steps:
   1. Data Ingestion - API Calls for Page Info and ORES Scores
   2. Data Merge
   3. Data Analysis

   ## 1. Data Ingestion:
      This step is the initial part of the project where we scrape the data from web sources or ingest the data files (csv) which will be later used for analysis.
      We use 3 data files:
      1.  us_cities_by_state_SEPT.2023.csv - File containing Wikipedia articles for State
      2.  US States by Region - US Census Bureau.xlsx - File containing regional and divisional agglomerations as defined by the US Census Bureau
      3.  State Population Totals and Components of Change: 2020-2022 - File containing Population estimates for all states in the US
     
      We use 2 API calls to get the Page information and ORES scores for each article in "us_cities_by_state_SEPT.2023.csv"
      1. Page Info API  -  This API is used to extract Revision IDs for each article along with some other Page Info. Code Example - https://drive.google.com/file/d/15UoE16s-IccCTOXREjU3xDIz07tlpyrl/view?usp=sharing
      2. ORES API - This API is used to extract the Quality scores for each article based on Revision ID. Code Example - https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=sharing

   ### Result:
      The result of this step is a data containing article and corresponding review ID and Quality score for a revision ID

   ## 2. Data Merge:
      In this step we merge all the generated datasets and the data files ingested using common keys like state, revision ID, etc

   ### Result:
      The result of this step is the final CSV file which will be used for analysis: wp_scored_city_articles_by_state.csv
      The schema for that file looks like:
      
   ### Columns
   1. state - State for the Article
   2. regional_division - Regional Division of the state based on the country. It can take 9 values: New England, Middle Atlantic, East North Central, West North Central, South Atlantic, East South Central, West South Central, Mountain, Pacific
   3. population  -  Population in 2022 for specific state
   4. article_title - Title of the article
   5. revision_id - Current Revision ID for the article
   6. article_quality - Quality of Article. It can take the following  values:
        1. FA - Featured article
        2. GA - Good article (sometimes called A-class)
        3. B - B-class article
        4. C - C-class article
        5. Start - Start-class article
        6. Stub - Stub-class article
     
  ## 3. Data Analysis:
  In this step, we will perform an analysis that will consist of calculating total-articles-per-population (a ratio representing the number of articles per person)  and high quality-articles-per-population (a ratio representing the number of high-quality articles per person) on a state-by-state and divisional basis. All of these values are “per capita” ratios.
  
  ### Results:
  The results from this analysis are produced in the form of 6 data tables:
  1. Top 10 US states by coverage: The 10 US states with the highest total articles per capita (in descending order):
     
     <img width="597" alt="Screenshot 2023-10-16 at 10 53 40 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/af9b3cb1-8c2a-44d1-83fd-36115e749e27">

  2. Bottom 10 US states by coverage: The 10 US states with the lowest total articles per capita (in ascending order):
     
     <img width="589" alt="Screenshot 2023-10-16 at 10 53 52 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/9370d4a3-44b1-4112-986d-171bafb5e48f">

  3. Top 10 US states by high quality: The 10 US states with the highest high quality articles per capita (in descending order):
     
     <img width="594" alt="Screenshot 2023-10-16 at 10 52 46 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/41909f22-9011-4443-a16a-160586bb63c8">

  4. Bottom 10 US states by high quality: The 10 US states with the lowest high quality articles per capita (in ascending order):
     
     <img width="612" alt="Screenshot 2023-10-16 at 10 52 57 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/3f358279-0c78-4370-a7f5-f8a9285c7fd0">

  5. Census divisions by total coverage: A rank ordered list of US census divisions (in descending order) by total articles per capita:
      
     <img width="520" alt="Screenshot 2023-10-16 at 10 53 09 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/ce9e5800-529f-4973-b2dd-5e0e3906da5b">

  6. Census divisions by high quality coverage: Rank ordered list of US census divisions (in descending order) by high quality articles per capita:
      
     <img width="518" alt="Screenshot 2023-10-16 at 10 53 29 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/c4426a17-8d17-4ac6-95d0-2b63dd623c84">


# Research Implication:

This is an end-to-end Data engineering and analysis  project. This project deals with analyzing the Wikipedia articles based on cities from each state and then seeing the quality of those articles based on ORES score. Based on the analysis I found that there are many tier 2 states Vermont, Maine, Iowa, etc which I didn't expect to be in the top 10 states for total articles per capita. Also in the bottom 10 states based on total articles per capita, there are states like California, Maryland, Washington, etc., which I felt where very important states, and cities in them would definitely have articles in Wikipedia. But per person, there are very less articles by these states. Especially California shocked me as it is one of the largest states in the US, it has most of the most talented people with rich cultures and elaborate lifestyles which definitely should have caused  more articles about the cities in Wikipedia.

Similarly, for the total Articles based on quality of articles, we have most of them in Vermont, Wyoming, Montana, Missouri, etc., which centrally situated desert or aloof states in the US. I definitely feel population is one of the main factors causing these results and bias. Nevada, Arizona, and California has the lowest number of high quality articles per capita which is similarly mysterious.

Aligning with these results, we also see that regions like New England, Mountain, and West North Central are top 3 for both total and high quality coverage. This clearly indicates that there are relatively higher city-based articles from these tier 2 regions based on population.

1. What biases did you expect to find in the data (before you started working with it), and why?
- City/Area Bias: Wikipedia articles can be biased towards more well-known cities, probably neglecting the smaller or less prominent ones.
- Quality Bias: Articles about larger or more economically significant cities may receive more attention and therefore be of higher quality compared to articles about smaller or less economically significant cities.
- Cultural Bias: There can be multiple perspectives of the different editors who contribute to these articles, leading to variations in thought. But this might affect less.

2. What (potential) sources of bias did you discover in the course of your data processing and analysis?
- Bias based on City/Area: There was an unexpectedly opposite bias of articles towards more developed or well-known states as they had less total and quality coverage than less developed and aloof states.
- Population Bias: The population of a specific state/region definitely created a bias indicating its impact on pre-capita coverage. Higher Population penalizes the ratio and despite a higher number of articles, the per capita value is lower.
- Data Quality Bias: Due to less number of articles from the popular cities per capita, raises a data quality bias questioning the data collection or quality issues with data. 

4. What might your results suggest about (English) Wikipedia as a data source?
- The data may provide valuable insights into well-documented cities but may not accurately represent lesser-known or marginalized places.

5. How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?
- Researchers can consider several strategies to mitigate biases and limitations:
1. Collect data from multiple sources, including academic databases, government reports, and community-driven platforms.
2. Use natural language processing techniques to identify and fill gaps in the data by extracting information from sources beyond Wikipedia.
3. Implement topic modeling and sentiment analysis to gauge the extent of bias in the articles.
4. Assess the demographic and geographic backgrounds of Wikipedia editors to understand potential cultural biases.


       

        




[![GitHub license](https://img.shields.io/github/license/ishank09/data-512-homework_1)](https://github.com/ishank09/data-512-homework_1/blob/main/LICENSE)

# Considering Bias in Data

# Goal of the project:
The goal of this assignment is to explore the concept of bias in data using Wikipedia articles. This assignment will consider articles about cities in different US states. For this assignment, you will combine a dataset of Wikipedia articles with a dataset of state populations, and use a machine learning service called ORES to estimate the quality of the articles about the cities.
You are expected to perform an analysis of how the coverage of US cities on Wikipedia and how the quality of articles about cities varies among states. Your analysis will consist of a series of tables that show:
The states with the greatest and least coverage of cities on Wikipedia compared to their population.
The states with the highest and lowest proportion of high quality articles about cities.
A ranking of US geographic regions by articles-per-person and proportion of high quality articles.
You are also expected to write a short reflection on the project that focuses on how both your findings from this analysis and the process you went through to reach those findings helps you understand the causes and consequences of biased data in large, complex data science projects.

# Licence: 
https://www.mediawiki.org/wiki/API:REST_API#Terms_and_conditions

# REST API Documentation: 
https://www.mediawiki.org/wiki/API:Info

# Implementation:

HW2_Data_Ingestion_and_Analysis.ipynb - This notebook will cover and run 3 high-level steps:
   1. Data Ingestion - API Calls for Page Info and ORES Scores
   2. Data Merge
   3. Data Analysis

   ## 1. Data Ingestion:
      This step is the initial part of the project where we scrape the data from web sources or ingest the data files (csv) which will be         later used for analysis.
      We use 3 data files:
      1.  us_cities_by_state_SEPT.2023.csv - File containing Wikipedia articles for State
      2.  US States by Region - US Census Bureau.xlsx - File containing regional and divisional agglomerations as defined by the US Census Bureau
      3.  State Population Totals and Components of Change: 2020-2022 - File containing Population estimates for all states in the US
     
      We use 2 API calls to get the Page information and ORES scores for each article in "us_cities_by_state_SEPT.2023.csv"
      1. Page Info API  -  This API is used to extract Revision IDs for each article along with some other Page Info. Code Example - https://drive.google.com/file/d/15UoE16s-IccCTOXREjU3xDIz07tlpyrl/view?usp=sharing
      2. ORES API - This API is used to extract the Quality scores for each article based on Revision ID. Code Example - https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=sharing

      Result:
      The result of this step is a data containing article and corresponding review ID and Quality score for a revision ID

   ## 2. Data Merge:
      In this step we merge all the generated datasets and the data files ingested using common keys like state, revision ID, etc

      Result:
      The result of this step is the final CSV file which will be used for analysis: wp_scored_city_articles_by_state.csv
      The schema for that file looks like:
      
      Columns
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
      In this step, we will perform an analysis that will consist of calculating total-articles-per-population (a ratio representing the          number of articles per person)  and high-quality-articles-per-population (a ratio representing the number of high quality articles          per person) on a state-by-state and divisional basis. All of these values are “per capita” ratios.

      Results:
      The results from this analysis are produced in the form of 6 data tables:
      1. Top 10 US states by coverage: The 10 US states with the highest total articles per capita (in descending order):
      <img width="597" alt="Screenshot 2023-10-16 at 10 53 40 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/275f45c7-f5b7-40c2-9854-cf5c4b85f250">

      2. Bottom 10 US states by coverage: The 10 US states with the lowest total articles per capita (in ascending order)
      <img width="589" alt="Screenshot 2023-10-16 at 10 53 52 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/e88c3b86-bc80-4452-bc24-127523e6bad9">

      3. Top 10 US states by high quality: The 10 US states with the highest high quality articles per capita (in descending order)
      <img width="594" alt="Screenshot 2023-10-16 at 10 52 46 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/350a80ca-8085-4ce4-98a6-2f7fdb8c3174">

      4. Bottom 10 US states by high quality: The 10 US states with the lowest high quality articles per capita (in ascending order)
      <img width="612" alt="Screenshot 2023-10-16 at 10 52 57 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/924f587c-ff13-4848-8ee5-bf4766acfc3d">

      5. Census divisions by total coverage: A rank ordered list of US census divisions (in descending order) by total articles per capita
      <img width="520" alt="Screenshot 2023-10-16 at 10 53 09 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/7cd749ba-ff3d-45a3-80be-43239447b1e2">

      6. Census divisions by high quality coverage: Rank ordered list of US census divisions (in descending order) by high quality articles per capita
      <img width="518" alt="Screenshot 2023-10-16 at 10 53 29 PM" src="https://github.com/neelshah2302/data-512-homework_2/assets/122260079/c3e304a3-571e-4a99-bc40-ace057d5e056">

# Research Implication:



       

        



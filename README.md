# Overview

In this project, I delve into the notion of data bias by examining Wikipedia articles. My objective is to collect data pertaining to Wikipedia article searches for various cities and towns across the United States, with a focus on assessing the quality of the Wikipedia articles related to these locations. Additionally, I aim to conduct an analysis of key metrics associated with the predicted quality of these articles. One crucial aspect of this analysis is identifying the states with the highest per capita coverage of articles.

The ultimate goal of this project is to gain insights into state-level trends in article coverage and the presence of high-quality articles. By scrutinizing the data and exploring these trends, we can better understand the potential biases that may exist in the portrayal of different regions within Wikipedia's content.

# Datasets

The project has three primary datasets, each serving a specific purpose:

1. data/us_cities_by_state_SEPT.2023.csv:

    This dataset contains information about Wikipedia article pages related to U.S. cities, with entries from each state. It likely includes details like the city's name, the associated state, and potentially information on the quality of the Wikipedia articles for each city.

2. data/NST-EST2022-POP.xlsx:

    This dataset is focused on population estimates for every U.S. state. It should provide information on the estimated population for each state, which is essential for various per capita calculations in your analysis.

3. data/US States by Region - US Census Bureau.xlsx:

    This dataset is related to the regional division of U.S. states, as defined by the U.S. Census Bureau. It likely categorizes states into their respective census divisions. This dataset is crucial for grouping states and understanding regional trends.

With these datasets, you can explore the quality and coverage of Wikipedia articles for U.S. cities and towns, calculate per capita coverage, and analyze how these metrics vary by state and region. It provides a comprehensive foundation for your project on bias in Wikipedia data.

# Dependencies

- Python 3
- Jupyter Notebook
- Pandas
- Requests

# Licensing

1. Wikimedia Foundation REST API terms of use : https://www.mediawiki.org/wiki/API:REST_API#Terms_and_conditions

2. Creative Commons License: https://creativecommons.org/licenses/by/4.0/

# Data Understanding/Caveats

It's essential to have a robust data acquisition and cleaning process, especially when dealing with a large dataset. Handling errors, deduplication, and addressing non-geographic articles are important steps to ensure the quality and accuracy of your analysis. Here's a breakdown of the key steps you've described:

1. **Efficient Data Acquisition with Error Handling:** <br>
    When accessing data from an external source or API, it's crucial to implement error handling mechanisms to manage issues like network failures, timeouts, and exceptions. This ensures that your data acquisition process runs smoothly and doesn't break when unexpected problems arise.

2. **Deduplication using a Dictionary:**<br>
    Deduplication is essential to avoid redundancy and maintain data integrity. Using a dictionary to store unique entries is a smart approach, as dictionaries inherently do not allow duplicate keys. This simplifies the process of removing duplicate articles.

3. **Handling Non-Geographic Articles:**<br>
    Identifying and excluding non-geographic articles is a critical part of your analysis. You can apply filters or conditions to your dataset to exclude entries that are not relevant to your project's geographic focus.

4. **Cleaning Population Data:**<br>
    Population data may have inconsistencies or anomalies, like the "District of Columbia0" entry you mentioned. Removing such entries is important to ensure that your population data is accurate and can be correctly associated with the geographic articles.

Handling these challenges is a key part of any data-driven project, particularly when working with extensive datasets.

# Helpful API Documentation

1. ORES Wiki : https://www.mediawiki.org/wiki/ORES
   
2. Wikipedia Content Assessment: https://en.wikipedia.org/wiki/Wikipedia:Content_assessment
   
3. Wikimedia API Documentation: https://www.mediawiki.org/wiki/API:Info
   
4. Python Notebook to call Wikipedia API to get article metadata: https://drive.google.com/file/d/15UoE16s-IccCTOXREjU3xDIz07tlpyrl/view?usp=sharing
    
5. Python Notebook to call ORES ML model to get article quality predictions: https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=sharing

# Coding Files (/code/)

The project comprises two notebooks, each focusing on distinct aspects of the project:

1. code/AM_DATA512_W2_Data_Acquisition.ipynb: <br>
    This notebook is dedicated to the process of collecting data from multiple sources, carrying out a range of data pre-processing tasks, and ultimately saving the outcomes in the form of CSVs and JSON files.

2. code/AM_DATA512_W2_Data_Analysis.ipynb: <br>
    In this notebook, the primary emphasis is on conducting various data analysis and data visualization activities. It is intended for exploring and deriving insights from the processed data.

These two notebooks together cover the comprehensive workflow of your project, from data acquisition and preparation to the subsequent data analysis and visualization stages.

# Coding Process/Steps to Reproduce

1. Data from Wikipedia, including information about U.S. cities, was collected, taking around 2 hours for over 20,000 articles.
2. Duplicate entries in the dataset were removed using Pandas' in-built functions.
3. Population data for each U.S. state was acquired from the US Census Bureau.
4. Regional divisions, defined by the US Census Bureau, were extracted.
5. Quality scores for Wikipedia articles were predicted using the ORES machine learning system, encompassing "FA" (Featured article) to "Stub" (Stub-class article). This process involved API calls for 20,000+ articles, taking about 5 hours. The initial round of calls yielded around 4,000 rows with prediction errors, which were addressed in a second round of API calls.
6. Data integration was executed by merging Wikipedia data, population data, and regional division data using state names as the key. Data inconsistencies and discrepancies were managed during this process.
7. The final consolidated dataset was generated and named "wp_scored_city_articles_by_state.csv."

    | Fields    |
    | -------- |
    | state  |
    | regional_division |
    | population    |
    | article_title |
    | revision_id |
    | article_quality |

4. Data Analysis

    In the Python Notebook *AM_DATA_512_W2 Data Analysis.ipynb*, the following data analysis steps are performed to address different questions using the dataset wp_scored_city_articles_by_state.csv:

    - Q1 and Q2: For the first and second questions, the data is grouped by state. The analysis includes counting the number of article titles and calculating the mean of populations for each state. This data can then be divided to obtain the per capita total articles per state. Sorting this data in descending order answers Q1, and sorting it in ascending order answers Q2.

    - Q3 and Q4: Questions three and four are addressed similarly, but the dataset is initially filtered to include only high-quality articles, namely those with predicted quality ratings of Featured (FA) or Good (GA). The same analysis as for Q1 and Q2 is then applied.

    - Q5 and Q6: For the fifth and sixth questions, the process differs slightly. The data is first grouped by state to obtain the total number of articles per state, the population of each state, and the regional division of each state. Subsequently, the data is grouped by regional division, and calculations are made to determine the sum of the population and article count for each division. This provides per capita information. Sorting this data in descending order answers Q5. Performing the same process but only with high-quality articles addresses Q6.

# Research Implications

This assignment provided fascinating insights into the world of Wikipedia as a data and information source. Here are some key observations and reflections that I noticed:

- The concept of quality rankings for Wikipedia articles was a new and intriguing aspect of the project. It shed light on which articles are of higher quality and prompted questions about why certain articles excel in quality.

- One noteworthy discovery was that less-populated states, such as Wyoming, Vermont, and the Dakotas, often exhibit better coverage of articles per capita. This is intuitively tied to their lower populations.

- Similarly, smaller states tend to have more highly ranked articles per capita compared to more populous states like Florida, California, and New York.

- A surprising finding was that major cities like San Francisco, Seattle, and New York City do not always have highly rated articles. Frequent edits might contribute to this, making it challenging to maintain a high level of quality consistently.

- The issue of how major cities are named in articles, often without including state names, highlights the need for different handling in the analysis.

- A positive revelation during data acquisition and analysis was the absence of missing data after the ORES calls, which underlines the scalability and reliability of the ORES model.

- An interest in understanding the inner workings of the ORES model emerged, including its criteria, weighting of parameters, and mathematical considerations for assigning probability scores.

- Wikipedia, as a data source, holds immense potential due to its vast and diverse content. This assignment focused on obtaining metadata about articles, but there are countless other possibilities for analysis.

- Wikipedia is widely considered a reliable data source and a primary online repository of information. However, its open-source nature means that anyone can edit it, leading to potential inaccuracies and challenges in maintaining data integrity.

- Biases are inherent in open-source data like Wikipedia, including geographical, racial, economic, and other biases. Algorithms trained on such data can amplify these biases, underscoring the need for cautious decision-making based on data science research.

- Wikipedia is valuable for historical data, making it suitable for time series analytics. Its ubiquity as an information resource and the availability of APIs and models from the Wikimedia Foundation make it an attractive option for data science research.

This project offers a glimpse into the potential and challenges of using Wikipedia as a data source, highlighting both its strengths and limitations in data-driven research.

# License

This project is licensed under the MIT License. Please see the LICENSE file for more details.

# Acknowledgements

- Wikipedia for the dataset about US cities.
- US Census Bureau for the population and regional division data.
- ORES for providing the article quality predictions.

# Contact Information

For any additional questions or feedback, please contact Akshit Miglani at amiglani@uw.edu
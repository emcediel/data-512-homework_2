# data-512-homework_2

Our goal is to analyze explore the concept of bias by using English Wikipedia articles. We will analyze politicians from different countries. 

## <u>Files inside repo</u>

## Source files

1. <em>politicians_by_country_SEPT.2022.csv.xlsx</em>: The Wikipedia [Category:Politicians](https://en.wikipedia.org/wiki/Category:Politicians_by_nationality) by nationality was crawled to generate a list of Wikipedia article pages about politicians from a wide range of countries
2. <em>population_by_country_2022.csv.xlsx</em>: This dataset is drawn from the [world population data sheet](https://www.prb.org/international/indicator/population/table/) published by the Population Reference Bureau.
3. <em>revision_ID</em>: We obtain the revision_ID for each article by requesting to the Media Wiki [API](https://www.mediawiki.org/wiki/API:Info)  
4. <em>ORES_score</em>: We obtain the ORES_Score for each article by requesting to the Media Wiki [API](https://www.mediawiki.org/wiki/API:Info)  

Additional information to the Wikimedia Foundation REST API terms of use can be found here: https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions

This is the link to the REST API: https://www.mediawiki.org/wiki/Wikimedia_REST_API

### Global Rules
Limit your clients to no more than 200 requests/s to this API. Each API endpoint's documentation may detail more specific usage limits.
Set a unique User-Agent or Api-User-Agent header that allows us to contact you quickly. Email addresses or URLs of contact pages work well.

By using this API, you agree to Wikimedia's Terms of Use and Privacy Policy. Unless otherwise specified in the endpoint documentation below, content accessed via this API is licensed under the CC-BY-SA 3.0 and GFDL licenses, and you irrevocably agree to release modifications or additions made through this API under these licenses. See https://www.mediawiki.org/wiki/REST_API for background and details.


## Output files

One CSV and one txt files were created:
1. <em>wp_politicians_by_country.csv</em> - The final consolidated table that contains:

country: The country of origin of the politician

region: The region associates with the country

population: The population of that country in millions

article_title: The name of the politician

revision_id: The last revision id

article_quality: 1 if article is considered high quality (featured article or good article), 0 otherwise. 

2. <em>wp_countries-no_match.txt</em> - All countries for which there are no matches and output a list of those countries, with each country on a separate line 

## <u>Data limitations and special considerations </u>

1. The initial crawling results had multiple duplicates for politicians. Duplicate politicians acting for the same country were deleted. 

2. 6 articles did not have revision_ID information from the API, these politicians were removed form the analysis

3. Countries with English as a primary language are not considered in the analysis in order to make a fair comparison

4. There are articles under the country Korea, given that this didn't exist in the populations table, we decided to remove these articles from the analysis.

5. There are countries whose population is <0.0 million, given that our comparison metrics are "per capita" we decide to remove articles from countries that have such small populations.

6. When obtaining data from the API remember that Global Rules limit your clients to no more than 200 requests/s to this API. Each API endpoint's documentation may detail more specific usage limits. Set a unique User-Agent or Api-User-Agent header that allows us to contact you quickly. Email addresses or URLs of contact pages work well. We recommend using delays when requesting data to comply with these terms.



## <u> Research Implications </u>

From table 1 we observe that the result is highly skewed towards countries that have very low population. On the other hand, in table 2, there is a more interesting mix, where some countries do have large populations, but most have very few articles. We observe these top 10 countries are poor. For table 3, we find more interesting results, where small but rich countries dominate the top positions, in table 4 we don't find interesting results as more than 10 countries have 0 high quality article, still we notice that the majority are poor countries. Table 5 helps conclude what we have been discovering previously, we find that richer regions such as EUROPE are at the top while poorer regions such as AFRICA, OCEANIA and ASIA are last. This gets further validated by table 6, where results are similar to table 5, this time with high quality articles. In general, we find that there are clear biases in writing more and higher quality articles for politicians that are from richer countries and regions. We might suspect that this has to do with the education level difference, poor English levels and number of people that speak English in these countries, lack of internet and computer access, lack of interest in politicians that are not relevant to the G8.

### What might your results suggest about (English) Wikipedia as a data source?

It suggests that Wikipedia is a biased data source that has to be handled with precaution, specially if we are trying to use it as input for ML. We notice that there are strong inherent biases towards favoring and showcasing richer and more famous countries while suffocating and almost removing poor countries.

### What might your results suggest about the internet and global society in general?

It suggests that internet is very biased towards English speaking countries, specially countries that have higher English speakers and higher education levels. It suggests that most of the data that we are ingesting daily has strong biases to these differences, making it very hard for algorithms not to begin to take these implicit biases into account in the moment of taking decisions. These might be small, unimportant decisions, but they could also potentially be life-threatening and crucial decisions as well. 

### Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?

Let's say that the USA has decided to give financial aid to combat politician murders in multiple countries in the world. If they decide to use this data as a source to understand how many politicians there are in each of the countries and with that information decide the amount of aid to give to each. In this case, they would get it completely wrong, as they would give aid to richer countries as they have more articles in English, but not necessarily a larger amount of politicians. 

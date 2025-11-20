# Cryptocurrency News Validation

**Date:** March 3, 2025  

**Data Sources:**  
- Coindesk (News Articles)  
- Yahoo Finance (Daily Cryptocurrency Prices)

**Tags:** Machine Learning, Regression, Cryptocurrency, Ensemble Models, BeautifulSoup

**Deployment:** https://cryptocurrencynewsvalidation-tykrhnbankvsagtaciqx4m.streamlit.app

---

## Project Overview

This project is an end-to-end pipeline designed to conduct sentiment analysis on cryptocurrency news sources and predict price movements. It spans across three different categories of cryptocurrencies, integrating multiple data sources and modeling techniques to deliver actionable insights.

---

## Pipeline

This project utilized the OSEMN methodology to split the pipeline into 5 key phases. The pipeline is as follows:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_1.png)

Sentiment Analysis models include using both VaDer and FinBert to conduct a comparison on the performance of the models on cryptocurrency related text.

- **Data Collection (Obtain)**

***Data Collection (News Data)***

Data collection is conducted on two different sources. Scraping from Coindesk requires using Selenium to bypass the website restrictions and collect articles related to the targetted tokens. The initial scrape is to index all articles related to the tokens within a given timeframe and this is followed by a second scrape to receive the article data.

***Data Collection (Pricing Data)***

Daily pricing data is scrapped via the YahooFinance API. The daily prices of each token is collected within the same timeframe set for the news articles.

- **Data Cleaning (Scrub)**

Scrubbing activities include removing unwanted data from the scrapped dataset (Articles outside of the specified range)

Data Pre-removal:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_2.png)

Data Post-removal:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_3.png)

Other Scrubbing activites include the following:
- Text cleaning from all three levels of the article (‘Header’, ’SubHeader’, ’Content’). 
- Calculating daily movement using formula: Movement=Close-Open
- Normalizing movement via using Z-Score normalization

These are further covered within the code Repository.

- **Data Exploration (Explore)**

The following are several plots conducted to explore the patterns in the data.

Distribution of sentiment score across both sentiment models:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_4.png)

Comparison of price movements by Cryptocurrency:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_5.png)

Movement by Trade Volume Comparison:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_6.png)

- **Data Models (Modelling)**

Due to the target column being a continuous integer value, regressive modelling was chosen to handle the predictions. The following table shows the different models trained on this data:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_7.png)

Tuning parameters accross the several different models was handled via RandomizedSearchCV to identify best parameters. The following is the grid used for every model parameter:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_8.png)

The following are a sample output of the performance metrics tracked for these models:

![Placeholder](Projects/Cryptocurrency-News-Validation/Image_9.png)
---

## Outcome

Based on the steps and analysis of results. The following conclusions were made:
- FinBert models were more suitable in handling text in relation to cryptocurrency as it had overall better performance compared to Vader sentiment models.
- Established and Meme tokens were able to be predicted within reasonable thresholds whereas Emerging tokens had various discrepancies.
- Ensemble models had overall better performance than single models across all three tokens.

---

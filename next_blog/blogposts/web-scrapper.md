---
title: 'Web-Scrapping'
date: '2023-06-23'
---

# Web-Scrapping

## YouTube Scrapper

### Data Retrieval
- Using [YouTube API](https://developers.google.com/youtube/v3) key provided by Google to extract data for [GoogleDevelopers]((https://www.youtube.com/@GoogleDevelopers)) YouTube channel. The code is in [retrieve_all_yt_vid_data.py](https://github.com/rukshar69/Web-Scrapping/blob/main/YoutubeScrapper/retrieve_all_yt_vid_data.py)
- Extracted data includes channel subscriber, total video, total views count (stored in [channel_stats.csv](https://github.com/rukshar69/Web-Scrapping/blob/main/YoutubeScrapper/data/channel_stats.csv)) and the individual video's id, views, likes, comments, and upload date (stored in [google_dev_channel_vid_details.csv](https://github.com/rukshar69/Web-Scrapping/blob/main/YoutubeScrapper/data/google_dev_channel_vid_details.csv)).
- **Data cleaning** is performed on *views* column in [google_dev_channel_vid_details.csv](https://github.com/rukshar69/Web-Scrapping/blob/main/YoutubeScrapper/data/google_dev_channel_vid_details.csv) because some values are corrupt. So we have to drop those rows and store the cleaned data in [google_dev_vid_details_cleaned.csv](https://github.com/rukshar69/Web-Scrapping/blob/main/YoutubeScrapper/data/google_dev_vid_details_cleaned.csv)

### Streamlit App
[YouTube API Scrapped Streamlit App](https://yt-api-6zp16ra8uc.streamlit.app/)

The app includes:
- Basic info about the channel
- Scrollable table to sort out channel videos by views/likes/upload date
- Distribution/box plots for video likes/views
- Scatter plot between views and likes along with their regression
- Views/Likes by year
- Time Series Plot for Videos vs Upload Date

## LuLu Market Place Scrapper

### Data Retrieval

- Using Scrapy library, product details have been scraped from various products listed for various sub categories under the [electronics](https://www.luluhypermarket.com/en-ae/electronics) section
- The scraped data is saved in a [JSON file](https://github.com/rukshar69/Web-Scrapping/blob/main/lulu_scraping/lulu_scraper/lulu_scraper/products_desc.json). This is a list of dictionaries where each dict element has product id, name price, url, and summary.
- The spider crawling code to extract this data is in file [lulu_product_details.py](https://github.com/rukshar69/Web-Scrapping/blob/main/lulu_scraping/lulu_scraper/lulu_scraper/spiders/lulu_product_details.py)

### Streamlit App

[LuLu Electronics Streamlit App](https://lulu-favbjo2p59m.streamlit.app/)

The app includes:
- Category distribution
- Price analysis
- Word cloud for each sub-category based on product descriptions

## Yahoo Finance Stock Market Data Mining

### Data Retrieval

- This crawler uses Scrapy to crawl [finance.yahoo.com](finance.yahoo.com), and collects information on stocks in various sectors including healthcare, technology, energy, and more. It collects information such as the ticker, name, price, change in price, etc. of stocks and stores them.     

    - An example [data](https://github.com/rukshar69/Web-Scrapping/blob/main/yahoo_finance_stocks/stocks_info.csv) is added. The data is collected on the 1st August, 2023
    - In order to practise storing data in PostgreSQL and MongoDB in the local machine using Scrapy, [2 pipeline scripts](https://github.com/rukshar69/Web-Scrapping/tree/main/yahoo_finance_stocks/yahoo_finance_stocks/pipelines) are written along with necessary additions in [settings.py](https://github.com/rukshar69/Web-Scrapping/blob/main/yahoo_finance_stocks/yahoo_finance_stocks/settings.py)

### Streamlit App

- A [streamlit app](https://yahoo-finance-aug-1-23.streamlit.app/) is developed to visualize the collected data. The app has following visualizations:
    - Top 10 companies based on selected sector and numerical column('avg_vol_3_month', 'intraday_price', 'market_cap', 'pe_ratio_ttm', 'percent_change', 'price_change', 'volume')
    - Data distribution and boxplot for selected sector and numerical column
    - Donut chart showing % distribution of companies within a sector based on a numerical column divided into 6 ranges. 
    - Scatter plot for Market Cap vs. PE Ratio for a selected sector. The size of a point is determined by average volume
    - Scatter matrix showing pairwise relationships between numerical columns 
    - Violin Plot showing distribution of selected numerical column by sector
    - Bar Chart showing average volume by sector
    - Pie Chart showing distribution of Companies by sector
    - Heatmap representing the correlation matrix between numerical columns
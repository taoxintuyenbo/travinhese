# **Objective**

The objective of this project is to analyze user search behavior over two specified time periods, June and July, to derive insights into their preferences regarding entertainment content. By processing raw search data, we aim to understand the popularity of various TV shows and movies, categorize them into specific genres, and identify any changes or trends in user preferences between the two months.

- Tech stacks: Pyspark, Python, MySQL, Google Studio.

## **Raw data**

- Log data from available PARQUET files.
- Log data schema

```sh
root
 |-- eventID: string (nullable = true)
 |-- datetime: string (nullable = true)
 |-- user_id: string (nullable = true)
 |-- keyword: string (nullable = true)
 |-- category: string (nullable = true)
 |-- proxy_isp: string (nullable = true)
 |-- platform: string (nullable = true)
 |-- networkType: string (nullable = true)
 |-- action: string (nullable = true)
 |-- userPlansMap: array (nullable = true)
 |    |-- element: string (containsNull = true)
```

![log_data](https://github.com/taoxintuyenbo/travinhese/blob/main/asset2/logdata.png?raw=true)

## **Processing data**

- Create a function that takes start and end dates as input parameters and generates a date range between those dates. Use this date range to read Parquet files for each date within the range. Select only the columns `user_id `and `keyword`, and filter out any rows where `user_id` is null.
- Utilize a ranking window function to rank the searches for each user based on their frequency. Select the `keyword` with a `rank of 1` for each user, indicating their top search.
- Analyze the `top 20` popular searches in both `June` and `July` to identify common patterns or themes. Based on these patterns, define `categories` for the `keywords`. Then, create a function to categorize each keyword into one of these specified categories.

<div style="display: flex; flex-direction: row;">
    <i>Top seach June<img src="https://github.com/taoxintuyenbo/travinhese/blob/main/asset2/topsearch_june.png?raw=true" alt="Image 1" style="width: 100%;"></i>
    <i>Top search July<img src="https://github.com/taoxintuyenbo/travinhese/blob/main/asset2/topsearch_july.png?raw=true" alt="Image 2" style="width: 100%;"></i>
</div>

- Merge the data from `June` and `July` to analyze `customer taste` and `trending type`. Compare the most searched keyword for each user in June and July. If there's a difference, identify it and extract the previous keyword as the `previous` column. If there's no change, keep the category `unchanged`. If there's a change, `replace the category with the most searched keyword from June`.

By following these steps, I effectively processed the data from Parquet files, analyzed search patterns, and identified any changes or trends in customer behavior between June and July.

## **Clean data**

- Clean data schema:

```sh
root
 |-- user_id: string (nullable = true)
 |-- most_search_june: string (nullable = true)
 |-- category_june: string (nullable = true)
 |-- most_search_july: string (nullable = true)
 |-- category_july: string (nullable = true)
 |-- Trending_Type: string (nullable = false)
 |-- Previous: string (nullable = true)
```

![clean_data](https://github.com/taoxintuyenbo/travinhese/blob/main/asset2/cleandata.png?raw=true)

## **Visualizing Data with Google Studio**

![visualize_grafana](https://github.com/taoxintuyenbo/travinhese/blob/main/asset2/chart.png?raw=true)

# Netflix

Data Specialist Exercise from YipitData

Exercise with previously scraped data from Netflix weekly Top 10 and IMDb

I've started this task taking a look into the data through excel and then
exporting the data into a CSV format, after that i loaded the Data into
BigQuery and started exploring the tables in order to take insights and 
answer the question.

Down below you can check the SQL for each question.

Question 1.

```SQL
SELECT
  show_title,
  COUNT(DISTINCT season_title) AS total,
  ROUND (AVG(weekly_hours_viewed), 2) AS avg_hours_w
FROM netflix.nf_top
WHERE category = "TV (English)" 
AND week != "2022-05-22"
GROUP BY show_title
ORDER BY total DESC
LIMIT 1;
```

Question 2.

```SQL
SELECT 
  show_title,
  MIN (rating) AS min_rating,
  ROUND (AVG(weekly_hours_viewed), 2) AS avg_hours_w
FROM netflix.nf_top t
LEFT JOIN netflix.nf_rating r on t.show_title = r.title
WHERE category = "Films (English)" 
AND week != "2022-05-22"
AND rating IS NOT NULL
AND rating != 0
GROUP BY show_title
ORDER BY min_rating ASC
LIMIT 1;
```

Question 3.

```SQL
SELECT
  show_title,
  MAX (cumulative_weeks_in_top_10) AS weeks_in_top_10,
  ROUND (AVG(weekly_hours_viewed), 2) AS avg_views
FROM netflix.nf_top
WHERE category = "Films (Non-English)"
AND week != "2022-05-22"
GROUP BY show_title
ORDER BY weeks_in_top_10 DESC;
```



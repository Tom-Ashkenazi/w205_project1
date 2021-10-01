# w205 project1

- In the Query Project, you will get practice with SQL while learning about Google Cloud Platform (GCP) and BiqQuery. You'll answer business-driven questions using public datasets housed in GCP. To give you experience with different ways to use those datasets, you will use the web UI (BiqQuery) and the command-line tools, and work with them in Jupyter Notebooks.

## Part 1 - Querying Data with BigQuery

### Some initial queries

Paste your SQL query and answer the question in a sentence. Be sure you properly format your queries and results using markdown.

- **What's the size of this dataset? (i.e., how many trips)**
  ```
  SELECT count(*) as number_of_trips
    FROM`bigquery-public-data.san_francisco.bikeshare_trips` 
  ```
  There are 983,648 trips in this dataset

- **What is the earliest start date and time and latest end date and time for a trip?**
```
SELECT min(start_date) as earliest_start_date, max(end_date) as latest_end_date
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
 ```
  The earliest start date for a trip in this dataset is August 29, 2013 at 9:08, the latest end date is August 31, 2016 at 23:48
 
- **How many bikes are there?**
```
SELECT count(distinct bike_number) as number_of_bikes
    FROM`bigquery-public-data.san_francisco.bikeshare_trips`
```
there are 700 bikes in this dataset

### Questions of your own

- Make up 3 questions and answer them using the Bay Area Bike Share Trips Data. These questions MUST be different than any of the questions and queries you ran above.

- **QUESTION 1: what are the top ten most popular start stations?**:
  - Answer:
    1. San Francisco Caltrain (Townsend at 4th)
    2. San Francisco Caltrain 2 (330 Townsend)
    3. Harry Bridges Plaza (Ferry Building)
    4. Embarcadero at Sansome
    5. 2nd at Townsend
    6. Temporary Transbay Terminal (Howard at Beale)
    7. Steuart at Market
    8. Market at Sansome
    9. Townsend at 7th
    10. Market at 10th

  - Sql Query:
  ```
  select start_station_name, count(distinct trip_id) as total_trips
    from `bigquery-public-data.san_francisco.bikeshare_trips`
    group by start_station_name
    order by total_trips desc
    limit 10;
  ```
 
- **QUESTION 2: what are the top five most popular destinations for bikers who start at the SF Caltrain (Townsend&4th) Station?**
  - Answer:
    1. Harry Bridges Plaza (Ferry Building)
    2. Temporary Transbay Terminal (Howard at Beale)
    3. Embarcadero at Folsom
    4. Steuart at Market
    5. Market at Sansome

  - Sql Query:
  ```
  select end_station_name, count(distinct trip_id) as total_trips
    from `bigquery-public-data.san_francisco.bikeshare_trips`
    where start_station_name='San Francisco Caltrain (Townsend at 4th)'
    group by end_station_name
    order by total_trips desc
    limit 5;
  ```
- **QUESTION 3: What is the subscriber/customer breakdown for number of trips in the top three most popular stations?**
  - Answer:
    - San Francisco Caltrain (Townsend at 4th): Subscribers - 68384, Customers - 4299
    - San Francisco Caltrain 2 (330 Townsend): Subscribers - 53694, Customers - 2406
    - Harry Bridges Plaza (Ferry Building): Subscribers - 36621, Customers - 12441
 
  - Sql Query:
  ```
  select start_station_name, subscriber_type, count(distinct trip_id) as total_trips
    from `bigquery-public-data.san_francisco.bikeshare_trips`
    where start_station_name='San Francisco Caltrain (Townsend at 4th)' 
        or start_station_name='San Francisco Caltrain 2 (330 Townsend)'
        or start_station_name='Harry Bridges Plaza (Ferry Building)'
    group by start_station_name, subscriber_type
    order by start_station_name, subscriber_type
  ```

## Part 2 - Querying data from the BigQuery CLI

### Queries

1.Rerun the first 3 queries from Part 1 using bq command line tool (Paste your bq queries and results here, using properly formatted markdown):

- **What's the size of this dataset? (i.e., how many trips)**
```
bq query --use_legacy_sql=false '
 SELECT count(*) as number_of_trips
 FROM`bigquery-public-data.san_francisco.bikeshare_trips`'
```
```
+-----------------+
| number_of_trips |
+-----------------+
|          983648 |
+-----------------+
```
- **What is the earliest start time and latest end time for a trip?**
```
bq query --use_legacy_sql=false '
 SELECT min(start_date) as earliest_start_date, max(end_date) as latest_end_date
 FROM `bigquery-public-data.san_francisco.bikeshare_trips`'
```
```
+---------------------+---------------------+
| earliest_start_date |   latest_end_date   |
+---------------------+---------------------+
| 2013-08-29 09:08:00 | 2016-08-31 23:48:00 |
+---------------------+---------------------+
```
- **How many bikes are there?**
```
bq query --use_legacy_sql=false '
  SELECT count(distinct bike_number) as number_of_bikes
    FROM`bigquery-public-data.san_francisco.bikeshare_trips`'
```
```
+-----------------+
| number_of_bikes |
+-----------------+
|             700 |
+-----------------+
```
2. **New Query (Run using bq and paste your SQL query and answer the question in a sentence, using properly formatted markdown):**

- **How many trips are in the morning vs in the afternoon?**
  
  MORNING TRIPS
  ```
  SELECT count(trip_id) as number_of_morning_trips
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE CAST(start_date as time) >= '6:00:00' 
        and  CAST(end_date as time) < '11:00:00'
  ```
  AFTERNOON TRIPS
  ```
  SELECT count(trip_id) as number_of_afternoon_trips
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE CAST(start_date as time) >= '12:00:00' 
        and  CAST(end_date as time) < '18:00:00'
  ```
    
    There are 350,818 total morning trips and 368,289 total afternoon trips.

### Project Questions - Answers

Answer at least 4 of the questions you identified above You can use either BigQuery or the bq command line tool. Paste your questions, queries and answers below.

- Question 1:
  - Answer: 
  - Sql Query: 
- Question 2:
  - Answer: 
  - Sql Query: 
- Question 3:
  - Answer: 
  - Sql Query: 
- Question 4:
  - Answer: 
  - Sql Query: 

## Part 3 - Employ notebooks to synthesize query project results

### Get Going

Create a Jupyter Notebook against a Python 3 kernel named Project_1.ipynb in the assignment branch of your repo.

**Run queries in the notebook**

At the end of this document is an example Jupyter Notebook you can take a look at and run.

You can run queries using the "bang" command to shell out, such as this:

``
! bq query --use_legacy_sql=FALSE '<your-query-here>'
``

- NOTE:
- Queries that return over 16K rows will not run this way,
- Run groupbys etc in the bq web interface and save that as a table in BQ.
- Max rows is defaulted to 100, use the command line parameter `--max_rows=1000000` to make it larger
- Query those tables the same way as in `example.ipynb`

Or you can use the magic commands, such as this:

```
%%bigquery my_panda_data_frame

select start_station_name, end_station_name
from `bigquery-public-data.san_francisco.bikeshare_trips`
where start_station_name <> end_station_name
limit 10
```
```
my_panda_data_frame
```

**Report in the form of the Jupter Notebook named Project_1.ipynb**

- Using markdown cells, MUST definitively state and answer the two project questions:
  - What are the 5 most popular trips that you would call "commuter trips"?
  - What are your recommendations for offers (justify based on your findings)?
- For any temporary tables (or views) that you created, include the SQL in markdown cells
- Use code cells for SQL you ran to load into Pandas, either using the !bq or the magic commands
- Use code cells to create Pandas formatted output tables (at least 3) to present or support your findings
- Use code cells to create simple data visualizations using Seaborn / Matplotlib (at least 2) to present or support your findings






 
 






 




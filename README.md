# w205 project1

- In the Query Project, you will get practice with SQL while learning about Google Cloud Platform (GCP) and BiqQuery. You'll answer business-driven questions using public datasets housed in GCP. To give you experience with different ways to use those datasets, you will use the web UI (BiqQuery) and the command-line tools, and work with them in Jupyter Notebooks.

## Part 1 - Querying Data with BigQuery

### Some initial queries

Paste your SQL query and answer the question in a sentence. Be sure you properly format your queries and results using markdown.

- What's the size of this dataset? (i.e., how many trips)
- What is the earliest start date and time and latest end date and time for a trip?
- How many bikes are there?

### Questions of your own

- Make up 3 questions and answer them using the Bay Area Bike Share Trips Data. These questions MUST be different than any of the questions and queries you ran above.

- Question 1:
  - Answer:
  - Sql Query:
- Question 2:
  - Answer:
  - Sql Query:
- Question 3:
  - Answer:
  - Sql Query:

## Part 2 - Querying data from the BigQuery CLI

- Use BQ from the Linux command line:
  - General query structure:
  
```bq query --use_legacy_sql=false '
    SELECT count(*)
    FROM
       `bigquery-public-data.san_francisco.bikeshare_trips`'
```

### Queries

1.Rerun the first 3 queries from Part 1 using bq command line tool (Paste your bq queries and results here, using properly formatted markdown):

- What's the size of this dataset? (i.e., how many trips)
- What is the earliest start time and latest end time for a trip?
- How many bikes are there?

2. New Query (Run using bq and paste your SQL query and answer the question in a sentence, using properly formatted markdown):

- How many trips are in the morning vs in the afternoon?

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






 
 






 




Project Details
=================

### Situation:- A Fictitious startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

### Task:- Define fact and dimension tables for a star schema and create ETL pipeline to transfer dataset into SQL tables which allows easy analysis of the data using Python and SQL. Running ETL pipeline on the dataset and ensuring the datatypes are correct and there are unique constraints on the rows inserted. Timestamps are in right format and we do not miss any data due to in correct data type.

### Action :- Execute the ETL without any errors and process log data for Next-Song page events.

### Result :- Analysis on the top users streaming the songs.


NOTE:-
The Database used in this project is on Amazon Web Services - RDS Service, while the notebooks used are hosted on Amazon Sagemaker.
The Data can also be kept on S3 , however i have just kept it locally as it was a small dataset.

The project uses Python 3.7.10 in the .py files.


Song Dataset
============
The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song.

data/song_data

Log Dataset
============
The log files in the dataset are partitioned by year and month. For example, here are filepaths to two files in this dataset.

data/log_data


Schema for Song Play Analysis
==============================

Using the song and log datasets, a star schema optimized for queries on song play analysis has been created. This includes the following tables.
Fact Table

    songplays - records in log data associated with song plays i.e. records with page NextSong
        songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

Dimension Tables

    users - users in the app
        user_id, first_name, last_name, gender, level
    songs - songs in music database
        song_id, title, artist_id, year, duration
    artists - artists in music database
        artist_id, name, location, latitude, longitude
    time - timestamps of records in songplays broken down into specific units
        start_time, hour, day, week, month, year, weekday



The Project included below Important files and the steps to run them:-

etl.ipynb --> This file is the ad-hoc jupyter notebook used to understand and run sample etl's to read and processe a single file from song_data and log_data and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.

create_tables.py --> drops and creates your tables. To drop and re-create your tables before each time you run your ETL scripts. 


test.ipynb -> displays the first few rows of each table to let you check your database. This also has SQL commands to terminate all DB connections to the target DB to be able to drop the tables in the create_tables.py. So, before running create_tables.py this notebook needs to be run and finally the kernel for this notebook needs to be re-started.

etl.py --> reads and processes files from song_data and log_data and loads them into ther tables. 

sql_queries.py --> contains all the sql queries, and is imported into the etl.py, create_tables.py and etl.ipynb
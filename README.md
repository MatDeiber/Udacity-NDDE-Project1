# Udacity-NDDE-Project1

This project is part of Udacity Data Engineer Nanodegree. 

In this project, I applied what I learned on data modeling with Postgres and build an ETL pipeline using Python. The project simulate a startup called Sparkify that wants to analyze the data they've been collecing on songs and user activity on their new music streaming app. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

The project consisted in defining fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.


## How to Run the Python Scripts

First run create_tables.py to reset the tables, then run etl.py to fill the database.

**create_tables.py**: drops and creates your tables.

**etl.py**: reads and processes files from song_data and log_data and loads them into your tables.

**sql_queries.py**: contains all your sql queries.

**etl.ipynb**: reads and processes a single file from song_data and log_data and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.

**test.ipynb**: displays the first few rows of each table to let you check your database.
./data: folder containing the song and log datasets

## Database Schema Design and ETL Pipeline

A standard star model was implemented. 

The song dataset and log dataset provided in JSON format were converted to a postgres database.

The song dataset contains the following entry:

['num_songs', 'artist_id', 'artist_latitude', 'artist_longitude',
       'artist_location', 'artist_name', 'song_id', 'title', 'duration',
       'year']

The log dataset contains the following entry:

['artist', 'auth', 'firstName', 'gender', 'itemInSession', 'lastName',
       'length', 'level', 'location', 'method', 'page', 'registration',
       'sessionId', 'song', 'status', 'ts', 'userAgent', 'userId']

The final database consists of the following tables:

### Fact Table
1. songplays - records in log data associated with song plays i.e. records with page NextSong
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
### Dimension Tables
2. users - users in the app
user_id, first_name, last_name, gender, level
3. songs - songs in music database
song_id, title, artist_id, year, duration
4. artists - artists in music database
artist_id, name, location, latitude, longitude
5. time - timestamps of records in songplays broken down into specific units
start_time, hour, day, week, month, year, weekday

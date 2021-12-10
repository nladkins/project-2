# Project-2-Data_Gurus

# ETL Using Pandas

## Background

The two largest companies by market capitalization are Google and Apple, according to Companies Market Cap (retrieved on 12/7/2021).  Performing a comparison of these two companies over the past 15 years to see how they performed against one another was the focus of this project.  However, the only goal was to perform the ETL portion that would lead to an analysis at a later point in time.  In other words, the actually analysis (e.g., plotting, etc.) is not in scope.  

## Datasets

Two datasets were retrieved from Kaggle that pertained to Apple and Microsoft trading data (https://www.kaggle.com/nikhilkohli/us-stock-market-data-60-extracted-features).  The timeframe for both company stocks that were analyzed were between October 2005 to August 2020.  These were in .csv format.

## Coding

### Dependencies

Dependencies included Pandas, date time, sqlalchemy, and psycopg2.  

![image size](/markdown/dependencies.jpg){:height="50px" width="50px"}


### Evaluating the data.

The Microsoft data (MSFT.csv) and the Apple data (AAPL.csv) was imported and the data was previewed using Pandas.  There were ~64 columns of data.  The first thing that was done is that the data was filtered (iloc) to six columns which was the trading date, the opening price, high and low prices for each session, the closing price, and the volume that was exchanged for each session.  These were still two separate data frames for each of the companies.

![Data Preview](markdown/preview_data.jpg?raw=true "Title"){:height="100px" width="125px"}  

![Data Preview](markdown/cleaning.jpg.jpg?raw=true "Title"){:height="100px" width="125px"}


### Data Cleansing

Following this, the data was evaluating to identify any null values which, had there been, we would have dropped those rows.  In this case, there were no null values.  Once this was known, a pd.merge script was run to join the two data sets using the "Date" field which only brought in those columns mentioned above as the others were dropped.  Because the join results in two columns with a "x" and "y" for each one (e.g., "Open_x", "Open_y", "High_x", etc.), the columns were renamed consistent with how we planned to import the data into Postgres.  

The next step was evaluating the data types.  With the exception of volume, every column reflected as a float.  The volume was an integer and the "date" was an object.  Therefore, the only column that required a change in the data type was the "date".  The datetime code was used to change the data type for that particular column.  

### Exporting to Postgres

For the export process, sql was used for this as it was clear that any future use of the datasets seemed relational in nature (e.g., the use of primary keys, etc.).  Sqlalchemy's "declaritive_base" and "create_engine" features were used for creating a Postgres path and exporting the DataFrame into sql file that can be imported into Postgres.  Furthermore, a sql query was generated that would streamline someone's ability to create a table with this new data.  A gitignore was used for the "secret" file that included the password.  If someone were to reuse this code, this file would need to be generated as well as a predefined database named "tech_stocks".  Lastly, the final data frame was also exported as a csv ("finalTechStocks.csv").

## Conclusion

As mentioned, this exercise was intended to serve as an illustration for ETL that could then support a follow-on analysis, such as the historical performance comparison between these two companies.  Perhaps an exercise for another time.  

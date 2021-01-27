# Movies-ETL

## Overview : 
    
   Wikipedia has a ton of information about movies, including budgets and box office returns, cast and crew, production and distribution, and so much more. Luckily, one of Britta's coworkers created a script to go through a list of movies on Wikipedia from 1990 to 2018 and extract the data from the sidebar into a JSON. 
    
   Amazing Prime loves the dataset and wants to keep it updated on a daily basis. Britta needs  help to create an automated pipeline that takes in new data, performs the appropriate transformations, and loads the data into existing tables. Code refactored  to create one function that takes in the three files Wikipedia data, Kaggle metadata, and the MovieLens rating data and performs the ETL process by adding the data to a PostgreSQL database.
    
   Results  
### Deliverable 1: Write an ETL function to read three data files
* An ETL function is written to read in the three data files.

* The function converts the Wikipedia JSON file to a Pandas DataFrame, and the [DataFrame](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d1_1_wiki_movies.png) is displayed in the ETL_function_test.ipynb file.

* The function converts the Kaggle metadata file to a Pandas DataFrame, and the [DataFrame](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d1_2_kaggle_md.png) is displayed in the ETL_function_test.ipynb file.

* The function converts the MovieLens ratings data file to a Pandas DataFrame, and the [DataFrame](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d1_3_ratingsdf.png) is displayed in the ETL_function_test.ipynb file.

### Deliverable 2: Extract and Transform the Wikipedia Data

* The TV shows are filtered out, and the wiki_movies_df DataFrame is created.

* A try-except block is used to catch errors while extracting the IMDb IDs with a regular expression and dropping duplicate IDs.

* The extraction and transformation of the Wikipedia data in the ETL function does the following:
 * A list comprehension is used to keep columns with non-null values.
 * The non-null box office data is converted to string values using the lambda and join functions.

* A regular expression is used to match the six elements of "form_one" of the box office data.

* A regular expression is used to match the three elements of "form_two" of the box office data.

* The following columns are cleaned in the Wikipedia DataFrame:
  * The box office column
  * The budget column
  * The release date column
  * The running time column
  
* The [movies_df](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d2_1.png) and the [movies_df columns](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d2_2.png) are displayed in the ETL_clean_wiki_movies.ipynb file.

### Deliverable 3: Extract and Transform the Kaggle Data

* The extraction and transformation of the Kaggle metadata using the ETL function does the following:
 * The Kaggle metadata is cleaned.
 * The Wikipedia and Kaggle DataFrames are merged.
 
 * The following is performed on the merged Wikipedia and Kaggle DataFrames to create the movies_df:
  * Unnecessary columns are dropped.
  * A function is used to fill in the missing Kaggle data.
  * The movies_df DataFrame is filtered to keep specific columns.
  * The movies_df DataFrame columns are renamed.

* The extraction and transformation of the MovieLens ratings data using the ETL function does the following:
 * The ratings counts are cleaned.
 * The movies_df DataFrame is merged with the cleaned ratings DataFrame to create the movies_with_ratings_df DataFrame.
 * The empty values in the movies_with_ratings_df DataFrame are filled with “0”.

* The [wiki_movies_df](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d3_1.png) , [movies_with_ratings_df](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d3_2.png)  and the [movies_df DataFrames](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/d3_3.png) are displayed in the ETL_clean_kaggle_data.ipynb file.

### Deliverable 4: Create the Movie Database

* The data from the movies_df DataFrame replaces the current data in the movies table in the SQL database, as determined by the [movies_query.png](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/movies_query.png).

* The data from the MovieLens rating CSV file is added to the ratings table in the SQL database, as determined by the [ratings_query.png](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/rating_query.png).

* The [time_elapsed](https://github.com/raajasrini/Movies-ETL/blob/main/Resources/time_elapsed.png) to add the data to the database is displayed in the ETL_create_database.ipynb file.
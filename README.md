
# Peter best Sellers
## Project 4
# Use tools learned and skills gained through the past modules to work as a team.

## Team
* Rob Cortes
* Fatou Gai
* Stephanie Wolter
* Ochirbat Munkhchuluun

# PeterbestSellers
* Given historical data, given specific parameters do we think a book will get on that list?
**lots more summary**

## SetUp

* Repository: [Peter best Sellers](https://github.com/StephWolter/PeterbestSellers.git)

* File Structure:

        * ReadMe.md


* Presentation in Google Slides: []()

# Project Overview


## Step 1: Setting Up
### Conceptualized
* Discussed logical next steps to extend our previous research.
* Discussed where machine learning and big data manipulation would work best.
### Scoped out data to support a plan
* Found fields provided by OpenLibrary API
### Collaboration SetUp
* Set up DataBricks Workspace and linked AWS account for collaborative workspace
* Set up GitHub Repository

## Step 2: Gathering, Cleaning, and Processing Data
###  Data Sources
* Open Library
* Previous NYT Bestseller List Data

### Cleaned and Processed Data
** Pulled large volumes of data from Open Library to expand and complement historical book data previously acquired from the NYT Bestsellers data .
* Removed columns that were not needed in our analysis.
* Filtered dataset down to books published and printed in English .

### Interfaces and libraries used:

* Databricks
       * Used DataBricks as a group to collaborate on processing Open Library big data
       *        * Databricks played a big role in its ability to import and handle big data, which we experienced through the Databricks File System (DBFS).
         1) Initially distributed data during preprocessing in order to do synchronous collaboration, however, after several GBs worth of files imported, we found it difficult to work there together as commands took significant amounts of time to load.
                * Team had to fight for resources, running script took long times
         3) Issues sharing files and tables.
       
       * Used DataBricks individually to process and run models
         1) Used Jupyter-notebook to create parquet files
         2) Was able to seamlessly integrate csv, parquet, and text files.
         3) Ran big data (27 mill rows) in a range from seconds - 10 minutes.
* List of Spark components and libraries used; SparkSQL, Spark Parquet.
* Adapted some libraries; does not work well with sklearn so had to switch to pyspark
* Libraries imported:
![image](https://github.com/StephWolter/PeterbestSellers/blob/main/Images/databricksImports.png?raw=true)

* Jupyter Notebook and Google Colab allowed for the performance of data preprocessing tasks including the handling of missing/null values, dropping and creating columns, transforming variables, visualizing data, and encoding categorical features. Most importantly, they allowed for the creation and export of dataframes in various file types, such as parquet, csv, and JSON which we imported and further manipulated in our collaborative Databricks workspace.

* Databricks, Colab as well as Jupyter Notebook were also used to evaluate the performance of our various trained models using various metrics like accuracy, precision, recall, F1-score, and AUC.
* PySpark was used extensively for big data loading and exploration.
*        Led to easy manipulation and of the large datasets we were dealing with.
  
## Step 3: Data Model Implementation and Optimizations
### Machine Learning Model - Predicting Fiction vs. Nonfiction
We created a text classification model that takes the titles and descriptions of NYT bestsellers and predicts whether the book is fiction or nonfiction. 

To create a DataFrame with title/descriptions and a binary is_fiction target array, the following steps were taken:
1) Read results.csv, books.csv, and lists.csv into Pandas, and merge the tables into a single DataFrame containing the book titles, book descriptions, and list id's. The first 5 rows of this DataFrame show the same book, because this book appeared on multiple bestseller lists.
![image](https://github.com/StephWolter/PeterbestSellers/assets/124944383/cad932e5-2080-470c-af40-9f24fb872cfd)
2) Create two arrays of list_id's: one array for fiction books and another for nonfiction books.
3) Define a function, is_fiction(value), that returns 1 if a given list_id is in the fiction array and a 0 if the list_id is in the nonfiction array.
4) Apply this function to the DataFrame and add a column by running bl_full['is_fiction'] = bl_full['list_id'].map(is_fiction).
5) Add a column, title_desc, that concatenates the book title and the book description.
6) Extract the title_desc and is_fiction columns from the bl_full DataFrame, then drop duplicates and drop NaN's.
The resulting DataFrame contains unique book title-descriptions and binary is_fiction values.
![image](https://github.com/StephWolter/PeterbestSellers/assets/124944383/ed8ab8c1-2065-4a1e-bf46-223059b693bd)

Next, we preprocess the book title-descriptions:
1) Remove punctuations by calling str.replace('[^\w\s]','') on the title_desc series.
2) Split the text into words or subword units using Tensor Flow's tokenizer class.
3) Pad the text so that all the strings are of the same length.
The outcome of this process is an array of tokenized, padded text values, called X_text_padded

After designating our target (y) array, we split X_text_padded and y into training and testing sets using sklearn's train_test_split(). 

Our first iteration of the model consists of three layers: 
1) An initial Dense layer with relu activation and 200 neurons.
2) A hidden Dense layer with relu activation and 32 neurons.
3) An output Dense layer with sigmoid activation.

Our second iteration of the model takes advantage of word embedding, which creates vector representations of the title_descriptions. The second model's layers are:
1) An initial embedding layer.
2) A dropout layer that randomly sets 0.2 of the input units to 0 during training. This mitigates overfitting.
3) A pooling layer that reduces the 2D vector output of the prior layers to 1D vector output.
4) A hidden Dense layer with relu activation and 32 neurons.
5) An output Dense layer with sigmoid activation.

The 2nd model performs better than the 1st model, as shown below. This demonstrates the benefits of embedding layers.

![image](https://github.com/StephWolter/PeterbestSellers/assets/124944383/aa0a0186-20fe-440b-9392-98423dd9017f)
![image](https://github.com/StephWolter/PeterbestSellers/assets/124944383/bf0e28e4-ad52-4def-97c0-e973e2b717d6)

### High-Rated Books in NYT Data

Downloading and Clearing Codes from Open Library Dump
1) Obtain the Open Library dump containing the codes you need.
2) Open the file using a text editor or spreadsheet software.
3) Remove unnecessary data and columns not needed for analysis.
4) Clean up the data, handle missing values, correct errors, and format inconsistencies.
5) Save the cleaned data.

Joining Works Data and Ratings Data
1) Download Works Data and Ratings Data from Open Library or other sources.
2) Import the data into your data analysis tool or programming environment.
3) Merge the Works Data and Ratings Data based on "work_key" to create a combined dataset.
4) Keep only "title" and "ratings" columns, removing unnecessary ones.
5) Filter the data to retain ratings of 4s and 5s, removing other ratings.
6) Save the filtered data.

Counting High-Rated Books
1) Upload CSV files to Google Colab or your environment.
2) Use pandas to read and merge the CSV files based on "title".
3) Filter the merged data to retain only books with high ratings (4s and 5s).
4) Count the number of high-rated books in the NYT data.

## Analysis of ML performance/ predictive power


## Step ___: Presenting
## Data Analysis and Vizualizations
*
## Created Powerpoint of presentation
* Created in Microsoft Powerpoint
* Shared with team and edited in Google Slides.
* Practiced

## Created ReadMe
* Huzzah!
















  

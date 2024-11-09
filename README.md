# Business Understanding

Your company now sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies. You are charged with exploring what types of films are currently doing the best at the box office. You must then translate those findings into actionable insights that the head of your company's new movie studio can use to help decide what type of films to create.

# Data Understanding

The data for the solving the business problem comes from the following sources: Box Office Mojo (https://www.boxofficemojo.com/), IMDB (https://www.imdb.com/), Rotten Tomatos (https://www.rottentomatoes.com/), The Movie Database (https://www.themoviedb.org/?language=en-US), and The Numbers (https://www.the-numbers.com/).

Before solving for the business problem, I want to examine data from the aforementioned sources.  When I conduct exploratory data analysis of data, I aim to understand the following attributes:

1. Number of columns
2. Number of rows
3. Columns Names

## IMDB | Data Understanding

The dataset for IMDB is contained within a zip file.  Before conducting exploratory data analysis, I will need to unzip the file.  Subsequently, I will utilize the following method - 'pd.read_sql' - to open any files and undestand the associated tables.

### Conclusion

I have completed the exploratory data analysis of the IMDB zip file. Within the zip file, there was only one file, which was titled "im.db". Upon unzipping the file, I utilized the following code - 'cursor.execute("SELECT name FROM sqlite_master WHERE type='table';")' - to understand the various tables.

The tables within the im.db file are the following: *movie_basics*, *directors*, *known_for*, *movie_akas*, *movie_ratings*, *persons*, *principals*, *writers*. This is congruent with the entity relationship diagram (ERD). Upon ascertaining the various tables, I explored the different columns within each table.

I decided to place the *movie_basics* table into a dataframe, which is titled *df_imdb_movie_basics*. The tables has a total of 146,144 rows and 6 columns. The movie_basics table has a column - *runtime_minutes* - that I am interested in using for analytics. However, there are 31,739 cells within the runtime_minutes column that has null values. I may have to delete the rows to further my eventual analysis.

## Box Office Mojo | Data Understanding

The dataset for Box Office Mojo is contained within a csv file.  I will utilize the following method - 'pd.read_csv()' - to examine the contents of the csv file.

### Conclusion

I have completed the exploratory data analysis of the csv file associated with Box Office Mojo.  I placed the contents of the csv file into a dataframe titled *df_bom*.  *Df_bom* has the following five columns - *title*, *studio*, *domestic_gross*, *foreign_gross*, and *year*.  *Df_bom* has a total of 3,387 rows. 

## Rotten Tomatoes (Movie Information) | Data Understanding

One of the datasets for Rotten Tomatoes is contained within a tsv file.  The data within the tsv file provides movie information.  I will utilize the following method - 'pd.read_csv()' - to examine the contents of the tsv file. 

### Conclusion

I have completed the exploratory data analysis of the tsv file associated with the Rotten Tomatoes dataset.  I placed the contents of the tsv file into a dataframe titled *df_rotten_movie*.  *Df_rotten_movie* has the following 12 columns - *id*, *synopsis*, *rating*, *genre*, *director*, *writer*, *theater_date*, *dvd_date*, *currency*, *box_office*, *runtime*, and *studio*.  *Df_rotten_movie* has a total of 1,560 rows.

## Rotten Tomatoes (Reviews) | Data Understanding

The second dataset for Rotten Tomatoes is also contained within a tsv file.  The data within the tsv file provides movie critic information.  I will utilize the following method - 'pd.read_csv()' - to examine the contents of the tsv file.

### Conclusion

I have completed the exploratory data analysis of the tsv file associated with the second Rotten Tomatoes dataset.  I placed the contents of the tsv file into a dataframe titled *df_rotten_reviews*.  *Df_rotten_reviews* has the following 8 columns - *id*, *review*, *rating*, *fresh*, *critic*, *top_critic*, *publisher*, *date*.  *Df_rotten_reviews* has a total of 54,432 rows of data.

## The Movie DB | Data Understanding

The dataset for the Movie Database is contained within a csv file.  I will utilize the following method - 'pd.read_csv()' - to examine the contents of the csv file.  

### Conclusion

I have completed the exploratory data analysis of the csv file associated with the Movie Database dataset.  I placed the contents of the csv file into a dataframe titled *df_movie_db*.  *Df_movie_db* has the following 9 columns - *genre_ids*, *id*, *original_language*, *original_title*, *popularity*, *release_date*, *title*, *vote_average*, and *vote_count*.  *Df_movie_db* has a total of 26,517 rows of data.

## The Numbers | Data Understanding

The dataset for the Numbers is contained within a csv file.  I will utilize the the following method - 'pd.read_csv()' - to examine the contents of the csv file.

### Conclusion

I have completed the exploratory data analysis of the csv file associated with the Numbers dataset.  I placed the contents of the csv file into a dataframe titled *df_numbers*.  *Df_numbers* has the following 6 columns - *id*, *release_date*, *movie*, *production_budget*, *domestic_gross*, and *worldwide_gross*.  *Df_numbers* has a total of 5,782 rows of data.

## Completing Exploratory Data Analysis

I completed my exploratory data analysis of the files from the following sources: IMDB, Box Office Mojo, Rotten Tomatos, the Movie DB, and the Numbers.  I want to combine the IMDB and the Numbers dataframes in order to acquire insights into the financial drivers of movies.  I can actually utilize the Box Office dataframe in lieu of The Numbers dataframe; however, I am using The Numbers dataframe for the following reasons:

- The Numbers dataframe contains more rows of data than Box Office Mojo (The Numbers dataset has 5,782 rows, while Box Office Mojo dataset has 3,387 rows)
- The Numbers dataframe contains financial data relatin to worldwide gross, and Box Office Mojo does not have this data

Before combining the IMDB and The Numbers dataframes, I will need to transform the Numbers dataframe.  Transformations will include the following:

- Converting the numerical data - in particular, the production budget, domestic gross, and worldwide gross data - from string data to float
- Creating a new column - *Net Profit* - by subtracting production budget from worldwide gross

# Data Preparation

## The Numbers Dataframe Transformation

As part of the first phase of Data Preparation, I am going to transform the Numbers dataframe via the following phases:  

- Converting the numerical data - in particular, the production budget, domestic gross, and worldwide gross data - from string data to float
- Creating a new column - *Net Profit* - by subtracting production budget from worldwide gross 

### The Numbers Dataframe Transformation (Conclusion)

I completed the transformation of the Numbers dataframe - "df_numbers".  Before converting the numerical data - in particular, the production budget, domestic gross, and worldwide gross data - from string data to float, I had to remove the dollar signs and commas.  I was then able to use the method - 'pd.to_numeric()' - to actually convert the production budget, domestic gross, and worldwide gross data from string to float.

## Merging IMDB with The Numbers

As a reminder, I want to perform the left join of both dataframes - "df_numbers" and "df_imdb_movie_basics" - with df_numbers as the left table.  I want to use the *movie* column from the df_numbers dataframe and the *primary title* column from the df_imdb_movie_basics in order to perform the left join.  Before performing the left join, I am going to check for duplicates in the aforementioned columns. 

I utilized the following code - 'df_numbers['movie'].duplicated().sum()' - to check for duplicates in the *movie* column of the Numbers dataframe. There is a sum of 84 duplicates for the *movie* column in the df_numbers dataframe.  I am going to visually inspect the duplicates in the respective dataframe.

After further reviewing the duplicates in the *movie* column in the df_numbers dataframe, I noticed that there are movies with the same title, but they have different release dates.  In reality, they are actually different movies.  For example, *Robin Hood* has release dates of May 14th, 2010, and November 21st, 2018.  These are different movies because Robin Hood has been created multiple times within Hollywood.  Now, I am going to check for duplicates in the *primary_title* column of the "df_imdb_movie_basics" dataframe.

I utilized the following code - 'df_imdb_movie_basics['primary_title'].duplicated().sum()' - to check for duplicates in the *primary title* column in the "df_imdb_movie_basics" dataframe.  There is a sum of 10,073 duplicates for the *primary title* column in the df_imdb_movie_basics dataframe.  I am going to examine the duplicates in the respective dataframe.

After running the following code - 'df_imdb_movie_basics[df_imdb_movie_basics['primary_title'].duplicated(keep=False)][0:60]' -  I still do not know why there are duplicates. However, I am only interested in the data for the following column - df_imdb_movie_basics['runtime_minutes']. There are null values for the column - df_imdb_movie_basics['runtime_minutes']. As a result, I am going to delete the rows with these null values from the dataframe.

Eliminating the rows with null values in the 'runtime_minutes' column reduced the number of duplicates from 10,073 to 6,946.  However, duplicates still persist in the df_imdb_movie_basics dataframe.  Instead of only using the movie column from the df_numbers dataframe and the primary title column from the df_imdb_movie_basics for the left join, I will enhance the left join by using an additional column that references the release year from both dataframes. 

### Merging IMDB with The Numbers (Conclusion)

I have completed performing the left join of both dataframes - "df_numbers" and "df_imdb_movie_basics" - with df_numbers as the left table.  After performing the join, I created a new dataframe - "df_imdb_numbers" - that had 5,833 rows of data.  There were also 4,312 cells in the *runtime_minutes* column that had null values.  Since the column - *runtime_minutes* - is crucial for my analysis and modeling, I decided to delete the respective rows.  The new dataframe - "df_imdb_numbers" - now has 1,521 rows of data.

# Modeling

I have concluded preparing the data.  To gain insights into the financial drivers of creating movies, I am going to start by determining the correlations and creating scatterplots for the following variable pairs.
 
 - Runtime (independent variable) vs. Production Budget (dependent variable)
 - Production Budget (independent variable) vs. Net Profit (dependent variable)
 - Runtime (independent variable) vs. Net Profit (depdendent variable)

If any of the scatterplots display linearity, I will progress with creating a simple linear regression model, and testing the assumptions of the respective simple linear regression model.

## Runtime vs. Production Budget

I am going to calculate the correlation coefficient between runtime (independent variable) vs. production budget (dependent variable).  I am also going create a scatterplot of runtime (independent variable) vs. production budget (dependent variable).  The correlation coefficient and visualization is below.

The correlation coefficient is 0.35, which is a weak correlation between runtime and production budget.

The data points are clustered in the bottom right of the visualization.  

Based on the correlation coefficient and visualization, I determine there is a lack of a linear relationship between runtime and production budget.  As a result, I will not progress with creating a simple linear regression with the aforementioned variables.

## Runtime vs. Net Profit

I am going to calculate the correlation coefficient between runtime (independent variable) vs. net profit (dependent variable).  I am also going create a scatterplot of runtime (independent variable) vs. net profit (dependent variable).  The correlation coefficient and visualization is below.

The correlation coefficient is 0.27, which is a weak correlation between runtime and net profit.

The data points are clustered in the bottom right of the visualization. 

Based on the correlation coefficient and visualization, I determine there is a lack of a linear relationship between runtime and net profit. As a result, I will not progress with creating a simple linear regression with the aforementioned variables.

## Production Budget vs. Net Profit

I am going to calculate the correlation coefficient between production budget (independent variable) vs. net profit (dependent variable).  I am also going create a scatterplot of production budget (independent variable) vs. net profit (dependent variable).  The correlation coefficient and visualization is below.

The correlation coefficient is 0.66, which is a strong correlation between production budget and net profit.

The majority of data points are clustered in the bottom left quadrant of the visualization.  Based on the visualization, it appears that not all movies become a *blockbuster* hit based on the production budget.  

In spite of the clustering, there still appears to be a linear relationship between production budget and net profit based on the correlation coefficient and visualization.  As a result, I will proceed with creating a simple linear regression model with the aforementioned variables.

### Production Budget vs. Net Profit | Simple Linear Regression Model

Based on the simple linear regression model, for every dollar that is spent on the production budget, net profit increases by approximately two dollars and twenty-nine cents.  The p-value for the production budget coefficient is 0.00.  Since it is less than the standard alpha of 0.05, the coefficient for production budget is statistically significant.

R-Squared, or the coefficient of determination, is 0.444.  In other words, the model is explaining 4.44% of the variation in net profit.

However, I am noticing a few problem areas within the model.

The value for skew is 1.792.  Common practice is that a value for skew between the range of -1 to 1 is a normal distribution.  Since the value for skew is 1.792, there is a positive skew, or a longer tail on the right side of the distribution.

The value for kurtosis is 15.806.  A kurtosis value of 3 indicates a normal distribution.  Since 15.806 is greater than 3, this indicates the model has many outliers.  This is congruent with a prior observation that not all movies become a blockbuster hit.

The Durbin-Watson number is 1.337.  The Durbin-Watson number can range from 0 to 4.  Since the Durbin-Watson number - 1.337 - is less than 1.5, there is an indication of positive autocorrelation.  Autocorrelation is a violation of the simple linear regression model assumption - independence of errors.

The model residuals p-value - or *Prob(JB)* - is 0.00.  This is less than the standard alpha of 0.05.  In the case of the Jarque-Bera test, the null hypothesis is that the model residuals distribution is normal.  As a result, the p-value of 0.00 informs that the null hypothesis can be rejected, or the distribution of the model residuals is not normal.  This is a violation of one of the assumptions of simple linear regression model, or homoscedasticity. 

I am going to examine the potential observed shortcomings of the model - in particular, the simple linear regression model assumptions.

#### Production Budget vs. Net Profit | Simple Linear Regression Model Assumptions

Based on my simple linear regression model results summary, there is evidence that the following simple linear regression model assumptions are not present within the model, which are the following:

- Indepdendence of Errors 
- Normal Distribution (of Residuals)
- Homoscedasticity

I will use visualizations to further examine the normal distribution of the residuals, and homoscedasticity within the simple linear regression model assumptions.

**Normal Distribution (of Residuals)**

I created a histogram of the residuals.  A normal distribution is associated with a bell-shaped curve, which is evident in the histogram plot.

I also created a Q-Q plot to evidence whether or not there is a normal distribution of the residuals, which is one of the assumptions of a simple linear regression.  The residuals do not remain constant on the diagonal line in the Q-Q plot.  

The aforementioned divergence in the Q-Q plot evidences that the residuals do not have a normal distribution. 

**Homoscedasticity**

Heteroscedasticity is present within the single linear regression model.  The residuals tend to fan out, which is a contrast of homoscedasticity.

# Overall Conclusion and Recommendations

Recommendations are the following:

**1. Runtime vs. Production Budget**

First recommendation is not to utilize runtime to establish or determine a linear relationship with production budget.  I attempted to determine whether or not there is a correlation between Runtime and Production Budget.  I did not determine a strong correlation.  As a result, I did not progress to create a single linear regression model.

**2. Runtime vs. Net Profit**

Second recommendation is not to utilize runtime to establish or determine a linear relationship with net profit.  I did not determine a strong corrleation between the two variables.  As a result, I did not progress to create a single linear regression model. 

**3. Production Budget vs. Net Profit**

My third recommendation is not to utilize a single linear regression model with Production Budget as the independent variable, and Net Profit as the dependent variable.  I determined a strong correlation between Production Budget and Net Profit.  As a result, I progressed with creating a single linear regression model.  However, the single linear regression model assumptions - 1) Independence of Errors, 2) Normal Distribution of Residuals, and 3) Homoscedasticity - did not hold.

# Next Steps

Next steps are the following:

**1. Refine Financial Metrics**

I created a Net Profit variable by subtracting Production Budget from Worldwide Gross.  However, there are more variables to consider when calculating Net Profit.  This includes, but not limited to, DVD sales, streaming sales, multiple releases, and intangible assets - for example, brand equity.  I will have to obtain more movie data to ascertain the aforementioned variable information.

**2. Consider other Attributes for Modeling**

There are attributes that may be utilized to understand the financial drivers for movies.  This includes genre, studio, and language.  Genre and studio are more intuitive.  An action movie may have a larger production budget than a romantic comedy due to the expenses of special effects.  A larger studio house - for example, Warner Brothers, Paramount Pictures, or Metro-Goldwyn-Mayer - would potentially have a higher capacity to allocate more funding to creating a movie than a boutique studio.

I state language as an attribute becuase it may be indicative of which country the movie production takes place.  For example, a Hollywood movie may have a larger production budget than a Korean drama.

**3. Apply Different Regression Models**

I aimed to demonstrate a linear relationship for the different variable pairs.

However, the same variable pairs may have different relationships - for example, exponential.  Moreover, logistic regression is more appropriate for categorical variables such as genre, studio, and language.

There are multiple datasets that I examined at the beginning of this project.  They can be revisited by applying different regression models.


# DSA 4060 – Week 2 Practical Task

**Student:** Samantha Nyatichi Masaki  
**Course:** DSA 4060  
**Practical:** Week 2 – Recommendation Data and Popularity Baselines

## Recommendation Data and Popularity-Based Movie Recommender

## Project Overview

This project was completed as part of the **DSA 4060 Week 2 Practical Task**. The objective is to clean and explore movie-rating interaction data, calculate user-item matrix sparsity, and develop a simple popularity-based recommender.

The practical covers:

- Loading and inspecting the movie-rating dataset
- Cleaning duplicate and incomplete records
- Exploring users, movies, and ratings
- Creating a user-item interaction matrix
- Calculating matrix sparsity
- Building a popularity-based recommender
- Selecting the top 10 eligible movies
- Interpreting the results, advantages, and limitations

The popularity-based recommender is a baseline system. It ranks movies using ratings across the dataset rather than personalising recommendations for individual users.

## Dataset

The dataset supplied for this practical is:

`DSA_4060_Week2_Movie_Ratings.csv`

The analysis uses these fields:

| Column | Description |
|---|---|
| `user_id` | Identifier for a user |
| `movie_id` | Identifier for a movie |
| `rating` | Rating given by a user |
| `timestamp` | Time associated with the rating |

The notebook checks the observed rating values before validating the rating scale. The expected rating range should match the lecturer-provided dataset.

## Project Objectives

1. Inspect the dataset's structure and quality.
2. Remove duplicate records and records with missing or blank user/movie IDs.
3. Validate ratings against the expected rating scale.
4. Calculate interaction statistics.
5. Create a user-item interaction matrix.
6. Calculate the matrix sparsity.
7. Build a popularity-based recommendation baseline.
8. Recommend up to 10 movies with at least 10 ratings.
9. Interpret the results and discuss limitations.

## 1. Data Loading and Inspection

The dataset was loaded using **pandas**. Initial inspection included the first 10 records, dataset dimensions, data types, missing values, and duplicate records. This helped establish the structure and quality of the data before analysis.

## 2. Data Cleaning

The cleaning process included:

- Removing duplicate records.
- Removing records with missing user IDs or movie IDs.
- Removing blank user and movie IDs.
- Converting ratings to numeric values.
- Removing missing or non-numeric ratings.
- Checking the observed rating range and excluding ratings outside the configured valid range.

The cleaned data was used for the remaining analysis. The rating validation settings in the notebook should be consistent with the scale documented for the supplied dataset.

## 3. Exploratory Data Analysis

The notebook calculated the following statistics from the cleaned dataset:

| Measure | Result |
|---|---:|
| Valid rating records | 500 |
| Unique users | 50 |
| Unique movies | 24 |
| Most active user | U010 |
| Most-rated movie | M005 |
| Average rating | Approximately 3.5 / 5 |

The most active user is the user with the highest number of rating records. The most-rated movie is the movie with the largest number of rating records. The average rating provides a general indication of how movies were rated across the dataset.

## 4. User-Item Interaction Matrix

A user-item interaction matrix was created with users as rows, movies as columns, and ratings as cell values. A missing cell indicates that the corresponding user-movie pair has no recorded rating.

The matrix contains:

- **50 user rows**
- **24 movie columns**
- **1,200 possible user-movie combinations**

The matrix provides a structured representation of the interactions and is useful for understanding how much rating data is available.

## 5. Dataset Sparsity

Sparsity measures the proportion of possible user-movie combinations that do not have an observed rating.

The formula used is:

```text
Sparsity = 1 - (Observed unique user-movie pairs /
                (Number of users × Number of movies))
```

The notebook reports a sparsity of approximately **64.17%**. This corresponds to 430 observed unique user-movie pairs out of 1,200 possible combinations. The remaining combinations have no recorded interaction.

The dataset contains 500 rating records, but the number of unique user-movie pairs can be lower if a user has more than one rating record for the same movie. This is why the sparsity calculation counts distinct user-movie pairs rather than simply counting all rating records.

A relatively sparse interaction matrix means that many possible user-movie combinations have no rating, which is a common challenge in recommender systems.

## 6. Popularity-Based Recommender

For every movie, the notebook calculates:

1. Average rating
2. Number of ratings

Only movies with **at least 10 ratings** are eligible for recommendation. Eligible movies are ranked by average rating in descending order. Number of ratings is used to break ties, followed by movie ID to make the ordering consistent.

The notebook identified **24 eligible movies** and returned **10 recommendations**.

The recommendations are saved to:

`outputs/top_10_recommendations.csv`

The CSV contains the results generated from the actual dataset. Movie titles are not included unless a movie-title field or separate movie metadata file is available and merged with the results.

## 7. Interpretation of the Results

The recommender selected the top 10 movies from the 24 eligible movies. These movies rank highest according to their average ratings, with the number of ratings used to break ties. The requirement of at least 10 ratings helps avoid ranking movies based on very limited feedback.

### Advantage

Popularity-based recommendation is simple, computationally inexpensive, and easy to explain. It also provides a useful baseline against which more advanced recommendation methods can be compared.

### Limitations

1. **Lack of personalisation:** Users with different preferences receive the same ranked list.
2. **Popularity bias:** Less popular or niche movies may be overlooked even when they would suit a particular user's interests.

## 8. Technologies Used

- **Python** — programming language used for the analysis
- **Jupyter Notebook** — interactive environment for code and explanations
- **pandas** — data loading, cleaning, grouping, and analysis
- **NumPy** — numerical computing support
- **Visual Studio Code** — development environment

## 9. Repository Structure

```text
DSA_4060_Week2/
├── DSA_4060_Week2_Movie_Ratings.csv
├── week2_recommender.ipynb
├── README.md
└── outputs/
    └── top_10_recommendations.csv
```

### File Descriptions

- **`DSA_4060_Week2_Movie_Ratings.csv`** — lecturer-provided movie-rating dataset.
- **`week2_recommender.ipynb`** — notebook containing the code, outputs, and Markdown explanations.
- **`outputs/top_10_recommendations.csv`** — CSV file containing the top 10 recommendations.
- **`README.md`** — project overview, methodology, findings, and instructions.

Only include the dataset in a public repository if you have permission to redistribute it.

## 10. How to Run the Project

### Step 1: Clone the repository

After uploading the project to GitHub, clone your repository using its actual URL:

```bash
git clone https://github.com/SamanthaMasaki/DSA4060-Week2-Recommendation.git
```

### Step 2: Open the project folder

```bash
cd DSA4060-Week2-Recommendation
```

If you use a different repository name, replace the folder name with your actual one.

### Step 3: Install the required packages

```bash
python -m pip install pandas numpy jupyter ipykernel
```

### Step 4: Open the notebook

Open `week2_recommender.ipynb` in Visual Studio Code with the Jupyter extension, or run:

```bash
jupyter notebook
```

### Step 5: Run the notebook

Run all cells from top to bottom. The notebook loads the dataset, inspects and cleans the records, performs exploratory analysis, creates the user-item matrix, calculates sparsity, generates the recommendations, and saves the output CSV.

## 11. Key Findings Summary

| Measure | Result |
|---|---:|
| Valid rating records | 500 |
| Unique users | 50 |
| Unique movies | 24 |
| Possible user-movie combinations | 1,200 |
| Observed unique user-movie pairs | 430 |
| Matrix sparsity | Approximately 64.17% |
| Average rating | Approximately 3.5 / 5 |
| Most active user | U010 |
| Most-rated movie | M005 |
| Minimum ratings for recommendation | 10 |
| Eligible movies | 24 |
| Recommendations generated | 10 |

## 12. Conclusion

This practical demonstrated how movie-rating data can be prepared and analysed for a recommendation system. The dataset was inspected and cleaned, and exploratory analysis was used to summarise user activity, movie activity, and overall ratings.

A user-item interaction matrix was created with 50 users and 24 movies. Based on 430 observed unique user-movie pairs out of 1,200 possible combinations, the notebook reports approximately 64.17% sparsity.

Finally, a popularity-based recommender calculated each movie's average rating and rating count, retained movies with at least 10 ratings, and selected the top 10 recommendations. Although this method does not personalise results for each user, it provides a straightforward baseline for future comparison with more advanced recommender systems.

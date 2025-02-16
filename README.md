# NYT-Bestsellers-Analysis

## Overview ###

This project is an end-to-end analysis and machine learning pipeline for the New York Times Fiction Bestsellers dataset. It includes:
- **Data Cleaning & Feature Engineering:**
Conversion of dates, extraction of year/quarter/month, and creation of text-based features (title length, word count). In addition, the reviews column (which is a string representation of a list with one dictionary) is parsed to extract review links, and binary flags are created to indicate the presence of various review types.
- **Interactive Dashboard:**
A multi-tab dashboard built with Dash and Plotly (using a dark theme) that includes:
    - ***Overview Tab:*** A slider for selecting a year (or "Total" for all years) that filters the data and updates three interactive graphs displaying:
        - Top 10 Publishers (by number of bestsellers)
        - Top 10 Authors (by number of bestsellers)
        - Top 10 Authors (by maximum weeks on the bestseller list)
    - ***Book Reviews Tab:*** A dropdown listing only those books that have at least one review (displayed as "Title - Author"). When a book is selected, the dashboard displays the book’s title, author, a clickable review link (if available), and the book cover image, which is dynamically fetched from the Open Library Covers API. The cover image is aligned to the right.
- **Machine Learning Pipeline:**
An ensemble model is built to predict the number of weeks a book stays on the bestseller list. Key points include:
    -Aggregated features are computed: the average weeks on the list for publishers and the maximum weeks on the list for authors.
    - The model uses additional features such as rank, previous week’s rank, and the review flags.
    - Synthetic data augmentation is applied to continuous features by adding Gaussian noise.
    - A VotingRegressor ensemble (combining RandomForestRegressor, GradientBoostingRegressor, and ExtraTreesRegressor) is trained and evaluated using Mean Squared Error (MSE) and Root Mean Squared Error (RMSE).

### Data Cleaning & Feature Engineering ###
- **Date Conversion:***
Convert the bestsellers_date to a datetime object and extract year, quarter, and month.
- **Text Features:**
Compute the length of the book title and the word count of the description.
- **Review Parsing:**
The reviews column is parsed to convert its string representation into a Python list of dictionaries. Then, binary flags are created for each review type (book review, first chapter, Sunday review, article chapter)

### Dashboard ###
- **Overview Tab:**
Uses a slider (with a minimum equal to the first available year and a maximum equal to last_year + 1, where the maximum is labeled "Total") to filter data by year. It displays three interactive graphs:
    - ***Publishers Graph:*** Top 10 publishers by the number of bestsellers.
    - ***Authors Graph:*** Top 10 authors by the number of bestsellers.
    - ***Weeks Graph:*** Top 10 authors by maximum weeks on the bestseller list.
- **Book Reviews Tab:**
The dropdown displays only books with at least one review. When a book is selected, the dashboard shows:
    - The title and author on the left.
    - A clickable review link.
    - The cover image on the right (fetched dynamically from the Open Library Covers API based on the book’s ISBN).

### Machine Learning ###
- **Feature Aggregation:***
Compute aggregated features:
    - ***Publisher:*** Average weeks on the bestseller list.
    - ***Author:*** Maximum weeks on the bestseller list.
- **Data Augmentation:**
Synthetic data augmentation is applied to continuous features (e.g., rank, aggregated features) by adding Gaussian noise.
- **Ensemble Modeling:**
A VotingRegressor ensemble is built combining:
    - `RandomForestRegressor`
    - `GradientBoostingRegressor`
    - `ExtraTreesRegressor`

The model is evaluated using Mean Squared Error (MSE) and Root Mean Squared Error (RMSE).

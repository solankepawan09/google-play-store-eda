# Google Play Store — EDA & Feature Engineering

Exploratory Data Analysis and feature engineering on the Google Play Store dataset (10,841 apps), covering data cleaning, missing value treatment, and business-relevant insights into app categories, installs, and ratings.

## 📌 Problem Statement

With millions of apps competing for user attention on the Google Play Store, understanding what drives an app's popularity, ratings, and installs is valuable for developers, marketers, and businesses. This project explores the Google Play Store dataset to uncover patterns in app categories, pricing, size, and user engagement.

## 🛠️ Tech Stack

- **Python**
- **Pandas** & **NumPy** — data manipulation and cleaning
- **Matplotlib** & **Seaborn** — data visualization

## 📊 Exploratory Data Analysis

Key questions explored:
- Which is the most popular app category?
- What are the top 10 app categories by count?
- Which category has the highest number of installations?
- What are the top 5 most installed apps in each popular category?
- How many apps have a perfect 5.0 rating?

## 🔎 Step-by-Step Breakdown

### 1. Data Loading & Initial Inspection
- Loaded the dataset (10,841 rows) using Pandas and previewed it with `.head()`
- Checked shape, data types (`.info()`), and summary statistics (`.describe()`)
- Created a working copy (`df_copy`) of the original dataframe to preserve raw data
- Checked for missing values across all columns using `.isnull().sum()`
- **Observation:** The dataset has missing values in several columns

### 2. Data Cleaning

**a) Fixing the `Reviews` column**
- Attempted to convert `Reviews` from string to integer — failed due to a non-numeric `'3.0M'` value
- Isolated non-numeric entries using `.str.isnumeric()` and found 1 row (index 10472) causing the issue
- Dropped that single row (negligible impact on a 10,841-row dataset)
- Converted `Reviews` to integer type and verified with `.info()`

**b) Fixing the `Size` column**
- Checked for null values (found none) and inspected unique values
- Found mixed units — some sizes in Megabytes, some in Kilobytes, and a `"Varies with device"` placeholder value
- Converted all values to a single consistent unit (Kilobytes)

**c) Fixing `Installs` and `Price` columns**
- Found special characters (`+`, `,`, `$`) embedded in these columns, preventing numeric conversion
- Stripped these characters using a loop across both columns
- Converted `Installs` to integer and `Price` to float

**d) Handling the `Last Updated` (date) column**
- Converted the column to proper datetime format using `pd.to_datetime()`
- Extracted `Day`, `Month`, and `Year` as separate feature columns for easier time-based analysis

### 3. Removing Duplicates
- Checked for duplicate app entries using `.duplicated('App')` — found 1,181 duplicates
- Dropped duplicates, keeping the first occurrence of each app
- Verified final row count after cleanup

### 4. Univariate Analysis
- Split features into numerical and categorical groups
- Calculated percentage distribution for categorical columns
- Plotted distributions for numerical features (Rating, Reviews, Size, Installs, Price)
  - **Observation:** Rating and Year are left-skewed; Reviews, Size, Installs, and Price are right-skewed
- Plotted distributions for categorical features

### 5. Category-Level Analysis
- **Most popular app category:** Visualized category share with a pie chart
  - Family, Games, and Tools dominate; Beauty, Comics, Arts, and Weather are least represented
- **Top 10 categories:** Built a bar chart of the 10 most common categories
  - Family leads with ~19% of all apps, followed by Games at ~9.9%
- **Category with the most installs:** Grouped and summed installs by category
  - GAME leads with ~35 billion installs — the most installed category overall

### 6. App-Level Analysis
- **Top 5 most installed apps per popular category:** Grouped by category and app, sorted by installs
  - Top apps: Subway Surfers (Games), Skype (Communication), Google Drive (Productivity), Facebook (Social)
- **Apps with a perfect 5.0 rating:** Grouped by category, installs, and app; filtered for top ratings
  - Found 271 apps with a 5.0 rating; top-most is "DN Employee" (Family category)

## 💡 Key Insights

- **Family** and **Games** are the most common categories, together making up ~29% of all apps
- **Games** dominate installs, with ~35 billion installations — the most installed category on the store
- **Subway Surfers** (Games), **Skype** (Communication), **Google Drive** (Productivity), and **Facebook** (Social) are the most installed apps in their respective categories
- 271 apps hold a perfect 5.0 rating, with **DN Employee** (Family category) among the top

## 📁 Project Structure

```
├── 11_1-Google_Play_Store.ipynb   # Main notebook: cleaning, EDA, insights
└── README.md
```

## 🚀 How to Run

1. Clone the repository
2. Install dependencies: `pip install pandas numpy matplotlib seaborn`
3. Open and run `11_1-Google_Play_Store.ipynb` in Jupyter Notebook / JupyterLab

## 📂 Dataset

The dataset used is the [Google Play Store Apps dataset](https://raw.githubusercontent.com/krishnaik06/playstore-Dataset/main/googleplaystore.csv), containing 10,841 records across 13 columns.

## 👤 Author

**Pawan Solanke**
Data Analyst | SQL, Python, Power BI

# 🎢 Course Project: Exploratory Data Analysis (EDA) of Roller Coaster Data

## Project Description

This project demonstrates a complete workflow for **Exploratory Data Analysis (EDA)** using a dataset containing information on over a thousand roller coasters. The primary goal was to apply the Python data analysis stack (Pandas, NumPy, Matplotlib, and Seaborn) to clean, understand, visualize, and extract meaningful insights from the data, culminating in answering a specific business question.

The analysis is documented in the accompanying Jupyter Notebook (`ANALYSING_FILE.ipynb`) and summarized in the PDF (`eda with pandas and plots.pdf`).

## Learning Objectives & Key Project Steps

This project successfully implemented the following core data science and programming concepts:

1.  **Initial Data Understanding (Step 1):**
      * Inspecting the dataset size (`.shape`) and structure.
      * Reviewing initial rows (`.head()`) and feature data types (`.dtypes`).
      * Generating descriptive statistics (`.describe()`).
2.  **Data Preparation (Step 2):**
      * **Data Subsetting:** Selecting only the relevant columns for analysis.
      * **Data Cleaning:** Renaming columns for consistency and converting date fields to the correct `datetime` format.
      * **Handling Missing/Duplicate Data:** Identifying null values (`.isna().sum()`) and strategically removing duplicates to ensure unique coaster entries.
3.  **Univariate Analysis (Step 3):**
      * Analyzing individual features using **value counts** (for categorical/discrete data like "Year Introduced").
      * Visualizing distributions with **Histograms** and **Kernel Density Estimates (KDE)** for continuous variables like "Speed".
4.  **Feature Relationship Analysis (Step 4):**
      * Exploring relationships between two features using **Scatter Plots** (e.g., Speed vs. Height).
      * Analyzing multiple feature relationships simultaneously using **Seaborn Pair Plots**.
      * Quantifying relationships with a **Correlation Heatmap** to identify strong dependencies between numeric variables.
5.  **Asking and Answering a Question (Step 5):**
      * Answering the question: **"Which parks have the highest average roller coaster speed, considering only parks with a minimum of 10 coasters?"** using an advanced chain of Pandas `query`, `groupby`, and `agg` methods.

## 🛠️ Tools and Libraries Used

| Tool / Library | Purpose |
| :--- | :--- |
| **Python** | Core programming language. |
| **Pandas (pd)** | Data manipulation, cleaning, and aggregation. |
| **NumPy (np)** | Numerical operations. |
| **Matplotlib (plt)** | Basic plotting and customization. |
| **Seaborn (sns)** | Advanced statistical data visualization. |
| **Jupyter Notebook** | Environment for interactive coding and documentation. |

## 📊 Key Findings Summary

The analysis produced several concrete insights:

  * **Clean Data Set Size:** After cleaning, the final data set contained **990 unique roller coasters**.
  * **Correlation:** A **strong positive correlation (0.73)** was confirmed between a roller coaster's **Speed** and its **Height**.
  * **Busiest Year:** The year **1999** saw the highest number of new roller coaster introductions in the dataset.
  * **Fastest Park:** The final analysis showed that **Busch Gardens** had the highest average roller coaster speed among parks with 10 or more coasters.

# NOW INDEPTH ANALYSIS



# 🎢 Deep Dive: Exploratory Data Analysis (EDA) of Roller Coaster Data

## 1\. Project Overview and Goal

This project is a comprehensive **Exploratory Data Analysis (EDA)**, meticulously documenting the process of transforming a raw dataset of over 1,000 roller coasters into a clean, structured, and insightful resource.

### Motivation (The 'Why')

The primary goal was to demonstrate proficiency in the complete EDA lifecycle using the Python data science stack. This includes mastering initial data diagnostics, rigorous data cleaning, descriptive statistics, advanced data visualization, and complex data aggregation to answer a real-world question.

### Technical Stack (The 'How')

| Tool / Library | Role in Project |
| :--- | :--- |
| **Pandas (pd)** | Core engine for data manipulation, filtering, aggregation (`groupby`, `query`, `agg`), and indexing. |
| **Seaborn (sns)** | High-level library for creating informative and statistically sophisticated visualizations (e.g., Heatmaps, Pair Plots). |
| **Matplotlib (plt)** | Used for customization, setting plot styles, and defining axis labels. |
| **Jupyter Notebook** | Provides the interactive environment (`ANALYSING_FILE.ipynb`) for step-by-step execution and documentation. |

-----

## 2\. Detailed 5-Step Analysis Breakdown

The entire analysis follows the industry-standard five-step EDA workflow, with each stage building upon the cleaned results of the previous one.

### ➡️ Step 1: Initial Data Understanding

| What Was Done | How It Was Done (Functions) | Why It Was Done (Rationale) | Key Result/Finding |
| :--- | :--- | :--- | :--- |
| **Data Ingestion & Shape** | `pd.read_csv()`, `df.shape` | To load the data and immediately check the number of rows and columns to gauge complexity. | Initial dataset had **1,087 rows** and **56 columns**. |
| **Data Preview** | `df.head(5)` | To visually inspect the first few rows and get a quick sense of the column values and potential data quality issues (e.g., text mixed with numbers). | Identified a mix of string (`object`) and numeric (`float64`, `int64`) data types. |
| **Data Types Check** | `df.dtypes` | Essential for confirming that Pandas interpreted the data correctly and identifying columns needing type conversion. | Found that `Opening_Date_Clean` was incorrectly stored as an `object` (string) instead of a `datetime`. |
| **Descriptive Statistics**| `df.describe()` | To understand the central tendency, dispersion, and shape of the numeric features (e.g., mean, median, min/max values). | Showed potential outliers in columns like `Height` and `Speed`, indicating a need for visual analysis. |

### ➡️ Step 2: Data Preparation & Cleaning

This is the most critical stage, ensuring the data is reliable for statistical analysis.

| What Was Done | How It Was Done (Functions) | Why It Was Done (Rationale) | Key Result/Finding |
| :--- | :--- | :--- | :--- |
| **Column Subsetting** | `df[['col1', 'col2', ...]].copy()` | The original dataset had 56 columns; many were redundant or incomplete. Subsetting reduced noise and focused the analysis on 13 key features. | The working dataset was reduced to **13 relevant feature columns**. |
| **Column Renaming** | `df.rename(columns={'old':'New'})` | To standardize column names (e.g., fixing inconsistent casing or removing suffixes like `_clean`) for easier coding and readability. | Clean, standardized names like `Speed_mph`, `Height_ft`, and `Inversions_count` were established. |
| **Type Conversion** | `pd.to_datetime()` | To correct the `Opening_Date_Clean` column from a string to a proper `datetime` object, enabling time-series analysis if needed. | Confirmed `Opening_Date_Clean` was successfully converted to a `datetime64` type. |
| **Handling Duplicates** | `df.duplicated(subset=['Coaster_Name', 'Location', 'Opening_Date']).sum()` followed by `~df.duplicated(...)` and `df.reset_index(drop=True)` | Identifying rows that are identical on key features. Removing them is crucial to prevent biased statistics where one physical coaster might be listed multiple times. | **97 duplicate rows were identified and removed**, resulting in a final clean dataset of **990 unique entries**. |

### ➡️ Step 3: Univariate Analysis (Single Feature)

| What Was Done | How It Was Done (Functions) | Why It Was Done (Rationale) | Key Result/Finding |
| :--- | :--- | :--- | :--- |
| **Categorical Counts** | `df['Year_Introduced'].value_counts().head(10).plot(kind='bar')` | To quickly see which categories or discrete values occur most frequently. For years, this shows periods of peak construction. | **1999** was found to be the year with the highest number of roller coaster introductions. |
| **Distribution Analysis** | `df['Speed_mph'].plot(kind='hist', bins=20, title=...)` | To visualize the shape of continuous data. Histograms and KDE plots are used to identify modality, skewness, and potential outliers. | The `Speed_mph` distribution showed a **peak around 50 mph**, confirming this as the most common operating speed. |
| **Density Estimation** | `df['Speed_mph'].plot(kind='kde')` | A smoother alternative to the histogram, helpful for comparing multiple distributions or identifying subtle peaks (modes). | KDE plot reinforced the two main modes of speed distribution. |

### ➡️ Step 4: Feature Relationship Analysis (Multi-Feature)

This stage explores how different variables in the dataset interact.

| What Was Done | How It Was Done (Functions) | Why It Was Done (Rationale) | Key Result/Finding |
| :--- | :--- | :--- | :--- |
| **Two-Feature Scatter** | `df.plot(kind='scatter', x='Speed_mph', y='Height_ft')` or `sns.scatterplot()` | To visualize the relationship between two numeric variables and spot potential linear or non-linear trends, clustering, and outliers. | Visually confirmed a general **positive trend**—taller coasters tend to be faster. |
| **Pair-wise Comparison** | `sns.pairplot(df[['Speed_mph', 'Height_ft', 'Inversions_count', 'Year_Introduced']], hue='Material_Type')` | A powerful technique to view all pair-wise relationships among a set of features, and to see their individual distributions on the diagonal. The `hue` argument added a third dimension (material type). | Revealed that **Steel** coasters are generally taller and faster than **Wood** coasters, especially in later years. |
| **Correlation Quantification** | `df[numeric_cols].dropna().corr()` | To calculate the Pearson correlation coefficient between all numeric features, quantifying the *strength* and *direction* of their linear relationships. | Generated a quantitative correlation matrix. |
| **Correlation Visualization**| `sns.heatmap(df_corr, annot=True)`  | To visually interpret the correlation matrix. The heatmap uses color intensity to represent correlation strength, with the `annot=True` parameter displaying the exact numerical value. | Confirmed a **strong positive correlation of 0.73** between `Speed_mph` and `Height_ft`. |

### ➡️ Step 5: Ask and Answer a Question with Data (Conclusion)

The final step is to leverage the cleaned, understood data to solve a complex, targeted business problem.

| What Was Done | How It Was Done (Functions) | Why It Was Done (Rationale) | Key Result/Finding |
| :--- | :--- | :--- | :--- |
| **Defining the Question**| The question asked was: **"What are the locations (parks) with the fastest roller coasters, on average, with a minimum of 10 coasters?"** | This requires filtering, grouping, aggregation, and sorting—a perfect test of advanced Pandas skills. | The question was successfully broken down into a single Pandas operation chain. |
| **Pandas Query Chain**| `df.query("Location != 'Other'").groupby('Location').agg({'Speed_mph': ['mean', 'count']}).query("count >= 10").sort_values(by='mean').plot(kind='barh')` | This chained command performs all operations in sequence: 1) Filter out generic 'Other' locations, 2) Group by `Location`, 3) Calculate the mean speed and coaster count for each group, 4) Filter for groups with $\geq 10$ coasters, 5) Sort by mean speed, and 6) Plot the result. | The final horizontal bar plot clearly showed the result: **Busch Gardens** has the highest average coaster speed among large parks, followed closely by **Cedar Point**.  |

-----


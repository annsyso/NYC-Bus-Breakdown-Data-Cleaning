# NYC School Bus Delays Data Cleaning Project

## Overview

The *NYC School Bus Delays* dataset requires extensive cleaning before analysis. This project involves systematically cleaning, structuring, and preparing the data to answer key questions about bus delays in NYC.

By following a structured approach, we ensure that the data is reliable and ready for analysis. The cleaning process includes removing duplicates, standardizing data entries, extracting relevant information, and transforming columns for better usability.

## Data Cleaning Process

### 1. Backup Raw Data

Before making any modifications, create a backup of the raw dataset to prevent data loss.

### 2. Identify Relevant Columns

We will focus on the following columns needed to answer our analysis questions:

- **Busbreakdown\_ID** – Unique identifier for each delay event.
- **Reason** – The cause of the delay.
- **Occurred\_On** – The date of the delay.
- **Boro** – The borough where the delay occurred.
- **Bus\_Company\_Name** – The bus company involved.
- **How\_Long\_Delayed** – The estimated delay time.
- **Breakdown\_or\_Running\_Late** – Specifies whether the issue was a breakdown or a general delay.

Other columns will be hidden for now but can be revisited if needed.

### 3. Initial Data Inspection

Apply filters to the selected columns to identify potential data quality issues such as:

- Missing values
- Inconsistent formatting
- Duplicates
- Outliers

### 4. Remove Duplicate Entries

To ensure data integrity, we check for duplicate values in the **Busbreakdown\_ID** column, as each entry should be unique. If duplicates exist, remove them using Excel:

#### In Excel:

1. Select the **Busbreakdown\_ID** column.
2. Go to **Data** → **Remove Duplicates**.
3. Ensure only **Busbreakdown\_ID** is checked.
4. Click **OK** to remove duplicate rows.

### 5. Standardize Bus Company Names

Due to inconsistencies in the **Bus\_Company\_Name** column, we will consolidate duplicate names:

#### In Excel:

1. Apply a **Filter** to the **Bus\_Company\_Name** column.
2. Identify variations of the same company name (e.g., “Consolidated Transit” vs. “C.B. Transit”).
3. Use **Find & Replace** (Ctrl + H) to standardize names.
4. Verify consistency by using a **Pivot Table** to count occurrences of each name.

### 6. Extract the Day of the Week from Dates

Since we need to analyze delays based on weekdays, we extract the day from the **Occurred\_On** column:

#### In Excel:

```excel
-- Convert date to numerical weekday
=WEEKDAY(F3)

-- Convert numerical weekday to text
=CHOOSE(WEEKDAY(F3), "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday")
```

### 7. Process Delay Time Estimates

The **How\_Long\_Delayed** column often contains ranges (e.g., "5-10 minutes"). We will split these into three new columns:

- **Min Delay** – The lower bound of the range.
- **Max Delay** – The upper bound of the range.
- **Avg Delay** – The average of the two.

#### In Excel:

1. Select the **How\_Long\_Delayed** column.
2. Use **Text to Columns** (under **Data** → **Text to Columns** → **Delimited** → **Hyphen (-)** as a delimiter) to separate values.
3. Label the new columns as **Min Delay** and **Max Delay**.
4. Calculate the average delay:

```excel
=IFERROR((A1 + B1) / 2, A1)
```

### 8. Final Review

After all transformations, review the dataset to:

- Ensure all necessary columns are cleaned and formatted.
- Check for any remaining inconsistencies.
- Validate the transformed data against the original dataset.

### 9. Ready for Analysis

Once the cleaning is complete, we can begin analyzing:

- **Most common reasons for bus delays.**
- **Patterns in delay times across bus companies and boroughs.**
- **Trends in breakdowns and delays based on days of the week.**

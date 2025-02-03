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

# 🚍 NYC School Bus Delays - Data Analysis & Insights

## 📌 Project Overview

As a **Data Analyst** for the **New York Division of Transportation**, my goal is to improve the efficiency and reliability of NYC’s bus system. With a growing number of bus breakdowns and delays, commuters are facing significant challenges, and the city’s transportation resources are being strained. 

Using a dataset of bus delays, I conducted an analysis to uncover patterns and key factors contributing to these delays. The insights from this project will help shape strategic decisions aimed at improving public transit efficiency. 

---

## 🔍 Key Questions & Insights

### 1️⃣ What are the most common reasons for delays and breakdowns?
- **Approach:**
  - Used the **Reason** and **Reason Type** columns to create a **Pivot Table** counting occurrences of each reason.
  - Created a **bar chart** for a clearer visual representation.
- **Findings:**
  - The top reason for delays is **Heavy Traffic**.
  - The second most common reason is **Other**, which lacks specificity.
- **Recommendations:**
  - Further breakdown of the **Other** category is needed to improve reporting accuracy.
  - Since **Heavy Traffic** is the top issue, strategies like optimized bus lanes and schedule adjustments should be explored.

---

### 2️⃣ How do delay times vary by bus company and borough?
- **Approach:**
  - Created a **Pivot Table** using **Bus Company Name** and the calculated **Low & High Delay Estimate** columns.
  - Used **Conditional Formatting** to highlight above-average delay times.
  - Filtered by **borough** to identify regional trends.
- **Findings:**
  - **Manhattan, Queens, and Staten Island** had above-average delays in both low and high estimates.
  - The **low delay average** across all boroughs was **~30 minutes**, while the **high delay average** was **~45 minutes**.
  - **23 out of 54 bus companies (43%) had consistently above-average delays.**
- **Recommendations:**
  - Focus on boroughs with higher delays for targeted interventions like increased bus frequency or route optimization.
  - Investigate high-delay bus companies for potential inefficiencies and policy improvements.

---

### 3️⃣ Is there a correlation between specific days of the week and the frequency of breakdowns or delays?
- **Approach:**
  - Created a **Pivot Table** using the **Day of the Week** column and counted incident reports for each weekday.
  - Generated a **line chart** to visualize trends.
- **Findings:**
  - **Monday** had the highest number of incidents.
  - **Friday** had the lowest number of incidents.
  - **Monday through Thursday** averaged **~5300 incidents per day**, indicating a consistent pattern.
- **Recommendations:**
  - Higher incidents on Mondays may indicate operational challenges after weekends, such as maintenance backlogs.
  - Conducting preventative maintenance over the weekend could help reduce Monday delays.
  - Further analysis of time-of-day patterns could provide additional insights into peak breakdown periods.

---

## 📊 Conclusion

This analysis provides valuable insights into the primary factors affecting NYC bus delays and breakdowns. Addressing heavy traffic delays, optimizing schedules in high-delay boroughs, and implementing preventative maintenance for high-risk days can significantly improve transit reliability.

By leveraging data-driven insights, the **New York Division of Transportation** can make informed decisions to enhance the public transit experience and improve overall operational efficiency. 🚍📈

---

## 🛠️ Technologies Used
- **Microsoft Excel** (Pivot Tables, Conditional Formatting, Data Cleaning & Analysis)
- **Data Visualization** (Bar Charts, Line Charts)

## 🚀 Next Steps
- Further analyze time-of-day breakdowns to understand peak delay periods.
- Investigate bus company-specific operational challenges.
- Propose actionable solutions for traffic mitigation and route optimization.



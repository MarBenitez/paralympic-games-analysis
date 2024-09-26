# Paralympic Games Dashboard

This repository contains a Power BI dashboard that visualizes key insights and metrics from the Paralympic Games. The data spans historical records from various editions of the Games, including information on athletes, medals, rankings, and country performances.

## Project Overview

The goal of this project is to build an interactive Power BI dashboard to explore and analyze the performance of athletes and countries in the Paralympic Games. The project involved extensive data cleaning, transformation, and modeling to ensure that the dashboard works seamlessly, with logical filtering and accurate visual representations of the data.

## Dataset

The initial dataset consisted of two raw Excel files:
1. **Data Athletes**: This dataset contains information on athletes, medals, sports, and events.
2. **Data Standings**: This dataset focuses on country rankings, medal counts, and performance across different editions of the Games.

The data in both files contained issues such as duplicates, missing values, and inconsistent data types. As such, extensive cleaning and transformation were required before modeling.

## Data Cleaning and Preprocessing

Here are the main steps undertaken to clean and prepare the data for modeling:

### 1. **City Names Normalization**
   - Some city names appeared duplicated due to spelling variations or slight differences (e.g., "Rio de Janeiro" vs. "Rio de Janeiro "). These were standardized to ensure consistency throughout the model.

### 2. **Geographical Coordinates Fix**
   - Missing latitude and longitude values were filled for cities or countries that lacked this information. External resources were used to ensure accurate geolocation data.

### 3. **Column Removal**
   - Removed unnecessary columns or those with a high number of null values that could not be reasonably imputed. For example, certain athlete-related columns were removed as they had excessive missing values and weren’t critical to the analysis.

### 4. **Date Handling**
   - Date fields such as `games_start` and `games_end` were standardized and transformed into Date format to ensure proper time-based filtering and analysis.
   - Custom date columns were created by combining and normalizing individual date components (e.g., year, month, and day).

### 5. **Data Type Changes**
   - Various columns were converted to their appropriate data types (e.g., converting text fields to dates or numbers where appropriate).

### 6. **Index Creation**
   - Custom indices were generated by combining columns to create unique identifiers where no natural primary key existed. For example, I created an index by concatenating `games_code` and `sport_code` to form a unique **games_sports_code**.
   - Other index columns were created as needed to serve as primary keys and ensure that relationships between tables were logically structured.

### 7. **Duplicate Removal**
   - After creating unique identifiers for each table, duplicates were removed where necessary. This was particularly important for dimensions like **Games**, **Sports**, and **Winning Countries**, which require unique values for each record to ensure logical relationships.
   - Duplicates were removed based on primary key fields like `games_code`, `sport_code`, and `npc_name`.

### 8. **Normalization and Consistency**
   - The data was normalized to reduce redundancy. For example, the data related to sports, events, and athletes was broken down into separate tables with foreign keys linking them to the main facts (e.g., **Athletes and Medals**).
   - Ensured that the data was consistent across all tables by normalizing the format of fields like city names, country names, and sport codes.

## Data Model

After cleaning the data, I created a relational model in Power BI. The model consists of five core tables, built from the original datasets:

1. **Games**: Contains detailed information about each Paralympic edition, including location, dates, and geographical coordinates.
2. **Sports**: Holds details about the sports, including event venues and sport codes.
3. **Athletes and Medals**: Tracks athlete participation in events, along with the medals they won.
4. **Winning Countries**: Contains country-level information, including latitude/longitude and country codes.
5. **Rankings**: Provides rankings for each country based on their performance in the Games.

### Relationships in the Model

To ensure a logical and efficient model, I established relationships between the tables, ensuring that the model remained consistent and allowed for accurate visualizations:

- **Games** is connected to **Athletes and Medals**, **Sports** and **Rankings** via `games_code`.
- **Sports** is connected to **Athletes and Medals** and **Raankings** via `games_sports_code`.
- **Winning Countries** is connected to both **Athletes and Medals** and **Rankings** via `npc_name`.

### Bidirectional Relationships
In some cases, I established **bidirectional relationships** to enable more complex filtering across tables:
- The relationship between **Athletes and Medals** and **Winning Countries** was set to **bidirectional** to allow filtering both ways, ensuring that selecting a country filters the relevant athletes and vice versa.

### Unidirectional Relationships
For most other tables, **unidirectional relationships** were maintained to avoid potential performance issues and ensure clear, logical filtering:
- **Games** → **Athletes and Medals** (unidirectional).
- **Games** → **Rankings** (unidirectional).
- **Sports** → **Athletes and Medals** (unidirectional).

## Dashboard Insights

The Power BI dashboard allows users to explore several key insights, including:
- **Medals by Country**: View the total number of medals won by countries across different editions of the Paralympics.
- **Athlete Participation**: Analyze how many times athletes have participated in different events and the medals they have won.
- **Performance by Sport**: Filter by sport and visualize country performance, including medal counts.
- **Ranking Analysis**: Track the overall performance and rankings of countries in each edition of the Paralympics.
- **Geographical Insights**: Use map visualizations to see where the Paralympic Games were hosted and the countries that excelled in specific sports.

## How to Use This Repository

1. **Download**: Clone the repository or download the `PBIX` file to explore the dashboard.
2. Click the **[link](https://app.powerbi.com/view?r=eyJrIjoiMjMzMzU5NjItMzIzNy00ZTlkLWFjMDgtZGUyODZiZDRmYTQzIiwidCI6IjhhZWJkZGI2LTM0MTgtNDNhMS1hMjU1LWI5NjQxODZlY2M2NCIsImMiOjl9&embedImagePlaceholder=true)** to the Power BI App.

## Conclusion

This Power BI dashboard provides an insightful and interactive way to explore historical data from the Paralympic Games. By cleaning and normalizing the data, I ensured that the model is consistent, efficient, and easy to filter, enabling rich data analysis with minimal redundancy.

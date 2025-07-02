# Cyclistic Bike-Share Analysis: Process Phase

## Overview

The Process Phase involved cleaning and transforming the Cyclistic dataset to ensure accuracy and usability for addressing the analysis questions. The dataset, stored in a SQLite database (`cyclistic.db`), was processed to remove invalid data, handle missing values, address outliers, and create new variables relevant to the SMART questions: (1) ride duration and frequency by day of week, (2) popular start stations, and (3) peak ride hours. SQLite was the primary tool, with Excel used for validation, to prepare the data for analysis.

## Data Cleaning Steps

1. **Removal of Invalid Dates**:
   - A query identified 227 rows (~0.004% of 5,860,568) with invalid dates (null `started_at` or `ended_at`, or `started_at > ended_at`) in the `trips` table. These were removed to ensure accurate ride duration calculations:
     ```sql
     CREATE TABLE trips_clean AS
     SELECT *
     FROM trips
     WHERE started_at IS NOT NULL
       AND ended_at IS NOT NULL
       AND started_at <= ended_at;
     ```
   - The resulting `trips_clean` table contains 5,860,341 rows, preserving 99.996% of the dataset.

2. **Handling Missing Values**:
   - Missing values were noted in `start_station_name` (18.33%), `start_station_id` (18.33%), `end_station_name` (18.85%), `end_station_id` (18.85%), `end_lat` (0.12%), and `end_lng` (0.12%). For SMART Question 2 (station popularity), rows with non-null `start_station_name` and `end_station_name` were filtered, creating a subset of 4,208,269 rows (~81% of the dataset):
     ```sql
     CREATE TABLE trips_station_valid AS
     SELECT *
     FROM trips_clean
     WHERE start_station_name IS NOT NULL
       AND end_station_name IS NOT NULL;
     ```
   - For SMART Questions 1 and 3 (time-based analyses), the full `trips_clean` table was retained, as missing station data does not impact ride duration or timing metrics.

3. **Creating New Variables**:
   - **Ride Duration**: A new column, `ride_duration_minutes`, was added and populated to calculate ride duration in minutes, supporting SMART Question 1:
     ```sql
     ALTER TABLE trips_clean ADD ride_duration_minutes REAL;
     UPDATE trips_clean
     SET ride_duration_minutes = (julianday(ended_at) - julianday(started_at)) * 1440;
     ```
   - **Day of Week**: A `day_of_week` column was added to extract the day of the week (0=Sunday, 6=Saturday) from `started_at`, supporting SMART Question 1:
     ```sql
     ALTER TABLE trips_clean ADD day_of_week TEXT;
     UPDATE trips_clean
     SET day_of_week = strftime('%w', started_at);
     ```
   - **Start Hour**: A `start_hour` column was added to extract the hour (0–23) from `started_at`, supporting SMART Question 3:
     ```sql
     ALTER TABLE trips_clean ADD start_hour INTEGER;
     UPDATE trips_clean
     SET start_hour = strftime('%H', started_at);
     ```
   - These variables were verified, with sample durations ranging from 7 to 30 minutes, days from 0 to 6, and hours from 0 to 23. The average ride duration is 17.32 minutes, with a maximum of 1559.93 minutes (~26 hours).

4. **Handling Outliers**:
   - A query identified 496 rows with zero or negative durations (`ride_duration_minutes <= 0`) and 7,596 rows with durations exceeding 24 hours (`ride_duration_minutes > 1440`). These outliers (~0.14% of the dataset) were removed to ensure realistic analysis:
     ```sql
     CREATE TABLE trips_clean_final AS
     SELECT *
     FROM trips_clean
     WHERE ride_duration_minutes BETWEEN 1 AND 1440;
     ```
   - The resulting `trips_clean_final` table contains 5,721,089 rows, preserving 97.6% of the original dataset.

## Tools and Validation

SQLite, via DB Browser for SQLite, was used to execute all cleaning and transformation queries, ensuring efficiency with the 5.8 million-row dataset. Excel was used to validate missing value percentages on a sample CSV, confirming consistency with SQLite results. The `trips_sample` table (10,000 rows) was used to test queries before applying them to `trips_clean`. R and PowerBI will be utilized in the Analyze and Share Phases for visualization.

## Observations

The cleaning process preserved 5,721,089 rows after removing invalid dates (227 rows) and outliers (8,092 rows), ensuring minimal data loss. The filtered station data (4,208,269 rows) provides a robust subset for analyzing station popularity, despite 18–19% missingness in station columns. The new variables (`ride_duration_minutes`, `day_of_week`, `start_hour`) are correctly populated and ready for analysis, enabling comparisons between casual riders and members. The low missingness in `end_lat`/`end_lng` (0.12%) suggests potential for spatial analysis if station data proves limiting. The removal of long-duration rides ensures realistic analysis, aligning with typical bike-share usage patterns.
# Cyclistic Bike-Share Analysis: Prepare Phase

## Data Source

The dataset for the Cyclistic Bike-Share Analysis was sourced from the official Divvy trip data repository ([https://divvy-tripdata.s3.amazonaws.com/index.html](https://divvy-tripdata.s3.amazonaws.com/index.html)), which provides real-world bike-share data used as the basis for Cyclistic’s fictional dataset. The data comprises 12 CSV files, one for each month from January 2024 to December 2024, named `2024XX-divvy-tripdata.csv` (e.g., `202401-divvy-tripdata.csv`). These files were downloaded, unzipped, and imported into a SQLite database (`cyclistic.db`) for analysis. The dataset is credible, publicly available, and anonymized, ensuring compliance with data privacy requirements.

## Data Structure

The dataset contains 5,860,568 bike trip records across the 12 files, combined into a single table (`trips`) with the following 13 columns:

- `ride_id`: TEXT, unique identifier for each ride.
- `rideable_type`: TEXT, type of bike (e.g., classic_bike, electric_bike, electric_scooter).
- `started_at`: DATETIME, ride start timestamp (format: YYYY-MM-DD HH:MM:SS).
- `ended_at`: DATETIME, ride end timestamp (format: YYYY-MM-DD HH:MM:SS).
- `start_station_name`: TEXT, name of the starting station.
- `start_station_id`: TEXT, ID of the starting station.
- `end_station_name`: TEXT, name of the ending station.
- `end_station_id`: TEXT, ID of the ending station.
- `start_lat`: REAL, starting latitude.
- `start_lng`: REAL, starting longitude.
- `end_lat`: REAL, ending latitude.
- `end_lng`: REAL, ending longitude.
- `member_casual`: TEXT, user type (casual or member).

The dataset covers all bike trips in Chicago for 2024, providing comprehensive data to analyze usage patterns between casual riders and annual members.

## Data Quality Assessment

Several quality checks were performed using SQLite to ensure the dataset’s suitability for analysis:

- **Completeness**: Missing values were identified in six columns, with the following percentages calculated across 5,860,568 rows:
  - `start_station_name`: 18.33%
  - `start_station_id`: 18.33%
  - `end_station_name`: 18.85%
  - `end_station_id`: 18.85%
  - `end_lat`: 0.12%
  - `end_lng`: 0.12%
  These gaps, common in bike-share data due to dockless bikes or scooters, were addressed in the Process Phase by filtering rows with non-null station names for station-based analyses.
- **Consistency**: The `member_casual` column contains two distinct values (“casual” and “member”), confirming its suitability for user type comparisons. The `rideable_type` column includes three valid values: “classic_bike”, “electric_bike”, and “electric_scooter”, providing additional context for analysis. The `started_at` and `ended_at` columns are consistently formatted as “YYYY-MM-DD HH:MM:SS” (e.g., “2024-01-12 15:30:27”), enabling accurate time-based calculations. A query identified 227 rows (~0.004%) with invalid dates (null timestamps or `started_at > ended_at`), which were removed during cleaning.
- **Credibility**: The Divvy dataset is reliable, sourced directly from the operator, and widely used for analytical studies. It is anonymized, containing no personally identifiable information, aligning with Cyclistic’s fictional context.
- **Relevance**: The dataset’s columns directly support the analysis questions, with `started_at` and `ended_at` enabling time-based analysis (e.g., ride duration, peak hours), `start_station_name` supporting station popularity, and `member_casual` facilitating user type comparisons.

## Tools and Organization

The 12 CSV files were imported into a SQLite database (`cyclistic.db`) using DB Browser for SQLite, creating a single `trips` table with 5,860,568 rows for efficient querying. A sample table (`trips_sample`) with 10,000 rows was created for testing queries. Excel was used for initial exploration of individual CSVs to confirm column names and identify missing values. R and PowerBI will be employed in subsequent phases for analysis and visualization. The database is backed up to ensure data integrity.

## Initial Observations

The dataset is comprehensive, with 5,860,568 rows covering a full year, enabling robust analysis of seasonal and daily trends. The presence of three rideable types (classic_bike, electric_bike, electric_scooter) suggests potential differences in user preferences, which may inform marketing strategies. Missing values in station-related columns (approximately 18–19%) likely reflect dockless bike or scooter usage, requiring filtering for station-based insights (4,208,269 rows remain usable). The availability of latitude and longitude data, with minimal missingness (0.12%), provides an alternative for spatial analysis. The small proportion of invalid dates (227 rows) indicates high data quality, with minimal cleaning needed for time-based analyses. These observations guided data cleaning and analysis strategies in the Process and Analyze Phases.
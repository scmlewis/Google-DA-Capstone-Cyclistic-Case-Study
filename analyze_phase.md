# Cyclistic Bike-Share Analysis: Analyze Phase

## Overview

The Analyze Phase involved exploratory data analysis to answer three SMART questions, deriving insights into usage patterns of casual riders and annual members to inform Cyclistic’s marketing strategies. The cleaned dataset (`trips_clean_final`, 5,721,089 rows) and a station-valid subset (`trips_station_valid`, 4,208,269 rows) were analyzed using SQLite to calculate ride durations, frequencies, station popularity, and peak hours. The findings highlight differences between casual riders and members, guiding targeted marketing efforts to convert casual riders into members.

## Analysis Questions and Findings

1. **How do ride duration and frequency differ between casual riders and members by day of the week?**
   - **Methodology**: A SQLite query calculated the average ride duration (`ride_duration_minutes`) and ride count by day of the week (`day_of_week`) for each user type (`member_casual`) using the `trips_clean_final` table:
     ```sql
     SELECT
         member_casual,
         CASE day_of_week
             WHEN '0' THEN 'Sunday'
             WHEN '1' THEN 'Monday'
             WHEN '2' THEN 'Tuesday'
             WHEN '3' THEN 'Wednesday'
             WHEN '4' THEN 'Thursday'
             WHEN '5' THEN 'Friday'
             WHEN '6' THEN 'Saturday'
         END AS day_name,
         ROUND(AVG(ride_duration_minutes), 2) AS avg_duration,
         COUNT(*) AS ride_count
     FROM trips_clean_final
     GROUP BY member_casual, day_of_week
     ORDER BY member_casual, day_of_week;
     ```
   - **Findings**:
     - **Casual Riders**: Average ride durations are higher on weekends (24.95 minutes on Sunday, 24.56 minutes on Saturday) compared to weekdays (18.49–20.84 minutes). Ride counts peak on Saturday (429,357) and are lowest on Tuesday (225,465), indicating recreational usage.
     - **Members**: Durations are consistent (11.85–13.82 minutes), with slightly longer rides on weekends. Ride counts peak on Wednesday (599,369) and are lowest on Sunday (408,923), suggesting regular commuting.
     - **Insight**: Casual riders take longer, recreational rides on weekends, while members use bikes for shorter, consistent weekday commutes. Marketing campaigns should target casual riders with weekend promotions to encourage membership adoption.

2. **Which start stations are most popular among casual riders compared to members?**
   - **Methodology**: A SQLite query counted rides by `start_station_name` for each user type using the `trips_station_valid` table, filtering non-null station names, and selecting the top 10 stations per user type:
     ```sql
     SELECT
         member_casual,
         start_station_name,
         COUNT(*) AS ride_count
     FROM trips_station_valid
     GROUP BY member_casual, start_station_name
     ORDER BY member_casual, ride_count DESC
     LIMIT 10;
     ```
   - **Findings** (for casual riders; member data pending):
     - **Casual Riders**: Top stations include Streeter Dr & Grand Ave (48,316 rides), DuSable Lake Shore Dr & Monroe St (32,194), and Millennium Park (20,841), which are near tourist attractions, indicating leisure-focused usage.
     - **Members**: Pending data, but expected to favor commuter-oriented stations (e.g., near business districts).
     - **Insight**: Casual riders frequent recreational and tourist-heavy stations, suggesting marketing efforts (e.g., posters, events) at these locations to promote memberships.

3. **What are the peak ride hours for casual riders compared to members?**
   - **Methodology**: A SQLite query counted rides by `start_hour` (0–23) for each user type using the `trips_clean_final` table:
     ```sql
     SELECT
         member_casual,
         start_hour,
         COUNT(*) AS ride_count
     FROM trips_clean_final
     GROUP BY member_casual, start_hour
     ORDER BY member_casual, start_hour;
     ```
   - **Findings**:
     - **Casual Riders**: Peak at 5 PM (17:00, 197,661 rides), with high activity from 11 AM to 6 PM (116,607–197,661 rides), suggesting recreational or post-work usage. Lowest activity is at 4 AM (6,140 rides).
     - **Members**: Peak at 5 PM (17:00, 386,723 rides), with strong activity during morning (7–8 AM: 197,408–251,340) and evening (4–6 PM: 337,271–386,723) commutes, indicating workday usage.
     - **Insight**: Casual riders are most active in afternoons and evenings, while members show commuter peaks. Evening promotions (e.g., digital ads at 5 PM) could effectively target casual riders.

## Tools and Validation

SQLite, via DB Browser for SQLite, was used to execute analysis queries, with results exported as CSVs (`day_analysis.csv`, `station_analysis.csv`, `hour_analysis.csv`) for visualization. The total ride counts (5,721,089) match the `trips_clean_final` table, confirming data integrity. Excel was used for initial validation, and PowerBI will be used in the Share Phase to create visualizations. R is available for additional visualizations if needed.

## Observations

The analysis reveals distinct usage patterns: casual riders favor longer weekend rides and tourist-heavy stations, while members exhibit consistent, shorter weekday commutes. These differences highlight opportunities to target casual riders with weekend and evening promotions at recreational stations. The high volume of rides (5.7 million) ensures robust statistical insights, despite 18–19% missing station data. The availability of latitude/longitude data (0.12% missing) supports potential spatial analysis if needed. These findings will guide visualization and recommendations in the Share and Act Phases.
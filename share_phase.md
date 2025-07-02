# Cyclistic Bike-Share Analysis: Share Phase

## Overview

The Share Phase involved creating visualizations to communicate the findings of the Cyclistic Bike-Share Analysis to the marketing team, enabling data-driven decisions to convert casual riders into annual members. Using PowerBI Desktop, an interactive dashboard was developed based on the analysis of 5,721,089 bike trips from January to December 2024, stored in a SQLite database (`cyclistic.db`). The visualizations highlight key differences in usage patterns between casual riders and members, supporting the business objective of increasing memberships.

## Visualizations and Purpose

1. **Ride Duration and Frequency by Day of Week**:
   - **Visualization**: Two clustered bar charts display average ride duration (in minutes) and ride count by day of the week for casual and member riders.
   - **Data Source**: Exported from SQLite as `day_analysis.csv`, derived from the `trips_clean_final` table.
   - **Purpose**: The duration chart reveals that casual riders have longer rides on weekends (e.g., 24.95 minutes on Sunday) compared to members (e.g., 13.81 minutes), while the ride count chart shows casual peaks on Saturdays (429,357 rides) and member peaks on Wednesdays (599,369 rides). This supports targeted weekend promotions for casual riders to encourage membership adoption.
   - **Design**: Days (Sunday–Saturday) on the x-axis, duration/count on the y-axis, with `member_casual` as the legend for comparison.

2. **Popular Start Stations**:
   - **Visualization**: A table or clustered bar chart presents the top 10 start stations for casual riders, with ride counts.
   - **Data Source**: Exported from SQLite as `station_analysis.csv`, derived from the `trips_station_valid` table (4,208,269 rows).
   - **Purpose**: The chart highlights that casual riders frequent tourist-heavy stations (e.g., Streeter Dr & Grand Ave: 48,316 rides, Millennium Park: 20,841 rides), indicating leisure usage. This suggests marketing efforts (e.g., station-based advertisements) at these locations to promote memberships to casual riders.
   - **Design**: Station names on the x-axis (or rows for a table), ride count on the y-axis, filtered to the top 10 casual stations.

3. **Peak Ride Hours**:
   - **Visualization**: A line chart displays ride counts by hour (0–23) for casual and member riders.
   - **Data Source**: Exported from SQLite as `hour_analysis.csv`, derived from the `trips_clean_final` table.
   - **Purpose**: The chart shows casual riders peaking at 5 PM (197,661 rides) with high afternoon/evening activity (11 AM–6 PM), while members peak at 5 PM (386,723 rides) with morning/evening commutes (7–8 AM, 4–6 PM). This supports evening-targeted promotions (e.g., digital ads) for casual riders.
   - **Design**: Hours (0–23) on the x-axis, ride count on the y-axis, with `member_casual` as the legend.

## Dashboard Design

The PowerBI dashboard, saved as `cyclistic_dashboard.pbix` and exported as `cyclistic_dashboard.pdf`, integrates these visualizations on a single page with the title “Cyclistic Bike-Share Analysis Dashboard.” Text boxes summarize key insights, such as “Casual riders prefer weekend rides, peaking on Saturday,” enhancing stakeholder understanding. A consistent theme (e.g., City Park) ensures a professional appearance, with interactive filters allowing exploration by user type or time period. The dashboard was uploaded to the GitHub repository for accessibility.

## Tools and Validation

PowerBI Desktop was used to import the CSVs and create the visualizations, leveraging its interactive features to engage stakeholders. The total ride counts (5,721,089) and station subset (4,208,269) were validated against SQLite query results, ensuring data integrity. SQLite facilitated the initial data preparation and analysis, while Excel provided preliminary validation. The dashboard’s effectiveness was confirmed through a screenshot (`image.png`), verifying the inclusion of all planned visualizations.

## Observations

The visualizations effectively highlight usage disparities: casual riders favor recreational patterns (weekends, tourist stations, afternoons), while members exhibit commuter behavior (weekdays, morning/evening peaks). The interactive nature of the PowerBI dashboard allows the marketing team to explore these trends dynamically, supporting data-driven decision-making. The focus on casual rider preferences aligns with the goal of increasing memberships, with potential for further spatial analysis using latitude/longitude data if needed.
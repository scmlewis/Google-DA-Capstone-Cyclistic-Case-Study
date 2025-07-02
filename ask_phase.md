# Cyclistic Bike-Share Analysis: Ask Phase

## Business Problem

Cyclistic, a Chicago-based bike-share company, seeks to increase its annual memberships to enhance revenue and customer loyalty. The marketing team aims to convert casual riders, who use single-ride or day passes, into annual members. This project analyzes 12 months of historical bike trip data to identify differences in usage patterns between casual riders and annual members, focusing on ride frequency, duration, timing, and station preferences. The objective is to derive actionable insights that inform targeted marketing strategies to encourage casual riders to adopt annual memberships, thereby supporting Cyclistic’s growth objectives.

## Analysis Questions

To guide the analysis, the following SMART (Specific, Measurable, Achievable, Relevant, Time-bound) questions were formulated:

1. **How do ride duration and frequency differ between casual riders and members by day of the week?**
   - **Purpose**: This question examines whether casual riders and members exhibit distinct ride patterns across weekdays and weekends. For example, casual riders may take longer, less frequent rides on weekends, while members may use bikes for daily commutes. These insights can inform when to launch promotions (e.g., weekend campaigns targeting casual riders).
   - **Relevance**: Understanding temporal differences supports the marketing goal by identifying optimal times for outreach, increasing the likelihood of converting casual riders.

2. **Which start stations are most popular among casual riders compared to members?**
   - **Purpose**: This question identifies high-traffic stations preferred by casual riders, enabling targeted marketing efforts such as station-based advertisements or promotional events. It compares station usage to highlight locations where casual riders are most active.
   - **Relevance**: Station-specific insights allow Cyclistic to focus marketing resources efficiently, maximizing impact on casual riders likely to consider memberships.

3. **What are the peak ride hours for casual riders compared to members?**
   - **Purpose**: This question analyzes ride start times to determine when casual riders are most active (e.g., evenings or afternoons) compared to members (e.g., morning commutes). These patterns can guide the timing of digital ads or membership incentives.
   - **Relevance**: Aligning marketing campaigns with peak usage hours increases visibility and engagement with casual riders, supporting the conversion goal.

## Methodology

These questions will be answered using a dataset of Cyclistic bike trips from January 2024 to December 2024, containing columns such as `ride_id`, `started_at`, `end_time`, `start_station_name`, and `member_casual`. Tools including Excel, SQLite, R, and PowerBI will be employed to clean, analyze, and visualize the data. The analysis will focus on metrics like ride duration (calculated as `ended_at` minus `started_at`), ride frequency (counts by day or hour), and station popularity (counts by `start_station_name`), ensuring actionable insights for Cyclistic’s marketing team.
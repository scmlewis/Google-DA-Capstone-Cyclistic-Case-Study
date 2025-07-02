# Cyclistic Bike-Share Analysis: Act Phase

## Overview

The Act Phase synthesizes the findings from the Cyclistic Bike-Share Analysis to provide actionable recommendations for converting casual riders into annual members, enhancing Cyclistic’s revenue and customer loyalty. Based on the analysis of 5,721,089 bike trips from January to December 2024 and the PowerBI dashboard visualizations, these recommendations target the distinct usage patterns of casual riders versus annual members, aligning with the marketing team’s objectives.

## Recommendations

1. **Weekend Membership Promotions at Tourist Stations**:
   - **Rationale**: The analysis revealed that casual riders take longer rides on weekends (e.g., 24.95 minutes on Sunday, 24.56 minutes on Saturday) and frequent tourist-heavy start stations (e.g., Streeter Dr & Grand Ave: 48,316 rides, Millennium Park: 20,841 rides). This suggests recreational usage, contrasting with members’ shorter, weekday commutes.
   - **Action**: Launch a weekend-specific membership promotion, offering a discounted annual pass (e.g., 20% off) for casual riders who sign up at these high-traffic stations. Implement on-site marketing (e.g., posters, QR code sign-up links) during peak weekend hours (Saturday/Sunday, 11 AM–6 PM).
   - **Expected Impact**: Increased visibility and convenience could convert up to 10–15% of casual weekend riders (approximately 78,620–118,000 riders, based on 429,357 Saturday rides and 356,848 Sunday rides) into members, boosting revenue.

2. **Evening Digital Advertising Campaigns**:
   - **Rationale**: Casual riders peak at 5 PM (197,661 rides) with high afternoon/evening activity (11 AM–6 PM), while members show commuter peaks at 5 PM (386,723 rides) and 7–8 AM. This indicates casual riders are active post-work or recreationally, offering a distinct marketing window.
   - **Action**: Deploy targeted digital ads on platforms like X or Google Ads at 5 PM, highlighting membership benefits (e.g., unlimited rides, cost savings) with a limited-time offer (e.g., 10% off for sign-ups within 24 hours). Use geofencing around popular casual stations (e.g., Streeter Dr & Grand Ave) to reach this audience.
   - **Expected Impact**: Evening ads could engage 5–10% of casual riders (approximately 9,883–19,766 riders, based on 197,661 rides), increasing membership conversions during high-activity periods.

3. **Incentive Program for Recreational Riders**:
   - **Rationale**: The preference for tourist stations and longer weekend rides suggests casual riders value flexibility and leisure. Members’ consistent usage indicates a need for reliability, which memberships provide.
   - **Action**: Introduce a trial membership program offering a 7-day pass for $10, available at recreational stations, with an option to upgrade to an annual membership at a reduced rate (e.g., $75 instead of $99) if used on multiple weekend days. Promote this via the PowerBI dashboard’s interactive filters to identify high-potential stations.
   - **Expected Impact**: A trial could attract 5–10% of weekend casual riders (approximately 39,310–78,620 riders), with 20–30% converting to annual memberships (7,862–23,586 new members), enhancing long-term loyalty.

## Tools and Validation

The recommendations were developed using insights from SQLite queries and validated through the PowerBI dashboard, which visualizes ride patterns, station popularity, and peak hours. The dataset’s integrity was confirmed with a total of 5,721,089 rides, and the station subset (4,208,269 rows) supports targeted station-based strategies. Excel provided preliminary validation, ensuring data accuracy.

## Implementation Plan

- **Short-Term (1–3 Months)**: Roll out weekend promotions and evening ads, tracking sign-up rates via a unique promo code (e.g., “WEEKEND2024”, “EVENING5PM”) to measure effectiveness.
- **Medium-Term (3–6 Months)**: Launch the trial membership program, monitoring participation and conversion rates at key stations using PowerBI filters.
- **Long-Term (6–12 Months)**: Evaluate membership growth, adjusting strategies based on data trends (e.g., expanding to additional stations with high casual activity).

## Observations

The recommendations leverage casual riders’ recreational patterns (weekends, tourist stations, afternoons) to drive conversions, contrasting with members’ commuter behavior. The PowerBI dashboard’s interactivity allows the marketing team to refine targeting dynamically. The removal of outliers (8,092 rows) ensures realistic insights, while the dataset’s comprehensiveness supports scalable implementation. These strategies align with Cyclistic’s goal of increasing annual memberships, with potential for further optimization using spatial data (latitude/longitude).
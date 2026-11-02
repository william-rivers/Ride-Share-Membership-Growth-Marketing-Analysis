# Ride-Share-Membership-Growth-Marketing-Analysis

A project focused on identifying differences between members and casual users in order to convert casuals into members.

## Background
A bike-share company operates a fleet of several thousand geotracked bicycles across a network of stations spread throughout Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, we need to understand how casual riders and members use bikes to design a new marketing strategy for converting casual riders into annual members.

## Business Task
Accelerate revenue and annual membership growth by analyzing aggregate trip metrics to discover distinct usage patterns for casual riders and annual members, equipping marketing teams with data-supported profiles needed to optimize conversion campaigns.

### Key Objectives
1) **Develop Behavioral Profiles**: Segment ride data to isolate casual use that mirrors member behavior.
2) **Optimize Campaign Timing**: Pinpoint high-yield seasonal windows for aggressive marketing by mapping fluctuations in ride volume.
3) **Locate Geographic Hotspots**: Identify high-density stations for high-ROI out-of-home (OOH) advertisements.
4) **Define Conversion Triggers**: Translate clear cost-benefit metrics to establish where annual membership becomes more economical.

## Data and Methodology

### Data Source
The [raw data source](https://divvy-tripdata.s3.amazonaws.com/index.html), stripped of personal identifying information, is publicly available where Divvy, the real-world counterpart to the fictional company, publishes their records from June 1, 2020 to present. It is available through Motivate International Inc. under this [license](https://divvybikes.com/data-license-agreement). The raw data used in this project is also available in the data folder of this repo.

### Primary Tools
- SQL (BigQuery)
- Tableau

### Secondary Tools
- Python
- Google Sheets

## Data Cleaning

1) Removed Duplicate Records
2) Handling Nulls
   - Filled several thousand null station names and ids with the nearest station within 50 meters
3) Checking Sanity
   - Removed rides with negative durations or zero duration
   - Removed rides with 0-2 min durations if they did not travel at least 50 meters or change stations
   - Removed classic bike rides that averaged more than 8.5 meters per second (19.0 mph)
   - Removed electric bike rides that averaged more than 11 meters per second (24.6 mph)

## Analysis

### Primary Focus

The primary objective of this analysis is to identify high-potential conversion segments within the casual rider user base and design a targeted acquisition campaign to convert them to annual members. Marketing capital should be concentrated on low friction conversions, casual riders whose behavior patterns already mimic the more utility-drivin member behaviors.

### Strategic Target Segments

1) **Short-Duration Commuters:** 
2) **Rush-Hour Commuters:**
3) **Micro-Mobility Inland Corridor:**
4) **Winter Riders:**

### Biphasic Go-To-Market Campaign

 * **Phase 1: Peak-Volume Acquisition (May-August)**
   * **Objective:**
   * **Tactics:** 
 * **Phase 2: High Conversion Retention (December-February)** 
   * **Objective:**
   * **Tactics:** 

Marketing should focus on targeting casuals that take rides:

1) with shorter durations
   - Especially May-September where the casual duration is highest
2) during weekdays
   - High focus on rides starting 6-10 am which is member-dominated
   - Slight focus on rides starting 3-7 pm which is used heavily by both groups
3) during the Winter
   - Slight focus on classic bike rides which are used more commonly by members during Winter
4) from/to stations that fall into member dominated areas

The marketing campaign should be biphasic. Phase 1 runs between May and August when there are more casuals active even though they are not displaying "member-like" behavior. During this phase, we primarily target the users behaving most like members and emphasize the potential savings at even light use for unlikely converts. Phase 2 runs between December and February when there is low casual activity but it is much more consistent with member behavior. These are all likely converts. In both phases, we should combine advertising through the app and OOH marketing at key stations to maximize exposure.

## Supporting Visualizations

<p align="center">
  <a href="https://public.tableau.com/views/ride_share_member_growth_marketing_analysis_resized/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link" target="_blank">
    <img src="/assets/ride_share_dashboard.png" alt="Ride-Share Marketing Dashboard" width="100%">
  </a>
  <br>
  <em>Figure 1: Interactive Member Conversion Dashboard. Click the preview image to open the live view on Tableau Public.</em>
</p>

<p align="center">
  <a href="https://public.tableau.com/views/ride_share_member_growth_marketing_analysis_resized/Story1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link" target="_blank">
    <img src="/assets/ride_share_story.png" alt="Ride-Share Marketing Story" width="100%">
  </a>
  <br>
  <em>Figure 2: Interactive Member Conversion Story. Click the preview image to open the live view on Tableau Public.</em>
</p>

## Recommendations



### Limitations

Only have access to aggregate data and are not able to track individuals. Members displayed very consistent behavior and I suspect that stays true at the individual level. 

### Next Steps

 
 
This project dataset was suggested by the Google Data Analytics Capstone project.

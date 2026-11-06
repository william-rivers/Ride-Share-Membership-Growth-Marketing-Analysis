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

The [raw data source](https://divvy-tripdata.s3.amazonaws.com/index.html), stripped of personal identifying information, is publicly available where Divvy, the real-world counterpart to the fictional company, publishes their records from June 1, 2020 to present. It is available through Motivate International Inc. under this [license](https://divvybikes.com/data-license-agreement). The raw data used in this project specifically is also available in a zipped format through this [link](https://drive.google.com/file/d/15kq_08r88PqiFFRycjoh1DGF9TfPrnz5/view?usp=sharing).

### Primary Tools

- Google BigQuery (SQL): Utilized as the primary cloud data warehouse to aggregate, clean, and query historical transactional logs.
- Tableau Public: Employed to build interactive charts, dashboards, and executive storyboards.

### Secondary Tools

- Python: Utilized locally for raw data preprocessing (chunking for file resizing) to optimize cloud data warehouse upload efficiency.
- Markdown: Used to document the analytical log and maintain tracking notes.
- Google Sheets: 

## Data Cleaning

The executable queries are located in the [/scripts_and_queries/02_data_cleaning.sql](./scripts_and_queries/02_data_cleaning.sql) file. The results and thought process can be found in the [/notebooks/analytical-log.md](./notebooks/analytical-log.md##-Step-3:-Process) file.

### Core Data Quality Operations

1) Deduplication: Identified and removed using GROUP BY and HAVING
2) Resolved Incomplete Records: Filled several thousand null station names and ids with the nearest station within 50 meters
3) Verified Data Sanity:
   - Removed rides with negative durations or zero duration
   - Removed rides with 0-2 min durations if they did not travel at least 50 meters or change stations
   - Removed classic bike rides that averaged more than 8.5 meters per second (19.0 mph)
   - Removed electric bike rides that averaged more than 11 meters per second (24.6 mph)

## Analysis

The executable queries are located in the [/scripts_and_queries/03_business_analysis.sql](./scripts_and_queries/03_business_analysis.sql) file. The results and thought process can be found in the [/notebooks/analytical-log.md](./notebooks/analytical-log.md##-Step-4:-Analyze) file.

### Primary Focus

Rather than deploying a broad marketing campaign across the entire casual footprint, this analysis focuses on identifying casual rides whose usage patterns already mimic the more utility-driven member behaviors. Targeting these low-friction conversions maximizes campaign efficiency.

### Behavioral Profiles

**Members**
1) Ride Duration: Lower average than casuals year-long
   - Greatest difference with casuals between May and September
   - More consistent difference on classic bikes
   - Longer duration than casuals on electric bikes during Winter
2) Season: Higher proportion of the rides between November and April
    - Most exaggerated during Winter (~80% of monthly rides)
    - Doubly true when looking at only classic bike rides or only weekdays
3) Day Type: Favor weekdays more than weekends
   - Especially high usage during traditional rush hours (6:00 AM - 10:00 AM and 3:00 PM - 7:00 PM)
4) Geography: Rides tend to be more spread out across the full service range
   - Especially true on weekends
   - Favor inland locations more than casuals
5) Overall: Very little variation in usage patterns

**Casuals**
1) Ride Duration: Higher average year-long
   - Duration rapidly increases as weather warms and rapidly drops as weather cools
2) Season: Higher proportion of the rides between May and October
   - Shift toward using electric bikes more often during Winter
3) Day Type: Favor weekends over weekdays
   - Weekdays only show rides clustered during the evening rush hour (3:00 PM - 7:00 PM)
   - Classic bike usage roughly doubles on weekends
4) Geography: Rides tend to be more concentrated in the same geographic area
   - Coastal areas in particular are highly popular
6) Overall: Large amounts of variation in usage pattern based on many factors

### Low Friction Target Segments

1) **The Short-Duration Commuters:** Annual members heavily favor taking short-duration, utility-driven rides. A significant cohort of casual riders mirrors this behavior, which marks them as likely converts.
2) **The Rush-Hour Commuters:** Temporal analysis shows that although the highest casual usage is on the weekends, a distinct segment of casual rides occur during traditional weekday rush hours (6:00 AM - 10:00 AM and 3:00 PM - 7:00 PM), matching member peak usage hours. The member-dominated morning rush identifies likely converts and the shared evening rush captures the highest traffic periods.
3) **The Inland Corridor:** Geographic mapping isolates a divide between members and casual users: casual rides concentrate more heavily along the coast while member rides concentrate more heavily inland. Analysis identified [24 stations](./notebooks/analytical-log.md###-4.6-Popular-Station-Analysis) that are member-dominated despite high popularity with casual users.
4) **The Seasonal Pivot:** Casual riders still active during winter months (December-February) are displaying member-like behavior since casual rides dropped to 1/10th of their peak usage during the winter months while member rides only dropped to 1/4th of their peak. Additionally, while the rest of the year matches the standard member ratio of 1:2 classic-to-electric rides, winter casual usage shifts to a 1:3 ratio. This indicates a high willingness to pay a premium for speed and cold-weather convenience.

### Campaign Timing

Peak volume among both annual members and casual users occurs May-October with over 70% of all rides and over 80% of casual rides happening during this window. The number of rides per month starts to fall in September but doesn't drop below 600,000 rides until November. This is an optimal time for broad reach.

The extreme drop in casual usage during the winter months identifies a lower volume but also lower friction segment for targeted marketing.

### Conversion Triggers

**Membership Annual Profit Point**
| Ride Duration | Single, classic | Single, electric | Day Pass, both  |
|:-------------:|:---------------:|:----------------:|:---------------:|
| 10 min        | 48 rides/year   | 27 rides/year    | 8 passes/year   |
| 15 min        | 36 rides/year   | 19 rides/year    | 8 passes/year   |

**Membership Monthly Profit Point**
| Ride Duration | Single, classic | Single, electric | Day Pass, both  |
|:-------------:|:---------------:|:----------------:|:---------------:|
| 10 min        | 4 rides/month   | 3 rides/month    | <1 pass/month   |
| 15 min        | 3 rides/month   | 2 rides/month    | <1 pass/month   |

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

### Biphasic Go-To-Market Campaign

 - **Phase 1: Peak-Volume Acquisition (May-August)**
   - **Objective:** Capture the massive summer surge of casual riders by separating high-utility riders from recreational users.
 - **Phase 2: High-Conversion Retention (December-February)** 
   - **Objective:** Capture the lower volume of casual users who display the strongest baseline alignment with annual member habits.

#### Implement In-App Loss Aversion Triggers

-  **General:** A membership would have saved you $X.XX on this ride
-  **General:** This month you would have saved $X.XX with a membership
-  **General:** Did you know the membership costs less than $12/month?
-  **Shorter Classic Rides:** Membership costs less per month than four 10 minute rides/month on classic bikes
-  **Longer Classic Rides:** Membership costs less per month than three 15 minute rides/month on classic bikes
-  **Shorter Electric Rides:** Membership costs less per month than three 10 minute rides/month on electric bikes
-  **Longer Electric Rides:** Membership costs less per month than two 15 minute rides/month on electric bikes
-  **Day Passes:** Did you know the annual membership costs less than 8 Day Passes?
-  **Classic Ride Under 45 Minutes:** This ride would be free with a membership!

#### Deploy Localized Out-of-Home (OOH) Station Marketing

Establish localized brand equity by deploying physical marketing (e.g. vinyl station wraps, dock signage, or digital terminal displays) at the 24 key stations identified during the analysis. 

### Offer Dynamic Membership Trial Discounts

Establish a system to identify casual users most likely to convert and lower their barrier to conversion for the new year by offering a small discounted trial. At the beginning of the year, people chose new habits or goals often related to health and exercise. Lowering the barrier encourages people to trial a healthy mode of transportation or exercise.

Example Algorithm: Points earned per ride and aggregated over the month 
- Ride Duration
   - Duration > 45 minutes: -2 pt
   - 25 minutes < duration <= 45 minutes: -1 pt
   - 15 minutes < duration <= 25 minutes: 0 pt
   - 10 minutes < duration <= 15 minutes: 1 pt
   - Duration <= 10 minutes: 1.5 pt
- Season
   - November, March, or April: 1 pt
   - December, January, or February: 2 pt
   - May-September and duration < 10 minutes: 0.5 pt
- Day Type
   - Weekday and 6-10 a.m. start: 2 pt
   - Weekday and 3-7 p.m. start: 1 pt
   - Weekday and other time: 0.5 pt
   - Weekend: 0 pt
- Rideable Type
   - November-April and electric: 0.5 pt
- Geography
   - Starts at a target station: 1 pt
   - Ends at a target station: 1 pt
   - Starts at an anti-target station: -1 pt
   - Ends at an anti-target station: -1 pt
   - Start station = end station: -1 pt
- Consistency (tracking individuals' behavior)
   - 3+ rides with 2+ pts last month: x1.5 pts
   - 3+ rides with 3+ pts last month: x2 pts

<6 points: No trial month offered
6-14 points: 20% discount on 1 month trial membership ($9.59 for the month)
15+ points: 50% discount on 1 month trial membership ($6.00 for the month)

Additional analysis is needed to identify whether this promotion should be limited to the winter phase. If the high volume of casual summer rides represents repeat customers, it could lead to a notable drop in summer revenue from casuals using the discounted trial without intending to purchase an annual membership. If the high volume is mostly from unique users, the promotion is unlikely to cut into revenue severely.

### Limitations

* No Customer IDs: The dataset lacks the unique customer IDs required to track individuals longitudinal usage.
* No Demographic Data:  The dataset lacks the demographic profiles required to track cohorts of users.
* Financial Redaction: The dataset lacks exact pricing tables, dynamic surge rates, and operational costs required to determine a precise Return on Investment (ROI) forecast for the campaign.

### Next Steps

1) User Tracking: Identify whether high summer casual usage is driven by repeat users or unique users
2) A/B Testing: Launch a small-scale pilot of the in-app loss aversion triggers to test conversion lift before global deployment.
3) First-Party Surveys: Deploy brief, incentivized in-app surveys to better understand blocks preventing membership acquisition.
   - Example Incentive: One ride at membership pricing
4) Use k-means clustering, random forest, or related machine learning concepts to optimize the algorithm for identifying likely converts
   - Planned future data science addendum

  
*This project dataset was suggested by the Google Data Analytics Certificate as part of the capstone project.

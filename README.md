# Cyclistic Data Analysis

## Understanding the scenario

As a junior data analyst on the marketing analytics team at Cyclistic, a bicycle-sharing company in Chicago, the marketing director believes that the company's future success hinges on maximizing annual memberships. Consequently, your team aims to discern the differences in the use of Cyclistic bicycles between occasional cyclists and annual members. Armed with this knowledge, your team will craft a new marketing strategy to convert occasional cyclists into annual members. However, before presenting your recommendations, Cyclistic executives must approve them; therefore, you need to substantiate your proposal with a compelling presentation of professional data and visualizations.

## Stakeholders

* **Cyclistic**: A bike-sharing program comprising 5,800 bicycles and 600 stations. Cyclistic stands out for offering recumbent bicycles, manual tricycles, and cargo bikes, providing a more inclusive experience for people with disabilities and cyclists who cannot use a standard two-wheeled bicycle. Although about 8% of cyclists opt for assisted options, most prefer traditional bicycles. Approximately 30% of Cyclistic users use bicycles for their daily commute to work.

* **Lily Moreno**: The marketing director and your manager. Moreno is responsible for developing campaigns and initiatives to promote the bike-sharing program, including email, social networks, and other channels.

* **Cyclistic Marketing Data Computational Analysis Team**: A team of data analysts responsible for collecting, analyzing, and reporting data to drive Cyclistic's marketing strategy. Having joined this team six months ago, you've dedicated yourself not only to understanding Cyclistic's mission and business goals but also to exploring how you can contribute to achieving them in your role as a junior data analyst.

* **Cyclistic Executive Team**: The detailed executive team that will decide whether to approve the recommended marketing program.

## About Cyclistic

In 2016, Cyclistic launched a successful bike-sharing program that has since grown to a fleet of 5,824 georeferenced and docked bicycles across 692 stations throughout Chicago. The bicycles can be unlocked from one station and returned to any other station in the system at any time.

Cyclistic's marketing strategy has historically focused on building general brand recognition and attracting a wide range of consumer segments. The flexibility of pricing plans, including single-trip passes, full-day passes, and annual memberships, has played a crucial role in this approach. Occasional cyclists purchase single-trip or full-day passes, while those opting for annual memberships are referred to as Cyclistic members.

Financial analysis by Cyclistic suggests that annual members are significantly more profitable than occasional cyclists. Despite the flexibility in pricing attracting more customers, Moreno believes that maximizing the number of annual members is key to future growth. Instead of launching a marketing campaign targeting all new customers, Moreno sees potential in converting casual cyclists, who are already familiar with the Cyclistic program, into members. She emphasizes that casual cyclists have already chosen Cyclistic for their mobility needs.

Moreno has set a clear goal: design marketing strategies aimed at turning occasional cyclists into annual members. However, achieving this requires the marketing analysts' team to gain a better understanding of how annual members and occasional cyclists differ, why casual cyclists would buy a membership, and how digital media could impact their marketing tactics. Moreno and her team are eager to analyze Cyclistic's historical bicycle travel data to identify trends.

## Data

Trip data includes the following columns:
* ride_id: **String**
  - Each ride_id corresponds to a unique trip and cannot be repeated.
* rideable_type: **String**
  - Referes to wether the bycicle with which each trip was made is electric. classic or a docked bike.
* started_at: **TimeStamp**
  - Includes year, month, day, hour, minute and second each ride was started.
* ended_at: **TimeStamp**
  - Includes year, month, day, hour, minute and second each ride was finished.
* start_station_name: **String**
  - Includes the station name each trip started. Tipically the intersection of two streets.
* start_station_id: **String**
  - Refers to the unique ID assigned to each station.
* end_station_name: **String**
  - Includes the station name each trip finished. Tipically the intersection of two streets.
* end_station_id: **String**
  - Refers to the unique ID assigned to each station.
* start_lat: **Float**
  - Refers to the latitude at which each trip started.
* start_lng: **Float**
  - - Refers to the longitude at which each trip started.
* end_lat: **Float**
  - Refers to the latitude at which each trip ended.
* end_lng: **Float**
  - Refers to the longitude at which each trip ended.
* member_casual: **String**
  - Specifies if the ride was made by a member or a casual user.

For this **Practical Case Analysis**, we will focus on the started_at, ended_at, and member_casual columns as they provide access to ride duration, day of the week, month, membership type, and total trips, offering powerful insights for this specific scenario.

All trip data can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

For data privacy reasons, usage of personally identifiable information of cyclists is prohibited. This means that connecting pass purchases with credit card numbers to determine if occasional cyclists live in the Cyclistic service area or if they bought several passes from a single trip is not allowed.

Data has been provided by **Motivate International Inc** under [this license](https://www.divvybikes.com/data-license-agreement).

## First steps

**1. What is the problem you are trying to solve?**

- Increase the number of users with memberships. Convert casual users into members.

**2. How can your knowledge drive business decisions?**

- Through a comprehensive analysis of historical bicycle travel data, the analyst provides data-driven insights that inform targeted marketing strategies. This includes understanding user segmentation, optimizing campaigns, and proposing initiatives to maximize annual memberships. The ability to present compelling visualizations and insights ensures executive support for the proposed strategies, contributing to the overall success and growth of Cyclistic.

**3. Where is the data located?**

- Google Cloud and BigQuery, processed with PopSQL.

**3. How is the data organized?**

- There is one table per month of the year, with column details available in the **Data** section.

**4. Are there problems with the bias or credibility of this data? Is your data reliable, original, comprehensive, current and cited (ROCCC)?**

- No, this data is automatically recorded by the stations, and all existing stations are included. It is directly provided by the company.

**5. How are you addressing authorization, privacy, security and accessibility?**

- Data is protected by Google encryption, and access is restricted to the configured Google account. Data authorization is covered by [this license](https://www.divvybikes.com/data-license-agreement).

**6. How did you verify the integrity of the data?**

- Verification involved executing a SELECT query on the tables to ensure the data aligns with expectations.

**7. How does it help you answer your question?**

- Knowing the type of data and confirming its reliability from a trustworthy source facilitates data interpretation.

**8. Is there a problem with the data?**

- No, the data is the most up-to-date with closure in December 2023.

## Prepare the data

1. For the preparation process, it is essential to create a new table to consolidate data from each month of 2023. This aids in organizing data and enables cleaner queries, incorporating data from all 12 months.

View the [Prepare SQL Sentence](/Prepare-Data) for detailed instructions.

## Process the data

1. Create a new column called "ride_length." This will be calculated per day of the week, per month, per year, and per membership type.
- The SQL query for this is:
```
 AVG(TIMESTAMP_DIFF(ended_at, started_at, minute)) AS avg_ride_length_min
```
The TIMESTAMP_DIFF function determines the duration of each ride_id (end time minus start time), and the AVG function calculates the average ride duration in terms of "minutes."

2. Create a new column called "day_of_week".
- The SQL query for this is:
```
 EXTRACT(
        DAYOFWEEK
        FROM
            started_at
    ) AS days_of_week
```
The EXTRACT function alongside the DAYOFWEEK function determines the day of the week from the started_at column. 
> [!NOTE]
> Note that days_of_week will be shown as integers from 1 through 7, where 1 is Sunday and 7 is Saturday.

3. Create a new column to get the mode of day_of_week. This reveals the day with the most rides made.
- The SQL query for this is:
```
 APPROX_TOP_COUNT(
        EXTRACT(
            DAYOFWEEK
            FROM
                started_at
        ),
        1
    ) AS mode
```
The APPROX_TOP_COUNT function helps identify the day of the week that repeats the most throughout the year. In this case, Saturday had the highest frequency with 883,566 rides in 2023.

4. Create a new column called "total_rides". This column will get the total rides per day of the week, per month, per year and per membership type.

> [!IMPORTANT]
> These columns will be run on four different SQL files to obtain different data according to the timeframe being inspected.

> Explore [this code](/Max-Mean-Mode) for an example of gathering data from the table year_23, which consolidates data from all 12 months.

> You can find all examples for year, month, day and membership type [here](/).

## Analyze the data

**1. How should you organize your data to perform an analysis?**

- Organize data per month and per year, with days of the week in ascending order (1-7).

**2. Is your data in the correct format?**

- Yes

**3. What surprises did you discover in the data?**

- Colder months have fewer trips than warmer months. Weekends are the most active days with the longest average duration, approximately 19 minutes. Weekdays average around 15 minutes. Mondays tend to have the longest trip durations but with fewer rides.

**4. How will this knowledge help you answer your business questions?**

- Focusing on travel time and quantity provides valuable insights to target specific market segments efficiently.

### 2023 as a Year

In 2023, there were a total of **5,719,877 rides**, with 64% made by members and 36% by casual users.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/52b51ee6-0bf8-4627-b0f2-73f5a237031e)

The average ride duration throughout the year was 18 minutes.

### 2023 in Months

June, July, and August stand out as the months with the highest ride numbers, consistent with vacation periods and better weather. The mean ride duration per month aligns with this observation.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/827af81c-41c4-4186-92ae-347cf977e1f6)

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/95e323c7-8fb2-4e74-87fe-ad82b08aa1d9)

### 2023 Each Day

Thursday through Saturday are the most active days of the week throughout the year, with up to 150,000 more members than on Mondays.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/74c6a0e0-1b29-4783-96c7-10034bdb2c99)

However, ride duration is higher on weekends (Saturday and Sunday), averaging 4 minutes more.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/290e6a1a-0f64-4659-9388-4734624fa40c)

### Dashboard

You can view the entire dashboard [here](https://popsql.com/dashboards/R1U5GmL6/cyclistic?access_token=38d1bdf4080079808bd6fb5e16f3d279) which contains all the vizualizations seen here and additional insights, such as member vs. casual user use over a month and day of the week. The dashboard presents data in chart mode and more.

Dashboard includes:

* Total Rides in 2023
* Total Rides per Membership in 2023
* Average Ride Duration in 2023
* Total Rides per Month in 2023
* Total Rides per Month per Membership
* Mean Ride Length per Month in 2023 (min)
* Total Rides per Day of the Week in 2023
* Total Rides per Day of the Week per Membership in 2023
* Mean Ride Length per Day of the Week in 2023 (min)
* Mean ride length per membership (min) in 2023

## Concluding remarks

In conclusion, the analysis conducted on Cyclistic's bicycle travel data offers valuable insights that can significantly influence business decisions. The strategic focus on converting occasional cyclists into annual members aligns with the company's goal of maximizing profitability. The data-driven approach, encompassing ride duration, day of the week trends, and membership types, provides a robust foundation for designing targeted marketing strategies.

Examining daily trends indicates that Thursday through Saturday are the most active days, presenting an opportune timeframe to engage potential annual members. Notably, weekends exhibit longer ride durations, suggesting a leisurely and more extended use of Cyclistic bicycles during this period.

Developing a targeted marketing campaign to increase the number of Cyclistic members involves leveraging the identified insights and tailoring strategies to address specific user behaviors and preferences. Here's a step-by-step plan:

- **Weekend Promotions**
   - Offer discounted annual memberships exclusively for rides on Saturdays and Sundays
- **Seasonal Campaigns**
   - Offer discounted seasonal memberships to encourage increased ridership during favorable weather conditions.
   - Pointed for peak ride periods in June, July, and August.
- **Membership Benefits Awareness**
  - Highlight the advantages of annual memberships over occasional passes.
  - Showcase member-exclusive benefits, such as priority access to special events, personalized ride recommendations, and loyalty rewards.
- **Targeted Email / Social Media Campaigns**
  - Emphasizing the benefits of becoming a member, including cost savings, convenience, and a sense of belonging to the Cyclistic community.
- **Referral Programs**
  - Implement a referral program where existing members earn rewards for successfully converting occasional cyclists into members.
- **Localized Marketing Initiatives**
  - Consider localized marketing initiatives, focusing on specific stations or neighborhoods with high casual rider activity.
 
By integrating these strategies into a comprehensive marketing campaign, Cyclistic can effectively target occasional cyclists, address their specific needs, and create a compelling case for transitioning to annual memberships. Continuous monitoring of campaign performance and user feedback will be crucial for refining strategies and ensuring long-term success.

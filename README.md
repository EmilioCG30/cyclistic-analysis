# Cyclistic Data Analysis

## Understanding the scenario

As a junior data analyst who works on the team of marketing analysts at Cyclistic, a bicycle sharing company in Chicago, the marketing director believes that the future success of the company depends on maximizing the number of annual memberships. Therefore, your team wants to understand what differences there are in the use of Cyclistic bicycles between occasional cyclists and annual members. Through this knowledge, your team will design a new marketing strategy to turn occasional cyclists into annual members. However, before that, Cyclistic executives must approve your recommendations; therefore, you must support your proposal with a convincing view of their professional data and visualizations.

## Stakeholders

* **Cyclistic**: A bike-sharing program that includes 5,800 bicycles and 600 stations. Cyclistic stands out for also offering recumbent bicycles, manual tricycles and cargo bikes that offer a more inclusive use of shared bicycles for people with disabilities and cyclists who cannot use a standard two-wheeled bicycle. Most cyclists choose traditional bicycles, about 8% of cyclists use assisted options. Cyclistic users are more likely to use the bicycle for recreation, but about 30% use it to go to work every day.

* **Lily Moreno**: The marketing director and your manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike sharing program. Campaigns can include email, social networks and other channels.

* **Cyclistic Marketing Data Computational Analysis Team**: A team of data analysts who are responsible for collecting, analyzing and reporting data that help drive Cyclistic's marketing strategy. You joined this team six months ago and have dedicated yourself not only to knowing Cyclistic's mission and business goals, but also to seeing how you can help Cyclistic achieve it, from your position as a junior data analyst.

* **Cyclistic Executive Team**: The executive team, highly detailed, will decide whether to approve the recommended marketing program.

## About Cyclistic

In 2016, Cyclistic launched a successful bike-sharing offer. Since then, the program has grown to reach a fleet of 5,824 georeferenced and blocked bicycles in a network of 692 stations throughout Chicago. The bicycles can be unlocked from one station and returned to any other station in the system at any time.

Until now, Cyclistic's marketing strategy was based on building a general brand recognition and attracting wide consumer segments. One of the approaches that helped make this possible was the flexibility of its pricing plans: single-trip passes, full-day passes and annual memberships. Customers who buy single-trip passes or full-day passes are called occasional cyclists. Customers who buy annual memberships are called Cyclistic members.

Cyclistic financial analysts came to the conclusion that annual members are much more profitable than occasional cyclists. Although price flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will be key to future growth. Instead of creating a marketing campaign that aims at all new customers, Moreno believes that there are many possibilities to turn casual cyclists into members. She points out that casual cyclists already know the Cyclistic program and have chosen Cyclistic for their mobility needs.

Moreno set a clear goal: Design marketing strategies aimed at turning occasional cyclists into annual members. However, to do that, the team of marketing analysts needs to better understand how annual members and occasional cyclists differ, why casual cyclists would buy a membership and how digital media could affect their marketing tactics. Moreno and his team are interested in analyzing Cyclistic's historical bicycle travel data to identify trends.

## Data

Trip data includes the following columns:
* ride_id: **String**
* rideable_type: **String**
* started_at: **TimeStamp**
* ended_at: **TimeStamp**
* start_station_name: **String**
* start_station_id: **String**
* end_station_name: **String**
* end_station_id: **String**
* start_lat: **Float**
* start_lng: **Float**
* end_lat: **Float**
* end_lng: **Float**
* member_casual: **String**

For this **Practical Case Analysis** we will be centering our attention in started_at, ended_at and member_casual columns as it gives us access to ride duration, day of the week, month, if the user is a member or casual rider and total trips, giving us access to powerful insights for this specific scenario.

All trip data can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

For data privacy reasons, you are prohibited from using personally identifiable information of cyclists. This means that you will not be able to connect pass purchases with credit card numbers to determine if occasional cyclists live in the Cyclistic service area or if they bought several passes from a single trip.

Data has been provided by **Motivate International Inc** under [this license](https://www.divvybikes.com/data-license-agreement).

## First steps

**1. What is the problem you are trying to solve?**

- Increase the number of members with membership. Turn those casual users into members.

**2. How can your knowledge drive business decisions?**

- To be able to determine the best way to do this considering the available data.

**3. Where is the data located?**

- Google Cloud and BigQuery, processed with PopSQL

**3. How is the data organized?**

- There is one table per month of the year, columns can be seen in the **Data** section.

**4. Are there problems with the bias or credibility of this data? Is your data reliable, original, comprehensive, current and cited (ROCCC)?**

- No, this data is automatically recorded by the stations and all existing stations are included. They are provided directly by the company.

**5. How are you addressing authorization, privacy, security and accessibility?**

- Data is protected by Google encryption, the data can only be accessed through the configured Google account. The authorization of the data is under [this license](https://www.divvybikes.com/data-license-agreement).

**6. How did you verify the integrity of the data?**

- Making a SELECT to the tables and verifying the data and that they are in the way they should.

**7. How does it help you answer your question?**

- Data detection is facilitated by knowing the type of data you are working with and it is confirmed that it comes from a reliable place.

**8. Is there a problem with the data?**

- No, they are the most up-to-date data with closure in December 2023.

## Prepare the data

1. For the preparation process first of all it is essential to create a new table in order to unite all tables from each month of 2023.

See [Prepare SQL Sentence](/Prepare-Data) for more details on how to do this.

2. Add two columns to the table in order to obtain the ride length and day of the week.

## Process the data

## Analyze the data

### 2023 as a Year

There was a total of **5'719,877 rides** on 2023, where 64% of them were made by members, leaving only a 36% of casual users.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/52b51ee6-0bf8-4627-b0f2-73f5a237031e)

The average ride duration was of 18min throughout the year 2023.

### 2023 in Months

June, July and August are the months with more rides, which is consistent with vacations and a better overall climate. The mean ride duration per month is consistent with this assumption.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/827af81c-41c4-4186-92ae-347cf977e1f6)

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/95e323c7-8fb2-4e74-87fe-ad82b08aa1d9)

### 2023 Each Day

Thursday through Saturday are the most active days of the week throughout the year with up to 150,000 more members than on Mondays.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/74c6a0e0-1b29-4783-96c7-10034bdb2c99)

However, the ride duration is higher on weekends (Saturday and Sunday), averaging 4 minutes more.

![image](https://github.com/EmilioCG30/cyclistic-analysis/assets/111447739/290e6a1a-0f64-4659-9388-4734624fa40c)

### Dashboard

You can view the entire dashboard [here](https://popsql.com/dashboards/R1U5GmL6/cyclistic?access_token=38d1bdf4080079808bd6fb5e16f3d279) which contains all the vizualizations seen here and a few others like member vs casual users use over a month and day of the week. You will be able to see the data being presented in chart mode and much more!


## Sharing the Analysis


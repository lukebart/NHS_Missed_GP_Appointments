# Bartholomew_Luke_DA201_Assignment
LSE Data Analytics Assignment 2

===========================================================================

# Assignment Activity 2: Import & Explore the Data

NOTE: In order to avoid repetition, I wrote a function used to describe the data imported from each csv file. Rather than count the number of records by location or category, I used the calculation of the sum of appointments as I thought this would be a more insightful measure.

Dataset actual_duration.csv
- shape, head() and tail() confirms the total rows to be 137,793 and 8 columns.
- info() shows appointment_date column has object datatype, this will need to be changed to datetime.
- isna() show no missing values.
- Unique count of locations shows sub_icb_location_ons_code = 106, icb_ons_code = 42 & region_ons_code = 7.
- sub_icb_location_ons_code 'E38000256' has the highest sum of appointments = 6,976,986
- icb_ons_code 'E54000050' has the highest sum of appointments = 9,584,943
- region_ons_code 'E40000011' has the highest sum of appointments = 32,574,555
- actual_duration category by highest sum of appointments is 'Unknown / Data Quality'. Most appointments are completed within 15 minutes. I will be able to write a script to calculate the percentage of appointments completed within 15 minutes. Why do some appointments take over 30 minutes (over 9 million)?

Notes: The dataset does not contain descriptive information for the locations (icb_ons_code, region_ons_code). I will need to wrangle the data to include this information to that it be presented informatively in a chart or table.

Dataset appointments_regional.csv
- shape, head() and tail() confirms there are 596,821 rows and 7 columns.
- info() shows appointment_month column has object datatype, this will need to be changed to datetime with format "01/01/2020"
- isna() show no missing values.
- Unique count of locations shows icb_ons_code = 42.
- icb_ons_code 'E54000050' has the highest sum of appointments = 43,083,535
- appointment_status 'DNA' (Did Not Attend) is direct interest to our analysis. DNA sum of appointments = 30,911,233
- appointment_mode 'Face-to-Face' has the highest sum of appointments = 439,981,729
- time_between_book_and_appointment category by highest sum of appointments is 'Same Day'. Most appointments seen within 1 week. Would be good to investigate any relationships between these categories and 'DNA' in appointment_status.

Notes: The dataset does not contain descriptive information for the location icb_ons_code. I will need to wrangle the data to include this information to that it be presented informatively in a chart or table. The location data is limited to ICB and not Sub-ICB. There are also no specific days, date will only be available by month and year in format "01/01/2020".

Dataset national_categories.xlsx
- shape, head() and tail() confirms there are 817,394 rows and 8 columns.
- info() shows appointment_month column has object datatype, this will need to be changed to datetime with format "01/01/2020"
- isna() show no missing values.
- Unique count of locations shows sub_icb_location_name = 106 & icb_ons_code = 42.
- sub_icb_location_name 'NHS North West London ICB - W2U3Z' has the highest sum of appointments = 12,142,390
- icb_ons_code 'E54000050' has the highest sum of appointments = 16,882,235
- service_setting 'General Practice' has by far the highest sum of appointments = 270,811,691
- context_type is unlikely to be usable due to 'Inconsistent Mapping' and 'Unmapped' making up 2 of the 3 categories.
- national_category 'General Consultation Routine' has the highest sum of appointments = 97,271,522. These categories could be useful to determine the use of resources in the NHS.

Notes: The dataset does not contain descriptive information for the location icb_ons_code. I will need to wrangle the data to include this information to that it be presented informatively in a chart or table. The complete date (including day) is available for time series analysis. 

===========================================================================

# Assignment Activity 3: Analyse The Data

Dataset actual_duration.csv
- Updated datatype of appointment_date from object to datetime

Dataset appointments_regional.csv
- Added appointment_date as datetime, mapped from appointment_month

Question 1: Between what dates were appointments scheduled?

Calcuated Min, Max for appointment_date of each dataframe and concatenated.
actual_duration.csv = appointment dates from 01/12/2021 to 30/06/2022
appointments_regional.csv = appointment dates from 01/01/2020 to 01/06/2022
national_categories.xlsx = appointment dates from 01/08/2021 to 30/06/2022

Notes: appointments_regional.csv dates aggregated by month, therefore every date will be format '01/mm/yyyy'. Each dataset ended in June 2022.

Question 2: Which service setting reported the most appointments in North West London from 1 January to 1 June 2022?

Analysed dataset national_categories.xlsx
1. subset by sub_icb_location_name = 'NHS North West London ICB - W2U3Z'
2. filter subset by appointment_date
3. groupby filtered subset and aggregated count_of_appointments using sum

Notes: Most appointments were at the General Practice (4,760,966). The next highest was Primary Care Network (108,901). There were many Unmapped (387,939).

Question 3: Which month had the highest number of appointments?

Analysed dataset national_categories.xlsx
1. groupby year & month, aggregate count_of_appointments by sum, sortby sum_of_appointments

Notes: October 2021 (30,405,070) & November 2011 (30,303,834) recorded the most appointments by month.

Question 4: What is the total number of records per month?

Analysed dataset national_categories.xlsx
1. groupby year & month, aggregate count_of_appointments by count, sortby count_of_records

Notes: March 2022 (82,822) & November 2021 (77,652) had the most number of records.

===========================================================================

# Assignment Activity 4: Visualise & Identify Trends

Objective 1
Create three visualisations indicating the number of appointments per month for service settings, context types, and national categories.

Service Settings (5)
- General Practice makes up over 90% of all appointments.
- General Practice appointments have been increasing over time. Demand was low in August & September 2021. Demand peaked in March 2022.
- An event occurred in December 2021, showing significantly reduced appointments.
- Unmapped appointments reduced significantly over time, indicating more accurate reporting.

Context Types (3)
- Unmapped appointments reduced significantly over time, indicating more accurate reporting.

National Categories (18 values)
- General Consultation Routine & General Consultation Acute are the top 2 categories.
- Top 7 categories make up 97% of total appointments.
- Unmapped category reduced over time, indicating more accurate data reporting.
- Planned Clinics & Planned Clinical Procedure dropped signifantly in December 2021 and rebounded strongly.

Objective 2
Create four visualisations indicating the number of appointments for service setting per season. The seasons are summer (August 2021), autumn (October 2021), winter (January 2022), and spring (April 2022).

August 2021
- Monthly data shows low (close to zero) appointments on Saturday and Sunday.
- Appointments peak on Monday and slows reduce until Friday.
- Overall daily appointments stay under the recognised capacity of 1,200,000 per day.

October 2021
- Saturday appointments showing in the results. Perhaps opened up due to demand and lack of available appointments during the week.
- Weekday appointments show average always above capacity of 1,200,000.

January 2022
- No appointments during the weekend.
- Weekday appointments show average always above capacity of 1,200,000.

April 2022
- No appointments during the weekend.
- Data in the middle of April shows no apointments for a long weekend (Fri to Mon)
- Daily appointments peaking every Monday.
- Weekday appointments show average almost always above capacity of 1,200,000.

Bar chart shows Tuesday is the busiest day, with just over 20% of weekly appointments.

===========================================================================

# Assignment Activity 5: Analyse the Twitter Data

The primary analysis in this section is using the hashtag, tweet retweet and favorite counts.

- Tweet retweet and favorite are similar as they measure the popularity of the original tweet. Further investigation could then be taken to determine the hashtags within the original tweet.
- Hashtags (denoted by the # sign) are used to index words or phrases, which help describe the content contained within the tweet, making it searchable and easy to follow. Tweets can be grouped by hashtags.

Analysis of real-time or historical social media data (including Twitter) can provide valuable information to the stakeholders as a measure of public sentiment towards the NHS services.

Sentiment analysis (emotions, attitudes, opinions, positive/negative) of the NHS services can provide patient feedback which can inform decision-making.

===========================================================================

# Assignment Activity 6: Make Recommendations

Analysis of missed appointments by region illustrates:

1. London has low numbers of GPs per 100000 population and high % of missed appointments.
2. North West high numbers of GPs per 100000 population and high % of missed appointments.
3. The other regions show a positive correlation between % of missed appointments and the sum of appointments.
4. The trend is the longer patients wait between booking the appointment and the actual appointment, increases the chances of that appointment being
missed.
5. London is a hotspot for missed appointments.

Appointment waiting times greater than 1 week can double the probability that the appointment will be missed. Therefore, we can say that efforts should be made to reduce waiting times between booking and appointment date.

Increased demand for acute (emergency, same-day) services may negatively affect planned services.

Key recommendations:
- Healthcare Professional (HCP) types: the data needs to be improved, to include more detail about which type in the "Other Practice Staff" category.
- Actual Duration: the data will be more useful if it can be assiged to a national category and/or HCP type, then we can see how long appointments take relating to the task.
- National category could include the data for missed appointments.
- Target improving the time between booking and appointment. Some appointments will require the longer time gap, but for others a shorter gap may reduce the amount of missed appointments (to less than 1 week).
- Anonymised social media sentiment analysis can be utilised during the busiest periods to identify when staff shortages are effecting patient.

Further analysis of missed appointments should be focused on:
- The usage of resources by national category, compare the ICB locations with high/low number of missed appointments to identify any trends or relationships.
- A more granular look into the Sub-ICB location level may show how the usage of resources can determine outcomes.
- GPs per 100000 population are low in the London region, could there be other staff shortages (e.g., Nurse, Physio) which increase the length of time between booking and appointment date?

===========================================================================

# Final Report



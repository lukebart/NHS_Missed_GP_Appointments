# Bartholomew_Luke_DA201_Assignment
LSE Data Analytics Assignment 2

Assignment Activity 2: Import & Explore the Data

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

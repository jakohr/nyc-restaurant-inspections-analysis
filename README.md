# nyc-restaurant-inspections-analysis

## Project Write-Up

Jack Kohr and Alex Casarella 
Final Project Data Visualization

Question: 

This project explores patterns in New York City restuarant health inspections using demographic data and Tableau dashboards. Our analysis investigates how restuarant inspection outcomes vary depending on geography, income level, cusine type, and season. 

Our interest in this project was sparked by a recent, surprising inspection violation at the critically acclaimed restaurant, Carbone. For reference, Carbone is one of the most exclusive, highly touted restaurants in NYC. Reservations are released thirty days in advance at 10 AM and are typically filled within seconds. Given the massive hype surrounding Carbone, one would expect their food preparation standards and operation safety to be top-notch. However, a recent health inspection revealed that Carbone received a “B” inspection grade from the NYC DOHMH, in addition to a fine for failing to display its letter grade card, which restaurants have been legally required to do for the past 15 years. Health officials found five violations during their inspection, ranging from improper storage of  temperature-controlled food to inadequate cleaning of kitchenware. Furthermore, we discovered that this was not an isolated incident for Carbone as they’ve held the “B” rating since at least 2023. Overall, this report led us to wonder if a high-end restaurant like Carbone could receive subpar inspection ratings, what might the inspection records for other restaurants look like? 

Project Audience: 

Our project and dashboards are intended to be used by NYC consumers, resturant owners, and public health officials. Consumers and NYC residents can use our findings to make more informed and safe dining decision, restuarants owners could use it to benchmark their performance against their peers, and health officials could use it to identify trends across boroguhs, cuisine types, neighborhoods and make decisions accordingly. 

Data Sourcing & Cleaning:

Our main data set was from the NYC Department of Health and Mental Hygiene (DOHMH) on the NYC Open Data portal. The dataset included inspection scores, violations, grades, cuisine types, restuarant locations (boroughs & zipcodes), and longitude & laditude coordinates. The dataset contained approximately 400,000 rows (inspections) and 26 columns (categories), providing a strong foundation for our analysis.

In order to inspect things like inspection scores and violations and how they change depending on cusine type, and the socio-economic status of the neighborhood we brought in an additional dataset sourced from Kaggle which included variables like unemployment rate, crime-rate, and cost of living measures by zipcode. Then finally, to get the most accurate median household income data by zipcode in NYC we integrated another data set from the U.S. Census Bureau American Community Survey API to improve how granularly we could analyze income. 

The raw DOHMH inspections dataset originally had multiple per inspection because each indivual violation was stored on its own. In order to prepare the data to be analyze by score in Tableau, we aggreagated records to the inspection level and removed duplicate inspection entries when it was appropriate. We also had to filter our placeholder inspection dates that were listed as 1/1/1900 that DOHMH had listed for uninspected establishments and potential data entry errors. Additionally, we examined missing values across our key analysis fields like inspection scores, grades, ZIP codes. 

During cleaning we used Python using pandas within a Juypter Notebook to: 
- Turn inspection dates into proper datetime format for time-series analysis
- Standardized ZIP code formatting to make sure they were consistent across data sets for joins
- Removed duplicate ZIP-code entries from our demogrpahic dataset before merging
- Made sure to keep latitude and longitude variables so we could do mapping visualizations in Tableau
- Checked missing grades and inspection scroes to see if they represented pending inspections or incomplete inspections
- Checked borough, cuisine, and inspection score distributions to see if there were anomolies

One challenge that we had during our analysis was that the original demographic data set sourced from Kaggle, that we left joined into the inspection data set on ZIP code, only provided median income information aggregated by borough. So when initially building our dashboards with that merged data we were only able to evaluate on the borough level as each ZIP code within the same borough incorrectly had the same median income attached to it. That's why we ended up brining in the Census ACS API to adress this as it allowed us to get unique median household income estimates for every ZIP code. We then merged those values into the final dataset using ZIP code as the join key. The remaining other demographic variables from the Kaggle dataset rwere retained in the final merged dataset, just this time the median household income data was by ZIP code. 

Use of LLMs/Chat GPT: 



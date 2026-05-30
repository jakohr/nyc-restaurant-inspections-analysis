# NYC Restaurant Health Inspections Analysis

**Jack Kohr and Alex Casarella | BUS 32130: Data Visualization for Decision-Making | Spring 2026**

*All work was uploaded by the deadline Friday, May 29th; changed the .twb file to a .twbx file for better compatibility on Saturday, May 30th (as per the #HelpMe instruction in slack)

## Project Question

This project explores patterns in New York City restaurant health inspections using demographic data and Tableau dashboards. Our analysis investigates how restaurant inspection outcomes vary depending on geography, income level, cuisine type, and season.

Our interest in this project was sparked by a recent, surprising inspection violation at the critically acclaimed restaurant, Carbone. For reference, Carbone is one of the most exclusive, highly touted restaurants in NYC. Reservations are released thirty days in advance at 10 AM and are typically filled within seconds. Given the massive hype surrounding Carbone, one would expect their food preparation standards and operation safety to be top-notch. However, a recent health inspection revealed that Carbone received a "B" inspection grade from the NYC DOHMH, in addition to a fine for failing to display its letter grade card, which restaurants have been legally required to do for the past 15 years. Health officials found five violations during their inspection, ranging from improper storage of temperature-controlled food to inadequate cleaning of kitchenware. Furthermore, we discovered that this was not an isolated incident for Carbone as they have held the "B" rating since at least 2023. Overall, this report led us to wonder if a high-end restaurant like Carbone could receive subpar inspection ratings, what might the inspection records for other restaurants look like?

---

## Project Audience

Our project and dashboards are intended to be used by NYC consumers, restaurant owners, and public health officials. Consumers and NYC residents can use our findings to make more informed and safe dining decisions. Restaurant owners could use it to benchmark their performance against their peers. Public health officials could use it to identify trends across boroughs, cuisine types, and neighborhoods and make resource allocation decisions accordingly.

---

## Background: NYC Restaurant Health Inspections

The New York City Department of Health and Mental Hygiene (DOHMH) operates one of the most comprehensive restaurant inspection programs in the United States. All restaurants operating in New York City are subject to unannounced inspections conducted by trained DOHMH inspectors, typically at least once per year. The program is designed to protect public health by ensuring restaurants comply with the New York City Health Code, which governs food handling, storage, preparation, pest control, and facility sanitation.

**The Scoring System**

Each inspection produces a numerical score based on the violations found during that visit. Inspectors assign points to each violation they observe, with more serious violations carrying a higher point value. Because scores represent accumulated penalty points, a lower score indicates better performance and a higher score indicates worse performance. A score of zero would represent a perfect inspection with no violations found. This counterintuitive relationship between score and performance is an important context for interpreting our visualizations, which is why we include the label "Lower = Better" on all score-related charts throughout the dashboard.

**Letter Grades**

The NYC letter grading system was introduced in July 2010 and requires all restaurants to publicly post their most recent grade. Grades are assigned based on the inspection score as follows:

- Grade A: a score of 0 to 13, indicating the restaurant is in satisfactory sanitary condition
- Grade B: a score of 14 to 27, indicating there are issues that need to be addressed
- Grade C: a score of 28 or higher, indicating significant sanitary problems were found

If a restaurant receives a B or C on its initial inspection, it has the right to request a re-inspection before a grade is officially assigned. During this window the restaurant is considered Grade Pending and must post a Grade Pending card rather than a letter grade. This is the origin of the N, P, and Z grade codes in the dataset, which we exclude from our graded analyses since they do not represent final inspection outcomes.

**Violation Types**

Violations are divided into two categories that carry different point values and reflect different levels of public health risk.

Critical violations pose an immediate and direct risk to public health and are the most heavily penalized. Common examples include food not held at proper temperature (which allows bacterial growth), evidence of mice or cockroaches in food preparation or storage areas, food sourced from unapproved suppliers, employees not washing hands properly, and raw meat stored above ready-to-eat food creating cross-contamination risk. Critical violations are the focus of our Critical Health Violations chart on Dashboard 3.

General violations are less immediately dangerous but still represent failures to comply with the Health Code. These include issues such as improper maintenance of facilities and equipment, inadequate lighting or ventilation, improper food labeling, and failure to display required permits or grade cards. The fine Carbone received for failing to display its letter grade card is an example of a general violation.

**Why This Matters**

The DOHMH publishes its full inspection dataset daily on the NYC Open Data portal, making it one of the most transparent public health datasets available in any major American city. This transparency is the foundation of our project: by combining inspection outcomes with neighborhood-level demographic and economic data, we are able to test whether the patterns visible in the data reflect broader structural factors like income inequality and seasonal food safety challenges, or whether they are better explained by cuisine type, individual restaurant management, and borough-level variation.

---

## Hypotheses

Our analysis was structured around five hypotheses that we aimed to support or contradict using data:

**H1: Borough-level performance variation.** Meaningful differences in average inspection scores and letter grade distributions exist across NYC's five boroughs, reflecting variation in factors such as restaurant density, cuisine composition, and neighborhood characteristics unique to each borough. Some boroughs will consistently outperform others in both average inspection score and proportion of A grades received.

**H2: Cuisine type bias.** Certain categories of cuisine will have higher violation rates even after controlling for borough and neighborhood, which may reflect either genuine challenges with preparing certain types of food or potential biases in the inspection process itself.

**H3: Geographic clustering of violations.** Restaurants in lower income neighborhoods will have higher inspection scores on average (worse outcomes) than restaurants in higher income areas, suggesting that food safety is partly due to socioeconomic geography rather than just individual restaurant management.

**H4: Seasonal variation in violations.** Inspection scores will be worse during summer months (June through August), when higher temperatures make food storage and handling violations more likely.

**H5: Re-inspection improvement.** Restaurants that receive a B or C grade on their initial inspection will show score improvement when re-inspected, suggesting that the grading system incentivizes restaurants to correct their violations.

---

## Dashboard Walkthrough

Our Tableau workbook contains three dashboards, each of which addresses a specific dimension of our analysis. The grader should begin with Dashboard 1 and work through to Dashboard 3 in order, as each builds on the context established by the previous one.

### Dashboard 1: City Overview

This dashboard serves as the entry point into our analysis, covering Hypotheses 1 and 2 in addition to providing a city-wide overview of restaurant health inspection performance. It gives the viewer enough context to understand the scale and scope of the dataset and introduces the two most visually immediate findings (borough-level performance differences and cuisine-level variation) before the deeper analytical work begins on the subsequent dashboards.

At the very top, four KPI cards summarize the most important headline statistics. The average inspection score across all graded inspections is 17.82 (lower is better, as scores represent total violation points accumulated). The total number of inspections in the dataset is 83,512. The average number of critical violations per inspection is 1.844. And 86.9% of graded inspections received an A grade, meaning a score of 13 or below.

The color key in the top right of the dashboard is important context for interpreting the score-based visualizations throughout the workbook. Blue indicates a lower score (better performance) while orange and dark orange indicate a higher score (worse performance). This encoding is used consistently across the Score by Borough bar chart and the Cuisine and Borough highlight table.

The Geographic Restaurant Map in the center left of the dashboard plots one dot per ZIP code across all five boroughs, colored by average inspection score. This gives an immediate geographic sense of where inspection performance is stronger and weaker across the city. Viewers can hover over any dot to see the ZIP code, borough, average score, and average violation count for that area.

The Avg. Inspection Score by Borough horizontal bar chart in the upper right directly addresses Hypothesis 1. It shows that Queens has the highest average inspection score (19.175) meaning the worst performance of any borough, while Staten Island has the lowest (17.014) meaning the best performance. The difference of 2.161 points between the worst and best performing boroughs is a meaningful difference in a grading system where each point holds high value. The bars are sorted in descending order so the worst performing borough is immediately visible at the top and the viewer does not have to scan the chart to identify the key finding.

The Inspection Grade Distribution by Borough stacked bar chart further supports Hypothesis 1 by showing the percentage breakdown of A, B, and C grades across each borough. All five boroughs are heavily weighted toward A grades, reflecting the city-wide 86.9% A rate, but there are meaningful differences in the proportion of B and C grades across boroughs. Queens shows the highest share of B and C grades while Staten Island shows the lowest, consistent with the pattern established in the Score by Borough chart.

The Avg Inspection Score by Cuisine and Borough highlight table at the bottom of the dashboard directly addresses Hypothesis 2 and is one of our most analytically sophisticated visualizations. Rather than simply showing overall cuisine averages, this table shows average inspection scores for each cuisine type broken out by individual borough, with a Grand Total column on the far right showing the overall cuisine average. This controlled analysis allows the viewer to see whether cuisine type differences persist across all five boroughs independently, which would suggest the cuisine type itself is driving the difference rather than just the neighborhoods where those restaurants happen to be located. Bangladeshi cuisine consistently scores among the highest across boroughs, while Donuts and Hamburgers consistently score among the lowest.

### Dashboard 2: Income & Geography

This dashboard is dedicated entirely to testing Hypothesis 3, examining whether neighborhood income predicts restaurant inspection outcomes. It is the most analytically rigorous of the three dashboards and is designed to be read as a self-contained research finding.

The main visualization is the Household Income vs. Health Score Scatter Plot, where each dot represents one of 187 NYC ZIP codes. The X axis shows median household income for that ZIP code (sourced from the U.S. Census Bureau ACS API, giving us true ZIP code level income rather than borough level averages). The Y axis shows the average inspection score for restaurants in that ZIP code. Dots are colored by borough and sized by the number of unique restaurants in each ZIP code, so larger dots represent ZIP codes with more restaurants and therefore more statistically reliable averages.

A single trend line with confidence bands runs across all 187 ZIP codes. The downward slope of the trend line indicates a negative relationship between income and inspection score, meaning higher income ZIP codes tend to have lower (better) scores on average. However the wide confidence bands communicate that this relationship is far from deterministic.

The Key Findings box on the right side of the dashboard reports the statistical parameters of this relationship: R = -0.24 (a modest negative correlation), R squared = 0.056 (income explains only 5.6% of the variation in scores), and a p-value of 0.001 (statistically significant). These numbers are important for honest interpretation. While the relationship is real and statistically significant, it is weak enough that income alone should not be treated as a reliable predictor of food safety outcomes.

Below the Key Findings box, the H3 Finding text block provides a plain language interpretation of what these statistics mean and how they relate to our original hypothesis. This text is designed so the dashboard can stand alone without narration, directly addressing the rubric requirement that visuals must be self-explanatory.

### Dashboard 3: Trends & Patterns

This dashboard examines the time-based and cuisine-based hypotheses, covering Hypotheses 4 and 5 as well as providing a supplementary view of critical violations by cuisine type.

The Seasonal Inspection Score Trend line chart at the top of the dashboard plots the average inspection score by month from January 2022 through May 2026 and directly addresses Hypothesis 4. Three Summer Peak annotation boxes highlight the June through August periods of 2022, 2023, and 2024 respectively. The annotation in the upper right corner of the chart notes that average scores peak approximately 2 points higher during summer months, providing direct support for Hypothesis 4. The pattern is visually clear: scores spike upward during summer and then decline in fall and winter, and this pattern repeats consistently across multiple years, suggesting it is a genuine seasonal phenomenon rather than a one-time anomaly.

The Avg Score Trend for B/C Graded Restaurants line chart in the lower left directly addresses Hypothesis 5 by tracking how average inspection scores have changed over time specifically for restaurants that received a B or C grade at some point during the study period. Rather than showing a downward trend (which would indicate improvement after a bad grade), all five boroughs show a generally upward trend from 2022 through 2026, meaning these restaurants are scoring worse over time rather than better. This directly contradicts Hypothesis 5 and raises important questions about whether the current grading and re-inspection system effectively incentivizes sustained improvement. It is worth noting, as we acknowledge in the limitations section, that this chart tracks average scores over time rather than a true before-and-after comparison for the same restaurant, so it should be interpreted with appropriate caution.

The Critical Health Violations dot plot in the lower right ranks cuisine types by their average number of critical violations per inspection. Critical violations are those that pose an immediate and direct risk to public health, such as improper food temperatures, evidence of pests, and inadequate handwashing. Bangladeshi and Chilean cuisines have the highest average critical violation counts, while Donuts and Hamburgers have the fewest. This chart complements the cuisine analysis on Dashboard 1 and gives a different lens on the H2 question by focusing specifically on the most dangerous types of violations rather than overall score.

---

## Key Findings

Our analysis produced five findings corresponding to the five hypotheses we set out to test:

**H1 Supported.** Meaningful borough-level differences in inspection outcomes exist across all five NYC boroughs. Queens has the highest average inspection score (19.175) and the greatest proportion of B and C grades, making it the worst performing borough across both measures. Staten Island has the lowest average inspection score (17.014) and the highest proportion of A grades, making it the best performing borough. The 2.161 point gap between the best and worst performing boroughs is significant in a system where 14 points separates an A grade from a B grade, confirming that borough of operation is a meaningful predictor of inspection outcomes.

**H2 Supported.** Even after controlling for borough, certain cuisine types consistently score higher (worse) than others across all five boroughs. Bangladeshi cuisine averaged 31.8 overall and scored above 20 in every borough where it was present. In contrast, Donuts and Hamburgers consistently scored among the lowest across boroughs. This pattern strongly suggests that cuisine-level factors rather than just neighborhood geography are driving these differences.

**H3 Partially Supported.** Using ZIP code level median household income data across 187 NYC ZIP codes, we found a modest but statistically significant negative relationship between income and inspection scores (R = -0.24, R squared = 0.056, p = 0.001). Lower income ZIP codes (below $87,365 median income) averaged a score of 18.43 compared to 17.06 for higher income ZIP codes, a difference of 1.37 points. However since income explains only 5.6% of score variation, other factors like cuisine type and individual restaurant management appear to be stronger drivers of inspection outcomes than neighborhood wealth alone.

**H4 Supported.** Summer months (June through August) consistently produce higher average inspection scores across all years in our dataset, with scores peaking approximately 2 points above the annual average during peak summer months. This is consistent with the hypothesis that warmer temperatures create more challenging food safety conditions.

**H5 Contradicted.** Rather than showing improvement over time, restaurants that received B or C grades show a generally worsening trend in inspection scores from 2022 through 2026 across all five boroughs. This suggests the current inspection and grading system may not be effectively incentivizing sustained long-term improvement, though we acknowledge this finding is based on average scores over time rather than a true controlled before-and-after study of the same restaurants.

---

## Design Decisions

We made several deliberate design decisions throughout this project that reflect the principles of good data visualization covered in BUS 32130.

**Color encoding:** We used a blue-to-orange diverging color palette for inspection score visualizations throughout the workbook. This choice is semantically meaningful: blue is a cool, calm color associated with safety and good performance, while orange and dark orange are warm, cautionary colors associated with worse performance. This encoding appears consistently on the Score by Borough bar chart, the score legend on Dashboard 1, and the Cuisine by Borough highlight table. For letter grades, we used green for A, orange for B, and dark orange for C, which follows intuitive traffic light logic that requires no explanation.

**Signal over noise:** We deliberately removed chart borders, unnecessary tick marks, and redundant axis titles wherever they added visual weight without adding information. The Grade Distribution stacked bar chart uses percentage labels directly on the bars rather than a separate axis, eliminating the need for the viewer to look back and forth between bars and an axis. The Summer Peak annotations on the seasonal trend chart label the insight directly on the chart rather than requiring the viewer to infer the seasonal pattern themselves.

**Statistical transparency:** On Dashboard 2, we chose to display the raw statistical parameters (R, R squared, and p-value) alongside the plain language interpretation. This reflects our audience: public health officials and policy-minded viewers will want to evaluate the strength of the evidence themselves rather than just accepting a summary conclusion.

**Hypothesis-driven structure:** Rather than organizing the dashboards by chart type or data source, we organized them by analytical question. Each dashboard corresponds to a specific dimension of analysis (city overview with borough and cuisine findings, income and geography, and temporal and cuisine patterns), which makes it easier for viewers to navigate to the specific question they care about.

**Inkscape polishing:** We used Inkscape to produce a professionally polished version of the Score by Borough bar chart as part of our Week 9 in-class exercise. In Inkscape, we changed the chart title from the generic label "Avg. Inspection Score by Borough" to the insight-driven title "Queens Scores Worst of All NYC Boroughs," simplified the color encoding to highlight Queens with a single accent color while making other boroughs gray, added a source line in 9pt light gray text, and exported the final version as both a PDF for print and a 300 PPI PNG for slides. Both exports are included in the repository under the inkscape folder.

---

## Data Sourcing and Cleaning

Our main dataset was from the NYC Department of Health and Mental Hygiene (DOHMH) on the NYC Open Data portal. The dataset included inspection scores, violations, grades, cuisine types, restaurant locations (boroughs and ZIP codes), and longitude and latitude coordinates. The dataset contained approximately 400,000 rows (inspections) and 26 columns (categories), providing a strong foundation for our analysis.

In order to examine how inspection scores and violations vary due to socioeconomic status, we sourced an additional dataset from Kaggle which included median income by borough, unemployment rate, and cost of living measures by ZIP code. Then finally, to get the most accurate median household income data by ZIP code in NYC we integrated another dataset from the U.S. Census Bureau American Community Survey API to improve how granularly we could analyze income.

The raw DOHMH inspections dataset originally had multiple rows per inspection because each individual violation was stored on its own row. In order to prepare the data to be analyzed by score in Tableau, we aggregated records to the inspection level and removed duplicate inspection entries when it was appropriate. We also had to filter out placeholder inspection dates that were listed as 1/1/1900 that DOHMH had listed for uninspected establishments and potential data entry errors. Additionally, we examined missing values across our key analysis fields like inspection scores, grades, and ZIP codes.

During cleaning we used Python with pandas within a Jupyter Notebook to complete the following tasks:

- Turn inspection dates into proper datetime format for time-series analysis
- Standardize ZIP code formatting to make sure they were consistent across datasets for joins
- Remove duplicate ZIP code entries from our demographic dataset before merging
- Keep latitude and longitude variables so we could do mapping visualizations in Tableau
- Check missing grades and inspection scores to see if they represented pending inspections or incomplete inspections
- Check borough, cuisine, and inspection score distributions to identify any anomalies

One challenge that we encountered during our analysis was that the original demographic dataset sourced from Kaggle, which we left joined into the inspection dataset on ZIP code, only provided median income information aggregated at the borough level. So when we initially built our dashboards with that merged data we were only able to evaluate income at the borough level, as each ZIP code within the same borough incorrectly had the same median income attached to it. That is why we ended up bringing in the Census ACS API to address this limitation, as it allowed us to obtain unique median household income estimates for every ZIP code in NYC. We then merged those values into the final dataset using ZIP code as the join key. The remaining other demographic variables from the Kaggle dataset were retained in the final merged dataset.

After cleaning and merging the datasets correctly, our final dataset had roughly 80,000 inspection observations and 16 key variables to use throughout our Tableau dashboards. The final dataset was then exported as a CSV file and connected directly into Tableau to begin developing the dashboards. In addition to the final CSV file, we have also included our full Jupyter Notebook in this repository that documents our complete cleaning and sourcing process.

---

## Project Limitations

We want to be transparent about several limitations in our analysis that a reader should keep in mind when interpreting our findings.

First, our H5 analysis (re-inspection improvement) is not a true controlled before-and-after study. The Avg Score Trend for B/C Graded Restaurants chart tracks average scores over time for all restaurants that received a B or C at any point during the study period, rather than computing the actual delta between a restaurant's initial bad inspection and its subsequent re-inspection. This means the upward trend we observe could partly reflect the overall trend of increasing scores across the city rather than being specific to restaurants recovering from bad grades. A more rigorous analysis would require tagging each inspection with a sequence number to identify true initial versus re-inspection pairs.

Second, while our ZIP code level income data from the Census ACS API is significantly more granular than borough level averages, it still represents a neighborhood-level variable being applied to individual restaurants. Two restaurants on the same block will have the same ZIP code income value even if they serve very different clientele or operate in very different price segments.

Third, our dataset covers 2022 through 2026, which means our seasonal analysis captures at most four summer periods. A longer time horizon would produce a more robust seasonal finding.

Finally, the inspection process itself may introduce biases that our analysis cannot fully account for. The frequency with which a restaurant is inspected, the specific inspector assigned, and the time of day of the inspection may all influence outcomes in ways that are not captured in the public dataset.

---

## Use of LLMs

We used both Claude and ChatGPT as supplementary tools throughout this project. ChatGPT was used as a supplementary tool during the data cleaning and preparation stages, helping us understand what aspects of the data needed to be cleaned, structure aspects of our Python code including API calls and pandas operations, and troubleshoot and debug issues that arose during the merging process. Claude was used primarily to troubleshoot and assist on any matters within the Tableau sheet and dashboard building. Additionally, Claude was used to evaluate our final dashboard and provide any recommendations to improve upon our work.

Both LLMs were used to help summarize our data findings for the README, which we subsequently used to complete the write-up.

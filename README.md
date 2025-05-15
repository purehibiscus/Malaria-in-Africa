# Malaria-in-Africa-Project
This repo contains all files concerning Malaria in Africa project

Project Report on Malaria in Africa



Dashboard download link: https://drive.google.com/file/d/15l6741sUKC8zOvHhSdQb2g7SLGykAlOX/view?usp=sharing

Title: Analyzing Malaria disease in Africa for Insights into Disease Burden, Treatment Access, Bed-nets usage, 

Introduction:
Malaria is a common disease in Africa. The disease is transmitted to humans through infected mosquito bites. Although you can take preventive measures against malaria, it can be life-threatening. This dataset includes the malaria cases in African countries, the incidence at risk, and data on preventive treatments against malaria.

About the dataset:
This dataset includes data on all African countries from 2007 till 2017. Each country has a unique ISO-3 country code, and the dataset includes the latitude and longitude point of each country as well. The dataset includes the cases of malaria that have been reported in each country and each year, as well as data on preventive measures that have been taken to prevent malaria. This project aimed to explore African health indicators, focusing on disease burden, healthcare access, usage treated bed-nets, access to safe water and sanitation services, using data from Kaggle public repository to ascertain out trends, patterns and insights from the dataset having 27 columns(20 decimal columns, 3 string columns, 2 integer columns and 2 other columns having location geometries) and 594 entries.

The incidence of malaria is a variable that counts the number of malaria cases per 1000 people in areas where malaria transmission occurs. The malaria cases reported include the number of malaria cases that have been confirmed by examination. In addition, the dataset includes preventive measures that have been taken to prevent malaria, such as the use of insecticide-treated bed nets, the percentage of children with fever receiving antimalarial medication, and the percentage of pregnant women receiving preventive treatment.


All data workflows is done using MS Power BI

A. Data Preparation and Cleaning:
Data validation, Profiling, Inconsistencies, Misspellings, Distribution, Duplicates is done using MS Power BI Power Query:

i. Data Validation:
Data types are checked and assigned the appropriate format(e.g. all numerical columns are found as text, which were highlighted by selecting the first column(Incidence of malaria (per 1,000 population at risk)) and holding CTRL+Shift keys and selecting the last column(People using at least basic sanitation services, urban  (% of urban population)), then they were converted to the appropriate data types. The date column was also been changed from text to Date in Power Query and then to Date(Year) format using DAX as the column have no specific Month nor Day.

ii. Data Profiling:

Numerical columns: Data Integrity, distribution and Column Statistics, checks for Minimum, Maximum, Average, Count, and Standard deviation of each numerical columns, values for all numerical columns, Checks for Unique and Distinct values, Error, and Value distribution were done with Microsoft Power BI Power Query's Data Preview tool from the View tab. Column quality is approximated at 70%, null values at 20% and Zeros at 10%. No duplicate in key fields. All Distinct values(Country) have not less than 9 entries ranging from 2007 to 2017.

Categorical Columns: Unique and Distinct values are checked to ensure there is no whitespaces, misspelt words, trailing spaces, and duplicates to ensure consistency. Column statistics is done with the Power Query View tools to ensure proper data distribution, this helped in ensuring there is no data out of normal range or that can be an anomaly, outlier or any value out of context. 

The Country code, Latitude, Longitude and Geometry columns are dropped using the "remove columns" option in Power Query. The columns have no relation to cause any data integrity problems at the time of analysis and even though we're conducting a geospatial analysis, we won't be needing these fields as we would be using the "Country" column as another column with spatial information and those dropped columns would not contribute to our Research questions.


Data Source and Attributes:
Data Source: Kaggle public datasets through: World Bank Open Data Source

Collection Methodology
Data has been retrieved from the World Bank Open Data Source. Geospatial concepts such as longitude and latitude have been collected manually. I transformed it into an understandable dataset with a time frame spanning over 10 years.

Dataset Columns and their attributes:
1.  Country Name: African Countries
2.  Year: Year in range 2007 till 2017
3.  Country Code: ISO-3 code for country or 3-digit code
4.  Incidence of Malaria(per 1000 people at risk): Number of cases per 1000 people in areas where malaria transmission occurs
5.  Malaria cases reported: Number of cases that were reported in certain year
6.  Use of insecticide-treated bed nets (% of under-5 population): Percentage of insecticide treated mosquito nets that are used
7.  Children with fever receiving antimalarial drugs (% of children under age 5 with fever): Percentage of children under 5 with fever that get medication against malaria
8.  Intermittent preventive treatment (IPT) of malaria in pregnancy (% of pregnant women): Percentage of pregnant women that receive preventive treatment against malaria
9.  People using safely managed drinking water services (% of population): Percentage of population using drinking water from improved source
10. People using safely managed drinking water services, rural (% of rural population): People in rural areas that use drinking water from improved source
11. People using safely managed drinking water services, urban (% of urban population): People in urban areas that use drinking water from improved source
12. People using safely managed sanitation services (% of population)
13. People using safely managed sanitation services, rural (% of rural population)
14. People using safely managed sanitation services, urban  (% of urban population)
15. Rural population (% of total population)
16. Rural population growth (annual %)
17. Urban population (% of total population)
18. Urban population growth (annual %)
19. People using at least basic drinking water services (% of population)
20. People using at least basic drinking water services, rural (% of rural population)
21. People using at least basic drinking water services, urban (% of urban population)
22. People using at least basic sanitation services (% of population)
23. People using at least basic sanitation services, rural (% of rural population)
24. People using at least basic sanitation services, urban  (% of urban population)
25. Latitude
26. Longitude
27. Geometry


Data Analysis:
Research Questions:

1. What is the trend of malaria incidence over time?
2. Which countries have the highest/lowest malaria incidence?
 - Top 10 countries with highest malaria incidence Rate
3. Is there a relationship between malaria incidence and use of treated bed-nets?
4. Is there a relationship between malaria incidence and access to peak safe water?
5. How does access to safely managed drinking water and sanitation services affect malaria incidence?
6. Are there any relationship between the usage of treated bed-nets, malaria incidence across Countries?
7. Are there any differences in malaria incidence between rural and urban populations?

Data Analysis Methodology:
Power Query and DAX functions are used to calculate the variables.

Power Query is used to drop columns that are not needed for analysis, and addressing data type errors to the appropriate format.

DAX formulas used:
Calendar table is created using the Calendar function "CALENDARTABLE" to create a table consisting the MIN date and MAX date for Business Intelligence Analysis.
All KPIs and calculations used for charts creation for specific questions were calculated using DAX functions from functions like (SUM, AVERAGE, COUNTROWS, TOPN, MAXX, FORMAT, FILTER) to mention a few.

Some calculations can be seen as:

1. for creating calendar table
CalendarTable = 
ADDCOLUMNS(
    CALENDAR(
        MIN('Malaria in Africa'[Year]),
        MAX('Malaria in Africa'[Year])
    ),
    "Year", YEAR([Date])
)

2. Calculating the rate for Children with Fever receiving anti-malaria drugs
Anti-MalariaTreatmentRate = AVERAGE('Malaria in Africa'[Children with fever receiving antimalarial drugs (% of children under age 5 with fever)])

3. Counting all records from the dataset
TotalRecords = COUNTROWS('Malaria in Africa')

4. Calculating all people in the rural area
TotalRuralPopulation = SUM('Malaria in Africa'[Rural population (% of total population)])

5. Calculating the Year with highest reports
TopYearwithHighestReports = 
FORMAT(
    MAXX(
        TOPN(
            1,
            'Malaria in Africa',
             'Malaria in Africa'[Malaria cases reported],
              DESC
              ),
              'Malaria in Africa'[Year]
    ),
    "YYYY"
)

6. Calculating the Country Name with most affected people
TopCountryAffectedName = 
MAXX(
    TOPN(
        1,
        'Malaria in Africa',
        'Malaria in Africa'[Malaria cases reported],
        DESC
    ),
    'Malaria in Africa'[Country Name]
)


Visualizations and Reports:

Dashboard Overview page 1
1. Malaria Incidence Rate (per 1,000 population at risk) by Year: Area chart
2. Annual Use of Treated bed-nets and Malaria Incidence Rate: Line and Stacked Column chart
3. Top 10 Countries by Malaria Incidence Rate: Stacked Bar chart
4. Annual Peak Safe Water Access and Malaria Incidence: Line and Stacked Column chart

Dashboard Drilldown page 2
5. Malaria Incidence vs. Bed-Net Usage by Country: Stacked Area chart
6. Access to Safe Water and Sanitation Services: Stacked Bar char
7. Annual Malaria Incidence between Rural and Urban Populations by Growth rate: Line chart
8. Malaria Incidence and Population Growth: Scatter chart

KPIs cards
1. Total Malaria cases Reported(Million)
2. Average Malaria Incidence per 1000 Rate(K)
3. Bed-Net Usage Rate(%)
4. Anti-malaria treatment rate(%)
5. Access to Safe Water Rate(%)
6. Access to Sanitation Services Rate(%)
7. Rural Growth Rate(%)
8. Urban Growth Rate(%)
9. IPT for Pregnant Women Rate(%)
10. Top Year with Highest Reports('YYYY')
11. Top Country Affected Name

Dashboard Page Navigation:
The dashboard pages are interactive, allowing users to navigate by selecting elements such as Country names, Year, or their corresponding bars in the charts. A slicer has been added to the first page, providing dropdown options for both Country name and Year. An information icon on Page 1 allows users to navigate to Page 2, while a back icon on Page 2 returns users to Page 1. These icons have been configured using the Action feature in the icon formatting pane. On some systems, holding the Ctrl key may be required when clicking the icons.
Slicer and filter options are configured to apply across both pages using the Show Panes group under the View tab. Additionally, features such as Drill-through, Cross-report, and Apply all filters have been enabled to improve dashboard navigation and provide more comprehensive insights.


Insights and Findings:
1. Malaria cases across Africa significantly declined between 2007 and 2013, largely due to increased usage of insecticide-treated bed nets, and improved access to clean water and sanitation facilities.
2. The top 10 countries with the highest malaria incidence are likely suffering from inadequate access to treated bed nets and limited water and sanitation services. A noticeable drop in reported cases for these countries starts around 2016.
3. The availability of clean water, sanitation, and treated nets greatly influenced malaria incidence trends from 2007 to 2015. However, starting in 2016, some countries began experiencing a resurgence in cases, likely due to reduced infrastructure investment or maintenance.
4. The average population growth rate is higher in rural areas (56%) compared to urban areas (43%). This disparity contributes to rising malaria incidence in rural areas, which generally face greater challenges accessing clean water and sanitation.
5. Increasing population correlates with higher malaria incidence, especially in rural regions with growth rates as high as 60%, compared to urban areas with 43%.



Recommendations:
1. Strengthening Rural Infrastructure, Prioritizing the expansion and maintenance of water, sanitation, and hygiene (WASH) infrastructure in rural areas, where population growth and disease risk are highest.
2. Ensuring continued and equitable distribution of insecticide-treated bed nets, especially in high-risk and underserved regions.
3. Designing targeted intervention programs for the top 10 high-incidence countries, focusing on community education, improved health facilities, and environmental control.
4. Use population growth trends to forecast malaria risk zones, enabling proactive planning and resource allocation.
5. Regularly assess the impact of interventions using up-to-date data to ensure timely adjustments and to avoid regression as observed post-2015. This would help for data-driven Intervention reviews.



Conclusions:

The analysis underscores that sustained access to clean water, improved sanitation, and widespread use of insecticide-treated bed nets were critical factors in the sharp decline of malaria cases across Africa between 2007 and 2013. However, the resurgence of cases in some regions after 2015—especially in the top 10 high-incidence countries—highlights the urgent need for renewed, consistent investment in health infrastructure. Re-establishing or expanding targeted intervention programs in these high-risk areas can play a vital role in reducing malaria cases and improving public health outcomes continent-wide. Additionally, rapid population growth in rural regions with limited access to healthcare and sanitation further exacerbates the disease burden. Proactive and sustained efforts, guided by data-driven strategies, are essential to mitigate these challenges effectively. 

To effectively combat malaria, a strategic focus on reinforcing rural health infrastructure, maintaining preventive measures, and deploying targeted, data-informed interventions is essential. These actions will not only reduce current incidence rates but also build resilience against future outbreaks.

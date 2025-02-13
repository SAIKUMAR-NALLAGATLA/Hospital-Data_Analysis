# Hospital Data Analysis

This Power BI dashboard provides an in-depth analysis of hospital wait lists, segmented by age profile, case type, and specialty. It offers interactive insights into patient wait times and trends, helping stakeholders make informed decisions.

## Overview

The Hospital Data Dashboard analyzes patient wait lists from January 2018 to March 2021. It provides:
- Key indicators: Latest and previous year’s wait list metrics.
- Time Band vs. Age Profile analysis.
- Case Type distribution (Outpatient, Day Case, Inpatient).
- Monthly trend analysis for each case type.
- Detailed view with dynamic filtering options.

## Key Features

- **Interactive Filters:** Archive Date, Case Type, Specialty, Age Profile, and Time Bands for customized analysis.
- **Dynamic Titles and Metrics:** Titles and key metrics dynamically change based on selected calculation methods (Average or Median).
- **Insightful Visualizations:** Bar charts, pie charts, and line graphs for comprehensive data interpretation.

## DAX Functions Used
```DAX
// Average and Median Calculations
AVG Waiting List = AVERAGE(Hospital_Data[Total])
Median Waiting List = MEDIAN(Hospital_Data[Total])

// Dynamic Calculation Method
Avg/Med Wait List = SWITCH(VALUES('Calculation Method'[Calc Method]),
                          "Average", [AVG Waiting List],
                          "Median", [Median Waiting List])

// Dynamic Title
Dynamic title = SWITCH(VALUES('Calculation Method'[Calc Method]),
                       "Average", "Key Indicators - Patient Wait List (Average)",
                       "Median", "Key Indicators - Patient Wait List (Median)")

// Wait List Metrics
Latest Month Wait List = CALCULATE(SUM(Hospital_Data[Total]),
                                  Hospital_Data[Archive_Date] = MAX(Hospital_Data[Archive_Date])) + 0

PY Latest Month Wait list = CALCULATE(SUM(Hospital_Data[Total]),
                                      Hospital_Data[Archive_Date] = EDATE(MAX(Hospital_Data[Archive_Date]),-12)) + 0

// No Data Messages
No Data left = IF(ISBLANK(CALCULATE(SUM(Hospital_Data[Total]),
                                    Hospital_Data[Case_Type] <> "Out patient")),
                  "No Data for Selected Criteria", "")

No Data right = IF(ISBLANK(CALCULATE(SUM(Hospital_Data[Total]),
                                     Hospital_Data[Case_Type] = "Out patient")),
                   "No Data for Selected Criteria", "")
```
## Insights and Observations
- Significant wait times observed for certain age profiles, particularly in the 18+ category.
- Outpatient wait lists show an increasing trend, whereas Day Case and Inpatient lists exhibit fluctuations.
- ENT, Orthopaedics, and Dermatology have the highest wait lists by specialty.

## File Structure
  Hospital-Data_Analysis/
│   README.md
│   requirements.txt
│   Hospital_Analysis.pbix
└───Images/
        Dashboard_Overview.png
        Detailed_View.png
## Requirements
- Power BI Desktop
- Data Source: Hospital wait list data from 2018 to 2021.

## Conclusion
This Power BI dashboard effectively visualizes hospital wait list trends and distributions, aiding healthcare administrators in resource allocation and decision-making.

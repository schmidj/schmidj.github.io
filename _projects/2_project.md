---
layout: page
title: Air Passenger Analysis
description: "Tools: <b>Power BI, Python</b>"
img: assets/img/Project_Air_Passengers.png
importance: 2
category: self-learning
giscus_comments: true
---

## 1. Project overview

This project explores global air passenger trends using [World Bank data](https://data.worldbank.org/indicator/IS.AIR.PSGR?end=2021&start=1970&view=chart) and visualizes key insights in an interactive Power BI dashboard.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Screenshot_Dashboard_AirPassengers.png" title="Dashboard example" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An example screenshot of the dashboard.
</div>

It consists of two main components:

`eda_preprocessing_powerbi.ipynb`: A Jupyter Notebook for exploratory data analysis (EDA) and preprocessing.

`Air_Passengers.pbix`: A Power BI Desktop report built on the cleaned dataset, including timeline, bar charts, and a geographic map.

## 2. Concept Overview
Python: EDA
Power Query, DAX, Filtering in Power BI...

## 3. Data Overview & Preparation

All raw data comes from the World Bank Open Data indicator:

Air transport, passengers carried (IS.AIR.PSGR), 
International Civil Aviation Organization (ICAO),
[https://data.worldbank.org/indicator/IS.AIR.PSGR](https://data.worldbank.org/indicator/IS.AIR.PSGR)

The project uses three CSV files provided by the World Bank:

* Main table: API_IS.AIR.PSGR_DS2_en_csv_v2_294362.csv
* Country metadata: Metadata_Country_API_IS.AIR.PSGR_DS2_en_csv_v2_294362.csv
* Indicator metadata: Metadata_Indicator_API_IS.AIR.PSGR_DS2_en_csv_v2_294362.csv

## 4. Application

The repository of the project can be found [here](https://github.com/schmidj/Air-Passengers-PowerBI).

### 1. Exploratory Data Analysis & Preprocessing

`eda_preprocessing_powerbi.ipynb`

This notebook performs data loading, cleaning, and validation to prepare the dataset for visualization.

Key processing steps:

1. Load and inspect data
* Read main passenger table and metadata files.
* Inspect dimensions, missing values, duplicates, and unique-value counts.
* Detect and remove invalid aggregations (e.g., regional summaries such as AFW, LAC, WLD).

2. Keep only true country-level data
* Rows representing aggregated regions are removed by checking Region values in the metadata table.

3. Validate totals
* A consistency check compares the row with aggregated World values vs. the sum of all country values. Differences are printed and visualized.

4. Export cleaned data
* The final preprocessed data is saved as `API_IS.AIR.PSGR_DS2_en_csv_v2_294362_clean.csv` and `Metadata_Country_API_IS.AIR.PSGR_DS2_en_csv_v2_294362_clean.csv`.
* These files are used directly in Power BI.

### 2. Power BI Dashboard

`Air_Passengers.pbix`

The dashboard provides an interactive exploration of global air passenger trends over time and across countries.

#### Main visuals included:

1. Timeline Line Chart
* Displays the evolution of air passengers over time.
* Dynamically responds to selections in Region, Country and time slider.

2. Bar Charts
* Two bar charts compare passenger numbers of the first selected year and the last selected year.
* These charts show the distribution of passengers across countries for the selected years.
* Country selection does NOT affect the bar charts → filter paths were adjusted (deactivated) so bar charts only respond to year-based and Region filters.

3. Geographic Map
* Displays the selected region or country on the world map.
* Allows intuitive spatial exploration.

#### Power Query Work

In Power Query, several transformations were applied:
* Unpivoting year columns to create a long-format table.
* Setting correct data types (text, numeric, date).
* Creating clean categorical fields for Countries, Regions, Years.
* Removing unnecessary columns.
* Ensuring temporal and spatial fields behave as proper hierarchies in Power BI.

#### Power BI Desktop Work

In Power BI Desktop, additional modeling and calculation steps were performed:

* Creating additional tables, including a Year_Slicer table used for selecting Start and End Years.
* Building custom DAX measures for:
* Bar charts showing Passengers in Start Year and Passengers in End Year.
* Dynamic card titles that display the currently selected years.
* Dynamic card values that calculate the total number of passengers for the selected start and end year.
* Designing the dashboard layout with interactive slicers, bar charts, and cards.
* Applying formatting to ensure visuals update automatically based on user selections (e.g., dynamic highlighting of selected countries or years).


## 5. Analysing The Results

## 6. Growth & Next Steps
Explain what would you do to improve this, or what you would do if you had more time!
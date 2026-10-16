# CO2 Emissions Data Analysis

## Stakeholder and Business Problem

A climate-and-energy nonprofit needs to decide where to direct community-protection and climate-support efforts, and has just received a new country-level energy and emissions dataset to help with that — but nobody has actually opened the file yet.

## Dataset Overview

The dataset is a table titled `co2_missions_2022.csv` which contains six columns. These columns are:

`country`, containing strings of country names,

`iso_code`, containing the 3 letter code for each country,

`year`, a four digit integer for each year,

`population`, an integer representing the total number of people in the country,

`gdp`, containing integers representing the country's GDP, and

`co2`, a float containing the amount of CO2 emitted that year.

The dataset is structured because it contains rows and columns, with consistent data types in each column.

## License and Sources

GitHub repo: [data/co2_emissions_2022.csv](data/co2_emissions_2022.csv)
MIT License

## Data Quality Question

I wondered about why some countries listed were actually just continents. Some were also groupings by income. Why were they grouped this way, and what determines income levels as high or low for each country? There were also some missing values within the dataset, so I was also curious on why that is.

## Reflection - AI Literacy Takeaway

What I took away from this assignment if AI were to be used is that AI's responses should not be fully trusted. AI often will say things confidently, even if the statement is wrong. Given that there's missing values in the dataset, it's possible that it could misconstrue results or overlook aspects of the dataset just from what it has (or doesn't have). I'll verify sources that AI pulls from if it's more than just the dataset that it's providing answers on, and ensure what it states is relevant to the dataset provided.

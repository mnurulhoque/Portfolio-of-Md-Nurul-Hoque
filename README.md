# Portfolio of Md Nurul Hoque

# Project 1: Analytical visualization of integrating renewable energy into energy consumption patterns in the Middle Atlantic region of the US

# Project Overview
This project was conducted as the final project required by the 'Data Visualization' course at E.J. Bloustein School of Planning and Public Policy, Rutgers University. Graphical visualization techniques have been employed to assess the impact of integrating renewable energy into energy consumption patterns in the Middle Atlantic region of the United States, particularly emphasizing New Jersey, New York, and Pennsylvania. Utilizing data spanning from 2001 to 2022, these visualizations offered insights into the evolving relationship between renewable energy adoption and energy consumption trends within this region. 

# Resources & Tools Used
Core programming language: R version 4.3.1

Development environment: RStudio

Libraries & packages: ggplot2, dplyr, viridis, hrbrthemes, GGally, plm, lmtest, car, patchwork, usmap, sf, raster, tmap, ggspatial, rnaturalearth, ggmap, leaflet, scales, cartography, sp, webshot2, magick, gganimate, corrplot

# Data Cleaning
In the initial data preparation phase, the following data cleaning tasks were performed:
1. Data loading and inspection
2. Handling missing values and formatting

# Exploratory Data Analysis

## Distribution of total energy consumption and total renewable energy generation data
![Box Plot Distribution for Renewable and Consumption](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/9f1959ff-e12b-4bab-9267-139e25a989cd)

![Violin plot-distribution of total energy consumption](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/b5cd7c8e-b039-46ea-8a70-ec5e1d759916)

![Violin plot-distribution of renew energy generation](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/cca37b56-039f-4f0e-bf03-2c4bdfad573a)

## Growth of total energy consumption and total renewable energy generation over the years
![Parallel coordinates plot](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/6580cb30-d482-4a56-8fc6-180bf0c9f810)

<img width="556" alt="Radar plot" src="https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/724c9fab-37a2-4b51-a01c-53b9e8a0e168">

## Trends of total energy consumption and total renewable energy generation over the years 
![unnamed-chunk-12-1](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/a6ff2b82-67a2-456e-857a-a00e4919305f)

![unnamed-chunk-12-2](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/328031cd-d204-4e1e-969d-f272514fb851)

## Choropleth map indicating the outline for the base year and the final year 
![Choropleth map-energy consumption](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/cc5d4a58-8437-4063-bb64-6e62391791c6)

![Choropleth map-renew energy generation](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/e418e583-2c74-4243-aa40-ef5d617bfd82)

# Data Analysis
## Main Graph
We have used the Correlogram and correlation matrix as our main graph to prove our hypothesis in this study that renewable energy generation does have an impact on the total energy consumption in the selected states.

## New Jersey
![Correlogram-NJ](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/fb1bfdb5-2a3f-4984-bd94-bf6543cd8c3f)
![Correlation matrix-NJ](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/b10f8bef-43cd-4cf8-ba99-ce5fcb896926)

## New York
![Correlogram-NY](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/ee3d53dc-b82d-4e28-bdaa-67292fc1089f)
![Correlation matrix-NY](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/6b648f61-25fa-493b-a304-a562968b9009)

## Pennsylvania
![Correlogram-PA](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/0dbb10c9-9671-4106-be41-7acc678b4e8b)
![Correlation matrix-PA](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/d70a32a2-6df3-4c34-abc5-d52c02454cfe)

## Alternate Graph
![Scatter Plot for impact analysis](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/5f956d76-9ca0-4c25-b926-540ec911d969)

![Dual Y-axix plot](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/02f8e424-39c4-4772-b2a7-675273cd7ab2)

![Dot plot](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/b74727a6-8c3f-4b43-b63b-0a9e02ab0bae)

# Conclusions
The conclusions drawn from the visualizations in this research highlight a noticeable correlation between the growth of renewable energy generation and the overall energy consumption within the studied context. The observed strong positive relationship indicates that as renewable energy integration increases, there's a concurrent rise in overall energy consumption. However, it's crucial to acknowledge the complexity of energy consumption as it's influenced by numerous interconnected variables beyond just renewable energy integration. Therefore, asserting that energy consumption solely increases due to the integration of renewable sources becomes challenging given this multifaceted nature which requires further research. 

# Policy Implications 
Governments and policymakers can use these insights to strengthen policies promoting renewable energy adoption. They can incentivize and invest in renewable energy projects, offer subsidies for clean energy technologies, and establish renewable energy targets to reduce reliance on coal and other fossil fuels. 


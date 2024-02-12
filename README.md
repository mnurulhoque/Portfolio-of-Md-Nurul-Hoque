
# [Project 1: Analytical Visualization of Integrating Renewable Energy into Energy Consumption Patterns in the Middle Atlantic Region of the US](https://mnurulhoque.github.io/integrating-renewable-energy-into-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-US/) 

## Project Overview
This project was conducted as the final project required by the 'Data Visualization' course at E.J. Bloustein School of Planning and Public Policy, Rutgers University. Graphical visualization techniques have been employed to assess the impact of integrating renewable energy into energy consumption patterns in the Middle Atlantic region of the United States, particularly emphasizing New Jersey, New York, and Pennsylvania. Utilizing data from 2001 to 2022, these visualizations offered insights into the evolving relationship between renewable energy adoption and energy consumption trends within this region. 

## Resources & Tools Used
Core programming language: R version 4.3.1

Development environment: RStudio

Libraries & packages: ggplot2, dplyr, viridis, hrbrthemes, GGally, plm, lmtest, car, patchwork, usmap, sf, raster, tmap, ggspatial, rnaturalearth, ggmap, leaflet, scales, cartography, sp, webshot2, magick, gganimate, corrplot

## Data Cleaning
In the initial data preparation phase, the following data cleaning tasks were performed:
1. Data loading and inspection
2. Handling missing values and formatting

## Exploratory Data Analysis
1. Examined the distribution of the data through Boxplot and Violin Plot
2. Examined the patterns, growth, and trends of the data through Line graph, Parallel coordinates plot, and Radar plot
3. Created Choropleth map indicating the outline of the data for the base year (2001) and the final year (2022)

## Data Analysis
1. Used Correlogram and correlation matrix as our main graph to prove the hypothesis that renewable energy generation does have an impact on the total energy consumption in the selected states.
2. Used Scatter Plot, Dual Y-axis Plot, and Dot Chart as our alternate graphs to support our findings in the main graph. 
![Scatter Plot for impact analysis](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/5f956d76-9ca0-4c25-b926-540ec911d969)

## Findings
The conclusions drawn from the visualizations in this project highlight a noticeable correlation between the growth of renewable energy generation and the overall energy consumption within the studied context. The observed strong positive relationship indicates that as renewable energy integration increases, there's a concurrent rise in overall energy consumption. However, it's crucial to acknowledge the complexity of energy consumption as it's influenced by numerous interconnected variables beyond just renewable energy integration. Therefore, asserting that energy consumption solely increases due to the integration of renewable sources becomes challenging given this multifaceted nature which requires further research. 

## Policy Implications 
Governments and policymakers can use these insights to strengthen policies promoting renewable energy adoption. They can incentivize and invest in renewable energy projects, offer subsidies for clean energy technologies, and establish renewable energy targets to reduce reliance on coal and other fossil fuels. 

# [Project 2: A Spatial Analysis of the Licensed Childcare Centers in New Jersey, USA](https://mnurulhoque.github.io/NJ-Childcare-Centers/)

## Project Overview 
This project was conducted as the final project required by the 'Seminar in Public Informatcs (Command Line Geographic Information System' course at E.J. Bloustein School of Planning and Public Policy, Rutgers University. This project aims to analyze the Licensed Childcare Centers in New Jersey, USA through Spatial Analysis tools. 

## Resources & Tools Used
Core programming language: Python

Development environment: Jupyter Notebook

Libraries & packages: pandas, geopandas, pygeos, arcgis, shapely, folium, mapclassify, matplotlib

## Data Wrangling 
1. Collected the dataset as csv file with no geographic coordinates information
2. Converted the address and ZIP codes into geographic coordinates through geocoding
3. Used Spatial Joins, and Geoprocessing tools like Buffer, Clip, Union Overlay Operation, Unary Union etc. to make the data appropriate to generate the desired maps
4. Encountered a bug in the heatmap of the interactive map and solved that issue by adjusting the heatmap layer style in the HTML codes

## Data Analysis
1. Created 3 static maps. one is given here as an example. 
![static map3](https://github.com/mnurulhoque/NJ-Childcare-Centers/assets/152673435/736c4625-79fb-4c1d-90c3-3945de4dd8ed)
2. Created one interactive web map.
You can explore [this interactive web map as its own web page here](https://mnurulhoque.github.io/NJ-Childcare-Centers/nj_childcare_centers.html)

## Policy Implications
This spatial analysis of licensed childcare centers in New Jersey, USA offers critical insights that have significant policy implications for urban planning, public transportation, and childcare services. The distribution of childcare centers relative to population density, their accessibility via public transit, and the proximity to residential areas provide a foundation for informed decision-making in in the mentioned policy areas. By leveraging such insights, policymakers can devise strategies that not only address the immediate needs of families for childcare but also contribute to the long-term welfare and development of communities across New Jersey.

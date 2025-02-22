# [Project 1: Prediction of Used Car Prices Leveraging Data and Machine Learning](https://mnurulhoque.github.io/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/) 

## OVERVIEW OF THE PROJECT
This project aims to develop a machine learning model capable of predicting the resale price of used cars listed on platforms like Craigslist. By leveraging historical data and machine learning algorithms, the project seeks to achieve the following objectives:

**i. Accurate Price Predictions:** Develop a predictive model to estimate car prices based on key features such as vehicle specifications (e.g., odometer, make, model, condition, transmission type) and seller information (e.g., location, fuel type, cylinders).

**ii. Feature Importance and Interpretability:** Identify and interpret the key features driving car price predictions using SHAP values.

This project bridges the gap between subjective car valuations and objective, data-driven pricing models, making car pricing more transparent, consistent, and fair for stakeholders.

## OVERVIEW OF THE DATASET
The dataset includes a variety of features describing cars listed on Craigslist. It contains 26 columns, including both numerical and categorical features. Some notable features include:

-`year`: The manufacturing year of the car.

-`odometer`: The total mileage of the car.

-`manufacturer`: The car's manufacturing company.

-`model`: The specific model of the car.

-`fuel`: The type of fuel used (e.g., gas, diesel, electric).

-`transmission`: The type of transmission (automatic, manual, etc.).

-`lat` and `long`: Geographic location coordinates of the car listing.

The target variable for the prediction task is `price`, which represents the sale price of each car. 

The dataset has been downloaded from Kaggle. Here is the Link: https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data

## INITIAL DATA EXPLORATION
To understand the structure of the dataset, the following actions were performed:

**Dataset Information:** The dataset has 14,101 rows and 26 columns. It includes numerical data (year, odometer, lat, long) and categorical data (manufacturer, model, fuel, transmission).

**Summary Statistics:** Basic statistics such as mean, standard deviation, minimum, and maximum values were calculated for numerical columns like year and odometer. For example, the mean year of cars is approximately 2011, and the average mileage (odometer) is 101,914.

**Missing Values:** A significant number of missing values were detected in several columns, such as condition, cylinders, drive, and size.
A missing values heatmap was generated to visually identify columns with high percentages of missing data.

![Missing values before cleaning](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/assets/df5cbe98-2e14-4cf7-94bc-0eb3cb1b4e47)

## DATA PREPROCESSING

**Handling Missing Data:** Given the presence of missing values in key columns, preprocessing steps were applied:
Columns such as url, region_url, VIN, image_url, description, and county were deemed irrelevant to the prediction task and removed.
We handled missing values in the dataset by imputing numerical and categorical columns with appropriate statistical measures. For numerical columns, identified using select_dtypes(include=[np.number]), missing values are replaced with the median of the column. The median is chosen because it is robust to outliers, ensuring the central tendency of the data remains unaffected by extreme values. This imputation is performed in-place, directly modifying the original dataset. For categorical columns, identified using select_dtypes(include=[object]), missing values are replaced with the mode of the column, which represents the most frequently occurring value. Using the mode for categorical data ensures the imputed values align with the most common category, preserving the original distribution. This method avoids the loss of information associated with dropping rows or columns with missing data and is dynamic, automatically identifying and imputing columns based on their data types. Overall, this approach effectively preserves data integrity and ensures the dataset is ready for analysis or modeling.
The heatmap of the missing values after data cleaning has been given below: 

![Missing values after cleaning](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/Missing%20values%20after%20cleaning.png)

**Balancing the Dataset:** Before balancing, the distribution of the target variable in the training data shows a significant imbalance across the defined bins. As evident in the first chart ("Distribution of Target Variable in Training Data"), one bin (e.g., bin 1) dominates the dataset with the highest frequency, while other bins, particularly bin 0, have considerably fewer samples. This imbalance can skew machine learning models, causing them to become biased towards the majority class, ultimately reducing their performance on underrepresented classes.

![Distribution of target variable in training data](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/Distribution%20of%20target%20variable%20in%20training%20data.png)

To address this, upsampling is used to balance the dataset. The process involves first combining the training features (X_train) and target variable (y_train) into a single DataFrame. Each target value is grouped into bins (e.g., bin column), which highlights the imbalance. Then, the resample function is applied to the underrepresented bins, duplicating their samples until each bin reaches the same number of samples as the majority class (the maximum bin count). The upsampling is performed with replacement, ensuring that the original distribution of each class within the bins is preserved while increasing their representation. The balanced dataset is then constructed by concatenating all the resampled subsets for each unique bin.

![Distribution of target variable after balancing](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/Distribution%20of%20target%20variable%20after%20balancing.png)

After balancing, as shown in the second chart ("Distribution of Target Variable After Balancing"), the frequencies of all bins are equalized. This improvement ensures that the dataset no longer exhibits class imbalance, which helps to mitigate biases during model training. As a result, the model can learn equally from all classes, improving its ability to generalize and predict accurately across all categories. This enhancement is particularly important for tasks requiring fair and representative predictions across different classes.

**Encoding Categorical Variables:** We implemented mean encoding to transform categorical features into numerical representations based on their relationship with the target variable (price). A list of categorical features, such as manufacturer, model, condition, fuel, transmission, drive, type, state, and cylinders, is specified for encoding. For each feature in this list, the code calculates the mean of the target variable (price) grouped by the unique categories of that feature using the groupby method. This results in a mapping where each category is replaced by the average price of the samples belonging to that category. The map function then applies this mapping to transform the original categorical values in the dataset to their corresponding mean-encoded values. By doing so, mean encoding captures the statistical relationship between each category and the target variable, enhancing the dataset's predictive power while converting categorical data into a numerical format suitable for machine learning models. This approach can be particularly useful for models that benefit from numerical features but requires careful handling to prevent data leakage, such as during cross-validation.

**Feature Scaling:** Numerical features like year and odometer were normalized using the QuantileTransformer method. This transformation ensures that the numerical values follow a normal distribution, improving model performance.

**Feature Engineering:** To enhance the predictive power of the model, an interaction feature year_odometer was created by multiplying year and odometer. Additionally, the target variable price was log-transformed using log1p to reduce skewness and stabilize variance.

## MACHINE LEARNING MODEL PIPELINE DESIGN, TRAINING, AND OPTIMIZATION 

### Model Selection:
Four machine learning models were selected for evaluation:

i. Random Forest: An ensemble model that builds multiple decision trees to improve accuracy.

ii. XGBoost: A gradient-boosting algorithm optimized for speed and performance.

iii. LightGBM: A lightweight boosting algorithm suitable for large datasets.

iv. CatBoost: A gradient-boosting algorithm specifically designed for categorical features.

### Model Justification and Fine-Tuning:
The models were chosen based on their proven performance with tabular datasets and their ability to handle numerical and categorical features (Varma et al., 2023; Wang et al., 2022). To improve performance, hyperparameter tuning was performed using Optuna, an automated optimization framework:

![Optimized hyperparameters](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/Optimized%20hyperparameters.png)

### Model Evaluation and Cross-Validation:
Model evaluation was performed using a 5-fold Cross-Validation strategy to ensure that the models generalize well across unseen data. Performance was measured using:

**i. Root Mean Squared Error (RMSE):** Measures prediction error magnitude. It is sensitive to large errors because it squares the residuals, making it an excellent measure when large deviations in price prediction are critical to detect (Hodson, 2022). Compared to Mean Absolute Error (MAE), RMSE penalizes large errors more severely, which aligns with the goal of minimizing significant mispredictions.

**ii. R² Score:** Explains the proportion of variance captured by the model. This metric indicates how well the model explains variance in the target variable. It helps evaluate the goodness-of-fit for regression models and compares model performance across iterations.

### Baseline Model Performance:
Each model was trained on the preprocessed dataset, and their performance was evaluated using Root Mean Squared Error (RMSE) and R² score. The baseline results are as follows:

![Baseline model performance](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/Baseline%20model%20performance.png)

### Model Performance After Optimization:
After hyperparameter tuning, the optimized performance results are as follows:

![Model performance after optimization](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/Model%20performance%20after%20optimization.png)

### Best Model Selection:
The best-performing model for predicting car prices is XGBoost, which achieved the lowest RMSE (Root Mean Square Error) of 0.4249 and the highest R² (coefficient of determination) of 0.7954 among the optimized models. These metrics indicate that XGBoost not only provides the most accurate predictions by minimizing the average squared differences between predicted and actual values but also explains approximately 79.54% of the variance in the target variable. Compared to the other models, including Random Forest, LightGBM, and CatBoost, XGBoost strikes the best balance between precision and generalizability, making it the optimal choice for this predictive task.

## MACHINE LEARNING MODEL INTERPRETABILITY 

![Feature Importance](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/Feature%20Importance.png)

The SHAP summary plot provides insights into the impact of features on the XGBoost model's predictions for car price prediction. The horizontal axis represents the SHAP values, which indicate the impact of each feature on the model's output, while the vertical axis lists the features in descending order of importance.
The most influential features are model, year, and odometer, as they have the widest range of SHAP values, meaning their variations significantly affect the predictions. For example, model shows both positive and negative SHAP values, indicating that different models can either increase or decrease the predicted price. Similarly, year shows that newer vehicles generally lead to higher predicted prices (positive SHAP values), while older vehicles decrease it.
Features such as latitude (lat), manufacturer, and type also play a substantial role, although their impacts are less pronounced than the top features. These features capture geographical and categorical distinctions that affect pricing. On the other hand, features like state, fuel, and condition have lower SHAP values, suggesting they contribute less to the model's predictions.
The color gradient represents feature values, where red indicates high values and blue indicates low values. For instance, for year, red points (newer cars) have positive SHAP values, contributing to higher predictions, while blue points (older cars) decrease predictions. This detailed visualization helps interpret the model's behavior and understand the factors influencing car price predictions.

![LIME explanation-1](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/LIME%20explanation-1.png)

This LIME explanation provides a detailed breakdown of a single prediction for car price, offering insights into how specific features influenced the model's output. The model predicted a price of 21,286.28, while the actual price was 16,094.99, indicating some lower predicted value. The prediction falls within a local range of possible values, from approximately 6.45 to 12.61. Key features influencing the prediction are displayed as either negative (blue), pulling the predicted value down, or positive (orange), pushing it up. The feature model contributes significantly in a negative direction, decreasing the predicted price by about 13,252.36 units, while condition and cylinders have strong positive contributions, adding approximately 4,545.74 and 2,716.17 units, respectively. Features such as drive and year also play a role, with drive slightly decreasing the prediction by 2,089.95 units and year (2013) increasing it by 2,020.40 units. Other features, including manufacturer, state, and type, have minor impacts on the prediction. The table on the right lists the actual input values for these features, providing context for their contributions. Overall, this explanation highlights the transparency of the model's decision-making process and identifies the most influential factors for this specific car's predicted price.

![LIME explanation-2](https://github.com/mnurulhoque/Prediction-of-Used-Car-Prices-Leveraging-Data-and-Machine-Learning/blob/main/LIME%20explanation-2.png)

This LIME explanation illustrates the model's prediction for a specific car, providing insights into the features that influenced the output. The model predicted a price of 30,958.29, while the actual price was 36,494.99, showing a moderate higher predicted value. The prediction falls within a local range, from a minimum of 5.95 to a maximum of 12.66. The key influencing features are categorized into negative (blue), reducing the predicted price, and positive (orange), increasing it. Among the features, odometer and year make the largest positive contributions, adding 28,137.00 and 20,014.00 units, respectively, to the prediction. Features such as cylinders and condition also push the prediction higher, contributing 2,716.17 and 4,545.74 units, respectively. On the other hand, model has a significant negative impact, decreasing the prediction by 13,252.36 units. Features like latitude (lat), longitude (long), and drive also slightly reduce the predicted price but with less influence compared to the top contributors. The table on the right provides the actual values for each feature, adding context to the analysis. Overall, this explanation highlights how critical features like odometer, year, and model drive the model's predictions, offering transparency into its decision-making process.

## Conclusions
The project successfully developed a machine learning model to predict car prices based on key car attributes. The XGBoost model outperformed other models, achieving the lowest RMSE of 0.4249 and the highest R² score of 0.7954. By leveraging SHAP values, we identified model, year, and odometer as the most influential predictors. 
Overall, the XGBoost model provides a reliable and interpretable solution for predicting car prices. Platforms like Craigslist can integrate this model to offer fair pricing suggestions to users, enhancing transparency and trust in the online used car market. Future work could focus on integrating additional features like car accident history or service records to improve the model's accuracy further.

# [Project 2: Analytical Visualization of Integrating Renewable Energy into Energy Consumption Patterns in the Middle Atlantic Region of the US](https://mnurulhoque.github.io/integrating-renewable-energy-into-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-US/) 

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

![Box Plot Distribution for Renewable and Consumption](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/9f1959ff-e12b-4bab-9267-139e25a989cd)

![Violin plot-distribution of total energy consumption](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/b5cd7c8e-b039-46ea-8a70-ec5e1d759916)

![Violin plot-distribution of renew energy generation](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/cca37b56-039f-4f0e-bf03-2c4bdfad573a)

![Parallel coordinates plot](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/6580cb30-d482-4a56-8fc6-180bf0c9f810)

<img width="556" alt="Radar plot" src="https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/724c9fab-37a2-4b51-a01c-53b9e8a0e168">

![Choropleth map-energy consumption](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/cc5d4a58-8437-4063-bb64-6e62391791c6)

![Choropleth map-renew energy generation](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/e418e583-2c74-4243-aa40-ef5d617bfd82)

## Data Analysis
1. Used Correlogram and correlation matrix as our main graph to prove the hypothesis that renewable energy generation does have an impact on the total energy consumption in the selected states.
2. Used Scatter Plot, Dual Y-axis Plot, and Dot Chart as our alternate graphs to support our findings in the main graph. 

![Correlogram-NJ](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/fb1bfdb5-2a3f-4984-bd94-bf6543cd8c3f)

![Correlation matrix-NJ](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/b10f8bef-43cd-4cf8-ba99-ce5fcb896926)

![Correlogram-NY](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/ee3d53dc-b82d-4e28-bdaa-67292fc1089f)

![Correlation matrix-NY](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/6b648f61-25fa-493b-a304-a562968b9009)

![Correlogram-PA](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/0dbb10c9-9671-4106-be41-7acc678b4e8b)

![Correlation matrix-PA](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/d70a32a2-6df3-4c34-abc5-d52c02454cfe)

![Scatter Plot for impact analysis](https://github.com/mnurulhoque/integrating-renewable-energy-on-energy-consumption-patterns-in-the-Middle-Atlantic-region-of-the-US/assets/152673435/5f956d76-9ca0-4c25-b926-540ec911d969)

## Findings
The conclusions drawn from the visualizations in this project highlight a noticeable correlation between the growth of renewable energy generation and the overall energy consumption within the studied context. The observed positive relationship indicates that as renewable energy integration increases, there's a concurrent rise in overall energy consumption. However, it's crucial to acknowledge the complexity of energy consumption as it's influenced by numerous interconnected variables beyond just renewable energy integration. Therefore, asserting that energy consumption solely increases due to the integration of renewable sources becomes challenging given this multifaceted nature which requires further research. 

## Policy Implications 
Governments and policymakers can use these insights to strengthen policies promoting renewable energy adoption. They can incentivize and invest in renewable energy projects, offer subsidies for clean energy technologies, and establish renewable energy targets to reduce reliance on coal and other fossil fuels. 

# [Project 3: A Spatial Analysis of the Licensed Childcare Centers in New Jersey, USA](https://mnurulhoque.github.io/NJ-Childcare-Centers/)

## Project Overview 
This project was conducted as the final project required by the 'Seminar in Public Informatcs (Command Line Geographic Information System' course at E.J. Bloustein School of Planning and Public Policy, Rutgers University. This project aims to analyze the Licensed Childcare Centers in New Jersey, USA through Spatial Analysis tools. 

## Resources & Tools Used
Core programming language: Python

Development environment: Jupyter Notebook

Libraries & packages: pandas, geopandas, pygeos, arcgis, arcpy, geocoder, shapely, folium, mapclassify, matplotlib, plotly, OSMNX

## Data Wrangling 
1. Collected the dataset as csv file with no geographic coordinates information
2. Converted the address and ZIP codes into geographic coordinates through geocoding
3. Used Spatial Joins, and Geoprocessing tools like Buffer, Clip, Union Overlay Operation, Unary Union etc. to make the data appropriate to generate the desired maps
4. Encountered a bug in the heatmap of the interactive map and solved that issue by adjusting the heatmap layer style in the HTML codes

## Data Analysis
## STATIC MAPS

## NJ Licensed Childcare Centers by County  
![static map1](https://github.com/mnurulhoque/NJ-Childcare-Centers/assets/152673435/340ebad6-df60-482f-8eeb-452bb042a8c5)

## NJ Licensed Childcare Centers per 100k Residents  
![static map2](https://github.com/mnurulhoque/NJ-Childcare-Centers/assets/152673435/6377a934-d0f5-4924-a1f4-ee463456fd94)

## NJ Licensed Childcare Centers: Five Mile Transit Accessibility by County  
![static map3](https://github.com/mnurulhoque/NJ-Childcare-Centers/assets/152673435/736c4625-79fb-4c1d-90c3-3945de4dd8ed)

## INTERACTIVE MAP  
<iframe src='nj_childcare_centers.html' width = '1000' height = '700' ></iframe>

You can explore [the interactive web map as its own web page here](https://mnurulhoque.github.io/NJ-Childcare-Centers/nj_childcare_centers.html)

## Policy Implications
This spatial analysis of licensed childcare centers in New Jersey, USA offers critical insights that have significant policy implications for urban planning, public transportation, and childcare services. The distribution of childcare centers relative to population density, their accessibility via public transit, and the proximity to residential areas provide a foundation for informed decision-making in in the mentioned policy areas. By leveraging such insights, policymakers can devise strategies that not only address the immediate needs of families for childcare but also contribute to the long-term welfare and development of communities across New Jersey.

# [Project 4: Does News Media Spread Fear of AI?-An Analytical Exploration through Natural Language Processing (NLP) and Machine Learning (ML)](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/blob/main/README.md) 

## Project Overview
The project investigates the media's role in shaping public perceptions of artificial intelligence (AI). It explores whether the news media spreads fear of AI by analyzing dominant themes in media coverage.
Project Objectives include:
i. Uncovering narratives surrounding AI in the media, 
ii. Utilizing text analytics and natural language processing (NLP) techniques to extract insights, and 
iii. Generating data-supported insights and visualizations to inform public discourse.

## Data Set
This [CSV file](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/blob/main/Dataset_3.5k.csv) was used here as the data set.  

## Resources & Tools Used
Core programming language: Python 

Development environment: Google Colab Notebook

Libraries & packages: pandas, numpy, matplotlib, seaborn, sklearn, lmfit, statsmodels, tabulate, textblob, nltk, spacy, string, wordcloud, LinearRegression

## Workflow of the Project
![Workflow of the Project](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/Workflow.png)

## Data loading and exploration
In the initial data preparation phase, the following tasks were performed:
1. Data loading and exploration to understand its structure, features and content
2. Handling missing values or inconsistency in the data 

## Text Processing
1. Non English text removal => this step is important because we only analyze English text, having non-English text might affect the outcomes
2. Contraction Expansion
3. Lowercasing the text.
4. Tokenization and removing stopwords (common words like 'and', 'the', 'is', etc.).
5. Lemmatization or stemming to reduce words to their base or root form.
6. Removing punctuation, special characters, and numbers

## Exploratory Data Analysis 
![Word Cloud](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/Word%20Cloud.png)

## Sentiment Analysis

![Line graph-Sentiment distribution over time](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/Line%20graph-Sentiment%20distribution%20over%20time.png)

The neutral sentiment shows the strongest upward trend over time, as indicated by the highest slope of 0.41

The positive sentiment also shows an increase but at a more moderate rate, with a slope of 0.17

The negative sentiment shows the weakest upward trend, with the lowest slope of 0.09

![Sentiment-regression line](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/Sentiment-regression%20line.png)

The trend line has a positive slope (m=0.10), which indicates that the count of negative sentiments is gradually increasing over time.

![Stacked bar-cumulative sentiment over time](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/Stacked%20bar-cumulative%20sentiment%20over%20time.png)

While the absolute counts of sentiments increase, the proportions of each sentiment type remain fairly consistent over time, with neutral sentiments consistently being the most common, followed by positive and then negative sentiments.

![Stacked bar-proportion of sentiment distribution over time](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/Stacked%20bar-proportion%20of%20sentiment%20distribution%20over%20time.png)

The overall pattern of sentiment distribution appears relatively stable across the time frame shown, with little variation in the proportions of each sentiment category.

![Sentiment Analysis-Pie Charts](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/Sentiment%20Analysis-Pie%20Charts.png)

The accuracy was relatively low comparing to pre-built models, one of the reason could be the training and testing data were not concerning similar topics. Also could because of the testing data are too simple in terms of length.

## Findings and Recommendations
It appears that the news media is not predominantly spreading fear of AI, at least not in the dataset we've analyzed. However, it's essential to consider the limitations of the dataset and the possibility that fear-based narratives may exist in other contexts or datasets not included in our analysis.

## Project Notebook 
[Notebooks](https://github.com/mnurulhoque/Does-News-Media-Spread-Fear-of-AI--Sentiment-Analysis-through-NLP/raw/main/RAISE_2024_Data_Dynamos_Final.ipynb)

# [Project 5: Microsoft PowerBI Dashboard](https://github.com/mnurulhoque/PowerBI-Dashboard/blob/main/README.md) 

## Project Overview
The objectives of this Dashboard is to present the daily picture of a Customer Service Company. The project is based on work I completed in one of my previous jobs, but the data and details have been altered. It does not represent the actual work or insights of the organization.

## Resources and Tools Used

### 1. Data Sources
- **Customer Feedback Data:** CSV file containing customer service complaints (daily).
- **Source:** Internal data from NJProject Custmer Service (anonymized for this project).

### 2. Tools and Platforms
- **Power BI Desktop:** For creating the interactive dashboard and performing data modeling.
- **Power BI Service:** For publishing and sharing the dashboard online.
- **Microsoft Excel:** Used for data cleaning and initial analysis.

### 3. Programming and Scripting Languages
- **SQL:** Queried data from the company database for analysis.
- **Python (pandas):** Cleaned and transformed the dataset before importing it into Power BI.

### 4. Other Tools
- **GitHub:** Hosted the project files, including `.pbix` file and supporting documents.

## NJProject Customer Service Dashboard (Interactive)

<iframe src='NJProject_dashboard.html' width = '1000' height = '1000' ></iframe>

Check out this interactive dashboard in PowerBI Website:  
[NJProject Customer Service Dashboard](https://app.powerbi.com/view?r=eyJrIjoiYzNkNmExMWItNjM3My00ZTlmLTk2OGQtNjYwMWMyOTM5MTZmIiwidCI6ImI5MmQyYjIzLTRkMzUtNDQ3MC05M2ZmLTY5YWNhNjYzMmZmZSIsImMiOjF9)

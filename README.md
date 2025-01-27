# COVID-19 Data Analysis and Visualization using Plotly Express

## Overview

This project performs an analysis of COVID-19 data and visualizes it using Plotly Express in Python. The analysis includes a variety of charts such as bar graphs, line graphs, bubble charts, scatter plots, and maps to understand the spread, impact, and preventive measures of COVID-19 across the world. The project utilizes three datasets containing COVID-19 statistics and death causes for real-world applications of data science and visual analytics.

## Tools and Technologies Used

- **Python**  
- **Plotly Express**  
- **Pandas**  
- **NumPy**  
- **Matplotlib**  
- **Google Colab (Runtime type – GPU)**  
- **Wordcloud**  
- **Plotly Choropleth Map**  

## Project Structure

The project is organized as follows:

1. **Data Preparation and Cleaning**:  
   - Importing necessary libraries and datasets.
   - Inspecting dataset structures and cleaning missing or irrelevant data.

2. **Data Analysis**:  
   - Performing various data analysis tasks like summarizing key COVID-19 statistics globally and per country.

3. **Data Visualization**:  
   - **Bar Graphs**: To compare total cases, deaths, recoveries, and tests for countries/regions.
   - **Bubble Charts**: To visualize COVID-19 data on a per-country and continent level.
   - **Scatter Plots**: To represent COVID-19 data comparisons.
   - **Choropleth Maps**: To visualize the spread of COVID-19 globally through maps.
   - **Line Graphs and Animations**: To track the trend of COVID-19 cases over time.

4. **Word Cloud Visualization**:  
   - Visualizing the major causes of death from COVID-19 using WordCloud for the 'Condition' column.

## Requirements

Before running this project, ensure that you have the following Python packages installed:

- `plotly`
- `pandas`
- `numpy`
- `matplotlib`
- `wordcloud`
- `plotly.express`
- `plotly.graph_objs`
- `plotly.figure_factory`
- `google.colab`

You can install them via pip:

```bash
pip install plotly pandas numpy matplotlib wordcloud
```

## Step-by-Step Implementation

### Step 1: Importing Necessary Libraries

We begin by importing the necessary libraries for data analysis, manipulation, and visualization. Below is an example:

```python
# Data analysis and manipulation
import plotly.graph_objs as go
import plotly.io as pio
import plotly.express as px
import pandas as pd

# Data Visualization
import matplotlib.pyplot as plt

# Importing Plotly
import plotly.offline as py
py.init_notebook_mode(connected=True)

# Initializing Plotly
pio.renderers.default = 'colab'
```

### Step 2: Importing Datasets

We import three datasets containing COVID-19 related data:

- **covid**: A dataset containing global COVID-19 statistics by country/region.
- **covid_grouped**: A dataset with time-series data for COVID-19 statistics.
- **coviddeath**: A dataset that provides information on the causes of COVID-19 deaths.

```python
dataset1 = pd.read_csv("covid.csv")
dataset2 = pd.read_csv("covid_grouped.csv")
dataset3 = pd.read_csv("coviddeath.csv")
```

### Step 3: Data Cleaning

Data cleaning is essential for removing missing or irrelevant columns. For example, we drop columns with high null values:

```python
dataset1.drop(['NewCases', 'NewDeaths', 'NewRecovered'], axis=1, inplace=True)
```

### Step 4: Visualizing Data

#### Bar Graphs

We create bar graphs to compare COVID-19 statistics across countries. Here's an example of visualizing total cases per country:

```python
px.bar(dataset1.head(15), x='Country/Region', y='TotalCases', color='TotalCases', height=500, hover_data=['Country/Region', 'Continent'])
```

#### Bubble Charts

Bubble charts are used to visualize the relationship between different COVID-19 statistics for countries:

```python
px.scatter(dataset1.head(100), x='Country/Region', y='TotalCases', hover_data=['Country/Region', 'Continent'], color='TotalCases', size='TotalCases', size_max=80)
```

#### Choropleth Maps

Choropleth maps provide a geographical representation of COVID-19 statistics:

```python
px.choropleth(dataset2, locations="iso_alpha", color="Confirmed", hover_name="Country/Region", color_continuous_scale="Blues", animation_frame="Date")
```

### Step 5: Word Cloud

To visualize the leading causes of death due to COVID-19, we generate a WordCloud:

```python
from wordcloud import WordCloud

sentences = dataset3["Condition"].tolist()
sentences_as_a_string = ' '.join(sentences)

plt.figure(figsize=(20, 20))
plt.imshow(WordCloud().generate(sentences_as_a_string))
```

### Step 6: Additional Visualizations

- **Line graphs**: Track the trend of COVID-19 cases over time.
- **Data Animations**: Using `animation_frame` for date-based animations.

## Example Outputs

- **Bar graph comparison** of confirmed cases, deaths, and recoveries.
- **Bubble chart** visualizing country-specific COVID-19 cases, deaths, and tests.
- **Choropleth map** visualizing confirmed COVID-19 cases globally.
- **WordCloud** showing common conditions associated with COVID-19 deaths.

## Conclusion

This project provides a comprehensive analysis of COVID-19 data and offers several visualizations to help understand the global impact of the virus. The use of Plotly Express allows for interactive and insightful graphs, making it easier to interpret complex data patterns.

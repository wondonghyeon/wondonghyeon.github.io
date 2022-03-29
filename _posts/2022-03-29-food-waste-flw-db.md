---
type: posts
title: Food Waste - Exploring Food Loss and Waste Database from FAO
header:
  image: /files/images/headers/rotten-fruits.jpg
  caption: "Photo credit: [**unsplash@jccards**](https://unsplash.com/@jccards)"
date:   2022-03-29 19:15:00 +0900
last_modified_at: 2022-03-29 19:15:00 +0900
categories: sustainability
tags:
 - food waste
 - sustainability
 - food loss
 - food loss and waste database
 - data visualization
 - seaborn
 - python
published: true
---
In this post, we'll take a quick look at the Food Loss and Waste Database (FLW DB) from the Food and Agriculture Organization (FAO) of the United Nations. The post will mostly be about data visualization. I'll discuss the limitation of the dataset at the end. 

I used Python and Pandas/Seaborn/Matplotlib libraries to visualize the data. You can find the full Python scripts on my [GitHub repository](https://github.com/wondonghyeon/codes-for-blog/tree/master/food-waste). 

## TL;DR
TODO: Fill this in.


## Database Overview
### Downloading the Data
Download data from FAO. (**Note: The following steps are valid as of March 2022**)
* Go to FAO's FLW data page. [link](https://www.fao.org/platform-food-loss-waste/flw-data/en/).
* Select "Year Range." I used 1965 - 2021 for this post.
* Download data by clicking the "Download Data" button on the bottom left of the page. 

Here are the first few rows of the dataset. 

```python
# read and show the first few rows of the dataframe
df = pd.read_csv('./data/Data.csv')
df[:8]
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>m49_code</th>
      <th>country</th>
      <th>region</th>
      <th>cpc_code</th>
      <th>commodity</th>
      <th>year</th>
      <th>loss_percentage</th>
      <th>loss_percentage_original</th>
      <th>loss_quantity</th>
      <th>activity</th>
      <th>food_supply_stage</th>
      <th>treatment</th>
      <th>cause_of_loss</th>
      <th>sample_size</th>
      <th>method_data_collection</th>
      <th>reference</th>
      <th>url</th>
      <th>notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>104</td>
      <td>Myanmar</td>
      <td>NaN</td>
      <td>0142</td>
      <td>Groundnuts, excluding shelled</td>
      <td>2009</td>
      <td>5.22</td>
      <td>5.22%</td>
      <td>68100</td>
      <td>NaN</td>
      <td>Whole supply chain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FAO's annual Agriculture Production Questionna...</td>
      <td>FAO Sources</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>104</td>
      <td>Myanmar</td>
      <td>NaN</td>
      <td>0142</td>
      <td>Groundnuts, excluding shelled</td>
      <td>2008</td>
      <td>5.43</td>
      <td>5.43%</td>
      <td>65240</td>
      <td>NaN</td>
      <td>Whole supply chain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FAO's annual Agriculture Production Questionna...</td>
      <td>FAO Sources</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>104</td>
      <td>Myanmar</td>
      <td>NaN</td>
      <td>0142</td>
      <td>Groundnuts, excluding shelled</td>
      <td>2007</td>
      <td>5.61</td>
      <td>5.61%</td>
      <td>61080</td>
      <td>NaN</td>
      <td>Whole supply chain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FAO's annual Agriculture Production Questionna...</td>
      <td>FAO Sources</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>104</td>
      <td>Myanmar</td>
      <td>NaN</td>
      <td>0142</td>
      <td>Groundnuts, excluding shelled</td>
      <td>2006</td>
      <td>5.40</td>
      <td>5.4%</td>
      <td>55270</td>
      <td>NaN</td>
      <td>Whole supply chain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FAO's annual Agriculture Production Questionna...</td>
      <td>FAO Sources</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>104</td>
      <td>Myanmar</td>
      <td>NaN</td>
      <td>0142</td>
      <td>Groundnuts, excluding shelled</td>
      <td>2005</td>
      <td>5.00</td>
      <td>5%</td>
      <td>51970</td>
      <td>NaN</td>
      <td>Whole supply chain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FAO's annual Agriculture Production Questionna...</td>
      <td>FAO Sources</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>104</td>
      <td>Myanmar</td>
      <td>NaN</td>
      <td>0142</td>
      <td>Groundnuts, excluding shelled</td>
      <td>2004</td>
      <td>5.00</td>
      <td>5%</td>
      <td>47310</td>
      <td>NaN</td>
      <td>Whole supply chain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FAO's annual Agriculture Production Questionna...</td>
      <td>FAO Sources</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>104</td>
      <td>Myanmar</td>
      <td>NaN</td>
      <td>0142</td>
      <td>Groundnuts, excluding shelled</td>
      <td>2003</td>
      <td>5.00</td>
      <td>5%</td>
      <td>43880</td>
      <td>NaN</td>
      <td>Whole supply chain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FAO's annual Agriculture Production Questionna...</td>
      <td>FAO Sources</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>108</td>
      <td>Burundi</td>
      <td>NaN</td>
      <td>0111</td>
      <td>Wheat</td>
      <td>2020</td>
      <td>3.50</td>
      <td>3.5</td>
      <td>NaN</td>
      <td>Shelling, Threshing</td>
      <td>Farm</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Modelled Estimates</td>
      <td>NaN</td>
      <td>https://www.aphlis.net/en/page/20/data-tables#...</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


### Columns
Here are the columns that I'll be primarily using for this post. I believe the column names are self explantory, but please look at [the Background of the Food Loss and Waste Database page](https://www.fao.org/platform-food-loss-waste/flw-data/background/en/) for the full details.
* year
  * e.g. 2017, 2018, ...
* country
  * There are 149 unique countries.
  * e.g. 'Austria', 'Jordan', 'Kenya', ...
* commodity
  * There are 194 unique commodities.
  * e.g. 'Apples', 'Pears', 'Apricots', 'Cherries', 'Peaches and nectarines', 'Plums and sloes', 'Kiwi fruit', 'Strawberries', 'Blueberries', ...
* food_supply_stage
  * There are 20 unique food supply stages.
  * e.g. 'Whole supply chain', 'Farm', 'Harvest', 'Storage', 'Processing', 'Trader', 'Retail', ...
* loss_percentage
  * e.g. 5%, 13.5%, 43.2%...

## Data Visualization
Appologies for the small font size of the plots. I'm too lazy to rewrite the code. Please open the plot images in new windows to see better.

### Which Commodity Has The Most Food Waste?
In this section, I'll visualize the data to see loss percentages for each commodity. 
### The U.S. (Whole Supply Chain)
Let's first look at the U.S. data. I'll be looking at the "Whole suppy chain" data from 2005. 

```python
country = 'United States of America'
year = 2005
supply_stage = "Whole supply chain"
df_filtered = df[(df['country']==country) & (df['food_supply_stage'] == supply_stage) & (df['year'] > year)]

plot_order = df_filtered.groupby(by='commodity').mean().sort_values(by='loss_percentage', ascending=False).index.tolist()
fig, ax = plt.subplots(figsize=(20, 6))
plot = sns.barplot(x='commodity', y='loss_percentage', data=df_filtered, order=plot_order, ci='sd')
ax.set_xticklabels(ax.get_xticklabels(), rotation = 45, horizontalalignment='right')
ax.set_title(f"Food Loss ({supply_stage}) by Commodity in {country}, (data from {year}, vertical bars show stddev)".title())
ax.set(xlabel=None)
plt.show()
```    
![png](/files/images/others/us-food-loss-whole-supply-chain-since-2005.png)

Here are some intersting findings.
* "Grape fruit juice" has large loss percentage while "Grape fruits" has small loss percentage.
* "Mixed grain" loss is large while individual grains ("Wheat" and "Barley") losses are very small. 
* There are no data for meat. I don't see beef, pork and chicken. 

### Other Countries (Whole Supply Chain)
Here are some plots for different countries that used the same code for as the [above](#the-us-whole-supply-chain). There are more plots in my [repo](https://github.com/wondonghyeon/codes-for-blog/blob/master/food-waste/fao-flw-dataset-exploration.ipynb).
#### Canada
![png](/files/images/others/canada-food-loss-whole-supply-chain-since-2005.png)
* Canada data is very similiar to the U.S. data.
* There is "Meat of pig, fresh or chilled" commodity in Candata data, which is not found in the U.S. data.
#### Germany, Hungary, Austria

![png](/files/images/others/germany-food-loss-whole-supply-chain-since-2005.png)
![png](/files/images/others/hungary-food-loss-whole-supply-chain-since-2005.png)
![png](/files/images/others/austria-food-loss-whole-supply-chain-since-2005.png)

#### 
### Distribution Per Commodity (Whole Supply Chain)

## Which Country Produces Most Food Waste?
### Potatoes
### Wheat
### Rice
### Raw Milk of Cattle

## Limitation of the Dataset

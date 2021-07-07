# Fintech-Workspace

Housing Rental Analysis for San Francisco
In this challenge, your job is to use your data visualization superpowers, including aggregation, interactive visualizations, and geospatial analysis, to find properties in the San Francisco market that are viable investment opportunities.

Instructions:

Use the san_francisco_housing.ipynb notebook to visualize and analyze the real-estate data.

Note that this assignment requires you to create a visualization by using the integration between Plotly and the Mapbox API. Be sure to create your environment file (.env) and include your Mapbox API access token. Then import your Mapbox API access token into the san_francisco_housing.ipynb notebook, and set it by using the px.set_mapbox_access_token function.

Additionally, you need to read the sfo_neighborhoods_census_data.csv file from the Resources folder into the notebook and create the DataFrame that you’ll use in the analysis.

The main task in this Challenge is to visualize and analyze the real-estate data in your Jupyter notebook. Use the san_francisco_housing.ipynb notebook to complete the following tasks:

Calculate and plot the housing units per year.

Calculate and plot the average prices per square foot.

Compare the average prices by neighborhood.

Build an interactive neighborhood map.

Compose your data story.

Calculate and Plot the Housing Units per Year
For this part of the assignment, use numerical and visual aggregation to calculate the number of housing units per year, and then visualize the results as a bar chart. To do so, complete the following steps:

Use the groupby function to group the data by year. Aggregate the results by the mean of the groups.

Use the hvplot function to plot the housing_units_by_year DataFrame as a bar chart. Make the x-axis represent the year and the y-axis represent the housing_units.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of the resulting bar chart.

Answer the following question:

What’s the overall trend in housing units over the period that you’re analyzing?
Calculate and Plot the Average Sale Prices per Square Foot
For this part of the assignment, use numerical and visual aggregation to calculate the average prices per square foot, and then visualize the results as a bar chart. To do so, complete the following steps:

Group the data by year, and then average the results. What’s the lowest gross rent that’s reported for the years that the DataFrame includes?

Create a new DataFrame named prices_square_foot_by_year by filtering out the “housing_units” column. The new DataFrame should include the averages per year for only the sale price per square foot and the gross rent.

Use hvPlot to plot the prices_square_foot_by_year DataFrame as a line plot.

Hint This single plot will include lines for both sale_price_sqr_foot and gross_rent.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of the resulting plot.

Use both the prices_square_foot_by_year DataFrame and interactive plots to answer the following questions:

Did any year experience a drop in the average sale price per square foot compared to the previous year?

If so, did the gross rent increase or decrease during that year?

Compare the Average Sale Prices by Neighborhood
For this part of the assignment, use interactive visualizations and widgets to explore the average sale price per square foot by neighborhood. To do so, complete the following steps:

Create a new DataFrame that groups the original DataFrame by year and neighborhood. Aggregate the results by the mean of the groups.

Filter out the “housing_units” column to create a DataFrame that includes only the sale_price_sqr_foot and gross_rent averages per year.

Create an interactive line plot with hvPlot that visualizes both sale_price_sqr_foot and gross_rent. Set the x-axis parameter to the year (x="year"). Use the groupby parameter to create an interactive widget for neighborhood.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of the resulting plot.

Use the interactive visualization to answer the following question:

For the Anza Vista neighborhood, is the average sale price per square foot for 2016 more or less than the price that’s listed for 2012?
Build an Interactive Neighborhood Map
For this part of the assignment, explore the geospatial relationships in the data by using interactive visualizations with Plotly and the Mapbox API. To build your map, use the sfo_data_df DataFrame (created during the initial import), which includes the neighborhood location data with the average prices. To do all this, complete the following steps:

Read the neighborhood_coordinates.csv file from the Resources folder into the notebook, and create a DataFrame named neighborhood_locations_df. Be sure to set the index_col of the DataFrame as “Neighborhood”.

Using the original sfo_data_df Dataframe, create a DataFrame named all_neighborhood_info_df that groups the data by neighborhood. Aggregate the results by the mean of the group.

Review the two code cells that concatenate the neighborhood_locations_df DataFrame with the all_neighborhood_info_df DataFrame. Note that the first cell uses the Pandas concat function to create a DataFrame named all_neighborhoods_df. The second cell cleans the data and sets the “Neighborhood” column. Be sure to run these cells to create the all_neighborhoods_df DataFrame, which you’ll need to create the geospatial visualization.

Using Plotly Express, create a scatter_mapbox for the all_neighborhoods_df DataFrame. Remember that you need your MapBox API key. Be sure to do the following:

Set the size parameter to “sale_price_sqr_foot”.

Set the color parameter to “gross_rent”.

Set the size_max parameter to “25”.

Set the zoom parameter to “11”.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of a scatter plot created with the Mapbox API.

Use the interactive map to answer the following question:

Which neighborhood has the highest gross rent, and which has the highest sale price per square foot?
Compose Your Data Story
Based on the visualizations that you created, answer the following questions:

How does the trend in rental income growth compare to the trend in sales prices? Does this same trend hold true for all the neighborhoods across San Francisco?

What insights can you share with your company about the potential one-click, buy-and-rent strategy that they're pursuing? Do neighborhoods exist that you would suggest for investment, and why?

# Import the required libraries and dependencies
import os
import pandas as pd
import plotly.express as px
import hvplot.pandas
from pathlib import Path
from dotenv import load_dotenv
Enable your Mapbox API access token
# Load the .env file into the notebook
load_dotenv("../Challenge_6/.env.ipynb")
​
# Read in your MAPBOX_API_KEY
mapbox_api_access_token = os.getenv("mapbox_api_access_token")
​
# Confirm the availability of your Mapbox API access token by checking its type
type(mapbox_api_access_token)
​
# Set your Mapbox API access token
px.set_mapbox_access_token(mapbox_api_access_token)
​
Import the data
# Using the read_csv function and Path module, create a DataFrame 
# by importing the sfo_neighborhoods_census_data.csv file from the Resources folder
sfo_data_df = pd.read_csv(Path("../Challenge_6/sfo_neighborhoods_census_data.csv"))
​
​
# Review the first and last five rows of the DataFrame
display(sfo_data_df.head())
display(sfo_data_df.tail())
​
year	neighborhood	sale_price_sqr_foot	housing_units	gross_rent
0	2010	Alamo Square	291.182945	372560	1239
1	2010	Anza Vista	267.932583	372560	1239
2	2010	Bayview	170.098665	372560	1239
3	2010	Buena Vista Park	347.394919	372560	1239
4	2010	Central Richmond	319.027623	372560	1239
year	neighborhood	sale_price_sqr_foot	housing_units	gross_rent
392	2016	Telegraph Hill	903.049771	384242	4390
393	2016	Twin Peaks	970.085470	384242	4390
394	2016	Van Ness/ Civic Center	552.602567	384242	4390
395	2016	Visitacion Valley	328.319007	384242	4390
396	2016	Westwood Park	631.195426	384242	4390
Calculate and Plot the Housing Units per Year
For this part of the assignment, use numerical and visual aggregation to calculate the number of housing units per year, and then visualize the results as a bar chart. To do so, complete the following steps:

Use the groupby function to group the data by year. Aggregate the results by the mean of the groups.

Use the hvplot function to plot the housing_units_by_year DataFrame as a bar chart. Make the x-axis represent the year and the y-axis represent the housing_units.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of the resulting bar chart.

Answer the following question:

What’s the overall trend in housing units over the period that you’re analyzing?
Step 1: Use the groupby function to group the data by year. Aggregate the results by the mean of the groups.
# Create a numerical aggregation that groups the data by the year and then averages the results.
housing_units_by_year = (
    sfo_data_df[['year','sale_price_sqr_foot','housing_units','gross_rent']]
    .groupby('year')
    .mean()
)
​
# Review the DataFrame
housing_units_by_year.head()
​
sale_price_sqr_foot	housing_units	gross_rent
year			
2010	369.344353	372560	1239
2011	341.903429	374507	1530
2012	399.389968	376454	2324
2013	483.600304	378401	2971
2014	556.277273	380348	3528
Step 2: Use the hvplot function to plot the housing_units_by_year DataFrame as a bar chart. Make the x-axis represent the year and the y-axis represent the housing_units.
Step 3: Style and format the line plot to ensure a professionally styled visualization.
F
# Create a visual aggregation explore the housing units by year
housing_units_by_year.hvplot.bar(
     x='year',
     y='housing_units',
     title="Average Housing Units in SF by Year",
     rot=30 ).opts(yformatter='%.0f',ylim=(360000, 390000))
​
Step 5: Answer the following question:
Housing units year over year rises roughly 2,000 - 3,000 units.
**Question** What is the overall trend in housing_units over the period being analyzed?
​
** The average housing units rise steadily year over year. Housing units year over year rises roughly 2,000 - 3,000 units.
Calculate and Plot the Average Sale Prices per Square Foot
For this part of the assignment, use numerical and visual aggregation to calculate the average prices per square foot, and then visualize the results as a bar chart. To do so, complete the following steps:

Group the data by year, and then average the results. What’s the lowest gross rent that’s reported for the years that the DataFrame includes?

Create a new DataFrame named prices_square_foot_by_year by filtering out the “housing_units” column. The new DataFrame should include the averages per year for only the sale price per square foot and the gross rent.

Use hvPlot to plot the prices_square_foot_by_year DataFrame as a line plot.

Hint This single plot will include lines for both sale_price_sqr_foot and gross_rent.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of the resulting plot.

Use both the prices_square_foot_by_year DataFrame and interactive plots to answer the following questions:

Did any year experience a drop in the average sale price per square foot compared to the previous year?

If so, did the gross rent increase or decrease during that year?

Step 1: Group the data by year, and then average the results.
# Create a numerical aggregation by grouping the data by year and averaging the results
​
​
# Review the resulting DataFrame
housing_units_by_year
​
sale_price_sqr_foot	housing_units	gross_rent
year			
2010	369.344353	372560	1239
2011	341.903429	374507	1530
2012	399.389968	376454	2324
2013	483.600304	378401	2971
2014	556.277273	380348	3528
2015	632.540352	382295	3739
2016	697.643709	384242	4390
Question What is the lowest gross rent reported for the years included in the DataFrame?

Answer The lowest gross rent reported is 1239 in the year 2010.

Step 2: Create a new DataFrame named prices_square_foot_by_year by filtering out the “housing_units” column. The new DataFrame should include the averages per year for only the sale price per square foot and the gross rent.
# Filter out the housing_units column, creating a new DataFrame 
# Keep only sale_price_sqr_foot and gross_rent averages per year
prices_square_foot_by_year = housing_units_by_year.drop(columns=['housing_units'])
​
# Review the DataFrame
prices_square_foot_by_year
​
sale_price_sqr_foot	gross_rent
year		
2010	369.344353	1239
2011	341.903429	1530
2012	399.389968	2324
2013	483.600304	2971
2014	556.277273	3528
2015	632.540352	3739
2016	697.643709	4390
Step 3: Use hvPlot to plot the prices_square_foot_by_year DataFrame as a line plot.
Hint This single plot will include lines for both sale_price_sqr_foot and gross_rent

Step 4: Style and format the line plot to ensure a professionally styled visualization.
# Plot prices_square_foot_by_year. 
# Inclued labels for the x- and y-axes, and a title.
prices_vs_rent = prices_square_foot_by_year.hvplot(
    x='year',
    y=['sale_price_sqr_foot','gross_rent']
)
​
plot_prices_vs_rent=prices_vs_rent.opts(
    title="Home Sale Prices vs. Rent in San Francisco by Year",
    xlabel='Year',
    ylabel='USD',
    yformatter='%.0f'
)
​
plot_prices_vs_rent
Step 6: Use both the prices_square_foot_by_year DataFrame and interactive plots to answer the following questions:
**Question** * Did any year experience a drop in the average sale price per square foot compared to the previous year?
​
**Answer** 2010 was the only year that had a very minor decay in sale price per square foot. All the other years had growth.
sale price per suare foot went down!
**Question** * If so, did the gross rent increase or decrease during that year?I
​
**Answer** The gross rent always increased every year including in 2010. It went up even though the sale price per suare foot went down!
Compare the Average Sale Prices by Neighborhood
For this part of the assignment, use interactive visualizations and widgets to explore the average sale price per square foot by neighborhood. To do so, complete the following steps:

Create a new DataFrame that groups the original DataFrame by year and neighborhood. Aggregate the results by the mean of the groups.

Filter out the “housing_units” column to create a DataFrame that includes only the sale_price_sqr_foot and gross_rent averages per year.

Create an interactive line plot with hvPlot that visualizes both sale_price_sqr_foot and gross_rent. Set the x-axis parameter to the year (x="year"). Use the groupby parameter to create an interactive widget for neighborhood.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of the resulting plot.

Use the interactive visualization to answer the following question:

For the Anza Vista neighborhood, is the average sale price per square foot for 2016 more or less than the price that’s listed for 2012?
Step 1: Create a new DataFrame that groups the original DataFrame by year and neighborhood. Aggregate the results by the mean of the groups.
# Group by year and neighborhood and then create a new dataframe of the mean values
prices_by_year_by_neighborhood = sfo_data_df.groupby(['year', 'neighborhood']).mean()
​
# Review the DataFrame
prices_by_year_by_neighborhood.head()
​
sale_price_sqr_foot	housing_units	gross_rent
year	neighborhood			
2010	Alamo Square	291.182945	372560	1239
Anza Vista	267.932583	372560	1239
Bayview	170.098665	372560	1239
Buena Vista Park	347.394919	372560	1239
Central Richmond	319.027623	372560	1239
Step 2: Filter out the “housing_units” column to create a DataFrame that includes only the sale_price_sqr_foot and gross_rent averages per year.
# Filter out the housing_units
prices_by_year_by_neighborhood = prices_by_year_by_neighborhood.drop(columns = ['housing_units'])
​
# Review the first and last five rows of the DataFrame
display(prices_by_year_by_neighborhood.head())
display(prices_by_year_by_neighborhood.tail())
​
sale_price_sqr_foot	gross_rent
year	neighborhood		
2010	Alamo Square	291.182945	1239
Anza Vista	267.932583	1239
Bayview	170.098665	1239
Buena Vista Park	347.394919	1239
Central Richmond	319.027623	1239
sale_price_sqr_foot	gross_rent
year	neighborhood		
2016	Telegraph Hill	903.049771	4390
Twin Peaks	970.085470	4390
Van Ness/ Civic Center	552.602567	4390
Visitacion Valley	328.319007	4390
Westwood Park	631.195426	4390
Step 3: Create an interactive line plot with hvPlot that visualizes both sale_price_sqr_foot and gross_rent. Set the x-axis parameter to the year (x="year"). Use the groupby parameter to create an interactive widget for neighborhood.
Step 4: Style and format the line plot to ensure a professionally styled visualization.
# Use hvplot to create an interactive line plot of the average price per square foot
# The plot should have a dropdown selector for the neighborhood
price_per_sq_foot= sfo_data_df.hvplot(
    x='year',
    y=['sale_price_sqr_foot','gross_rent'],
    groupby='neighborhood',
    title = "SF Home Selling Prices vs. Rent by Neighborhood",
    legend="top_left"
)
​
price_per_sq_foot
​
neighborhood

Outer Mission
Step 6: Use the interactive visualization to answer the following question:
**Question** For the Anza Vista neighborhood, is the average sale price per square foot for 2016 more or less than the price that’s listed for 2012? 
​
**Answer** For the Anza Vista neighborhood, the sale price in per square foot in 2012 was 344.49. The averages sale price per square foot in 2016 was 88.40. The average sale price per square foot is lower in 2016 than it was in 2012.
Build an Interactive Neighborhood Map
For this part of the assignment, explore the geospatial relationships in the data by using interactive visualizations with Plotly and the Mapbox API. To build your map, use the sfo_data_df DataFrame (created during the initial import), which includes the neighborhood location data with the average prices. To do all this, complete the following steps:

Read the neighborhood_coordinates.csv file from the Resources folder into the notebook, and create a DataFrame named neighborhood_locations_df. Be sure to set the index_col of the DataFrame as “Neighborhood”.

Using the original sfo_data_df Dataframe, create a DataFrame named all_neighborhood_info_df that groups the data by neighborhood. Aggregate the results by the mean of the group.

Review the two code cells that concatenate the neighborhood_locations_df DataFrame with the all_neighborhood_info_df DataFrame. Note that the first cell uses the Pandas concat function to create a DataFrame named all_neighborhoods_df. The second cell cleans the data and sets the “Neighborhood” column. Be sure to run these cells to create the all_neighborhoods_df DataFrame, which you’ll need to create the geospatial visualization.

Using Plotly Express, create a scatter_mapbox for the all_neighborhoods_df DataFrame. Remember that you need your MapBox API key. Be sure to do the following:

Set the size parameter to “sale_price_sqr_foot”.

Set the color parameter to “gross_rent”.

Set the size_max parameter to “25”.

Set the zoom parameter to “11”.

Style and format the line plot to ensure a professionally styled visualization.

Note that your resulting plot should appear similar to the following image:

A screenshot depicts an example of a scatter plot created with the Mapbox API.

Use the interactive map to answer the following question:

Which neighborhood has the highest gross rent, and which has the highest sale price per square foot?
Step 1: Read the neighborhood_coordinates.csv file from the Resources folder into the notebook, and create a DataFrame named neighborhood_locations_df. Be sure to set the index_col of the DataFrame as “Neighborhood”.
.
# Load neighborhoods coordinates data
neighborhood_locations_df = pd.read_csv(Path('../Challenge_6/neighborhoods_coordinates.csv'), index_col='Neighborhood')
​
# Review the DataFrame
neighborhood_locations_df
​
Lat	Lon
Neighborhood		
Alamo Square	37.791012	-122.402100
Anza Vista	37.779598	-122.443451
Bayview	37.734670	-122.401060
Bayview Heights	37.728740	-122.410980
Bernal Heights	37.728630	-122.443050
...	...	...
West Portal	37.740260	-122.463880
Western Addition	37.792980	-122.435790
Westwood Highlands	37.734700	-122.456854
Westwood Park	37.734150	-122.457000
Yerba Buena	37.792980	-122.396360
73 rows × 2 columns

Step 2: Using the original sfo_data_df Dataframe, create a DataFrame named all_neighborhood_info_df that groups the data by neighborhood. Aggregate the results by the mean of the group.
# Calculate the mean values for each neighborhood
all_neighborhood_info_df = sfo_data_df.rename(columns={"neighborhood": "Neighborhood" })
all_neighborhood_info_df = all_neighborhood_info_df.groupby('Neighborhood').mean().drop(columns=['year'])
​
# Review the resulting DataFrame
all_neighborhood_info_df
​
sale_price_sqr_foot	housing_units	gross_rent
Neighborhood			
Alamo Square	366.020712	378401.00	2817.285714
Anza Vista	373.382198	379050.00	3031.833333
Bayview	204.588623	376454.00	2318.400000
Bayview Heights	590.792839	382295.00	3739.000000
Bernal Heights	576.746488	379374.50	3080.333333
...	...	...	...
West Portal	498.488485	376940.75	2515.500000
Western Addition	307.562201	377427.50	2555.166667
Westwood Highlands	533.703935	376454.00	2250.500000
Westwood Park	687.087575	382295.00	3959.000000
Yerba Buena	576.709848	377427.50	2555.166667
73 rows × 3 columns

Step 3: Review the two code cells that concatenate the neighborhood_locations_df DataFrame with the all_neighborhood_info_df DataFrame.
Note that the first cell uses the Pandas concat function to create a DataFrame named all_neighborhoods_df.

The second cell cleans the data and sets the “Neighborhood” column.

Be sure to run these cells to create the all_neighborhoods_df DataFrame, which you’ll need to create the geospatial visualization.

# Using the Pandas `concat` function, join the 
# neighborhood_locations_df and the all_neighborhood_info_df DataFrame
# The axis of the concatenation is "columns".
# The concat function will automatially combine columns with
# identical information, while keeping the additional columns.
all_neighborhoods_df = pd.concat(
    [neighborhood_locations_df, all_neighborhood_info_df], 
    axis="columns",
    sort=False
)
​
# Review the resulting DataFrame
display(all_neighborhoods_df.head())
display(all_neighborhoods_df.tail())
​
Lat	Lon	sale_price_sqr_foot	housing_units	gross_rent
Alamo Square	37.791012	-122.402100	366.020712	378401.0	2817.285714
Anza Vista	37.779598	-122.443451	373.382198	379050.0	3031.833333
Bayview	37.734670	-122.401060	204.588623	376454.0	2318.400000
Bayview Heights	37.728740	-122.410980	590.792839	382295.0	3739.000000
Bernal Heights	37.728630	-122.443050	NaN	NaN	NaN
Lat	Lon	sale_price_sqr_foot	housing_units	gross_rent
Yerba Buena	37.79298	-122.39636	576.709848	377427.5	2555.166667
Bernal Heights	NaN	NaN	576.746488	379374.5	3080.333333
Downtown	NaN	NaN	391.434378	378401.0	2817.285714
Ingleside	NaN	NaN	367.895144	377427.5	2509.000000
Outer Richmond	NaN	NaN	473.900773	378401.0	2817.285714
# Call the dropna function to remove any neighborhoods that do not have data
all_neighborhoods_df = all_neighborhoods_df.reset_index().dropna()
​
# Rename the "index" column as "Neighborhood" for use in the Visualization
all_neighborhoods_df = all_neighborhoods_df.rename(columns={"index": "Neighborhood"})
​
# Review the resulting DataFrame
display(all_neighborhoods_df.head())
display(all_neighborhoods_df.tail())
Neighborhood	Lat	Lon	sale_price_sqr_foot	housing_units	gross_rent
0	Alamo Square	37.791012	-122.402100	366.020712	378401.0	2817.285714
1	Anza Vista	37.779598	-122.443451	373.382198	379050.0	3031.833333
2	Bayview	37.734670	-122.401060	204.588623	376454.0	2318.400000
3	Bayview Heights	37.728740	-122.410980	590.792839	382295.0	3739.000000
5	Buena Vista Park	37.768160	-122.439330	452.680591	378076.5	2698.833333
Neighborhood	Lat	Lon	sale_price_sqr_foot	housing_units	gross_rent
68	West Portal	37.74026	-122.463880	498.488485	376940.75	2515.500000
69	Western Addition	37.79298	-122.435790	307.562201	377427.50	2555.166667
70	Westwood Highlands	37.73470	-122.456854	533.703935	376454.00	2250.500000
71	Westwood Park	37.73415	-122.457000	687.087575	382295.00	3959.000000
72	Yerba Buena	37.79298	-122.396360	576.709848	377427.50	2555.166667
Step 4: Using Plotly Express, create a scatter_mapbox for the all_neighborhoods_df DataFrame. Remember that you need your MapBox API key. Be sure to do the following:
* Set the `size` parameter to “sale_price_sqr_foot”.
* Set the `color` parameter to “gross_rent”.
* Set the `size_max` parameter to “25”.
* Set the `zoom` parameter to “11”.
Step 5: Style and format the line plot to ensure a professionally styled visualization.
# Create a scatter mapbox to analyze neighborhood info
px.scatter_mapbox(
     all_neighborhoods_df,
     lat='Lat',
     lon='Lon',
     size='sale_price_sqr_foot',
     color='gross_rent',
     zoom=11,
     size_max=25,
     text='Neighborhood'
)
​
Step 7: Use the interactive map to answer the following question:
**Question** Which neighborhood has the highest gross rent, and which has the highest sale price per square foot?
​
**Answer** The neighborhood with the highest gross rent is Westwood Part and the neighborhood with the highest sale price per square foot is Union Square District.
Compose Your Data Story
Based on the visualizations that you have created, compose a data story that synthesizes your analysis by answering the following questions:

**Question**  How does the trend in rental income growth compare to the trend in sales prices? Does this same trend hold true for all the neighborhoods across San Francisco?
​
**Answer** Gross rents always went up year by year in all the neighborhoods. Sales prices didn't always go up each year in all the neighboorhods. Even when the sale price went down in neighborhoods gross rental prices still went up. Not all neighborhoods had sale price increases. Same varied by year for when sale prices went down and up. Gross rent always went up in all neighborhoods every year.
​
Question What insights can you share with your company about the potential one-click, buy-and-rent strategy that they're pursuing? Do neighborhoods exist that you would suggest for investment, and why?

Answer Outter mission has the best buy and rent strategy. The rent to price ratio is the best compared to all the other neighborhoods.

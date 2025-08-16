# Covid-19-
import pandas as pd

# Load the dataset from the JHU repository
url = 'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv'
df = pd.read_csv(url)

# Display the first few rows of the dataset
print("First few rows of the dataset:")
print(df.head())

# Data Cleaning
# Melt the DataFrame to have a long format
df_melted = df.melt(id_vars=['Province/State', 'Country/Region', 'Lat', 'Long'],
                    var_name='Date', value_name='Confirmed Cases')

# Convert the 'Date' column to datetime format
df_melted['Date'] = pd.to_datetime(df_melted['Date'])

# Group by date and country to get total confirmed cases
df_grouped = df_melted.groupby(['Date', 'Country/Region'])['Confirmed Cases'].sum().reset_index()

# Display the cleaned and grouped data
print("\nGrouped data (total confirmed cases by date and country):")
print(df_grouped.head())

# Example: Filter data for a specific country (e.g., United States)
us_data = df_grouped[df_grouped['Country/Region'] == 'US']

# Display the US data
print("\nCOVID-19 data for the United States:")
print(us_data.head())


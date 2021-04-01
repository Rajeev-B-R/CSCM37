### Visualization 5
**Aim (aim):** In this visualization, we see that number of records for plotting a bounded area for pleiades in four differnt plots.

**Visual Design Type (vistype):** Interactive Crossfilter

**Image:** 
- - -
![Visualization 5](https://github.com/Rajeev-B-R/CSCM37/blob/main/4%20-%20interactive%20crossfilter.gif?raw=true)

Source Code
```python
import altair as alt
import pandas as pd
from vega_datasets import data
alt.data_transformers.disable_max_rows()

places_data_url = 'https://raw.githubusercontent.com/SwanseaU-TTW/csc337_coursework1/master/pleiades-places-latest.csv'
places_data = pd.read_csv(places_data_url)
bbox = places_data['bbox'].str.split(",", n = 3, expand = True)
bbox.columns = ['minimum longitude','minimum latitude','maximum longitude','maximum latitude']

brush = alt.selection(type = 'interval', encodings = ['x'])

base = alt.Chart().mark_line().encode(
    x = alt.X(alt.repeat('column'), type = 'quantitative', bin = alt.Bin(maxbins = 20)),
    y = 'count()'
).properties(
    width = 160,
    height = 130
)

background = base.encode(
    color = alt.value('#ddd')
).add_selection(brush)

highlight = base.transform_filter(brush)

alt.layer(
    background,
    highlight,
    data = bbox
).repeat(column = ['minimum longitude','minimum latitude','maximum longitude','maximum latitude'])
```

**Visual Mappings (vismapping):** The concept was to identify number of records and compare the occurrences of most two ends of the bounded area. Altair is used for creating this visualization with the help of repeat functions we are able to make the four differnt plots to make an interactive crossfilter. Interactivity is added to chart for comparing number of records for each location coordinate. Y axis is taken for plotting the count of records and geo coordinate points are plotted on X axis. X axis values are binned for avoiding minor observation errors.

**Data Preparation (dataprep):** The required data is present in the column bbox in the file pleiades-places-latest.csv. The challenge was to separate values of bbox to different columns in a new dataframe so that we could plot directly from that dataframe. Pandas library functions are used for reading the data from url and python's split function is used for separating the content in this column. After splitting, appropriate column headings are given. 

**Observations:** Minimum latitude and minimum longitude which represent the bottom right corner of the bounded area has more records of data when longitude between -20 to 60. At the same time, minimum latitude has more records when the values in between 20 and 60, and has more than 10000 records at approximately 40. Maximum latitude and longitude have the similar range of records like in minimum. Analysing the data, we understood that the geographical coordinates are separated by comma.

**Improvements (improvements):** Plotting latitude and longitude value of location along with bbox would give us the relation between bounded area and location. Hence, it woud be a precise location.

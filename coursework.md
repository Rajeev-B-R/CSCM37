### Visualization 1

**Visual Design Type (vistype):** A chloropleth map: geographical shape, scatter-cum-bar chart and point plot.

**Image:** 
- - -
![Visualization 1](https://github.com/Rajeev-B-R/CSCM37/blob/main/5%20-%20chloropleth%20map.png?raw=true)

![Visualization 1](https://github.com/Rajeev-B-R/CSCM37/blob/main/6%20-%20point%20and%20bar%20chart.png?raw=true)

![Visualization 1](https://github.com/Rajeev-B-R/CSCM37/blob/main/7%20-%20bar%20chart.png?raw=true)

![Visualization 1](https://github.com/Rajeev-B-R/CSCM37/blob/main/8%20-%20point%20chart.png?raw=true)

Source Code
```python
import altair as alt
import pandas as pd
import numpy as np
from vega_datasets import data

pleiades_loc = pd.read_csv('https://raw.githubusercontent.com/SwanseaU-TTW/csc337_coursework1/master/pleiades-places-latest.csv')  

pleiades_loc.head()

pleiades_loc['minDate']

pleiades_loc.dtypes

pleiades_loc.info()

pleiades_loc = pleiades_loc.dropna()

points = alt.Chart(pleiades_loc).mark_circle().encode(
    longitude = 'reprLong:Q',
    latitude = 'reprLat:Q',
    color = 'featureType:N',
    size = alt.value(10),
    tooltip = 'id'
).project(
    "equalEarth"
).properties(
    width = 500,
    height = 400
)

countries = alt.topo_feature(data.world_110m.url, 'countries')

background = alt.Chart(countries).mark_geoshape(
    fill = 'lightgray',
    stroke = 'white'
).project(
    "equalEarth"
).properties(
    width = 500,
    height = 400
)

background + points

ts_data = pd.to_datetime(pleiades_loc['created'])
pleiades_loc['Ts_data'] = pd.Series(ts_data, index = pleiades_loc.index)

chart1 = alt.Chart(pleiades_loc).mark_point().encode(
    alt.X('monthdate(Ts_data):O', title = 'date'),
    alt.Y('creators:N', title = 'AUTHORS'),
).properties(
    height = 500,
    width = 300
)

chart2 = alt.Chart(pleiades_loc).mark_bar().encode(
    x = 'count()',
    y = alt.Y('creators:N', title = 'AUTHORS'),
    
).properties(
    height = 500,
    width = 300
)

chart1|chart2

pleiades_loc['range_time'] = pleiades_loc['minDate'] + pleiades_loc['maxDate']

y_axis = alt.Axis(
    title = 'FeatureType',
    ticks = False,
    domain = False
)

alt.Chart(pleiades_loc).mark_bar().encode(
    x = 'minDate:Q',
    x2 = 'maxDate:Q',
    y = alt.Y('timePeriodsKeys:N', axis = y_axis),
    color = 'range_time:Q'
)
```

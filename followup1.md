### Visualization 2
**Aim (aim):** The purpose of this visualization is to find the geographical position of the object by mapping its latitude and longitude including the version. With this, we infer what kind of feature type is existing.
**Visual Design Type (vistype):** Scatter Plot

**Image:** 
- - -
![Visualization 2](https://github.com/Rajeev-B-R/CSCM37/blob/main/1%20-%20scatter%20plot.png?raw=true)

Source Code
```python
import altair as alt
import pandas as pd
alt.data_transformers.disable_max_rows()

places_data_url = 'https://raw.githubusercontent.com/SwanseaU-TTW/csc337_coursework1/master/pleiades-places-latest.csv'
places_data = pd.read_csv(places_data_url)

selector = alt.selection_single(empty = 'all', fields = ['X','Y'])
base_main = alt.Chart(places_data, title = 'Geographical Location').properties(
    width = 700,
    height = 350
).add_selection(selector)

geo_points = base_main.mark_circle().encode(
    alt.X('reprLat',title = "Latitude in degrees N",
          scale = alt.Scale(domain = (-30, 70))),
    alt.Y('reprLong',title = "Longitude in degrees E",
          scale = alt.Scale(domain = (-20, 120))),
    alt.Color('currentVersion', scale = alt.Scale(scheme = 'yelloworangered')),
    tooltip = ['reprLat', 'reprLong', 'currentVersion', 'featureTypes', 'timePeriods']).interactive()

geo_points
```

**Visual Mappings (vismapping):** The concept is to visualize the objects for their different versions along with geographical locations with the help of latitude and longitude from the data. This is done by plotting the latitude on X axis and longitude on Y axis. Next, we plot versions of each entry and be able to make the color factor to define the versions. More instensity implies latest version. An interactive element is made by giving a tooltip for every points to display the details including feature types and timeperiod.

**Data Preparation (dataprep):** Data is taken from pleiades-places-latest.csv. It has fields for latitude and longitude to plot the location and a field for storing version. To identify feature type of that location, data was taken from featureTypes and timePeriods and used for plotting time period into the tooltip.

**Observations:** Here, we see most of the data points are on south-east part of the chart and there are outliers around the cluster.

**Improvements (improvements):** Time periods and feature types could be specifically given. For the feature types, a unique small icon for every points. 




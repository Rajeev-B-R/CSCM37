### Visualization 3
**Aim (aim):** Here, we see information regarding six known creators and their respective records in different time periods and versions. The precision of locations that they plotted are also communicating to the user. From the plot we could easily infer that most of the records are referred by its location. When the version increases the location is more precise. 

**Visual Design Type (vistype):** Multi Feature Scatter Plot

**Image:** 
- - -
![Visualization 3](https://github.com/Rajeev-B-R/CSCM37/blob/main/2%20-%20multi%20feature%20scatter%20plot.png?raw=true)

Source Code
```python
import altair as alt
import pandas as pd
from vega_datasets import data
alt.data_transformers.disable_max_rows()

places_data_url = 'https://raw.githubusercontent.com/SwanseaU-TTW/csc337_coursework1/master/pleiades-places-latest.csv'
places_data = pd.read_csv(places_data_url)

df1 = pd.DataFrame(places_data)
df1_selected_columns = df1[['id','locationPrecision','timePeriods','creators','featureTypes','minDate','maxDate','currentVersion']]
df2 = df1_selected_columns.copy()

creator_avarveri = df2.loc[df2['creators'].isin(['avarveri'])]
creator_mjredondo = df2.loc[df2['creators'].isin(['mjredondo'])]
creator_vvitale = df2.loc[df2['creators'].isin(['vvitale'])]
creator_spann = df2.loc[df2['creators'].isin(['P.O. Spann'])]
creator_euzennat = df2.loc[df2['creators'].isin(['M. Euzennat'])]
creator_potter = df2.loc[df2['creators'].isin(['T.W. Potter'])]

frames = [creator_avarveri, creator_mjredondo, creator_vvitale, creator_spann, creator_euzennat, creator_potter]
creators = pd.concat(frames)

creators

source = creators

alt.Chart(source).mark_circle().encode(
    alt.X('timePeriods', scale = alt.Scale(zero = False)),
    alt.Y('currentVersion', scale = alt.Scale(zero = False, padding = 1)),
    color = 'creators',
    size = 'locationPrecision'
)
```

**Visual Mappings (vismapping):** The visualization is created by scatter plot with multiple features in it. The x and y axes are mapped to time periods and current version respectively. The size of the circle is mapped to location precision and color is mapped to creators. There are unique colors for each creator. A lot of different time periods available in data frame prompted us to plot time frame in X axis.

**Data Preparation (dataprep):** The creator data  has been filtered to select six known creators from the whole data in pleiades-places-latest.csv. The selected creators are Avarveri, Mjredondo, Vvitale, P.O. Spann, M. Euzennat and T.W. Potter. A new data frame is created and filtered the following columns: 'id', 'locationPrecision', 'timePeriods', 'creators', 'featureTypes', 'minDate', 'maxDate', 'currentVersion'. Next, we filter the selected six creators and join them together. Six different data frames are created for creators and concat() method from pandas library was used for concatenating the frames together.

**Observations:** Vvitale has only one unlocated data and its in the version 0. According to the visualisation T.W. Potter has more number of unlocated data and when version increases the the data had been more precised. Precise locations are hard to notice.

**Improvements (improvements):** Some data are overlapping and this makes it difficult to identify which creator's data is the point. Time Periods could be mapped to colors.



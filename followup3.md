### Visualization 4

**Visual Design Type (vistype):** Scatter plot with configurable point shapes.

**Image:** 
- - -
![Visualization 4](https://github.com/Rajeev-B-R/CSCM37/blob/main/3%20-%20scatter%20plot%20with%20point.png?raw=true)

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

df2 = df2.loc[df2['timePeriods'].isin(['M', 'HM', 'RM', 'R'])]
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

alt.Chart(source).mark_point().encode(
    alt.X('currentVersion', scale = alt.Scale(zero = False)),
    y = 'locationPrecision',
    color = 'timePeriods',
    facet = alt.Facet('creators', columns = 2),
).properties(
    width = 200,
    height = 100,
)
```

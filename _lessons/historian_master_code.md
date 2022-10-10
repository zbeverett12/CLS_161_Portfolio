---
layout: page
title: Visualizing Data with Bokeh and Pandas
description: In this lesson you will learn how to visually explore and present data in Python by using the Bokeh and Pandas libraries.
---

## Source
Charlie Harper, "Visualizing Data with Bokeh and Pandas," Programming Historian 7 (2018), https://doi.org/10.46430/phen0081.

## Bokeh and Pandas: Exploring the WWII THOR Dataset
### My First Plot


```python
#my_first_plot

#Prints figure into output rather than opening a new tab 
#Source: https://stackoverflow.com/questions/46893131/bokeh-not-showing-in-jupyter-notebook/62534728#62534728?newreg=cae038d324bf40feb63b1905f8591d5c
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

#Start lesson creates a figure using my own values 
from bokeh.plotting import figure, show

#My values, see plotted below, they get flipped for triangles
x = [1, 3, 5, 7]
y = [2, 4, 6, 8]

p = figure()

p.circle(x, y, size = 10, color = 'red', legend_label = 'circle')
p.line(x, y, color = 'blue', legend_label = 'line')
p.triangle(y, x, color = 'gold', size = 10, legend_label = 'triangle')

p.legend.click_policy= 'hide'
show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1001">Loading BokehJS ...</span>
</div>











<div class="bk-root" id="b9a70ad4-fdd8-4417-973f-d43c509f7dc9" data-root-id="1003"></div>





### Loading Data in Pandas


```python
#loading_data
import pandas as pd
df = pd.read_csv("thor_wwii.csv")

print(df)
```

               MSNDATE      THEATER COUNTRY_FLYING_MISSION    NAF   UNIT_ID  \
    0       03/30/1941          ETO          GREAT BRITAIN    RAF   84 SQDN   
    1       11/24/1940          ETO          GREAT BRITAIN    RAF  211 SQDN   
    2       12/04/1940          ETO          GREAT BRITAIN    RAF  211 SQDN   
    3       12/31/1940          ETO          GREAT BRITAIN    RAF  211 SQDN   
    4       01/06/1941          ETO          GREAT BRITAIN    RAF  211 SQDN   
    ...            ...          ...                    ...    ...       ...   
    178276  08/01/1945          PTO                    USA  20 AF     73 BW   
    178277  07/22/1942          MTO          GREAT BRITAIN    RAF       NaN   
    178278  08/17/1940  EAST AFRICA          GREAT BRITAIN    RAF   47 SQDN   
    178279  08/06/1945          PTO                    USA  20 AF    509 CG   
    178280  08/09/1945          PTO                    USA  20 AF    509 CG   
    
           AIRCRAFT_NAME  AC_ATTACKING TAKEOFF_BASE TAKEOFF_COUNTRY  \
    0           BLENHEIM          10.0          NaN             NaN   
    1           BLENHEIM           9.0          NaN             NaN   
    2           BLENHEIM           9.0          NaN             NaN   
    3           BLENHEIM           9.0          NaN             NaN   
    4           BLENHEIM           9.0          NaN             NaN   
    ...              ...           ...          ...             ...   
    178276           B29          99.0          NaN             NaN   
    178277      BLENHEIM           NaN          NaN             NaN   
    178278     WELLESLEY           6.0      ERKOWIT           SUDAN   
    178279           B29           1.0          NaN             NaN   
    178280           B29           1.0          NaN             NaN   
    
            TAKEOFF_LATITUDE  TAKEOFF_LONGITUDE TGT_COUNTRY  TGT_LOCATION  \
    0                    NaN                NaN     ALBANIA       ELBASAN   
    1                    NaN                NaN     ALBANIA       DURAZZO   
    2                    NaN                NaN     ALBANIA      TEPELENE   
    3                    NaN                NaN     ALBANIA        VALONA   
    4                    NaN                NaN     ALBANIA        VALONA   
    ...                  ...                ...         ...           ...   
    178276               NaN                NaN       JAPAN        TOYAMA   
    178277               NaN                NaN       EGYPT  MERSA MATRUH   
    178278             18.75               37.0       SUDAN       KASSALA   
    178279               NaN                NaN       JAPAN     HIROSHIMA   
    178280               NaN                NaN       JAPAN      NAGASAKI   
    
            TGT_LATITUDE  TGT_LONGITUDE  TONS_HE  TONS_IC  TONS_FRAG  TOTAL_TONS  
    0          41.100000      20.070000      0.0      0.0        0.0         0.0  
    1          41.320000      19.450000      0.0      0.0        0.0         0.0  
    2          40.300000      20.020000      0.0      0.0        0.0         0.0  
    3          40.470000      19.490000      0.0      0.0        0.0         0.0  
    4          40.470000      19.490000      0.0      0.0        0.0         0.0  
    ...              ...            ...      ...      ...        ...         ...  
    178276     36.700000     137.216667      0.0    999.0        0.0       999.0  
    178277     31.330000      27.200000      0.0      0.0        0.0      1300.0  
    178278     15.450000      36.400000   4750.0      0.0        0.0      4750.0  
    178279     34.400000     132.466667  15000.0      0.0        0.0     15000.0  
    178280     32.733333     129.866667  20000.0      0.0        0.0     20000.0  
    
    [178281 rows x 19 columns]


### The Bokeh ColumnDataSource


```python
#column_datasource

#To visualize in Juypter output 
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

import pandas as pd 
from bokeh.plotting import figure, show
from bokeh.models import ColumnDataSource
from bokeh.models.tools import HoverTool

df = pd.read_csv("thor_wwii.csv")

sample = df.sample(50)
source = ColumnDataSource(sample)

p = figure()
p.circle(x = "TOTAL_TONS", y = "AC_ATTACKING", source = source, size = 10, color = "green")

p.title.text = "Attacking Aircraft and Munitions Dropped"
p.xaxis.axis_label = "Tons of Munitions Dropped"
p.yaxis.axis_label = "Number of Attacking Airfract"

hover = HoverTool()
hover.tooltips = [
    ("Attack Date", "@MSNDATE"),
    ("Attacking Aircraft", "@AC_Attacking"),
    ("Tons of Munitions", "@TOTAL_TONS"),
    ("Type of Aircraft", "@AIRCRAFT_NAME")
]

p.add_tools(hover)

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1185">Loading BokehJS ...</span>
</div>











<div class="bk-root" id="c377edd1-68ac-49f9-8d29-534d9faaa4e3" data-root-id="1187"></div>





## Categorical Data and Bar Charts: Munitions Dropped by Country


```python
#munitions_by_country

#To visualize in Juypter output 
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

import pandas as pd 
from bokeh.plotting import figure, show
from bokeh.models import ColumnDataSource
from bokeh.models.tools import HoverTool
from bokeh.palettes import Spectral5
from bokeh.transform import factor_cmap

df = pd.read_csv("thor_wwii.csv")

grouped = df.groupby('COUNTRY_FLYING_MISSION')['TOTAL_TONS', 'TONS_HE', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = grouped / 1000

source = ColumnDataSource(grouped)
countries = source.data["COUNTRY_FLYING_MISSION"].tolist()
p = figure(x_range = countries)

color_map = factor_cmap(field_name = "COUNTRY_FLYING_MISSION", palette = Spectral5, factors = countries)
p.vbar(x = "COUNTRY_FLYING_MISSION", top = "TOTAL_TONS", source = source, width = 0.70, color = color_map)


p.title.text = "Munitions Dropped by Allied Country"
p.xaxis.axis_label = "Country"
p.yaxis.axis_label = "Kilotons of Munitions"

hover = HoverTool()
hover.tooltips = [
    ("Totals", "@TONS_HE High Explosive / @TONS_IC Incendiary / @TONS_FRAG Fragmentation")]

hover.mode = "vline"
p.add_tools(hover)

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1308">Loading BokehJS ...</span>
</div>




    /var/folders/3f/sl59rz9n52g9fs2vwzb49_5m0000gn/T/ipykernel_40492/718895185.py:18: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby('COUNTRY_FLYING_MISSION')['TOTAL_TONS', 'TONS_HE', 'TONS_IC', 'TONS_FRAG'].sum()









<div class="bk-root" id="d2ce30d8-89eb-47dd-a37a-76a3ab318b06" data-root-id="1310"></div>





## Stacked Bar Charts and Sub-sampling Data: Types of Munitions Dropped by Country 


```python
#To visualize in Juypter output 
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

import pandas as pd 
from bokeh.plotting import figure, show 
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3

df = pd.read_csv("Thor_wwii.csv")

filter = df["COUNTRY_FLYING_MISSION"].isin(("USA", "GREAT BRITAIN"))
df = df[filter]

#tons --> kilotons 
grouped = df.groupby("COUNTRY_FLYING_MISSION")["TONS_IC", "TONS_FRAG", "TONS_HE"].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)
countries = source.data["COUNTRY_FLYING_MISSION"].tolist()
p = figure(x_range = countries)

p.vbar_stack(stackers = ["TONS_HE", "TONS_FRAG", "TONS_IC"],
            x = "COUNTRY_FLYING_MISSION", source = source,
            legend = ["High Explosive", "Fragmentation", "Incendiary"],
            width = 0.5, color = Spectral3)

p.title.text = "Types of Munitions Dropped by Allied Country"
p.legend.location = "top_left"
p.xaxis.axis_label = "Country"
p.yaxis.axis_label = "Kilotons of Munitions"

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1442">Loading BokehJS ...</span>
</div>




    /var/folders/3f/sl59rz9n52g9fs2vwzb49_5m0000gn/T/ipykernel_40492/903732979.py:18: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby("COUNTRY_FLYING_MISSION")["TONS_IC", "TONS_FRAG", "TONS_HE"].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="730e7520-4703-43bc-9093-e4514cc351fa" data-root-id="1444"></div>





## Categorical Data and Bar Charts: Munitions Dropped by Country

### Time-Series and Annotations: Bombing Operations over Time


```python
#To visualize in Juypter output 
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

import pandas as pd
from bokeh.plotting import figure, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3

df = pd.read_csv("thor_wwii.csv")

df["MSNDATE"] = pd.to_datetime(df["MSNDATE"], format = "%m/%d/%Y")

grouped = df.groupby("MSNDATE")["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type = "datetime")

p.line(x = "MSNDATE", y = "TOTAL_TONS", line_width = 2, source = source, legend = "All Munitions")
p.line(x = "MSNDATE", y = "TONS_FRAG", line_width = 2, source = source, color = Spectral3[1], legend = "Fragmentation") 
p.line(x = "MSNDATE", y = "TONS_IC", line_width = 2, source = source, color = Spectral3[2], legend = "Incendiary")

p.yaxis.axis_label = "Kilotons of Munitions Dropped"

show(p)

```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1639">Loading BokehJS ...</span>
</div>




    /var/folders/3f/sl59rz9n52g9fs2vwzb49_5m0000gn/T/ipykernel_40492/3787246016.py:16: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby("MSNDATE")["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="53c7e304-a68e-49fb-80bd-26a5e258f5d5" data-root-id="1641"></div>





### Resampling Time-Series Data


```python
#To visualize in Juypter output 
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

import pandas as pd
from bokeh.plotting import figure, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3

df = pd.read_csv("thor_wwii.csv")

df["MSNDATE"] = pd.to_datetime(df["MSNDATE"], format = "%m/%d/%Y")
grouped = df.groupby(pd.Grouper(key = "MSNDATE", freq = "M"))["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type = "datetime")

p.line(x = "MSNDATE", y = "TOTAL_TONS", line_width = 2, source = source, legend = "All Munitions")
p.line(x = "MSNDATE", y = "TONS_FRAG", line_width = 2, source = source, color = Spectral3[1], legend = "Fragmentation") 
p.line(x = "MSNDATE", y = "TONS_IC", line_width = 2, source = source, color = Spectral3[2], legend = "Incendiary")

p.yaxis.axis_label = "Kilotons of Munitions Dropped"

show(p)

```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1949">Loading BokehJS ...</span>
</div>




    /var/folders/3f/sl59rz9n52g9fs2vwzb49_5m0000gn/T/ipykernel_40492/864256814.py:15: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby(pd.Grouper(key = "MSNDATE", freq = "M"))["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="a76c8af0-6d2e-40ad-b9d0-533619e9bd46" data-root-id="1951"></div>





### Annotating Trends in Plots 


```python
#To visualize in Juypter output 
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

import pandas as pd
from bokeh.plotting import figure, show
from bokeh.models import ColumnDataSource
from bokeh.palettes import Spectral3
from bokeh.models import BoxAnnotation

df = pd.read_csv("thor_wwii.csv")

filter = df["THEATER"] == "ETO"
df = df[filter]

df["MSNDATE"] = pd.to_datetime(df["MSNDATE"], format = "%m/%d/%Y")

grouped = df.groupby("MSNDATE")["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
grouped = df.groupby(pd.Grouper(key = "MSNDATE", freq = "M"))["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type = "datetime")

p.line(x = "MSNDATE", y = "TOTAL_TONS", line_width = 2, source = source, legend = "All Munitions")
p.line(x = "MSNDATE", y = "TONS_FRAG", line_width = 2, source = source, color = Spectral3[1], legend = "Fragmentation") 
p.line(x = "MSNDATE", y = "TONS_IC", line_width = 2, source = source, color = Spectral3[2], legend = "Incendiary")

p.title.text = "European Theater of operations"
p.yaxis.axis_label = "Kilotons of Munitions Dropped"

box_left = pd.to_datetime("6-6-1944")
box_right = pd.to_datetime("16-12-1944")
box = BoxAnnotation(left = box_left, right = box_right, line_width = 1, line_color = "black",
                    line_dash = "dashed", fill_alpha = 0.2, fill_color = "orange")
p.add_layout(box)

show(p)
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="2282">Loading BokehJS ...</span>
</div>




    /var/folders/3f/sl59rz9n52g9fs2vwzb49_5m0000gn/T/ipykernel_40492/4091567530.py:20: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby("MSNDATE")["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
    /var/folders/3f/sl59rz9n52g9fs2vwzb49_5m0000gn/T/ipykernel_40492/4091567530.py:21: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby(pd.Grouper(key = "MSNDATE", freq = "M"))["TOTAL_TONS", "TONS_IC", "TONS_FRAG"].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    /var/folders/3f/sl59rz9n52g9fs2vwzb49_5m0000gn/T/ipykernel_40492/4091567530.py:36: UserWarning: Parsing '16-12-1944' in DD/MM/YYYY format. Provide format or specify infer_datetime_format=True for consistent parsing.
      box_right = pd.to_datetime("16-12-1944")









<div class="bk-root" id="667fbf63-b7ad-4efc-8c3e-f2a71934eb83" data-root-id="2284"></div>





## Spatial Data: Mapping Target Locations


```python
#To visualize in Juypter output 
from bokeh.resources import INLINE
import bokeh.io
from bokeh import *
bokeh.io.output_notebook(INLINE)

import pandas as pd
from bokeh.plotting import figure, output_notebook, show
from bokeh.models import ColumnDataSource, Range1d
from bokeh.layouts import layout
from bokeh.palettes import Spectral3
from bokeh.tile_providers import CARTODBPOSITRON, get_provider
from pyproj import Proj, transform
from bokeh.models.tools import HoverTool

def LongLat_to_EN(long, lat):
    try:
        transformer = Transformer.from_crs("epsg:4326", "epsg:3857")
        easting, northing = transformer.transform(long,lat)
        return easting, northing
    except:
        return None, None

df = pd.read_csv("thor_wwii.csv")

df["E"], df ["N"] = zip(*df.apply(lambda x: LongLat_to_EN(x["TGT_LONGITUDE"], x["TGT_LATITUDE"]), axis = 1))

grouped = df.groupby(["E", "N"])[["TONS_IC", "TONS_FRAG"]].sum().reset_index()

filter = grouped["TONS_FRAG"] != 0
grouped = grouped[filter]

source = ColumnDataSource(grouped)

left = -2150000
right = 18000000
bottom = -5300000
top = 11000000

provider = get_provider("CARTODBPOSITRON")
p.add_title(provider)

p.circle(x = "E", y = "N", source = source, line_color = "grey", fill_color = "yellow")
p.axis.visible = false

show(p)

#*I couldn't get the code that I wrote or even the source code to display this figure
##I'd guess that the guide was written before a significant update which changed what code needs to be written
##It's beyond me to figure out what to do but I did want to post what I had written. 
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="2642">Loading BokehJS ...</span>
</div>





    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    Input In [13], in <cell line: 41>()
         38 top = 11000000
         40 provider = get_provider("CARTODBPOSITRON")
    ---> 41 p.add_title(provider)
         43 p.circle(x = "E", y = "N", source = source, line_color = "grey", fill_color = "yellow")
         44 p.axis.visible = false


    File ~/opt/anaconda3/lib/python3.9/site-packages/bokeh/core/has_props.py:264, in HasProps.__getattr__(self, name)
        261 if isinstance(descriptor, property): # Python property
        262     return super().__getattr__(name)
    --> 264 self._raise_attribute_error_with_matches(name, properties)


    File ~/opt/anaconda3/lib/python3.9/site-packages/bokeh/core/has_props.py:272, in HasProps._raise_attribute_error_with_matches(self, name, properties)
        269 if not matches:
        270     matches, text = sorted(properties), "possible"
    --> 272 raise AttributeError(f"unexpected attribute {name!r} to {self.__class__.__name__}, {text} attributes are {nice_join(matches)}")


    AttributeError: unexpected attribute 'add_title' to Figure, similar attributes are title


## Reflection

Created in 2013 Bokeh is a library used to create interactive infographics which are generally used as a tool embedded into web pages. In his lesson “Visualizing Data with Bokeh and Pandas,” Charlie Harper emphasizes that while Bokeh is frequently compared to Matlabplot, Bokeh differs significantly as Matlabplot is not interactive and is generally used to make duller graphics for publishing academic papers. While Harper went into less detail about Pandas, I understand that it is a massively popular library within Python used to work with big data in disciplines like data science. Thus, in this lesson, it was Pandas which worked behind the scenes to process the data, and Bokeh was used on the front end to create visually pleasing graphics.

Overall I intentionally chose this lesson because of my interest in data visualization and really appreciated the thought and accessibility that Harper put into the guide. At first, I didn’t quite understand the code that I was writing, but after writing a few programs and rereading Harper's explanation, I felt that I could understand a good chunk of what was going on, but would be playing a different ballgame if I were to have to do this independently without his in-depth explanations.

Thinking about this lesson's broader applications, Harper mentions that the lesson is applied to other data sets, providing links to data on “Scottish Witchcraft Trials”, “Civil Unrest Events”, and the “Trans-Atlantic Slave Trade Database.” It seems like this could be feasibly replicated on other data which is already well-complied and in a similar format as the “thor_wwii.csv” document that I was using. Part of the massive utility that comes with Bokeh and Panda is that researchers can start by visualizing and analyzing broad trends, then look at more specific data and the causes/correlations behind it; this is what we did in the lesson as we started by plotting all ammunition dropped, then looked at the specific countries, and types of ammunition that were being dropped, and the historical events that are linked to it. Of course, for a researcher to be able to utilize these tools, the data must already be processed, so perhaps these tools come a bit later in the research process. 


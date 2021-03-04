# Analyzing US Economic Data and Building a Dashboard

<h1>Analyzing US Economic Data and  Building a Dashboard  </h1>
<h2>Description</h2>


Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some essential economic indicators from some data, you will then display these economic indicators in a Dashboard. You can then share the dashboard via an URL.

<p>
<a href="https://en.wikipedia.org/wiki/Gross_domestic_product"> Gross domestic product (GDP)</a> is a measure of the market value of all the final goods and services produced in a period. GDP is an indicator of how well the economy is doing. A drop in GDP indicates the economy is producing less; similarly an increase in GDP suggests the economy is performing better. In this lab, you will examine how changes in GDP impact the unemployment rate. You will take screen shots of every step, you will share the notebook and the URL pointing to the dashboard.</p>


<h2>Table of Contents</h2>
<div class="alert alert-block alert-info" style="margin-top: 20px">
    <ul>
<p>1.Define a Function that Makes a Dashboard 
<p>2.Create a dataframe that contains the GDP data and display it
<p>3.Create a dataframe that contains the unemployment data and display it
<p>4.Display a dataframe where unemployment was greater than 8.5%
<p>5.Use the function make_dashboard to make a dashboard
<p>6.Save the dashboard on IBM cloud and display it

   

<h2 id="Section_1"> 1:Define Function that Makes a Dashboard  </h2>


Import the following libraries.



```python
import pandas as pd
from bokeh.plotting import figure, output_file, show,output_notebook
output_notebook()
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1001">Loading BokehJS ...</span>
</div>




Define the function <code>make_dashboard</code>. 


```python
def make_dashboard(x, gdp_change, unemployment, title, file_name):
    output_file(file_name)
    p = figure(title=title, x_axis_label='year', y_axis_label='%')
    p.line(x.squeeze(), gdp_change.squeeze(), color="firebrick", line_width=4, legend="% GDP change")
    p.line(x.squeeze(), unemployment.squeeze(), line_width=4, legend="% unemployed")
    show(p)
```

The dictionary  <code>links</code> contain the CSV files with all the data. The value for the key <code>GDP</code> is the file that contains the GDP data. The value for the key <code>unemployment</code> contains the unemployment data.



```python
links={'GDP':'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/FinalModule_Coursera/data/clean_gdp.csv',\
       'unemployment':'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/FinalModule_Coursera/data/clean_unemployment.csv'}
```

<h3 id="Section_2"> 2:Creating a dataframe that contains the GDP data and display the first five rows of the dataframe.</h3>


Using the dictionary <code>links</code> and the function <code>pd.read_csv</code> to create a Pandas dataframes that contains the GDP data. Links["GDP"] contains the path or name of the file.



```python
!wget clean_gdp.csv https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/FinalModule_Coursera/data/clean_gdp.csv
df_gdp = pd.read_csv (r'clean_gdp.csv')
print (df_gdp)



```

    --2021-01-13 20:36:30--  http://clean_gdp.csv/
    Resolving clean_gdp.csv (clean_gdp.csv)... failed: Name or service not known.
    wget: unable to resolve host address ‘clean_gdp.csv’
    --2021-01-13 20:36:30--  https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/FinalModule_Coursera/data/clean_gdp.csv
    Resolving cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)... 198.23.119.245
    Connecting to cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)|198.23.119.245|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 1965 (1.9K) [text/csv]
    Saving to: ‘clean_gdp.csv.2’
    
    clean_gdp.csv.2     100%[===================>]   1.92K  --.-KB/s    in 0s      
    
    2021-01-13 20:36:30 (62.7 MB/s) - ‘clean_gdp.csv.2’ saved [1965/1965]
    
    FINISHED --2021-01-13 20:36:30--
    Total wall clock time: 0.1s
    Downloaded: 1 files, 1.9K in 0s (62.7 MB/s)
        date  level-current  level-chained  change-current  change-chained
    0   1948          274.8         2020.0            -0.7            -0.6
    1   1949          272.8         2008.9            10.0             8.7
    2   1950          300.2         2184.0            15.7             8.0
    3   1951          347.3         2360.0             5.9             4.1
    4   1952          367.7         2456.1             6.0             4.7
    ..   ...            ...            ...             ...             ...
    64  2012        16155.3        15354.6             3.6             1.8
    65  2013        16691.5        15612.2             4.4             2.5
    66  2014        17427.6        16013.3             4.0             2.9
    67  2015        18120.7        16471.5             2.7             1.6
    68  2016        18624.5        16716.2             4.2             2.2
    
    [69 rows x 5 columns]
    

Using the method <code>head()</code> to display the first five rows of the GDP data.


```python
df_gdp.head()
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
      <th>date</th>
      <th>level-current</th>
      <th>level-chained</th>
      <th>change-current</th>
      <th>change-chained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>274.8</td>
      <td>2020.0</td>
      <td>-0.7</td>
      <td>-0.6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>272.8</td>
      <td>2008.9</td>
      <td>10.0</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>300.2</td>
      <td>2184.0</td>
      <td>15.7</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>347.3</td>
      <td>2360.0</td>
      <td>5.9</td>
      <td>4.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>367.7</td>
      <td>2456.1</td>
      <td>6.0</td>
      <td>4.7</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_2">Creating a dataframe that contains the unemployment data then I display the first five rows of the dataframe. </h3>


Use the dictionary <code>links</code> and the function <code>pd.read_csv</code> to create a Pandas dataframes that contains the unemployment data.



```python
# Type your code here
!wget clean_unemployment.csv https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/FinalModule_Coursera/data/clean_unemployment.csv
df_unemployment = pd.read_csv (r'clean_unemployment.csv')
print (df_unemployment)

```

    --2021-01-13 20:08:48--  http://clean_unemployment.csv/
    Resolving clean_unemployment.csv (clean_unemployment.csv)... failed: Name or service not known.
    wget: unable to resolve host address ‘clean_unemployment.csv’
    --2021-01-13 20:08:48--  https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/FinalModule_Coursera/data/clean_unemployment.csv
    Resolving cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)... 198.23.119.245
    Connecting to cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)|198.23.119.245|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 1446 (1.4K) [text/csv]
    Saving to: ‘clean_unemployment.csv’
    
    clean_unemployment. 100%[===================>]   1.41K  --.-KB/s    in 0s      
    
    2021-01-13 20:08:49 (57.2 MB/s) - ‘clean_unemployment.csv’ saved [1446/1446]
    
    FINISHED --2021-01-13 20:08:49--
    Total wall clock time: 0.6s
    Downloaded: 1 files, 1.4K in 0s (57.2 MB/s)
        date  unemployment
    0   1948      3.750000
    1   1949      6.050000
    2   1950      5.208333
    3   1951      3.283333
    4   1952      3.025000
    ..   ...           ...
    64  2012      8.075000
    65  2013      7.358333
    66  2014      6.158333
    67  2015      5.275000
    68  2016      4.875000
    
    [69 rows x 2 columns]
    

Using the method <code>head()</code> to display the first five rows of the unemployment data.



```python
df_unemployment.head()
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
      <th>date</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>3.750000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>6.050000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>5.208333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>3.283333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>3.025000</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_3">3: Display a dataframe where unemployment was greater than 8.5%. Take a screen-shot.</h3>



```python
df_unemployment[df_unemployment.unemployment > 8.5]
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
      <th>date</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>1982</td>
      <td>9.708333</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1983</td>
      <td>9.600000</td>
    </tr>
    <tr>
      <th>61</th>
      <td>2009</td>
      <td>9.283333</td>
    </tr>
    <tr>
      <th>62</th>
      <td>2010</td>
      <td>9.608333</td>
    </tr>
    <tr>
      <th>63</th>
      <td>2011</td>
      <td>8.933333</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_4">4: Use the function make_dashboard to make a dashboard</h3>


Creating a new dataframe with the column <code>'date'</code> called <code>x</code> from the dataframe that contains the GDP data.



```python
# Create your dataframe with column date
x = df_gdp['date']
x

```




    0     1948
    1     1949
    2     1950
    3     1951
    4     1952
          ... 
    64    2012
    65    2013
    66    2014
    67    2015
    68    2016
    Name: date, Length: 69, dtype: int64



Creating a new dataframe with the column <code>'change-current' </code> called <code>gdp_change</code>  from the dataframe that contains the GDP data.



```python
# Create dataframe with column change-current
gdp_change = df_gdp['change-current']
gdp_change
```




    0     -0.7
    1     10.0
    2     15.7
    3      5.9
    4      6.0
          ... 
    64     3.6
    65     4.4
    66     4.0
    67     2.7
    68     4.2
    Name: change-current, Length: 69, dtype: float64



Creating a new dataframe with the column <code>'unemployment' </code> called <code>unemployment</code>  from the dataframe that contains the  unemployment data.



```python
# Create dataframe with column unemployment
unemployment = df_unemployment['unemployment']
unemployment
```




    0     3.750000
    1     6.050000
    2     5.208333
    3     3.283333
    4     3.025000
            ...   
    64    8.075000
    65    7.358333
    66    6.158333
    67    5.275000
    68    4.875000
    Name: unemployment, Length: 69, dtype: float64



Giving the dashboard a string title, and assign it to the variable <code>title</code>



```python
title = "dashboard"
```

Finally, the function <code>make_dashboard</code> will output an <code>.html</code> in the direictory, just like a <code>csv</code> file. The name of the file is <code>"index.html"</code> and it will be stored in the varable  <code>file_name</code>.



```python
file_name = "index.html"
```

Calling the function <code>make_dashboard</code> , to produce a dashboard.  


```python
# Fill up the parameters in the following function:
make_dashboard(x, gdp_change, unemployment, title, file_name)
```

    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    








<div class="bk-root" id="88e76c3c-c09b-4bdf-8d64-1926515253dc" data-root-id="1002"></div>





<h2>References :</h2> 


<ul>
 <il>
     1) <a href="https://research.stlouisfed.org/">Economic Research at the St. Louis Fed </a>:<a href="https://fred.stlouisfed.org/series/UNRATE/"> Civilian Unemployment Rate</a>
   </il>   
    <p>
     <il>
    2) <a href="https://github.com/datasets">Data Packaged Core Datasets
       </a>
   </il> 
    </p>
    
</ul>
</div>


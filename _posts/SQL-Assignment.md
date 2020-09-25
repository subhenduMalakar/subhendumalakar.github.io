# SQL Assignment


```python
import pandas as pd
import sqlite3

from IPython.display import display, HTML
```


```python
# Note that this is not the same db we have used in course videos, please download from this link
# https://drive.google.com/file/d/1O-1-L1DdNxEK6O6nG2jS31MbrMh-OnXM/view?usp=sharing
```


```python
conn = sqlite3.connect("Db-IMDB-Assignment.db")
```

#### Overview of all tables


```python
tables = pd.read_sql_query("SELECT NAME AS 'Table_Name' FROM sqlite_master WHERE type='table'",conn)
tables = tables["Table_Name"].values.tolist()
```


```python
for table in tables:
    query = "PRAGMA TABLE_INFO({})".format(table)
    schema = pd.read_sql_query(query,conn)
    print("Schema of",table)
    display(schema)
    print("-"*100)
    print("\n")
```

    Schema of Movie
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>title</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>year</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>rating</td>
      <td>REAL</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>num_votes</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of Genre
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Name</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>GID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of Language
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Name</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>LAID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of Country
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Name</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>CID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of Location
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Name</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>LID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of M_Location
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>LID</td>
      <td>REAL</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of M_Country
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>CID</td>
      <td>REAL</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of M_Language
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>LAID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of M_Genre
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>GID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of Person
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>PID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Name</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Gender</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of M_Producer
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>PID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of M_Director
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>PID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    Schema of M_Cast
    


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
      <th>cid</th>
      <th>name</th>
      <th>type</th>
      <th>notnull</th>
      <th>dflt_value</th>
      <th>pk</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>index</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>MID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>PID</td>
      <td>TEXT</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ID</td>
      <td>INTEGER</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    ----------------------------------------------------------------------------------------------------
    
    
    

## Useful tips:

1. the year column in 'Movie' table, will have few chracters other than numbers which you need to be preprocessed, you need to get a substring of last 4 characters, its better if you convert it as int type, ex: CAST(SUBSTR(TRIM(m.year),-4) AS INTEGER)

2. For almost all the TEXT columns we have show, please try to remove trailing spaces, you need to use TRIM() function

3. When you are doing count(coulmn) it won't consider the "NULL" values, you might need to explore other alternatives like Count(*)

## Q1 --- List all the directors who directed a 'Comedy' movie in a leap year. (You need to check that the genre is 'Comedy’ and year is a leap year) Your query should return director name, the movie name, and the year.

<h4>To determine whether a year is a leap year, follow these steps:</h4>

<ul>
    <li><b>STEP-1:</b> If the year is evenly divisible by 4, go to step 2. Otherwise, go to step 5.</li>
    <li><b>STEP-2:</b> If the year is evenly divisible by 100, go to step 3. Otherwise, go to step 4.</li>
    <li><b>STEP-3:</b> If the year is evenly divisible by 400, go to step 4. Otherwise, go to step 5.</li>
    <li><b>STEP-4:</b> The year is a leap year (it has 366 days).</li>
    <li><b>STEP-5:</b> The year is not a leap year (it has 365 days).</li>
</ul>

Year 1900 is divisible by 4 and 100 but it is not divisible by 400, so it is not a leap year.


```python
%%time
def grader_1(q1):
    q1_results  = pd.read_sql_query(q1,conn)
    print(q1_results.head(10))
    assert (q1_results.shape == (232,3))

query1 = """ *** Write your query for the question 1 *** """
grader_1(query1)
```

         director name       movie name  mod_year
    0       Amit Mitra       Jagte Raho      1956
    1     Chetan Anand         Funtoosh      1956
    2      Satyen Bose          Jagriti      1956
    3      Mohan Segal        New Delhi      1956
    4       S.U. Sunny         Kohinoor      1960
    5        Bimal Roy           Parakh      1960
    6      R.K. Nayyar    Love in Simla      1960
    7       K. Shankar         Rajkumar      1964
    8   Shakti Samanta  Kashmir Ki Kali      1964
    9    Ram Mukherjee           Leader      1964
    (232, 3)
    Wall time: 205 ms
    

## Q2 --- List the names of all the actors who played in the movie 'Anand' (1971)


```python
%%time
def grader_2(q2):
    q2_results  = pd.read_sql_query(q2,conn)
    print(q2_results.head(10))
    assert (q2_results.shape == (17,1))


query2 = """ *** Write your query for the question 2 *** """
grader_2(query2)
```

            Actor_Names
    0  Amitabh Bachchan
    1     Rajesh Khanna
    2     Sumita Sanyal
    3        Ramesh Deo
    4         Seema Deo
    5    Asit Kumar Sen
    6        Dev Kishan
    7      Atam Prakash
    8     Lalita Kumari
    9            Savita
    Wall time: 43 ms
    

## Q3 --- List all the actors who acted in a film before 1970 and in a film after 1990. (That is: < 1970 and > 1990.)


```python
%%time

def grader_3a(query_less_1970, query_more_1990):
    q3_a = pd.read_sql_query(query_less_1970,conn)
    q3_b = pd.read_sql_query(query_more_1990,conn)
    return (q3_a.shape == (4942,1)) and (q3_b.shape == (62570,1))

query_less_1970 =""" *** write the query to get all the id's of actors who acted before 1970 *** """
query_more_1990 =""" *** write the query to get all the id's of actors who acted after 1990  *** """
print(grader_3a(query_less_1970, query_more_1990))

# using the above two queries, you can find the answer to the given question 
```

    True
    Wall time: 220 ms
    


```python
%%time
def grader_3(q3):
    q3_results  = pd.read_sql_query(q3,conn)
    print(q3_results.head(10))
    assert (q3_results.shape == (300,1))

query3 = """ *** Write your query for the question 3 *** """
grader_3(query3)
```

             Actor_Name
    0      Rishi Kapoor
    1  Amitabh Bachchan
    2            Asrani
    3      Zohra Sehgal
    4   Parikshat Sahni
    5     Rakesh Sharma
    6       Sanjay Dutt
    7         Ric Young
    8             Yusuf
    9    Suhasini Mulay
    Wall time: 227 ms
    

## Q4 --- List all directors who directed 10 movies or more, in descending order of the number of movies they directed. Return the directors' names and the number of movies each of them directed.


```python
%%time

def grader_4a(query_4a):
    query_4a = pd.read_sql_query(query_4a,conn)
    print(query_4a.head(10)) 
    return (query_4a.shape == (1462,2))

query_4a =""" *** Write a query, which will return all the directors(id's) along with the number of movies they directed *** """
print(grader_4a(query_4a))

# using the above query, you can write the answer to the given question
```

      Director_ID  Movie_Count
    0   nm0000180            1
    1   nm0000187            1
    2   nm0000229            1
    3   nm0000269            1
    4   nm0000386            1
    5   nm0000487            2
    6   nm0000965            1
    7   nm0001060            1
    8   nm0001162            1
    9   nm0001241            1
    True
    Wall time: 16 ms
    


```python
%%time
def grader_4(q4):
    q4_results  = pd.read_sql_query(q4,conn)
    print(q4_results.head(10))
    assert (q4_results.shape == (58,2))

query4 = """ *** Write your query for the question 4 *** """
grader_4(query4)
```

               Director_Name  Movie_Count
    0           David Dhawan           39
    1           Mahesh Bhatt           35
    2           Priyadarshan           30
    3        Ram Gopal Varma           30
    4           Vikram Bhatt           29
    5   Hrishikesh Mukherjee           27
    6            Yash Chopra           21
    7        Basu Chatterjee           19
    8         Shakti Samanta           19
    9           Subhash Ghai           18
    Wall time: 32 ms
    

## Q5.a --- For each year, count the number of movies in that year that had only female actors.


```python
%%time

# note that you don't need TRIM for person table

def grader_5aa(query_5aa):
    query_5aa = pd.read_sql_query(query_5aa,conn)
    print(query_5aa.head(10)) 
    return (query_5aa.shape == (8846,3))

query_5aa =""" *** Write your query that will get movie id, and number of people for each geneder *** """

print(grader_5aa(query_5aa))

def grader_5ab(query_5ab):
    query_5ab = pd.read_sql_query(query_5ab,conn)
    print(query_5ab.head(10)) 
    return (query_5ab.shape == (3469, 3))

query_5ab =""" *** Write your query that will have at least one male actor try to use query that you have written above *** """

print(grader_5ab(query_5ab))


# using the above queries, you can write the answer to the given question
```

             MID    Gend  Count
    0  tt0021594    None      1
    1  tt0021594  Female      3
    2  tt0021594    Male      5
    3  tt0026274    None      2
    4  tt0026274  Female     11
    5  tt0026274    Male      9
    6  tt0027256    None      2
    7  tt0027256  Female      5
    8  tt0027256    Male      8
    9  tt0028217  Female      3
    True
             MID  Gend  Count
    0  tt0021594  Male      5
    1  tt0026274  Male      9
    2  tt0027256  Male      8
    3  tt0028217  Male      7
    4  tt0031580  Male     27
    5  tt0033616  Male     46
    6  tt0036077  Male     11
    7  tt0038491  Male      7
    8  tt0039654  Male      6
    9  tt0040067  Male     10
    (3469, 3)
    True
    Wall time: 1.5 s
    


```python
%%time
def grader_5a(q5a):
    q5a_results  = pd.read_sql_query(q5a,conn)
    print(q5a_results.head(10))
    assert (q5a_results.shape == (4,2))

query5a = """ *** Write your query for the question 5a *** """
grader_5a(query5a)
```

       YEAR  Female_Cast_Only_Movies
    0  1939                        1
    1  1999                        1
    2  2000                        1
    3  2018                        1
    Wall time: 264 ms
    

## Q5.b --- Now include a small change: report for each year the percentage of movies in that year with only female actors, and the total number of movies made that year. For example, one answer will be: 1990 31.81 13522 meaning that in 1990 there were 13,522 movies, and 31.81% had only female actors. You do not need to round your answer.


```python
%%time
def grader_5b(q5b):
    q5b_results  = pd.read_sql_query(q5b,conn)
    print(q5b_results.head(10))
    assert (q5b_results.shape == (4,3))

query5b = """ *** Write your query for the question 5b *** """
grader_5b(query5b)
```

       YEAR  Percentage_Female_Only_Movie  Total_Movies
    0  1939                      0.500000             2
    1  1999                      0.015152            66
    2  2000                      0.015625            64
    3  2018                      0.009615           104
    Wall time: 324 ms
    

## Q6 --- Find the film(s) with the largest cast. Return the movie title and the size of the cast. By "cast size" we mean the number of distinct actors that played in that movie: if an actor played multiple roles, or if it simply occurs multiple times in casts, we still count her/him only once.


```python
%%time
def grader_6(q6):
    q6_results  = pd.read_sql_query(q6,conn)
    print(q6_results.head(10))
    assert (q6_results.shape == (3473, 2))

query6 = """ *** Write your query for the question 5b *** """
grader_6(query6)
```

                            title  count
    0               Ocean's Eight    238
    1                    Apaharan    233
    2                        Gold    215
    3             My Name Is Khan    213
    4  Captain America: Civil War    191
    5                    Geostorm    170
    6                     Striker    165
    7                        2012    154
    8                      Pixels    144
    9       Yamla Pagla Deewana 2    140
    Wall time: 232 ms
    

### Q7 --- A decade is a sequence of 10 consecutive years. 
### For example, say in your database you have movie information starting from 1931. 
### the first decade is 1931, 1932, ..., 1940,
### the second decade is 1932, 1933, ..., 1941 and so on. 
### Find the decade D with the largest number of films and the total number of films in D.


```python
%%time
def grader_7a(q7a):
    q7a_results  = pd.read_sql_query(q7a,conn)
    print(q7a_results.head(10))
    assert (q7a_results.shape == (78, 2))

query7a = """ *** Write a query that computes number of movies in each year *** """
grader_7a(query7a)

# using the above query, you can write the answer to the given question
```

       Movie_Year  Total_Movies
    0        1931             1
    1        1936             3
    2        1939             2
    3        1941             1
    4        1943             1
    5        1946             2
    6        1947             2
    7        1948             3
    8        1949             3
    9        1950             2
    Wall time: 12 ms
    


```python
%%time
def grader_7b(q7b):
    q7b_results  = pd.read_sql_query(q7b,conn)
    print(q7b_results.head(10))
    assert (q7b_results.shape == (713, 4))

query7b = """   
    *** 
    Write a query that will do joining of the above table(7a) with itself 
    such that you will join with only rows if the second tables year is <= current_year+9 and more than or equal current_year
    *** 
          """
grader_7b(query7b)
# if you see the below results the first movie year is less than 2nd movie year and 
# 2nd movie year is less or equal to the first movie year+9

# using the above query, you can write the answer to the given question
```

       Movie_Year  Total_Movies  Movie_Year  Total_Movies
    0        1931             1        1931             1
    1        1931             1        1936             3
    2        1931             1        1939             2
    3        1936             3        1936             3
    4        1936             3        1939             2
    5        1936             3        1941             1
    6        1936             3        1943             1
    7        1939             2        1939             2
    8        1939             2        1941             1
    9        1939             2        1943             1
    Wall time: 24 ms
    


```python
%%time
def grader_7(q7):
    q7_results  = pd.read_sql_query(q7,conn)
    print(q7_results.head(10))
    assert (q7_results.shape == (1, 2))

query7 = """ *** Write a query that will return the decade that has maximum number of movies ***"""
grader_7(query7)
# if you check the output we are printinng all the year in that decade, its fine you can print 2008 or 2008-2017
```

       Decade_Movie_Count                                             Decade
    0                1203  2008-2009-2010-2011-2012-2013-2014-2015-2016-2017
    Wall time: 21 ms
    

## Q8 --- Find all the actors that made more movies with Yash Chopra than any other director.


```python
%%time
def grader_8a(q8a):
    q8a_results  = pd.read_sql_query(q8a,conn)
    print(q8a_results.head(10))
    assert (q8a_results.shape == (73408, 3))

query8a = """ *** Write a query that will results in number of movies actor-director worked together ***"""
grader_8a(query8a)

# using the above query, you can write the answer to the given question
```

           actor   director  movies
    0  nm0000002  nm0496746       1
    1  nm0000027  nm0000180       1
    2  nm0000039  nm0896533       1
    3  nm0000042  nm0896533       1
    4  nm0000047  nm0004292       1
    5  nm0000073  nm0485943       1
    6  nm0000076  nm0000229       1
    7  nm0000092  nm0178997       1
    8  nm0000093  nm0000269       1
    9  nm0000096  nm0113819       1
    Wall time: 534 ms
    


```python
%%time

def grader_8(q8):
    q8_results  = pd.read_sql_query(q8,conn)
    print(q8_results.head(10))
    print(q8_results.shape)
    assert (q8_results.shape == (245, 2))

query8 = """ *** Write a query that answers the 8th question ***"""
grader_8(query8)
```

                    Name  count
    0        Jagdish Raj     11
    1   Manmohan Krishna     10
    2           Iftekhar      9
    3      Shashi Kapoor      7
    4      Rakhee Gulzar      5
    5     Waheeda Rehman      5
    6           Ravikant      4
    7     Achala Sachdev      4
    8        Neetu Singh      4
    9      Leela Chitnis      3
    (245, 2)
    Wall time: 864 ms
    

## Q9 --- The Shahrukh number of an actor is the length of the shortest path between the actor and Shahrukh Khan in the "co-acting" graph. That is, Shahrukh Khan has Shahrukh number 0; all actors who acted in the same film as Shahrukh have Shahrukh number 1; all actors who acted in the same film as some actor with Shahrukh number 1 have Shahrukh number 2, etc. Return all actors whose Shahrukh number is 2.


```python
%%time
def grader_9a(q9a):
    q9a_results  = pd.read_sql_query(q9a,conn)
    print(q9a_results.head(10))
    print(q9a_results.shape)
    assert (q9a_results.shape == (2382, 1))

query9a = """ *** Write a query that answers the 9th question ***"""
grader_9a(query9a)
# using the above query, you can write the answer to the given question

# selecting actors who acted with srk (S1)
# selecting all movies where S1 actors acted, this forms S2 movies list
# selecting all actors who acted in S2 movies, this gives us S2 actors along with S1 actors
# removing S1 actors from the combined list of S1 & S2 actors, so that we get only S2 actors
```

          S1_PID
    0  nm0004418
    1  nm1995953
    2  nm2778261
    3  nm0631373
    4  nm0241935
    5  nm0792116
    6  nm1300111
    7  nm0196375
    8  nm1464837
    9  nm2868019
    (2382, 1)
    Wall time: 178 ms
    


```python
%%time
def grader_9(q9):
    q9_results  = pd.read_sql_query(q9,conn)
    print(q9_results.head(10))
    print(q9_results.shape)
    assert (q9_results.shape == (25698, 1))

query9 = """ *** Write a query that answers the 9th question ***"""
grader_9(query9)
```

                  Actor_Name
    0           Freida Pinto
    1            Rohan Chand
    2           Damian Young
    3        Waris Ahluwalia
    4  Caroline Christl Long
    5          Rajeev Pahuja
    6      Michelle Santiago
    7        Alicia Vikander
    8           Dominic West
    9         Walton Goggins
    (25698, 1)
    Wall time: 591 ms
    

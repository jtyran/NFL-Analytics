# Dive into NFL based Data and Analytics 


```python
# By Tyran Javon Johnson

# This project demonstrates a few of the capabilities of python.Purpose is to 
# gain insight and a enhanced understanding of player and team performances in the NFL

# Libraries required to start
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
# All data collected on players is year by year, not by season. Each year a team plays 14-16 games, and 2-3 games in the following year
# First lets pull some data and start solving some questions. 
df = pd.read_csv("./FOOTBALL/ALL NFL pbp/Team Stats/nfl_offense_stats.csv")
#df.head()
```


```python
# offensive NFL plays 2021
nfl = df
```


```python
# Recieving stats
df3 = pd.read_csv("./FOOTBALL/ALL NFL pbp/player_stats/2021_player_stats/2021_player_receiving.csv")
```


```python
# rushing stats
df4 = pd.read_csv("./FOOTBALL/ALL NFL pbp/player_stats/2021_player_stats/2021_player_rushing.csv")
```


```python
#passing stats
df5 = pd.read_csv("./FOOTBALL/ALL NFL pbp/player_stats/2021_player_stats/2021_player_passing.csv")
```


```python
# All stats in one
df_merge = pd.merge(df3, df4, on="player")
```


```python
# Below is offensive stats for rushing, passing and recieving. Before merging, I made column in each df was unique minus the most left column ("player")
off_2021 = pd.merge(df_merge, df5, on="player")
off_2021.head()
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
      <th>player</th>
      <th>rec</th>
      <th>rec_yds</th>
      <th>rec_td</th>
      <th>rec_20+</th>
      <th>rec_40+</th>
      <th>rec_lng</th>
      <th>rec_1st</th>
      <th>rec_1st%</th>
      <th>rec_fum</th>
      <th>...</th>
      <th>pass_td</th>
      <th>int</th>
      <th>rate</th>
      <th>pass_1st</th>
      <th>pass_1st%</th>
      <th>pass_20+</th>
      <th>pass_40+</th>
      <th>pass_long</th>
      <th>sck</th>
      <th>scky</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Justin Jefferson</td>
      <td>108</td>
      <td>1616</td>
      <td>10</td>
      <td>27</td>
      <td>5</td>
      <td>56</td>
      <td>75</td>
      <td>0.694</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>106.2</td>
      <td>2</td>
      <td>0.667</td>
      <td>1</td>
      <td>0</td>
      <td>24</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Deebo Samuel</td>
      <td>77</td>
      <td>1405</td>
      <td>6</td>
      <td>23</td>
      <td>9</td>
      <td>83</td>
      <td>51</td>
      <td>0.662</td>
      <td>4</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>133.3</td>
      <td>1</td>
      <td>0.500</td>
      <td>1</td>
      <td>0</td>
      <td>24</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Christian Kirk</td>
      <td>77</td>
      <td>982</td>
      <td>5</td>
      <td>16</td>
      <td>4</td>
      <td>50</td>
      <td>44</td>
      <td>0.571</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>118.8</td>
      <td>1</td>
      <td>1.000</td>
      <td>1</td>
      <td>0</td>
      <td>33</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jakobi Meyers</td>
      <td>83</td>
      <td>866</td>
      <td>2</td>
      <td>12</td>
      <td>0</td>
      <td>39</td>
      <td>42</td>
      <td>0.506</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>118.8</td>
      <td>1</td>
      <td>0.500</td>
      <td>1</td>
      <td>0</td>
      <td>30</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tyler Boyd</td>
      <td>67</td>
      <td>828</td>
      <td>5</td>
      <td>10</td>
      <td>2</td>
      <td>68</td>
      <td>37</td>
      <td>0.552</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>118.8</td>
      <td>1</td>
      <td>1.000</td>
      <td>1</td>
      <td>1</td>
      <td>46</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 36 columns</p>
</div>




```python
off_2021.columns
```




    Index(['player', 'rec', 'rec_yds', 'rec_td', 'rec_20+', 'rec_40+', 'rec_lng',
           'rec_1st', 'rec_1st%', 'rec_fum', 'tgts', 'yd/rec', 'rush_yds',
           'rush_att', 'rush_td', 'rush_20+', 'Rush_40+', 'rush_lng', 'rus_1st',
           'rush_1st%', 'rush_fum', 'pass _yds', 'pass_yat', 'pass_att',
           'pass_cmp', 'cmp%', 'pass_td', 'int', 'rate', 'pass_1st', 'pass_1st%',
           'pass_20+', 'pass_40+', 'pass_long', 'sck', 'scky'],
          dtype='object')




```python
# Concating the dfs results in me losing some data.
df_concat = pd.concat([df3, df4, df5])
df_concat.head()
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
      <th>player</th>
      <th>rec</th>
      <th>rec_yds</th>
      <th>rec_td</th>
      <th>rec_20+</th>
      <th>rec_40+</th>
      <th>rec_lng</th>
      <th>rec_1st</th>
      <th>rec_1st%</th>
      <th>rec_fum</th>
      <th>...</th>
      <th>pass_td</th>
      <th>int</th>
      <th>rate</th>
      <th>pass_1st</th>
      <th>pass_1st%</th>
      <th>pass_20+</th>
      <th>pass_40+</th>
      <th>pass_long</th>
      <th>sck</th>
      <th>scky</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cooper Kupp</td>
      <td>145.0</td>
      <td>1947.0</td>
      <td>16.0</td>
      <td>30.0</td>
      <td>9.0</td>
      <td>59.0</td>
      <td>89.0</td>
      <td>0.614</td>
      <td>0.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Justin Jefferson</td>
      <td>108.0</td>
      <td>1616.0</td>
      <td>10.0</td>
      <td>27.0</td>
      <td>5.0</td>
      <td>56.0</td>
      <td>75.0</td>
      <td>0.694</td>
      <td>1.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Davante Adams</td>
      <td>123.0</td>
      <td>1553.0</td>
      <td>11.0</td>
      <td>19.0</td>
      <td>4.0</td>
      <td>59.0</td>
      <td>84.0</td>
      <td>0.683</td>
      <td>0.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ja'Marr Chase</td>
      <td>81.0</td>
      <td>1455.0</td>
      <td>13.0</td>
      <td>22.0</td>
      <td>8.0</td>
      <td>82.0</td>
      <td>56.0</td>
      <td>0.691</td>
      <td>2.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Deebo Samuel</td>
      <td>77.0</td>
      <td>1405.0</td>
      <td>6.0</td>
      <td>23.0</td>
      <td>9.0</td>
      <td>83.0</td>
      <td>51.0</td>
      <td>0.662</td>
      <td>4.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 36 columns</p>
</div>




```python
# This is adding Yahoo default fantasy points per offensive stats minus any special teams points scored for offensive players.
# Fantasy points vary depending on league and scoring setting

off_2021 = off_2021.assign(fan_rush = round(off_2021["rush_yds"] / 8, 2))
off_2021 = off_2021.assign(fan_pass = round(off_2021["pass _yds"] / 20, 2))
off_2021 = off_2021.assign(fan_int = round(off_2021["int"] * -2, 2))
off_2021 = off_2021.assign(fan_pass_td = round(off_2021["pass_td"] * 5, 2))
off_2021 = off_2021.assign(fan_rush_td = round(off_2021["rush_td"] * 5, 2))
off_2021 = off_2021.assign(fan_rec_yds = round(off_2021["rec_yds"] / 8, 2))
off_2021 = off_2021.assign(fan_rec_td = round(off_2021["rec_td"] * 5, 2))
off_2021 = off_2021.assign(fan_rec = round(off_2021["rec"] * .5, 2))
off_2021 = off_2021.assign(fan_rush_fum = round(off_2021["rush_fum"] * -2, 2))
off_2021 = off_2021.assign(fan_rec_fum = round(off_2021["rec_fum"] * -2, 2))



```


```python
# Total Fantasy points for offensive players during the 2021 season
off_2021["total_fp"] = off_2021[["fan_rush", "fan_pass", "fan_int", "fan_pass_td", "fan_rush_td", "fan_rec_yds", "fan_rec_td", "fan_rec", "fan_rush_fum", "fan_rec_fum"]].sum(axis=1)
```


```python
off_2021.head()
# I want to find the average points scored for each player, but unfortunately games played is missing
# To fix this problem, I will extract this df and add more details to it using excel
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
      <th>player</th>
      <th>rec</th>
      <th>rec_yds</th>
      <th>rec_td</th>
      <th>rec_20+</th>
      <th>rec_40+</th>
      <th>rec_lng</th>
      <th>rec_1st</th>
      <th>rec_1st%</th>
      <th>rec_fum</th>
      <th>...</th>
      <th>fan_pass</th>
      <th>fan_int</th>
      <th>fan_pass_td</th>
      <th>fan_rush_td</th>
      <th>fan_rec_yds</th>
      <th>fan_rec_td</th>
      <th>fan_rec</th>
      <th>fan_rush_fum</th>
      <th>fan_rec_fum</th>
      <th>total_fp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Justin Jefferson</td>
      <td>108</td>
      <td>1616</td>
      <td>10</td>
      <td>27</td>
      <td>5</td>
      <td>56</td>
      <td>75</td>
      <td>0.694</td>
      <td>1</td>
      <td>...</td>
      <td>1.75</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>202.00</td>
      <td>50</td>
      <td>54.0</td>
      <td>0</td>
      <td>-2</td>
      <td>307.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Deebo Samuel</td>
      <td>77</td>
      <td>1405</td>
      <td>6</td>
      <td>23</td>
      <td>9</td>
      <td>83</td>
      <td>51</td>
      <td>0.662</td>
      <td>4</td>
      <td>...</td>
      <td>1.20</td>
      <td>0</td>
      <td>5</td>
      <td>40</td>
      <td>175.62</td>
      <td>30</td>
      <td>38.5</td>
      <td>0</td>
      <td>-8</td>
      <td>327.94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Christian Kirk</td>
      <td>77</td>
      <td>982</td>
      <td>5</td>
      <td>16</td>
      <td>4</td>
      <td>50</td>
      <td>44</td>
      <td>0.571</td>
      <td>0</td>
      <td>...</td>
      <td>1.65</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>122.75</td>
      <td>25</td>
      <td>38.5</td>
      <td>0</td>
      <td>0</td>
      <td>189.28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jakobi Meyers</td>
      <td>83</td>
      <td>866</td>
      <td>2</td>
      <td>12</td>
      <td>0</td>
      <td>39</td>
      <td>42</td>
      <td>0.506</td>
      <td>1</td>
      <td>...</td>
      <td>2.25</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>108.25</td>
      <td>10</td>
      <td>41.5</td>
      <td>0</td>
      <td>-2</td>
      <td>161.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tyler Boyd</td>
      <td>67</td>
      <td>828</td>
      <td>5</td>
      <td>10</td>
      <td>2</td>
      <td>68</td>
      <td>37</td>
      <td>0.552</td>
      <td>1</td>
      <td>...</td>
      <td>2.30</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>103.50</td>
      <td>25</td>
      <td>33.5</td>
      <td>0</td>
      <td>-2</td>
      <td>165.05</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 47 columns</p>
</div>




```python
# Saving off_2021 as an csv file

off_2021.to_csv('off_2021.csv', index=False)
off_2021.to_excel('offf_2021.xlsx', index=False)



```


```python
off_2021.columns
```




    Index(['player', 'rec', 'rec_yds', 'rec_td', 'rec_20+', 'rec_40+', 'rec_lng',
           'rec_1st', 'rec_1st%', 'rec_fum', 'tgts', 'yd/rec', 'rush_yds',
           'rush_att', 'rush_td', 'rush_20+', 'Rush_40+', 'rush_lng', 'rus_1st',
           'rush_1st%', 'rush_fum', 'pass _yds', 'pass_yat', 'pass_att',
           'pass_cmp', 'cmp%', 'pass_td', 'int', 'rate', 'pass_1st', 'pass_1st%',
           'pass_20+', 'pass_40+', 'pass_long', 'sck', 'scky', 'fan_rush',
           'fan_pass', 'fan_int', 'fan_pass_td', 'fan_rush_td', 'fan_rec_yds',
           'fan_rec_td', 'fan_rec', 'fan_rush_fum', 'fan_rec_fum', 'total_fp'],
          dtype='object')




```python
# Receiving Average Metrics
off_2021.iloc[:,1:10].apply(np.mean)
```




    rec          41.466667
    rec_yds     536.466667
    rec_td        2.733333
    rec_20+       7.466667
    rec_40+       1.800000
    rec_lng      37.933333
    rec_1st      23.466667
    rec_1st%      0.489533
    rec_fum       0.600000
    dtype: float64




```python
# theres a ton of columns in the df. Here is a way to see all the column names
nfl.head().T
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>player</th>
      <td>Garrett Bradbury</td>
      <td>C.J. Goodwin</td>
      <td>Adam Prentice</td>
      <td>Adam Prentice</td>
      <td>Andy Janovich</td>
    </tr>
    <tr>
      <th>year</th>
      <td>2022</td>
      <td>2022</td>
      <td>2022</td>
      <td>2022</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>position</th>
      <td>C</td>
      <td>CB</td>
      <td>FB</td>
      <td>FB</td>
      <td>FB</td>
    </tr>
    <tr>
      <th>team</th>
      <td>MIN</td>
      <td>DAL</td>
      <td>NOR</td>
      <td>NOR</td>
      <td>CLE</td>
    </tr>
    <tr>
      <th>pass_cmp</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Humidity</th>
      <td>60</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
      <td>60</td>
    </tr>
    <tr>
      <th>wind_speed</th>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>vegas_line</th>
      <td>-13.0</td>
      <td>-3.0</td>
      <td>-6.5</td>
      <td>-3.5</td>
      <td>-2.0</td>
    </tr>
    <tr>
      <th>vegas_favorite</th>
      <td>GNB</td>
      <td>DAL</td>
      <td>NOR</td>
      <td>NOR</td>
      <td>PIT</td>
    </tr>
    <tr>
      <th>over_under</th>
      <td>42.5</td>
      <td>51.0</td>
      <td>37.5</td>
      <td>40.0</td>
      <td>42.0</td>
    </tr>
  </tbody>
</table>
<p>66 rows × 5 columns</p>
</div>






```python
# Average for a few metrics
nfl.iloc[:,47:53].apply(np.mean)
```




    rush_broken_tackles     0.145096
    rec_air_yds            21.977875
    rec_yac                 9.532569
    rec_drops               0.133731
    offense                32.708857
    off_pct                48.993691
    dtype: float64




```python
# Max for the above metrics
nfl.iloc[:,47:53].apply(np.max)
```




    rush_broken_tackles     11.0
    rec_air_yds            320.6
    rec_yac                153.0
    rec_drops                6.0
    offense                100.0
    off_pct                100.0
    dtype: float64



# Task 1: Find the average rec yac of only pass catchers. Mininum of at least one target.


```python
nfl_max_yac = nfl.iloc[:,49:50].apply(np.max)
```


```python
# Im all over the place. This is the max rec yac.
nfl_max_yac = nfl.iloc[:,49:50].apply(np.max)
print(nfl_max_yac)
```

    rec_yac    153
    dtype: int64
    


```python
mean_yac = (nfl['rec_yac'].loc[nfl['rec_yac'] != 0]).mean()
print(mean_yac)
```

    17.35904449307075
    

# Task 2: List QBs that had 300+ passing yards games in a game


```python
# First I will try to set a value of 300+ passing yards.
nfl_qb_top_tier = nfl['pass_yds'] >=300
nfl[nfl_qb_top_tier]
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
      <th>player</th>
      <th>year</th>
      <th>position</th>
      <th>team</th>
      <th>pass_cmp</th>
      <th>pass_att</th>
      <th>pass_yds</th>
      <th>pass_td</th>
      <th>pass_int</th>
      <th>pass_sacked</th>
      <th>...</th>
      <th>home_score</th>
      <th>ot</th>
      <th>roof</th>
      <th>surface</th>
      <th>temperature</th>
      <th>Humidity</th>
      <th>wind_speed</th>
      <th>vegas_line</th>
      <th>vegas_favorite</th>
      <th>over_under</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>Joe Burrow</td>
      <td>2022</td>
      <td>QB</td>
      <td>CIN</td>
      <td>30</td>
      <td>39</td>
      <td>446</td>
      <td>4</td>
      <td>0</td>
      <td>4</td>
      <td>...</td>
      <td>34</td>
      <td>False</td>
      <td>outdoors</td>
      <td>fieldturf</td>
      <td>33</td>
      <td>81</td>
      <td>13</td>
      <td>-4.0</td>
      <td>KAN</td>
      <td>51.5</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Tom Brady</td>
      <td>2022</td>
      <td>QB</td>
      <td>TAM</td>
      <td>34</td>
      <td>50</td>
      <td>410</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>24</td>
      <td>False</td>
      <td>outdoors</td>
      <td>fieldturf</td>
      <td>57</td>
      <td>82</td>
      <td>9</td>
      <td>-13.5</td>
      <td>TAM</td>
      <td>45.5</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Patrick Mahomes</td>
      <td>2022</td>
      <td>QB</td>
      <td>KAN</td>
      <td>30</td>
      <td>39</td>
      <td>404</td>
      <td>5</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>42</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>30</td>
      <td>78</td>
      <td>8</td>
      <td>-12.5</td>
      <td>KAN</td>
      <td>46.5</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Justin Herbert</td>
      <td>2022</td>
      <td>QB</td>
      <td>LAC</td>
      <td>34</td>
      <td>64</td>
      <td>383</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>35</td>
      <td>True</td>
      <td>dome</td>
      <td>grass</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.0</td>
      <td>LAC</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Patrick Mahomes</td>
      <td>2022</td>
      <td>QB</td>
      <td>KAN</td>
      <td>33</td>
      <td>44</td>
      <td>378</td>
      <td>3</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>42</td>
      <td>True</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>35</td>
      <td>54</td>
      <td>6</td>
      <td>-2.0</td>
      <td>KAN</td>
      <td>54.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>14292</th>
      <td>Dak Prescott</td>
      <td>2019</td>
      <td>QB</td>
      <td>DAL</td>
      <td>23</td>
      <td>33</td>
      <td>303</td>
      <td>4</td>
      <td>0</td>
      <td>3</td>
      <td>...</td>
      <td>47</td>
      <td>False</td>
      <td>retractable roof (closed)</td>
      <td>fieldturf</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-12.5</td>
      <td>DAL</td>
      <td>47.5</td>
    </tr>
    <tr>
      <th>14293</th>
      <td>Joe Flacco</td>
      <td>2019</td>
      <td>QB</td>
      <td>DEN</td>
      <td>22</td>
      <td>38</td>
      <td>303</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>24</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>87</td>
      <td>11</td>
      <td>14</td>
      <td>-2.5</td>
      <td>DEN</td>
      <td>37.0</td>
    </tr>
    <tr>
      <th>14294</th>
      <td>Daniel Jones</td>
      <td>2019</td>
      <td>QB</td>
      <td>NYG</td>
      <td>28</td>
      <td>47</td>
      <td>301</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>...</td>
      <td>17</td>
      <td>False</td>
      <td>outdoors</td>
      <td>fieldturf</td>
      <td>42</td>
      <td>69</td>
      <td>5</td>
      <td>-4.0</td>
      <td>PHI</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>14295</th>
      <td>Jameis Winston</td>
      <td>2019</td>
      <td>QB</td>
      <td>TAM</td>
      <td>21</td>
      <td>43</td>
      <td>301</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>...</td>
      <td>27</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>59</td>
      <td>67</td>
      <td>3</td>
      <td>-2.0</td>
      <td>TEN</td>
      <td>45.5</td>
    </tr>
    <tr>
      <th>14296</th>
      <td>Russell Wilson</td>
      <td>2019</td>
      <td>QB</td>
      <td>SEA</td>
      <td>29</td>
      <td>35</td>
      <td>300</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>...</td>
      <td>26</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>81</td>
      <td>51</td>
      <td>3</td>
      <td>-4.0</td>
      <td>PIT</td>
      <td>47.0</td>
    </tr>
  </tbody>
</table>
<p>397 rows × 66 columns</p>
</div>




```python
# Here is a second way to get the same table which shows all passing yards of 300 and greater.
# nfl.query('pass_yds >=300')
```


```python
nfl_qb = nfl[nfl_qb_top_tier]
```


```python
# Now I will try to count exactly how many times each player had over 300 passing yards in a game
nfl_qb = nfl_qb.sort_values(by="pass_yds", ascending=False)
```


```python
new_qb_df = nfl_qb.sort_values(by="pass_yds", ascending=False)
```


```python
results = new_qb_df['player'].value_counts()
```


```python
# The above shows leaders for the most 300 more passing yards in a game from 2019 to 2022.
```


```python
# Testing a function 
def my_first_function(a, b, c):
    if a > b:
        return("LEGENDARY")
    if b > c:
        return("ELITE")
    return("GOOD")
# The result below are the top 5 QBs total 300+ passing yard games over 2021-2022 season.
results.head()
```




    Patrick Mahomes    25
    Tom Brady          23
    Matt Ryan          20
    Josh Allen         17
    Justin Herbert     17
    Name: player, dtype: int64




```python
# heres a bar graph for players with the most 300 or more yards thrown in a game since 2019.
new_qb_df['player'].value_counts()[:20].plot(kind='barh')
```




    <AxesSubplot:>




    
![png](output_34_1.png)
    



```python
# All the occurrences a QB has thrown for 3 tds or more in a game.
# if you want to just see the names, put in 'player' at the end. 
nfl.loc[nfl['pass_td'] >= 3,]
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
      <th>player</th>
      <th>year</th>
      <th>position</th>
      <th>team</th>
      <th>pass_cmp</th>
      <th>pass_att</th>
      <th>pass_yds</th>
      <th>pass_td</th>
      <th>pass_int</th>
      <th>pass_sacked</th>
      <th>...</th>
      <th>home_score</th>
      <th>ot</th>
      <th>roof</th>
      <th>surface</th>
      <th>temperature</th>
      <th>Humidity</th>
      <th>wind_speed</th>
      <th>vegas_line</th>
      <th>vegas_favorite</th>
      <th>over_under</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>Joe Burrow</td>
      <td>2022</td>
      <td>QB</td>
      <td>CIN</td>
      <td>30</td>
      <td>39</td>
      <td>446</td>
      <td>4</td>
      <td>0</td>
      <td>4</td>
      <td>...</td>
      <td>34</td>
      <td>False</td>
      <td>outdoors</td>
      <td>fieldturf</td>
      <td>33</td>
      <td>81</td>
      <td>13</td>
      <td>-4.0</td>
      <td>KAN</td>
      <td>51.5</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Tom Brady</td>
      <td>2022</td>
      <td>QB</td>
      <td>TAM</td>
      <td>34</td>
      <td>50</td>
      <td>410</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>24</td>
      <td>False</td>
      <td>outdoors</td>
      <td>fieldturf</td>
      <td>57</td>
      <td>82</td>
      <td>9</td>
      <td>-13.5</td>
      <td>TAM</td>
      <td>45.5</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Patrick Mahomes</td>
      <td>2022</td>
      <td>QB</td>
      <td>KAN</td>
      <td>30</td>
      <td>39</td>
      <td>404</td>
      <td>5</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>42</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>30</td>
      <td>78</td>
      <td>8</td>
      <td>-12.5</td>
      <td>KAN</td>
      <td>46.5</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Justin Herbert</td>
      <td>2022</td>
      <td>QB</td>
      <td>LAC</td>
      <td>34</td>
      <td>64</td>
      <td>383</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>35</td>
      <td>True</td>
      <td>dome</td>
      <td>grass</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.0</td>
      <td>LAC</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Patrick Mahomes</td>
      <td>2022</td>
      <td>QB</td>
      <td>KAN</td>
      <td>33</td>
      <td>44</td>
      <td>378</td>
      <td>3</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>42</td>
      <td>True</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>35</td>
      <td>54</td>
      <td>6</td>
      <td>-2.0</td>
      <td>KAN</td>
      <td>54.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>14593</th>
      <td>Lamar Jackson</td>
      <td>2019</td>
      <td>QB</td>
      <td>BAL</td>
      <td>15</td>
      <td>20</td>
      <td>169</td>
      <td>5</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>6</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>62</td>
      <td>64</td>
      <td>5</td>
      <td>-3.5</td>
      <td>BAL</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>14597</th>
      <td>Brian Hoyer</td>
      <td>2019</td>
      <td>QB</td>
      <td>IND</td>
      <td>17</td>
      <td>26</td>
      <td>168</td>
      <td>3</td>
      <td>1</td>
      <td>4</td>
      <td>...</td>
      <td>26</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>48</td>
      <td>47</td>
      <td>12</td>
      <td>-1.0</td>
      <td>PIT</td>
      <td>39.5</td>
    </tr>
    <tr>
      <th>14612</th>
      <td>Carson Wentz</td>
      <td>2019</td>
      <td>QB</td>
      <td>PHI</td>
      <td>16</td>
      <td>27</td>
      <td>160</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>27</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>60</td>
      <td>62</td>
      <td>3</td>
      <td>-3.5</td>
      <td>GNB</td>
      <td>46.0</td>
    </tr>
    <tr>
      <th>14633</th>
      <td>Jacoby Brissett</td>
      <td>2019</td>
      <td>QB</td>
      <td>IND</td>
      <td>17</td>
      <td>28</td>
      <td>146</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>17</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>93</td>
      <td>45</td>
      <td>1</td>
      <td>-3.0</td>
      <td>TEN</td>
      <td>43.5</td>
    </tr>
    <tr>
      <th>14635</th>
      <td>Lamar Jackson</td>
      <td>2019</td>
      <td>QB</td>
      <td>BAL</td>
      <td>16</td>
      <td>25</td>
      <td>145</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>17</td>
      <td>False</td>
      <td>outdoors</td>
      <td>astroturf</td>
      <td>43</td>
      <td>48</td>
      <td>18</td>
      <td>-6.5</td>
      <td>BAL</td>
      <td>44.0</td>
    </tr>
  </tbody>
</table>
<p>337 rows × 66 columns</p>
</div>



# Task 3: QB data with TDS > Turnovers


```python
# This is what I got so far. I will need to work on cleaning up my results to show only QB stats
nfl[nfl['position'].isin(['QB'])]
qb_data = nfl[nfl['position'].isin(['QB'])]
qb_data.query('pass_td > fumbles_lost + pass_int')
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
      <th>player</th>
      <th>year</th>
      <th>position</th>
      <th>team</th>
      <th>pass_cmp</th>
      <th>pass_att</th>
      <th>pass_yds</th>
      <th>pass_td</th>
      <th>pass_int</th>
      <th>pass_sacked</th>
      <th>...</th>
      <th>home_score</th>
      <th>ot</th>
      <th>roof</th>
      <th>surface</th>
      <th>temperature</th>
      <th>Humidity</th>
      <th>wind_speed</th>
      <th>vegas_line</th>
      <th>vegas_favorite</th>
      <th>over_under</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>Joe Burrow</td>
      <td>2022</td>
      <td>QB</td>
      <td>CIN</td>
      <td>30</td>
      <td>39</td>
      <td>446</td>
      <td>4</td>
      <td>0</td>
      <td>4</td>
      <td>...</td>
      <td>34</td>
      <td>False</td>
      <td>outdoors</td>
      <td>fieldturf</td>
      <td>33</td>
      <td>81</td>
      <td>13</td>
      <td>-4.0</td>
      <td>KAN</td>
      <td>51.5</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Tom Brady</td>
      <td>2022</td>
      <td>QB</td>
      <td>TAM</td>
      <td>34</td>
      <td>50</td>
      <td>410</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>24</td>
      <td>False</td>
      <td>outdoors</td>
      <td>fieldturf</td>
      <td>57</td>
      <td>82</td>
      <td>9</td>
      <td>-13.5</td>
      <td>TAM</td>
      <td>45.5</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Patrick Mahomes</td>
      <td>2022</td>
      <td>QB</td>
      <td>KAN</td>
      <td>30</td>
      <td>39</td>
      <td>404</td>
      <td>5</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>42</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>30</td>
      <td>78</td>
      <td>8</td>
      <td>-12.5</td>
      <td>KAN</td>
      <td>46.5</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Justin Herbert</td>
      <td>2022</td>
      <td>QB</td>
      <td>LAC</td>
      <td>34</td>
      <td>64</td>
      <td>383</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>...</td>
      <td>35</td>
      <td>True</td>
      <td>dome</td>
      <td>grass</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.0</td>
      <td>LAC</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Patrick Mahomes</td>
      <td>2022</td>
      <td>QB</td>
      <td>KAN</td>
      <td>33</td>
      <td>44</td>
      <td>378</td>
      <td>3</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>42</td>
      <td>True</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>35</td>
      <td>54</td>
      <td>6</td>
      <td>-2.0</td>
      <td>KAN</td>
      <td>54.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>14688</th>
      <td>Matt Schaub</td>
      <td>2019</td>
      <td>QB</td>
      <td>ATL</td>
      <td>6</td>
      <td>6</td>
      <td>65</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>10</td>
      <td>False</td>
      <td>retractable roof (open)</td>
      <td>fieldturf</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.0</td>
      <td>LAR</td>
      <td>54.5</td>
    </tr>
    <tr>
      <th>14691</th>
      <td>Matt Schaub</td>
      <td>2019</td>
      <td>QB</td>
      <td>ATL</td>
      <td>5</td>
      <td>9</td>
      <td>55</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>22</td>
      <td>False</td>
      <td>retractable roof (closed)</td>
      <td>fieldturf</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.5</td>
      <td>ATL</td>
      <td>51.5</td>
    </tr>
    <tr>
      <th>14692</th>
      <td>Robert Griffin III</td>
      <td>2019</td>
      <td>QB</td>
      <td>BAL</td>
      <td>6</td>
      <td>6</td>
      <td>55</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>10</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>91</td>
      <td>56</td>
      <td>8</td>
      <td>-7.0</td>
      <td>BAL</td>
      <td>41.0</td>
    </tr>
    <tr>
      <th>14697</th>
      <td>Mike Glennon</td>
      <td>2019</td>
      <td>QB</td>
      <td>LVR</td>
      <td>2</td>
      <td>3</td>
      <td>36</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>42</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>55</td>
      <td>74</td>
      <td>6</td>
      <td>-5.5</td>
      <td>GNB</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>14700</th>
      <td>Tyrod Taylor</td>
      <td>2019</td>
      <td>QB</td>
      <td>LAC</td>
      <td>3</td>
      <td>5</td>
      <td>26</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>10</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.5</td>
      <td>LAC</td>
      <td>42.0</td>
    </tr>
  </tbody>
</table>
<p>896 rows × 66 columns</p>
</div>



# Task 4: Filter out the data to only see offensive stats using PBP Data


```python
# This syntax shows a dataframse of the primary offensive skill positions
nfl[nfl['position'].isin(['QB', 'WR', 'RB', 'HB', 'FB', 'TE'])]
offensive_skill = nfl[nfl['position'].isin(['QB', 'WR', 'RB', 'HB', 'FB', 'TE'])]
```


```python
# This will only show QB data
nfl[nfl['position'].isin(['QB'])]
qb_data = nfl[nfl['position'].isin(['QB'])]
```


```python
# WRs only
nfl[nfl['position'].isin(['WR'])]
wr_data = nfl[nfl['position'].isin(['WR'])]
```


```python
# RBs only
nfl[nfl['position'].isin(['RB','HB'])]
rb_data = nfl[nfl['position'].isin(['RB','HB'])]
```


```python
# TEs only
nfl[nfl['position'].isin(['TE'])]
te_data = nfl[nfl['position'].isin(['TE'])]
```

# Task 5: Further evaluate wr_data dataframe


```python
# Top receivers in the league in yards.

new_wr_data = wr_data[wr_data['year'].isin([2022, 2021])]
wr_stats = new_wr_data.groupby(new_wr_data['player']).aggregate({'rec': 'sum', 'rec_yds': 'sum', 'rec_td': 'sum', 'rec_long': 'max', 'rush_td': 'sum', 'rec_yac': 'sum', 'targets': 'sum'})
top_wr = wr_stats.sort_values(by='rec_yds', ascending=False).iloc[0:50]

```


```python
# Top 5 WR in the NFL
rec_yac = wr_data.groupby(wr_data['player']).aggregate({'rec_yac': 'sum'})
rec_yac.sort_values(by=['rec_yac'],ascending = False).head(5)
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
      <th>rec_yac</th>
    </tr>
    <tr>
      <th>player</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cooper Kupp</th>
      <td>2122</td>
    </tr>
    <tr>
      <th>Deebo Samuel</th>
      <td>1841</td>
    </tr>
    <tr>
      <th>Davante Adams</th>
      <td>1786</td>
    </tr>
    <tr>
      <th>Chris Godwin</th>
      <td>1547</td>
    </tr>
    <tr>
      <th>Tyreek Hill</th>
      <td>1516</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Yards per reception shows how many yards a receiver gain by every catch. 
wr_stats['yards_per_rec'] = wr_stats['rec_yds'] / wr_stats['rec']

# YAC Percentage. Percent of total yards that come after catch. 
wr_stats['yac_pct'] = wr_stats['rec_yac'] / wr_stats['rec_yds'] * 100

# Catch percentage will represent the percent of catches a playes gets. These numbers can vary
wr_stats['catch_p'] = wr_stats['rec'] / wr_stats['targets'] * 100
wr1 = wr_stats.round(decimals = 2)
```


```python
wr1.sort_values(by='rec_yds', ascending=False).head(10)
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
      <th>rec</th>
      <th>rec_yds</th>
      <th>rec_td</th>
      <th>rec_long</th>
      <th>rush_td</th>
      <th>rec_yac</th>
      <th>targets</th>
      <th>yards_per_rec</th>
      <th>yac_pct</th>
      <th>catch_p</th>
    </tr>
    <tr>
      <th>player</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cooper Kupp</th>
      <td>182</td>
      <td>2503</td>
      <td>22</td>
      <td>70</td>
      <td>0</td>
      <td>1059</td>
      <td>242</td>
      <td>13.75</td>
      <td>42.31</td>
      <td>75.21</td>
    </tr>
    <tr>
      <th>Tyreek Hill</th>
      <td>158</td>
      <td>1879</td>
      <td>12</td>
      <td>75</td>
      <td>0</td>
      <td>765</td>
      <td>218</td>
      <td>11.89</td>
      <td>40.71</td>
      <td>72.48</td>
    </tr>
    <tr>
      <th>Ja'Marr Chase</th>
      <td>106</td>
      <td>1823</td>
      <td>14</td>
      <td>82</td>
      <td>0</td>
      <td>822</td>
      <td>163</td>
      <td>17.20</td>
      <td>45.09</td>
      <td>65.03</td>
    </tr>
    <tr>
      <th>Davante Adams</th>
      <td>156</td>
      <td>1822</td>
      <td>14</td>
      <td>59</td>
      <td>0</td>
      <td>696</td>
      <td>211</td>
      <td>11.68</td>
      <td>38.20</td>
      <td>73.93</td>
    </tr>
    <tr>
      <th>Justin Jefferson</th>
      <td>117</td>
      <td>1749</td>
      <td>10</td>
      <td>56</td>
      <td>0</td>
      <td>531</td>
      <td>179</td>
      <td>14.95</td>
      <td>30.36</td>
      <td>65.36</td>
    </tr>
    <tr>
      <th>Stefon Diggs</th>
      <td>136</td>
      <td>1679</td>
      <td>12</td>
      <td>61</td>
      <td>0</td>
      <td>449</td>
      <td>213</td>
      <td>12.35</td>
      <td>26.74</td>
      <td>63.85</td>
    </tr>
    <tr>
      <th>Deebo Samuel</th>
      <td>87</td>
      <td>1559</td>
      <td>7</td>
      <td>83</td>
      <td>9</td>
      <td>922</td>
      <td>135</td>
      <td>17.92</td>
      <td>59.14</td>
      <td>64.44</td>
    </tr>
    <tr>
      <th>Mike Evans</th>
      <td>105</td>
      <td>1521</td>
      <td>18</td>
      <td>55</td>
      <td>0</td>
      <td>380</td>
      <td>166</td>
      <td>14.49</td>
      <td>24.98</td>
      <td>63.25</td>
    </tr>
    <tr>
      <th>Chris Godwin</th>
      <td>119</td>
      <td>1468</td>
      <td>8</td>
      <td>52</td>
      <td>1</td>
      <td>724</td>
      <td>166</td>
      <td>12.34</td>
      <td>49.32</td>
      <td>71.69</td>
    </tr>
    <tr>
      <th>Diontae Johnson</th>
      <td>126</td>
      <td>1408</td>
      <td>9</td>
      <td>50</td>
      <td>0</td>
      <td>575</td>
      <td>199</td>
      <td>11.17</td>
      <td>40.84</td>
      <td>63.32</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Here is the percentage of yards after catch for the top 25 wrs. 
top_wr['rec_yac'] / top_wr['rec_yds'] * 100
# Hey look at Jarvis Landry sitting at 49.8% of yards after the catch. I cant wait to see what he can do for the BLACK & GOLD!!
```




    player
    Cooper Kupp            42.309229
    Tyreek Hill            40.713145
    Ja'Marr Chase          45.090510
    Davante Adams          38.199780
    Justin Jefferson       30.360206
    Stefon Diggs           26.742108
    Deebo Samuel           59.140475
    Mike Evans             24.983563
    Chris Godwin           49.318801
    Diontae Johnson        40.838068
    Tee Higgins            30.285714
    Tyler Lockett          25.152905
    D.J. Moore             34.658188
    Mike Williams          34.529506
    Marquise Brown         36.385542
    A.J. Brown             25.542169
    Brandin Cooks          31.005819
    Michael Pittman Jr.    34.666667
    Terry McLaurin         28.167808
    CeeDee Lamb            39.193825
    Darnell Mooney         36.062718
    Keenan Allen           29.613357
    Hunter Renfrow         45.000000
    D.K. Metcalf           32.749077
    Chase Claypool         30.526316
    Christian Kirk         23.523717
    Jaylen Waddle          43.251232
    Marvin Jones           16.798419
    Van Jefferson          30.300000
    Gabriel Davis          21.261445
    DeVonta Smith          27.663934
    Jakobi Meyers          25.359343
    Amari Cooper           26.082474
    Brandon Aiyuk          40.062435
    Kendrick Bourne        46.694648
    Tyler Boyd             46.219382
    Cole Beasley           44.165758
    Amon-Ra St. Brown      46.491228
    Mecole Hardman         76.574586
    Russell Gage           33.101045
    A.J. Green             21.344340
    Odell Beckham Jr.      28.121212
    Emmanuel Sanders       17.424242
    Adam Thielen           33.205619
    Tim Patrick            30.897436
    Courtland Sutton       17.396907
    Antonio Brown          39.659686
    Marquez Callaway       21.628838
    Byron Pringle          34.278003
    Jarvis Landry          49.795362
    dtype: float64




```python
import math

# I'm going to attempt to calculate percentiles of yards for WRs. 

def my_percentile(top_wr, percentile):
    n = len(wr1.rec_yds)
    p = n * percentile/100
    if p.is_integer():
        return sorted(wr1.rec_yds)[int(p)]
    else:
        return sorted(wr1.rec_yds)[int(math.ceil(p)) - 1]

dist = np.random.randn(10)
index = [5, 25, 50, 75, 95]
perc_func = [my_percentile(dist, i) for i in index]
print(perc_func)
# Key: There is a huge jump in percentile from WRs in the 75 and 95 percent. 
```

    [0, 21, 148, 507, 1245]
    


```python
# Who leads in YAC from 2019-2022?
wr_data.sort_values(by=['rec_yac', 'rec', 'rec_yds'])

more_results = wr_data.groupby('player')['rec_yac'].sum()
print(more_results)
```

    player
    A.J. Brown        1214
    A.J. Green         267
    Aaron Fuller         0
    Adam Humphries     320
    Adam Thielen       626
                      ... 
    Vyncint Smith      106
    Will Fuller        541
    Willie Snead       349
    Zach Pascal        600
    Zay Jones          314
    Name: rec_yac, Length: 367, dtype: int64
    


```python
# Just for reference
r = nfl.columns.tolist()
print(r)
```

    ['player', 'year', 'position', 'team', 'pass_cmp', 'pass_att', 'pass_yds', 'pass_td', 'pass_int', 'pass_sacked', 'pass_sacked_yds', 'pass_long', 'pass_rating', 'rush_att', 'rush_yds', 'rush_td', 'rush_long', 'targets', 'rec', 'rec_yds', 'rec_td', 'rec_long', 'fumbles_lost', 'rush_scrambles', 'designed_rush_att', 'comb_pass_rush_play', 'comb_pass_play', 'comb_rush_play', 'opponent_abbrev', 'two_point_conv', 'total_ret_td', 'offensive_fumble_recovery_td', 'pass_yds_bonus', 'rush_yds_bonus', 'rec_yds_bonus', 'Total_DKP', 'Off_DKP', 'total_fdp', 'off_fdp', 'total_sdp', 'off_sdp', 'pass_target_yds', 'pass_poor_throws', 'pass_blitzed', 'pass_hurried', 'rush_yds_before_contact', 'rush_yac', 'rush_broken_tackles', 'rec_air_yds', 'rec_yac', 'rec_drops', 'offense', 'off_pct', 'vis_team', 'home_team', 'vis_score', 'home_score', 'ot', 'roof', 'surface', 'temperature', 'Humidity', 'wind_speed', 'vegas_line', 'vegas_favorite', 'over_under']
    

# Task 6: Further analyze rb data


```python
rb_data[["player", "year", "position", "team", "rush_yds", "rush_att", "rush_td", "rec_td", "targets", "rec_yds"]].head()
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
      <th>player</th>
      <th>year</th>
      <th>position</th>
      <th>team</th>
      <th>rush_yds</th>
      <th>rush_att</th>
      <th>rush_td</th>
      <th>rec_td</th>
      <th>targets</th>
      <th>rec_yds</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>151</th>
      <td>Joe Mixon</td>
      <td>2022</td>
      <td>RB</td>
      <td>CIN</td>
      <td>72</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>152</th>
      <td>Aaron Jones</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>76</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>30</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Aaron Jones</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>41</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>129</td>
    </tr>
    <tr>
      <th>154</th>
      <td>AJ Dillon</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>63</td>
      <td>14</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>20</td>
    </tr>
    <tr>
      <th>155</th>
      <td>AJ Dillon</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>63</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# A look into the top 10 rushers in 2021
rush_rank = df4.sort_values(by='rush_yds', ascending=False)
#These are the top 10 rushers for 2021
rush_rank.iloc[0:10]
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
      <th>player</th>
      <th>rush_yds</th>
      <th>rush_att</th>
      <th>rush_td</th>
      <th>rush_20+</th>
      <th>Rush_40+</th>
      <th>rush_lng</th>
      <th>rus_1st</th>
      <th>rush_1st%</th>
      <th>rush_fum</th>
      <th>ypc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jonathan Taylor</td>
      <td>1811</td>
      <td>332</td>
      <td>18</td>
      <td>14</td>
      <td>5</td>
      <td>83</td>
      <td>107</td>
      <td>3.103</td>
      <td>3</td>
      <td>5.454819</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nick Chubb</td>
      <td>1259</td>
      <td>228</td>
      <td>8</td>
      <td>12</td>
      <td>2</td>
      <td>70</td>
      <td>61</td>
      <td>3.738</td>
      <td>2</td>
      <td>5.521930</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Joe Mixon</td>
      <td>1205</td>
      <td>292</td>
      <td>13</td>
      <td>6</td>
      <td>0</td>
      <td>32</td>
      <td>60</td>
      <td>4.867</td>
      <td>1</td>
      <td>4.126712</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Najee Harris</td>
      <td>1200</td>
      <td>307</td>
      <td>7</td>
      <td>6</td>
      <td>0</td>
      <td>37</td>
      <td>62</td>
      <td>4.952</td>
      <td>0</td>
      <td>3.908795</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Dalvin Cook</td>
      <td>1159</td>
      <td>249</td>
      <td>6</td>
      <td>9</td>
      <td>1</td>
      <td>66</td>
      <td>57</td>
      <td>4.368</td>
      <td>3</td>
      <td>4.654618</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Antonio Gibson</td>
      <td>1037</td>
      <td>258</td>
      <td>7</td>
      <td>4</td>
      <td>0</td>
      <td>27</td>
      <td>65</td>
      <td>3.969</td>
      <td>5</td>
      <td>4.019380</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Ezekiel Elliott</td>
      <td>1002</td>
      <td>237</td>
      <td>10</td>
      <td>3</td>
      <td>1</td>
      <td>47</td>
      <td>55</td>
      <td>4.309</td>
      <td>1</td>
      <td>4.227848</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Elijah Mitchell</td>
      <td>963</td>
      <td>207</td>
      <td>5</td>
      <td>6</td>
      <td>0</td>
      <td>39</td>
      <td>47</td>
      <td>4.404</td>
      <td>0</td>
      <td>4.652174</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Derrick Henry</td>
      <td>937</td>
      <td>219</td>
      <td>10</td>
      <td>3</td>
      <td>2</td>
      <td>76</td>
      <td>49</td>
      <td>4.469</td>
      <td>1</td>
      <td>4.278539</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Damien Harris</td>
      <td>929</td>
      <td>202</td>
      <td>15</td>
      <td>8</td>
      <td>1</td>
      <td>64</td>
      <td>55</td>
      <td>3.673</td>
      <td>2</td>
      <td>4.599010</td>
    </tr>
  </tbody>
</table>
</div>




```python
# YPC for the top 50
ypc = rb_data['rush_yds'] / rb_data['rush_att']
rb_data["ypc"] = ypc
rb_data = rb_data.round(2)
rb_data.head()
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
      <th>player</th>
      <th>year</th>
      <th>position</th>
      <th>team</th>
      <th>pass_cmp</th>
      <th>pass_att</th>
      <th>pass_yds</th>
      <th>pass_td</th>
      <th>pass_int</th>
      <th>pass_sacked</th>
      <th>...</th>
      <th>ot</th>
      <th>roof</th>
      <th>surface</th>
      <th>temperature</th>
      <th>Humidity</th>
      <th>wind_speed</th>
      <th>vegas_line</th>
      <th>vegas_favorite</th>
      <th>over_under</th>
      <th>ypc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>151</th>
      <td>Joe Mixon</td>
      <td>2022</td>
      <td>RB</td>
      <td>CIN</td>
      <td>1</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>False</td>
      <td>dome</td>
      <td>matrixturf</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-4.0</td>
      <td>LAR</td>
      <td>48.5</td>
      <td>4.80</td>
    </tr>
    <tr>
      <th>152</th>
      <td>Aaron Jones</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>11</td>
      <td>60</td>
      <td>9</td>
      <td>-13.0</td>
      <td>GNB</td>
      <td>42.5</td>
      <td>9.50</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Aaron Jones</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>15</td>
      <td>53</td>
      <td>12</td>
      <td>-5.5</td>
      <td>GNB</td>
      <td>47.0</td>
      <td>3.42</td>
    </tr>
    <tr>
      <th>154</th>
      <td>AJ Dillon</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>11</td>
      <td>60</td>
      <td>9</td>
      <td>-13.0</td>
      <td>GNB</td>
      <td>42.5</td>
      <td>4.50</td>
    </tr>
    <tr>
      <th>155</th>
      <td>AJ Dillon</td>
      <td>2022</td>
      <td>RB</td>
      <td>GNB</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>False</td>
      <td>dome</td>
      <td>fieldturf</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.0</td>
      <td>GNB</td>
      <td>44.5</td>
      <td>4.50</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 67 columns</p>
</div>




```python
# Top 10 YPC (yards per carry) leaders 2021-2022
df4['ypc'] = df4['rush_yds'] / df4['rush_att']
# Sort the DataFrame by 'ypc' in descending order and select the top 10
top_10 = df4.sort_values(by='ypc', ascending=False).head(10)

# Print the 'player' and 'ypc' columns for these top 10 players
print(top_10[['player', 'ypc']])
```

                   player        ypc
    303       Dawson Knox        inf
    206        C.J. Moore  28.000000
    215       Greg Dortch  24.000000
    174      Scott Miller  21.500000
    238         John Ross  16.000000
    123       Jamal Agnew  15.857143
    201  Emmanuel Sanders  15.500000
    156  D'Wayne Eskridge  14.750000
    244     Cyril Grayson  14.000000
    245     Sean Chandler  14.000000
    


```python
# Although the above is true, Im only interested in seeing players who got a min of 100 carries
df4_filtered = df4[df4['rush_att'] >= 100]
# Sort the DataFrame by 'ypc' in descending order and select the top 10
top_10_ = df4_filtered.sort_values(by='ypc', ascending=False).head(10)
# Printing filtered 10 leading rushers with a minimum of 100 carries, not excluding other positions 
print(top_10_[['player', 'ypc']])
```

                  player       ypc
    28     Rashaad Penny  6.294118
    25        Josh Allen  6.254098
    24     Lamar Jackson  5.766917
    22       Jalen Hurts  5.640288
    29      Tony Pollard  5.530769
    1         Nick Chubb  5.521930
    26     Miles Sanders  5.503650
    0    Jonathan Taylor  5.454819
    44  D'Ernest Johnson  5.340000
    40     Chase Edmonds  5.103448
    

# Task 7: Futher analyze TE data


```python
# TE's only
te_data
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
      <th>player</th>
      <th>year</th>
      <th>position</th>
      <th>team</th>
      <th>pass_cmp</th>
      <th>pass_att</th>
      <th>pass_yds</th>
      <th>pass_td</th>
      <th>pass_int</th>
      <th>pass_sacked</th>
      <th>...</th>
      <th>home_score</th>
      <th>ot</th>
      <th>roof</th>
      <th>surface</th>
      <th>temperature</th>
      <th>Humidity</th>
      <th>wind_speed</th>
      <th>vegas_line</th>
      <th>vegas_favorite</th>
      <th>over_under</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>401</th>
      <td>Travis Kelce</td>
      <td>2022</td>
      <td>TE</td>
      <td>KAN</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>42</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>30</td>
      <td>78</td>
      <td>8</td>
      <td>-12.5</td>
      <td>KAN</td>
      <td>46.5</td>
    </tr>
    <tr>
      <th>402</th>
      <td>Adam Shaheen</td>
      <td>2022</td>
      <td>TE</td>
      <td>MIA</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>34</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>43</td>
      <td>93</td>
      <td>13</td>
      <td>-3.0</td>
      <td>TEN</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>403</th>
      <td>Adam Shaheen</td>
      <td>2022</td>
      <td>TE</td>
      <td>MIA</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>33</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>75</td>
      <td>79</td>
      <td>8</td>
      <td>-6.0</td>
      <td>NWE</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>404</th>
      <td>Adam Trautman</td>
      <td>2022</td>
      <td>TE</td>
      <td>NOR</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>18</td>
      <td>False</td>
      <td>dome</td>
      <td>sportturf</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-6.5</td>
      <td>NOR</td>
      <td>37.5</td>
    </tr>
    <tr>
      <th>405</th>
      <td>Adam Trautman</td>
      <td>2022</td>
      <td>TE</td>
      <td>NOR</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>20</td>
      <td>False</td>
      <td>retractable roof (closed)</td>
      <td>fieldturf</td>
      <td>72</td>
      <td>45</td>
      <td>0</td>
      <td>-3.5</td>
      <td>NOR</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>17557</th>
      <td>Zach Ertz</td>
      <td>2019</td>
      <td>TE</td>
      <td>PHI</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>17</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>47</td>
      <td>46</td>
      <td>7</td>
      <td>-2.0</td>
      <td>DAL</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>17558</th>
      <td>Zach Gentry</td>
      <td>2019</td>
      <td>TE</td>
      <td>PIT</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>24</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>79</td>
      <td>36</td>
      <td>3</td>
      <td>-6.0</td>
      <td>SFO</td>
      <td>44.5</td>
    </tr>
    <tr>
      <th>17559</th>
      <td>Zach Gentry</td>
      <td>2019</td>
      <td>TE</td>
      <td>PIT</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>27</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>76</td>
      <td>72</td>
      <td>1</td>
      <td>-3.5</td>
      <td>PIT</td>
      <td>45.5</td>
    </tr>
    <tr>
      <th>17560</th>
      <td>Zach Gentry</td>
      <td>2019</td>
      <td>TE</td>
      <td>PIT</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>17</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>71</td>
      <td>61</td>
      <td>9</td>
      <td>-6.0</td>
      <td>LAC</td>
      <td>42.5</td>
    </tr>
    <tr>
      <th>17561</th>
      <td>Zach Gentry</td>
      <td>2019</td>
      <td>TE</td>
      <td>PIT</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>10</td>
      <td>False</td>
      <td>outdoors</td>
      <td>grass</td>
      <td>31</td>
      <td>67</td>
      <td>6</td>
      <td>-1.0</td>
      <td>PIT</td>
      <td>37.0</td>
    </tr>
  </tbody>
</table>
<p>4711 rows × 66 columns</p>
</div>




```python
# The only TEs to produce over 2000 yards over the last 3 full seasons. 
te_stats = te_data.groupby(te_data['player']).aggregate({'rec': 'sum', 'rec_yds': 'sum', 'rec_td': 'sum', 'rec_long': 'max', 'rush_td': 'sum', 'rec_yac': 'sum', 'targets': 'sum'})
top_te = te_stats[(te_stats['rec_yds'] > 2000)]
print(top_te)
```

                    rec  rec_yds  rec_td  rec_long  rush_td  rec_yac  targets
    player                                                                   
    Dallas Goedert  173     2126      12        45        0      974      248
    Darren Waller   259     3082      14        75        0     1400      367
    George Kittle   215     2740      14        61        0     1417      284
    Mark Andrews    241     3022      26        51        0      963      363
    Mike Gesicki    177     2053      13        70        0      550      286
    Travis Kelce    361     4593      34        69        2     1899      498
    Zach Ertz       203     2079      12        47        0      721      327
    

# Task 8: Dive into factors that may determine win/lose probability.


```python
# Lets first try to define wins and losses. Since the data takes in every play, there is duplicate data for scores that exist.
# I will create a new column to the dataframe outlining which team (visitor or home) won. 


conditions = [nfl['vis_score'] > nfl['home_score'],
              nfl['vis_score'] < nfl['home_score']]

choices = ['visitor', 'home']

nfl['winning_team'] = np.select(conditions, choices, default='tie')
nfl.winning_team
```




    0           home
    1        visitor
    2           home
    3        visitor
    4           home
              ...   
    19968       home
    19969    visitor
    19970    visitor
    19971    visitor
    19972       home
    Name: winning_team, Length: 19973, dtype: object




```python
# Lets get rid of duplicate games since the dataframe is factoring in players from the same team.
# Below are 5 different variables that will remain constant for duplicates.
wins_losses_data = nfl[['year', 'vis_team', 'home_team', 'home_score', 'vis_score', 'winning_team']]
wins_loss_data = wins_losses_data.drop_duplicates()
wins_loss_data
# The data below shows all wins in regular season and playoff games from 2019 to 2022. 
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
      <th>year</th>
      <th>vis_team</th>
      <th>home_team</th>
      <th>home_score</th>
      <th>vis_score</th>
      <th>winning_team</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022</td>
      <td>MIN</td>
      <td>GNB</td>
      <td>37</td>
      <td>10</td>
      <td>home</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022</td>
      <td>SFO</td>
      <td>DAL</td>
      <td>17</td>
      <td>23</td>
      <td>visitor</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022</td>
      <td>CAR</td>
      <td>NOR</td>
      <td>18</td>
      <td>10</td>
      <td>home</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022</td>
      <td>NOR</td>
      <td>ATL</td>
      <td>20</td>
      <td>30</td>
      <td>visitor</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022</td>
      <td>CLE</td>
      <td>PIT</td>
      <td>26</td>
      <td>14</td>
      <td>home</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>14552</th>
      <td>2019</td>
      <td>CHI</td>
      <td>LAR</td>
      <td>17</td>
      <td>7</td>
      <td>home</td>
    </tr>
    <tr>
      <th>14555</th>
      <td>2019</td>
      <td>NYJ</td>
      <td>PHI</td>
      <td>31</td>
      <td>6</td>
      <td>home</td>
    </tr>
    <tr>
      <th>14563</th>
      <td>2019</td>
      <td>PIT</td>
      <td>NYJ</td>
      <td>16</td>
      <td>10</td>
      <td>home</td>
    </tr>
    <tr>
      <th>14599</th>
      <td>2019</td>
      <td>WAS</td>
      <td>MIA</td>
      <td>16</td>
      <td>17</td>
      <td>visitor</td>
    </tr>
    <tr>
      <th>14624</th>
      <td>2019</td>
      <td>NWE</td>
      <td>CIN</td>
      <td>13</td>
      <td>34</td>
      <td>visitor</td>
    </tr>
  </tbody>
</table>
<p>820 rows × 6 columns</p>
</div>




```python
# This is all the years I have on wins and losses
wins_losses_data['year'].unique()
```




    array([2022, 2021, 2020, 2019], dtype=int64)




```python
# The probability the home team won a game
import seaborn as sns
%matplotlib inline

plt_wins = wins_loss_data['winning_team'].value_counts().rename_axis('the_values').reset_index(name='counts')
plt_wins
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
      <th>the_values</th>
      <th>counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>home</td>
      <td>418</td>
    </tr>
    <tr>
      <th>1</th>
      <td>visitor</td>
      <td>399</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tie</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Here is the wins, losses, and ties in percentage
(wins_loss_data['winning_team'].value_counts()/wins_loss_data['winning_team'].count())*100
```




    home       50.975610
    visitor    48.658537
    tie         0.365854
    Name: winning_team, dtype: float64




```python
fig = plt.figure()
your_labels = plt_wins.the_values
your_values = plt_wins.counts
ax = fig.add_subplot(111)
ax.axis('equal')
ax.pie(your_values, labels = your_values, autopct='%1.2f%%')
plt.show()
```


    
![png](output_68_0.png)
    



```python
# Derive a win/loss indicator
nfl['win'] = (nfl['winning_team'] == nfl['team'])
```


```python
# Next I want to specifically look at passers to derive efficiency with winning
passing_columns = ['pass_cmp', 'pass_att', 'pass_yds', 'pass_td', 'pass_int', 'pass_rating', 'win']
passing_data = nfl[passing_columns]
# Filtering out rows where pass attempts are zero to avoid skewing the analysis
passing_data = passing_data[passing_data['pass_att'] > 0]
```


```python
# average passing statistics for winning scenarios
passing_win_rate = passing_data.groupby('win').mean()
passing_win_rate
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
      <th>pass_cmp</th>
      <th>pass_att</th>
      <th>pass_yds</th>
      <th>pass_td</th>
      <th>pass_int</th>
      <th>pass_rating</th>
    </tr>
    <tr>
      <th>win</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>False</th>
      <td>18.325871</td>
      <td>28.419403</td>
      <td>204.355721</td>
      <td>1.308955</td>
      <td>0.645771</td>
      <td>89.695721</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Applying the provided logic to determine the winning team
conditions = [nfl['vis_score'] > nfl['home_score'],
              nfl['vis_score'] < nfl['home_score']]
choices = ['visitor', 'home']
nfl['winning_team'] = np.select(conditions, choices, default='tie')

# Adjusting the win/loss indicator
# A team wins if it is the home team and the winning_team is 'home', or if it is the visitor team and the winning_team is 'visitor'
nfl['win'] = ((nfl['team'] == nfl['vis_team']) & (nfl['winning_team'] == 'visitor')) | \
                  ((nfl['team'] == nfl['home_team']) & (nfl['winning_team'] == 'home'))

# Rechecking the average passing statistics for winning and losing scenarios
passing_data = nfl[passing_columns]
passing_data = passing_data[passing_data['pass_att'] > 0]
passing_win_rate = passing_data.groupby('win').mean()

passing_win_rate

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
      <th>pass_cmp</th>
      <th>pass_att</th>
      <th>pass_yds</th>
      <th>pass_td</th>
      <th>pass_int</th>
      <th>pass_rating</th>
    </tr>
    <tr>
      <th>win</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>False</th>
      <td>18.461463</td>
      <td>30.012683</td>
      <td>197.492683</td>
      <td>1.012683</td>
      <td>0.882927</td>
      <td>78.324488</td>
    </tr>
    <tr>
      <th>True</th>
      <td>18.184772</td>
      <td>26.761421</td>
      <td>211.497462</td>
      <td>1.617259</td>
      <td>0.398985</td>
      <td>101.528731</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Setting up the data for the bar graph
bar_data = passing_win_rate[['pass_td', 'pass_int']]

# Plotting
plt.figure(figsize=(10, 6))
bar_data.plot(kind='bar', rot=0)
plt.title('Average Passing Touchdowns and Interceptions for Winning and Losing Teams')
plt.xlabel('Winning Team')
plt.ylabel('Average Count')
plt.xticks([0, 1], ['Losing Teams', 'Winning Teams'])
plt.legend(title='Stat')
plt.grid(axis='y')

plt.show()
```


    <Figure size 1000x600 with 0 Axes>



    
![png](output_73_1.png)
    



```python
# Setting up the data for the bar graph
bar_data = passing_win_rate[['pass_td', 'pass_int']]

# Plotting
plt.figure(figsize=(10, 6))
bar_data.plot(kind='bar', rot=0)
plt.title('Average Passing Touchdowns and Interceptions for Winning and Losing Teams')
plt.xlabel('Winning Team')
plt.ylabel('Average Count')
plt.xticks([0, 1], ['Losing Teams', 'Winning Teams'])
plt.legend(title='Stat')
plt.grid(axis='y')

plt.show()
```


    <Figure size 1000x600 with 0 Axes>



    
![png](output_74_1.png)
    



```python
# Preparing data for scatter plot - passer rating vs win probability
scatter_data = passing_data[['pass_rating', 'win']]

# Binning passer ratings for better visualization
scatter_data['pass_rating_binned'] = pd.cut(scatter_data['pass_rating'], bins=10)

# Calculating win probability for each bin
win_probability = scatter_data.groupby('pass_rating_binned')['win'].mean()

# Plotting
plt.figure(figsize=(12, 6))
win_probability.plot(kind='bar', color='skyblue', rot=45)
plt.title('Win Probability by Passer Rating')
plt.xlabel('Passer Rating')
plt.ylabel('Win Probability')
plt.grid(axis='y')

plt.show()

```

    C:\Users\Owner\AppData\Local\Temp\ipykernel_18016\2005130408.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      scatter_data['pass_rating_binned'] = pd.cut(scatter_data['pass_rating'], bins=10)
    


    
![png](output_75_1.png)
    


# # Aanalyzing DATA on NFL plays


```python
plays = pd.read_csv("./FOOTBALL/ALL NFL pbp/plays.csv")
```


```python
# Making a year column from the game id info.

plays['year'] = plays['game_id'].astype(str).str[:4]
plays.head(3)
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
      <th>game_id</th>
      <th>play_id</th>
      <th>home_id</th>
      <th>away_id</th>
      <th>play_description</th>
      <th>quarter</th>
      <th>down</th>
      <th>yards_togo</th>
      <th>possession_team</th>
      <th>special_teams_play_type</th>
      <th>...</th>
      <th>penalty_jersey_numbers</th>
      <th>penalty_yards</th>
      <th>preSnapHomeScore</th>
      <th>presnap_visitor_score</th>
      <th>pass_result</th>
      <th>kick_length</th>
      <th>kick_return_yardage</th>
      <th>play_result</th>
      <th>absolute_yardline_number</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2021010315</td>
      <td>42</td>
      <td>SF</td>
      <td>SEA</td>
      <td>M.Wishnowsky kicks 65 yards from SF 35 to end ...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>SF</td>
      <td>Kickoff</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>75.0</td>
      <td>NaN</td>
      <td>40</td>
      <td>45</td>
      <td>2021</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2021010315</td>
      <td>175</td>
      <td>SF</td>
      <td>SEA</td>
      <td>(13:07) M.Dickson punts 47 yards to SF 20, Cen...</td>
      <td>1</td>
      <td>4</td>
      <td>12</td>
      <td>SEA</td>
      <td>Punt</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>47.0</td>
      <td>5.0</td>
      <td>42</td>
      <td>77</td>
      <td>2021</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2021010315</td>
      <td>283</td>
      <td>SF</td>
      <td>SEA</td>
      <td>(10:58) M.Wishnowsky punts 49 yards to SEA 17,...</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>SF</td>
      <td>Punt</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>49.0</td>
      <td>NaN</td>
      <td>49</td>
      <td>44</td>
      <td>2021</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 28 columns</p>
</div>




```python
# Number of times from 2019-2020 that an extra point kicked was missed
plays_19_20 = plays[plays['year'].isin(['2019', '2020'])]

plays_19_20['special_teams_result'].value_counts()

```




    Kick Attempt Good           3466
    Touchback                   3337
    Return                      3310
    Fair Catch                  1026
    Downed                       517
    Out of Bounds                416
    Kick Attempt No Good         389
    Muffed                       128
    Non-Special Teams Result      64
    Blocked Kick Attempt          46
    Blocked Punt                  23
    Kickoff Team Recovery         11
    Name: special_teams_result, dtype: int64




```python
# of the total kicks missed, how many were for extra point?

extra_point = plays_19_20[plays_19_20['special_teams_play_type'].isin(['Extra Point'])]
(extra_point['special_teams_result'].value_counts()/extra_point['special_teams_result'].count())*100

```




    Kick Attempt Good           92.921551
    Kick Attempt No Good         5.816050
    Blocked Kick Attempt         0.901713
    Non-Special Teams Result     0.360685
    Name: special_teams_result, dtype: float64




```python
# Heres a pie chart showing the extra point kick success rate

labels = 'Good', 'No Good', 'Blocked', 'Special Teams Play'
sizes = [92.92, 5.82, 0.92, 0.36]
explode = (0.1, 1, 2, 3)

fig1, ax1 = plt.subplots()
ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
        shadow=True, startangle=90)
ax1.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.

plt.show()

```


    
![png](output_81_0.png)
    



```python
# I feel that 2021 season experienced higher than average made extra point kicks. Let check it out. 
plays_2021 = plays[plays['year'].isin(['2021'])]
extra_point_2021 = plays_2021[plays_2021['special_teams_play_type'].isin(['Extra Point'])]
(extra_point_2021['special_teams_result'].value_counts()/extra_point_2021['special_teams_result'].count())*100
# The above findings shows there were no blocked extra point field goal attempts in 2021.
# It appears the rate of missed extra point attempts was about the same from 2019-2020 compared to 2021. 

```




    Kick Attempt Good       94.117647
    Kick Attempt No Good     5.882353
    Name: special_teams_result, dtype: float64



# Analyzing NFL play-by-play data


```python
# 2021 pbp data only shows plays of teams for the year of 2021. There are one or possibly 2 games missing for each team that were played in Janaury 2021
#  (relevant_plays['yard_gained'] >= 5)
pbp_data = pd.read_csv("./FOOTBALL/ALL NFL pbp/pbp-2021.csv")
```


```python
##Success Rate by play type

relevant_plays['yard_gained'] = pd.to_numeric(relevant_plays['yard_gained'], errors='coerce')

# Plays that are either passes or rushes
relevant_plays = pbp_data[(pbp_data['is_pass'] == 1) | (pbp_data['is_rush'] == 1)]
# Converting yards_gained to intgers
relevant_plays['yard_gained'] = pd.to_numeric(relevant_plays['yard_gained'], errors='coerce')
# Define success (you can adjust the criteria as per your analysis need)
relevant_plays['success'] = (relevant_plays['is_touchdown'] == 1) | \
                            (relevant_plays['series_first_down'] == 1) | \
                            (relevant_plays['yard_gained'] >= 5) | \
                            (relevant_plays['down_picked_up'] == 1)

# Plotting
plt.figure(figsize=(10, 6))
sns.barplot(x=success_rate.index, y=success_rate.values)
plt.title('Success Rate by Play Type')
plt.xlabel('Play Type')
plt.ylabel('Success Rate')
plt.show()
```

    C:\Users\Owner\AppData\Local\Temp\ipykernel_18016\1628489439.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      relevant_plays['yard_gained'] = pd.to_numeric(relevant_plays['yard_gained'], errors='coerce')
    C:\Users\Owner\AppData\Local\Temp\ipykernel_18016\1628489439.py:8: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      relevant_plays['yard_gained'] = pd.to_numeric(relevant_plays['yard_gained'], errors='coerce')
    C:\Users\Owner\AppData\Local\Temp\ipykernel_18016\1628489439.py:10: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      relevant_plays['success'] = (relevant_plays['is_touchdown'] == 1) | \
    


    
![png](output_85_1.png)
    



```python
# Printing success rates per play
success_rate = relevant_plays.groupby('play_type')['success'].mean()
success_rate
```




    play_type
    PASS        0.332381
    RUSH        0.239363
    SCRAMBLE    0.370023
    Name: success, dtype: float64




```python
pbp_data.columns

```




    Index(['gameId', 'game_date', 'quarter', 'minute', 'second', 'offense_team',
           'defense_team', 'down', 'togo', 'yard_line', 'penalty_type',
           'series_first_down', 'penalty_yards', 'isno_play', 'description',
           'season_year', 'Unnamed: 16', 'yards', 'yard_gained', 'down_picked_up',
           'formation', 'play_type', 'is_rush', 'is_pass', 'is_incomplete',
           'rush_yds', 'pass_yds', 'is_touchdown', 'pass_type', 'is_sack',
           'is_challenge', 'is_challenge_reversed', 'is_measurement',
           'is_interception', 'is_fumble', 'is_penalty', 'is_twopoint_conversion',
           'is_twopoint_conversion_success', 'rush_direction', 'yard_line_fixed',
           'yard_line_direction', 'is_penalty_accepted', 'penalty_team'],
          dtype='object')




```python

```


```python
## Turnover Analysis

# Filter plays that are turnovers
turnovers = pbp_data[(pbp_data['is_interception'] == 1) | (pbp_data['is_fumble'] == 1)]

# Count turnovers by type
turnover_counts = turnovers['play_type'].value_counts()

# Plotting
plt.figure(figsize=(8, 8))
turnover_counts.plot(kind='pie', autopct='%1.1f%%')
plt.title('Turnover Distribution by Play Type')
plt.ylabel('')  # Hide the y-label
plt.show()

```


    
![png](output_89_0.png)
    



```python
# Team yards during the 2021 year. Not season. 
pbp_data.groupby('offense_team')[['yards', 'is_touchdown', 'is_sack']].sum().sort_values(by = "yards", ascending = False)
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
      <th>yards</th>
      <th>is_touchdown</th>
      <th>is_sack</th>
    </tr>
    <tr>
      <th>offense_team</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>DAL</th>
      <td>6638</td>
      <td>51</td>
      <td>31</td>
    </tr>
    <tr>
      <th>TB</th>
      <td>6404</td>
      <td>55</td>
      <td>21</td>
    </tr>
    <tr>
      <th>LAC</th>
      <td>6324</td>
      <td>56</td>
      <td>33</td>
    </tr>
    <tr>
      <th>KC</th>
      <td>6251</td>
      <td>49</td>
      <td>28</td>
    </tr>
    <tr>
      <th>BUF</th>
      <td>6112</td>
      <td>54</td>
      <td>27</td>
    </tr>
    <tr>
      <th>BAL</th>
      <td>6039</td>
      <td>46</td>
      <td>51</td>
    </tr>
    <tr>
      <th>CIN</th>
      <td>6023</td>
      <td>54</td>
      <td>52</td>
    </tr>
    <tr>
      <th>ARI</th>
      <td>6022</td>
      <td>50</td>
      <td>37</td>
    </tr>
    <tr>
      <th>MIN</th>
      <td>5996</td>
      <td>45</td>
      <td>27</td>
    </tr>
    <tr>
      <th>LA</th>
      <td>5945</td>
      <td>52</td>
      <td>25</td>
    </tr>
    <tr>
      <th>LV</th>
      <td>5918</td>
      <td>40</td>
      <td>36</td>
    </tr>
    <tr>
      <th>PHI</th>
      <td>5848</td>
      <td>50</td>
      <td>29</td>
    </tr>
    <tr>
      <th>SF</th>
      <td>5844</td>
      <td>48</td>
      <td>32</td>
    </tr>
    <tr>
      <th>NE</th>
      <td>5720</td>
      <td>46</td>
      <td>27</td>
    </tr>
    <tr>
      <th>GB</th>
      <td>5612</td>
      <td>48</td>
      <td>29</td>
    </tr>
    <tr>
      <th>IND</th>
      <td>5591</td>
      <td>48</td>
      <td>33</td>
    </tr>
    <tr>
      <th>CLE</th>
      <td>5510</td>
      <td>37</td>
      <td>40</td>
    </tr>
    <tr>
      <th>TEN</th>
      <td>5499</td>
      <td>42</td>
      <td>45</td>
    </tr>
    <tr>
      <th>DEN</th>
      <td>5250</td>
      <td>36</td>
      <td>40</td>
    </tr>
    <tr>
      <th>WAS</th>
      <td>5208</td>
      <td>37</td>
      <td>37</td>
    </tr>
    <tr>
      <th>NYJ</th>
      <td>5104</td>
      <td>33</td>
      <td>47</td>
    </tr>
    <tr>
      <th>PIT</th>
      <td>5063</td>
      <td>32</td>
      <td>35</td>
    </tr>
    <tr>
      <th>MIA</th>
      <td>5044</td>
      <td>32</td>
      <td>38</td>
    </tr>
    <tr>
      <th>CHI</th>
      <td>5029</td>
      <td>32</td>
      <td>52</td>
    </tr>
    <tr>
      <th>CAR</th>
      <td>5023</td>
      <td>32</td>
      <td>44</td>
    </tr>
    <tr>
      <th>DET</th>
      <td>4935</td>
      <td>29</td>
      <td>35</td>
    </tr>
    <tr>
      <th>NO</th>
      <td>4912</td>
      <td>43</td>
      <td>39</td>
    </tr>
    <tr>
      <th>JAX</th>
      <td>4893</td>
      <td>30</td>
      <td>32</td>
    </tr>
    <tr>
      <th>ATL</th>
      <td>4874</td>
      <td>34</td>
      <td>34</td>
    </tr>
    <tr>
      <th>NYG</th>
      <td>4856</td>
      <td>27</td>
      <td>32</td>
    </tr>
    <tr>
      <th>SEA</th>
      <td>4679</td>
      <td>39</td>
      <td>44</td>
    </tr>
    <tr>
      <th>HOU</th>
      <td>4415</td>
      <td>27</td>
      <td>42</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Most penalized team

# Filter plays where a penalty occurred
penalty_plays = pbp_data[pbp_data['is_penalty'] == 1]
# Penalties for each team on offense
offense_penalties = penalty_plays['offense_team'].value_counts()
# Penalties for each team on defense
defense_penalties = penalty_plays['defense_team'].value_counts()
# Combine counts to get total penalties for each team
total_penalties = offense_penalties.add(defense_penalties, fill_value=0)
# Create a DataFrame for the consolidated information
teams_penalties = pd.DataFrame({
    'Team': total_penalties.index,
    'Offensive Penalties': offense_penalties,
    'Defensive Penalties': defense_penalties,
    'Total Penalties': total_penalties
}).reset_index(drop=True)
# The Result
print(teams_penalties)
```

       Team  Offensive Penalties  Defensive Penalties  Total Penalties
    0   ARI                   99                  112              211
    1   ATL                  103                  109              212
    2   BAL                  105                  107              212
    3   BUF                  110                  118              228
    4   CAR                  102                  125              227
    5   CHI                  101                  116              217
    6   CIN                   93                  100              193
    7   CLE                   98                  121              219
    8   DAL                  121                  134              255
    9   DEN                  102                   88              190
    10  DET                  128                   88              216
    11   GB                   89                   85              174
    12  HOU                  115                   89              204
    13  IND                  108                   85              193
    14  JAX                  115                   95              210
    15   KC                  125                  101              226
    16   LA                   75                   98              173
    17  LAC                  108                  109              217
    18   LV                  115                  105              220
    19  MIA                  113                  105              218
    20  MIN                  105                  105              210
    21   NE                   98                   94              192
    22   NO                   95                   91              186
    23  NYG                  106                   87              193
    24  NYJ                   87                  114              201
    25  PHI                   96                  103              199
    26  PIT                  126                  117              243
    27  SEA                   93                   96              189
    28   SF                   88                  107              195
    29   TB                   89                   94              183
    30  TEN                  105                  121              226
    31  WAS                  101                   95              196
    


```python
# Average number of penalties called per NFL game 2019-2021


# Count the total number of penalties
total_penalties = pbp_data[pbp_data['is_penalty'] == 1].shape[0]
# Count the total number of unique games
total_games = pbp_data['gameId'].nunique()

# Calculate the average number of penalties per game
average_penalties_per_game = total_penalties / total_games

# Print the result
print(f"Average number of penalties per game: {average_penalties_per_game}")
```

    Average number of penalties per game: 13.808333333333334
    


```python
# The sucess rate of picking up a 4th and down

fourth_down_plays = pbp_data[pbp_data['down'] == 4]

# Determine success (first down or touchdown)
fourth_down_successes = fourth_down_plays[(fourth_down_plays['series_first_down'] == 1) | (fourth_down_plays['is_touchdown'] == 1)]
# Calculate success rate
success_rate = len(fourth_down_successes) / len(fourth_down_plays)
# Print the success rate
print(f"Success rate of picking up a 4th down: {success_rate:.2%}")
```

    Success rate of picking up a 4th down: 10.09%
    


```python
# Heres a bar chart showing all the successful and unsuccessful 4th down conversions by quarter.
#Teams tend to take more chance and go for it in the 2nd and 4th quarter.

labels = ['Q1', 'Q2', 'Q3', 'Q4', 'OT']
successful = [61, 81, 69, 150, 4]
unsuccessful = [68, 110, 91, 246, 3]

x = np.arange(len(labels))  # the label locations
width = 0.20  # the width of the bars

# Adjust the figsize (width, height) to make the plot smaller
fig, ax = plt.subplots(figsize=(6, 4))  # Example: 6 inches by 4 inches
rects1 = ax.bar(x - width/2, successful, width, label='Successful')
rects2 = ax.bar(x + width/2, unsuccessful, width, label='Unsuccessful')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Instances')
ax.set_title('Success Rates by Quarter')
ax.set_xticks(x)
ax.set_xticklabels(labels)
ax.legend()

ax.bar_label(rects1, padding=3)
ax.bar_label(rects2, padding=3)

fig.tight_layout()

plt.show()
```


    
![png](output_94_0.png)
    


## Team specific Analytics using pbp data


```python
# First lets take my team, the New Orleans Saints
# Match playtype with the team

saints_pbp = pbp_data[pbp_data['offense_team'].isin(['NO'])]
```


```python
# Sum by playtype for the Saints

saints_counts = saints_pbp["play_type"].value_counts()
saints_counts
```




    PASS                    471
    RUSH                    392
    PUNT                     81
    KICK OFF                 72
    SACK                     39
    EXTRA POINT              34
    SCRAMBLE                 32
    NO PLAY                  30
    FIELD GOAL               22
    QB KNEEL                 11
    TWO-POINT CONVERSION      5
    FUMBLES                   1
    Name: play_type, dtype: int64




```python
# Offensive Efficiency by downs. Total yards on average gained on different downs
# Saints

efficiency_by_down = saints_pbp.groupby('down')['yards'].mean()
print("Offensive Efficiency on Different Downs:")
print(efficiency_by_down)
```

    Offensive Efficiency on Different Downs:
    down
    0    0.000000
    1    4.940476
    2    5.167173
    3    5.280193
    4    0.335878
    Name: yards, dtype: float64
    


```python
# Red Zone Success Rate
# Saints

#all redzone plays
red_zone_plays = saints_pbp[(saints_pbp['yard_line'] <= 20) & (saints_pbp['yard_line'] > 0)]
red_zone_successes = red_zone_plays[red_zone_plays['is_touchdown'] == 1]
red_zone_success_rate = len(red_zone_successes) / len(red_zone_plays)
print("\nRed Zone Saints Success Rate:")
print(f"{red_zone_success_rate:.2%}")
```

    
    Red Zone Saints Success Rate:
    0.85%
    


```python
tracking.columns
```




    Index(['time', 'x', 'y', 's', 'a', 'dis', 'o', 'dir', 'event', 'nflId',
           'displayName', 'jerseyNumber', 'position', 'team', 'frameId', 'gameId',
           'playId', 'playDirection'],
          dtype='object')




```python
# Identifiers in the team column
print(tracking['team'].unique())
```

    ['home' 'away' 'football']
    


```python
# More saints 2021 stats using pbp
offense_list =  ['series_first_down', 'penalty_yards', 'yards', 'is_rush', 'is_pass', 'is_touchdown', 'is_incomplete', 'is_sack', 'is_challenge', 'is_challenge_reversed', 'is_measurement', 'is_fumble', 'is_penalty', 'is_penalty_accepted']
saints_offense = saints_pbp_2021[offense_list]
saints_offense.sum()
```




    series_first_down         350
    penalty_yards             716
    yards                    4912
    is_rush                   424
    is_pass                   471
    is_touchdown               43
    is_incomplete             187
    is_sack                    39
    is_challenge                0
    is_challenge_reversed       0
    is_measurement              0
    is_fumble                  14
    is_penalty                 95
    is_penalty_accepted        86
    dtype: int64




```python
#league average offensive metrics
league_offense = pbp_2021[offense_list]
league_offense.sum()/32
# The NO Saints were below league averages in most categories. 
```




    series_first_down         502.12500
    penalty_yards             769.68750
    yards                    5518.15625
    is_rush                   391.71875
    is_pass                   546.71875
    is_touchdown               41.68750
    is_incomplete             186.50000
    is_sack                    36.06250
    is_challenge                3.65625
    is_challenge_reversed       1.56250
    is_measurement              0.00000
    is_fumble                  18.15625
    is_penalty                103.56250
    is_penalty_accepted        91.59375
    dtype: float64




```python
# For fantasy Foorball

# Passing
POINTS_PASS_TD = 4
POINTS_PASS_25_YARDS = 1
POINTS_PASS_2PT_CONVERSION = 2
POINTS_PASS_INTERCEPTED = -2

# Rushing
POINTS_RUSH_TD = 6
POINTS_RUSH_10_YARDS = 1
POINTS_RUSH_2PT_CONVERSION = 2

# Receiving
POINTS_RECEIVE_TD = 6
POINTS_RECEIVE_10_YARDS = 1
POINTS_RECEIVE_2PT_CONVERSION = 2

# Misc. Offense
POINTS_KICKOFF_RETURN_TD = 6
POINTS_PUNT_RETURN_TD = 6
POINTS_FUMBLE_RECOVERED = 6
POINTS_FUMBLE_LOST = -2








```


```python
run_plays = pbp_2021[pbp_2021['play_type'] == 'RUSH']
```

# Player specific Analysis


```python
#  Stats on Lamar Jackson, QB
big_truss = pbp_2021[pbp_2021['description'].str.contains('L.JACKSON')]
cool_joe = pbp_2021[pbp_2021['description'].str.contains('J.BURROW')]
```


```python
# Lamar, formation, play type, yards on play, rush, pass
for index, row in big_truss.iterrows():
    if 'L.JACKSON' in row['description']:
        print(index, row['formation'], row['play_type'],
             row['yards'], row['is_rush'], row['is_pass'])

```

    50 SHOTGUN PASS 10 0 1
    67 SHOTGUN PASS 8 0 1
    79 SHOTGUN PASS 7 0 1
    168 SHOTGUN SCRAMBLE 2 1 0
    184 SHOTGUN PASS 1 0 1
    185 SHOTGUN PASS 1 0 1
    234 SHOTGUN FUMBLES 0 0 0
    374 SHOTGUN RUSH -1 1 0
    402 SHOTGUN RUSH -3 1 0
    408 SHOTGUN SACK -4 0 0
    437 SHOTGUN PASS -5 0 1
    463 SHOTGUN SACK -6 0 0
    740 SHOTGUN PASS 49 0 1
    741 SHOTGUN PASS 49 0 1
    812 SHOTGUN PASS 43 0 1
    825 UNDER CENTER PASS 42 0 1
    868 SHOTGUN PASS 41 0 1
    904 SHOTGUN PASS 39 0 1
    912 SHOTGUN PASS 39 0 1
    925 SHOTGUN SCRAMBLE 39 1 0
    973 SHOTGUN PASS 37 0 1
    998 SHOTGUN PASS 36 0 1
    1013 SHOTGUN PASS 35 0 1
    1074 SHOTGUN PASS 34 0 1
    1133 SHOTGUN PASS 32 0 1
    1160 SHOTGUN PASS 32 0 1
    1219 SHOTGUN SCRAMBLE 31 1 0
    1226 SHOTGUN PASS 30 0 1
    1237 SHOTGUN PASS 30 0 1
    1276 SHOTGUN PASS 29 0 1
    1285 SHOTGUN PASS 29 0 1
    1288 SHOTGUN PASS 29 0 1
    1327 SHOTGUN PASS 29 0 1
    1355 SHOTGUN PASS 28 0 1
    1391 SHOTGUN PASS 28 0 1
    1409 SHOTGUN SCRAMBLE 28 1 0
    1467 SHOTGUN PASS 27 0 1
    1474 SHOTGUN PASS 27 0 1
    1481 SHOTGUN PASS 27 0 1
    1650 SHOTGUN PASS 25 0 1
    1706 SHOTGUN PASS 24 0 1
    1767 SHOTGUN PASS 24 0 1
    1786 SHOTGUN PASS 24 0 1
    1908 SHOTGUN PASS 23 0 1
    1964 SHOTGUN PASS 22 0 1
    1995 SHOTGUN PASS 22 0 1
    1997 SHOTGUN PASS 22 0 1
    2005 SHOTGUN PASS 22 0 1
    2100 SHOTGUN SCRAMBLE 22 1 0
    2122 SHOTGUN PASS 21 0 1
    2229 SHOTGUN PASS 21 0 1
    2233 SHOTGUN PASS 21 0 1
    2244 SHOTGUN RUSH 21 1 0
    2301 SHOTGUN PASS 20 0 1
    2309 SHOTGUN PASS 20 0 1
    2322 SHOTGUN PASS 20 0 1
    2370 SHOTGUN PASS 20 0 1
    2379 SHOTGUN PASS 20 0 1
    2394 SHOTGUN PASS 20 0 1
    2405 SHOTGUN PASS 20 0 1
    2407 SHOTGUN PASS 20 0 1
    2424 UNDER CENTER PASS 20 0 1
    2476 SHOTGUN SCRAMBLE 20 1 0
    2534 SHOTGUN PASS 19 0 1
    2633 NO HUDDLE SHOTGUN PASS 19 0 1
    2658 SHOTGUN PASS 19 0 1
    2661 SHOTGUN PASS 19 0 1
    2713 SHOTGUN PASS 18 0 1
    2719 NO HUDDLE SHOTGUN PASS 18 0 1
    2723 SHOTGUN PASS 18 0 1
    2744 SHOTGUN PASS 18 0 1
    2855 SHOTGUN PASS 18 0 1
    2873 SHOTGUN PASS 18 0 1
    2960 UNDER CENTER SCRAMBLE 18 1 0
    3019 SHOTGUN PASS 17 0 1
    3051 SHOTGUN PASS 17 0 1
    3145 SHOTGUN PASS 17 0 1
    3149 SHOTGUN PASS 17 0 1
    3159 SHOTGUN PASS 17 0 1
    3182 SHOTGUN PASS 17 0 1
    3273 SHOTGUN PASS 16 0 1
    3295 SHOTGUN PASS 16 0 1
    3319 SHOTGUN PASS 16 0 1
    3333 SHOTGUN PASS 16 0 1
    3559 SHOTGUN RUSH 16 1 0
    3592 SHOTGUN PASS 15 0 1
    3623 NO HUDDLE SHOTGUN PASS 15 0 1
    3680 SHOTGUN PASS 15 0 1
    3691 SHOTGUN PASS 15 0 1
    3764 SHOTGUN PASS 15 0 1
    3774 SHOTGUN PASS 15 0 1
    3817 SHOTGUN PASS 15 0 1
    3890 SHOTGUN RUSH 15 1 0
    4040 SHOTGUN PASS 14 0 1
    4051 SHOTGUN PASS 14 0 1
    4087 SHOTGUN PASS 14 0 1
    4181 SHOTGUN PASS 14 0 1
    4260 SHOTGUN PASS 14 0 1
    4413 SHOTGUN RUSH 14 1 0
    4453 SHOTGUN PASS 13 0 1
    4461 SHOTGUN PASS 13 0 1
    4465 SHOTGUN PASS 13 0 1
    4486 SHOTGUN PASS 13 0 1
    4526 SHOTGUN PASS 13 0 1
    4599 SHOTGUN PASS 13 0 1
    4600 SHOTGUN PASS 13 0 1
    4645 SHOTGUN PASS 13 0 1
    4655 SHOTGUN PASS 13 0 1
    4656 SHOTGUN PASS 13 0 1
    4657 SHOTGUN PASS 13 0 1
    4685 SHOTGUN PASS 13 0 1
    4722 SHOTGUN PASS 13 0 1
    4769 SHOTGUN PASS 13 0 1
    4784 SHOTGUN SCRAMBLE 13 1 0
    4844 SHOTGUN SCRAMBLE 13 1 0
    4885 SHOTGUN SCRAMBLE 13 1 0
    4962 NO HUDDLE SHOTGUN PASS 12 0 1
    5211 SHOTGUN PASS 12 0 1
    5278 SHOTGUN PASS 12 0 1
    5303 SHOTGUN PASS 12 0 1
    5340 SHOTGUN PASS 12 0 1
    5422 SHOTGUN RUSH 12 1 0
    5441 SHOTGUN SCRAMBLE 12 1 0
    5499 SHOTGUN RUSH 12 1 0
    5517 SHOTGUN SCRAMBLE 12 1 0
    5599 SHOTGUN PASS 11 0 1
    5608 SHOTGUN PASS 11 0 1
    5611 SHOTGUN PASS 11 0 1
    5622 SHOTGUN PASS 11 0 1
    5659 SHOTGUN PASS 11 0 1
    5661 SHOTGUN PASS 11 0 1
    5700 SHOTGUN PASS 11 0 1
    5722 SHOTGUN PASS 11 0 1
    5732 SHOTGUN PASS 11 0 1
    5748 SHOTGUN PASS 11 0 1
    5890 SHOTGUN PASS 11 0 1
    5895 SHOTGUN PASS 11 0 1
    5957 SHOTGUN PASS 11 0 1
    5989 SHOTGUN PASS 11 0 1
    6165 SHOTGUN RUSH 11 1 0
    6175 SHOTGUN RUSH 11 1 0
    6186 NO HUDDLE SHOTGUN SCRAMBLE 11 1 0
    6247 SHOTGUN RUSH 11 1 0
    6248 SHOTGUN SCRAMBLE 11 1 0
    6320 SHOTGUN RUSH 11 1 0
    6333 SHOTGUN SCRAMBLE 11 1 0
    6366 SHOTGUN PASS 10 0 1
    6400 SHOTGUN PASS 10 0 1
    6439 SHOTGUN PASS 10 0 1
    6531 SHOTGUN PASS 10 0 1
    6598 SHOTGUN PASS 10 0 1
    6738 NO HUDDLE SHOTGUN PASS 10 0 1
    6816 SHOTGUN PASS 10 0 1
    6822 SHOTGUN PASS 10 0 1
    7003 SHOTGUN RUSH 10 1 0
    7018 SHOTGUN SCRAMBLE 10 1 0
    7019 SHOTGUN SCRAMBLE 10 1 0
    7182 SHOTGUN PASS 9 0 1
    7188 SHOTGUN PASS 9 0 1
    7228 SHOTGUN PASS 9 0 1
    7319 SHOTGUN PASS 9 0 1
    7320 SHOTGUN PASS 9 0 1
    7354 SHOTGUN PASS 9 0 1
    7355 SHOTGUN PASS 9 0 1
    7468 SHOTGUN PASS 9 0 1
    7562 NO HUDDLE SHOTGUN PASS 9 0 1
    7593 SHOTGUN PASS 9 0 1
    7679 SHOTGUN PASS 9 0 1
    7680 SHOTGUN PASS 9 0 1
    7682 NO HUDDLE SHOTGUN PASS 9 0 1
    7717 SHOTGUN PASS 9 0 1
    7758 SHOTGUN PASS 9 0 1
    7915 SHOTGUN RUSH 9 1 0
    7929 SHOTGUN SCRAMBLE 9 1 0
    8004 SHOTGUN RUSH 9 1 0
    8103 SHOTGUN RUSH 9 1 0
    8169 SHOTGUN RUSH 9 1 0
    8170 SHOTGUN RUSH 9 1 0
    8174 SHOTGUN RUSH 9 1 0
    8175 SHOTGUN RUSH 9 1 0
    8236 SHOTGUN PASS 8 0 1
    8250 SHOTGUN PASS 8 0 1
    8281 NO HUDDLE SHOTGUN PASS 8 0 1
    8355 SHOTGUN PASS 8 0 1
    8394 NO HUDDLE SHOTGUN PASS 8 0 1
    8402 NO HUDDLE SHOTGUN PASS 8 0 1
    8425 SHOTGUN PASS 8 0 1
    8450 SHOTGUN PASS 8 0 1
    8542 SHOTGUN PASS 8 0 1
    8543 SHOTGUN PASS 8 0 1
    8616 SHOTGUN PASS 8 0 1
    8617 SHOTGUN PASS 8 0 1
    8631 SHOTGUN PASS 8 0 1
    8705 SHOTGUN PASS 8 0 1
    8717 SHOTGUN PASS 8 0 1
    8722 SHOTGUN PASS 8 0 1
    8723 SHOTGUN PASS 8 0 1
    8724 SHOTGUN PASS 8 0 1
    8751 SHOTGUN PASS 8 0 1
    8815 SHOTGUN PASS 8 0 1
    8816 SHOTGUN PASS 8 0 1
    8834 SHOTGUN PASS 8 0 1
    8959 SHOTGUN RUSH 8 1 0
    8998 SHOTGUN SCRAMBLE 8 1 0
    9024 SHOTGUN SCRAMBLE 8 1 0
    9025 SHOTGUN RUSH 8 1 0
    9114 SHOTGUN SCRAMBLE 8 1 0
    9279 SHOTGUN SCRAMBLE 8 1 0
    9411 SHOTGUN PASS 7 0 1
    9438 SHOTGUN PASS 7 0 1
    9462 SHOTGUN PASS 7 0 1
    9580 SHOTGUN PASS 7 0 1
    9587 SHOTGUN PASS 7 0 1
    9779 SHOTGUN PASS 7 0 1
    9780 SHOTGUN PASS 7 0 1
    9893 SHOTGUN PASS 7 0 1
    9894 SHOTGUN PASS 7 0 1
    9924 SHOTGUN PASS 7 0 1
    9928 SHOTGUN PASS 7 0 1
    10005 SHOTGUN PASS 7 0 1
    10006 SHOTGUN PASS 7 0 1
    10008 NO HUDDLE SHOTGUN PASS 7 0 1
    10009 SHOTGUN PASS 7 0 1
    10011 SHOTGUN PASS 7 0 1
    10016 NO HUDDLE SHOTGUN PASS 7 0 1
    10017 SHOTGUN PASS 7 0 1
    10052 SHOTGUN PASS 7 0 1
    10053 SHOTGUN PASS 7 0 1
    10061 SHOTGUN PASS 7 0 1
    10123 SHOTGUN PASS 7 0 1
    10142 SHOTGUN PASS 7 0 1
    10329 SHOTGUN RUSH 7 1 0
    10556 SHOTGUN SCRAMBLE 7 1 0
    10557 NO HUDDLE SHOTGUN SCRAMBLE 7 1 0
    10591 SHOTGUN SCRAMBLE 7 1 0
    10598 SHOTGUN SCRAMBLE 7 1 0
    10600 SHOTGUN RUSH 7 1 0
    10673 SHOTGUN SCRAMBLE 7 1 0
    10770 SHOTGUN PASS 6 0 1
    10843 NO HUDDLE SHOTGUN PASS 6 0 1
    10891 SHOTGUN PASS 6 0 1
    10893 SHOTGUN PASS 6 0 1
    10903 SHOTGUN PASS 6 0 1
    10912 SHOTGUN PASS 6 0 1
    10933 SHOTGUN PASS 6 0 1
    10948 SHOTGUN PASS 6 0 1
    10974 SHOTGUN PASS 6 0 1
    11018 SHOTGUN PASS 6 0 1
    11152 SHOTGUN PASS 6 0 1
    11260 SHOTGUN PASS 6 0 1
    11262 SHOTGUN PASS 6 0 1
    11288 SHOTGUN PASS 6 0 1
    11346 SHOTGUN PASS 6 0 1
    11379 SHOTGUN PASS 6 0 1
    11486 SHOTGUN PASS 6 0 1
    11514 SHOTGUN PASS 6 0 1
    11515 SHOTGUN PASS 6 0 1
    11611 SHOTGUN RUSH 6 1 0
    11617 SHOTGUN RUSH 6 1 0
    11782 SHOTGUN SCRAMBLE 6 1 0
    11810 SHOTGUN SCRAMBLE 6 1 0
    11945 SHOTGUN RUSH 6 1 0
    12041 NO HUDDLE SHOTGUN SCRAMBLE 6 1 0
    12042 SHOTGUN RUSH 6 1 0
    12105 SHOTGUN RUSH 6 1 0
    12136 SHOTGUN RUSH 6 1 0
    12137 SHOTGUN SCRAMBLE 6 1 0
    12139 NO HUDDLE SHOTGUN SCRAMBLE 6 1 0
    12147 SHOTGUN RUSH 6 1 0
    12369 SHOTGUN PASS 5 0 1
    12374 SHOTGUN PASS 5 0 1
    12403 NO HUDDLE SHOTGUN PASS 5 0 1
    12499 SHOTGUN PASS 5 0 1
    12556 SHOTGUN PASS 5 0 1
    12565 SHOTGUN PASS 5 0 1
    12699 SHOTGUN PASS 5 0 1
    12700 SHOTGUN PASS 5 0 1
    12701 SHOTGUN PASS 5 0 1
    12812 NO HUDDLE SHOTGUN PASS 5 0 1
    12814 SHOTGUN PASS 5 0 1
    12837 SHOTGUN PASS 5 0 1
    12942 SHOTGUN PASS 5 0 1
    12943 SHOTGUN PASS 5 0 1
    13040 SHOTGUN PASS 5 0 1
    13042 SHOTGUN PASS 5 0 1
    13148 SHOTGUN RUSH 5 1 0
    13242 UNDER CENTER RUSH 5 1 0
    13322 SHOTGUN RUSH 5 1 0
    13375 SHOTGUN SCRAMBLE 5 1 0
    13378 SHOTGUN RUSH 5 1 0
    13449 SHOTGUN RUSH 5 1 0
    13605 SHOTGUN RUSH 5 1 0
    13735 SHOTGUN SCRAMBLE 5 1 0
    13763 UNDER CENTER RUSH 5 1 0
    13765 SHOTGUN RUSH 5 1 0
    13846 SHOTGUN SCRAMBLE 5 1 0
    13883 SHOTGUN SCRAMBLE 5 1 0
    13941 SHOTGUN RUSH 5 1 0
    14180 NO HUDDLE SHOTGUN PASS 4 0 1
    14181 SHOTGUN PASS 4 0 1
    14183 SHOTGUN PASS 4 0 1
    14239 SHOTGUN PASS 4 0 1
    14299 SHOTGUN PASS 4 0 1
    14300 NO HUDDLE SHOTGUN PASS 4 0 1
    14322 NO HUDDLE SHOTGUN PASS 4 0 1
    14446 SHOTGUN PASS 4 0 1
    14508 SHOTGUN PASS 4 0 1
    14601 SHOTGUN PASS 4 0 1
    14607 SHOTGUN PASS 4 0 1
    14608 SHOTGUN PASS 4 0 1
    14634 SHOTGUN PASS 4 0 1
    14636 SHOTGUN PASS 4 0 1
    14711 SHOTGUN PASS 4 0 1
    14712 SHOTGUN PASS 4 0 1
    14905 SHOTGUN SCRAMBLE 4 1 0
    14972 SHOTGUN RUSH 4 1 0
    15180 SHOTGUN SCRAMBLE 4 1 0
    15224 SHOTGUN SCRAMBLE 4 1 0
    15655 SHOTGUN SCRAMBLE 4 1 0
    15790 SHOTGUN RUSH 4 1 0
    15954 SHOTGUN SCRAMBLE 4 1 0
    16017 SHOTGUN RUSH 4 1 0
    16090 SHOTGUN PASS 3 0 1
    16097 SHOTGUN PASS 3 0 1
    16265 SHOTGUN PASS 3 0 1
    16407 SHOTGUN PASS 3 0 1
    16424 SHOTGUN PASS 3 0 1
    16425 SHOTGUN PASS 3 0 1
    16471 SHOTGUN PASS 3 0 1
    16497 SHOTGUN PASS 3 0 1
    16561 SHOTGUN PASS 3 0 1
    16706 SHOTGUN RUSH 3 1 0
    16966 SHOTGUN RUSH 3 1 0
    16997 SHOTGUN SCRAMBLE 3 1 0
    16998 SHOTGUN SCRAMBLE 3 1 0
    17018 SHOTGUN RUSH 3 1 0
    17038 SHOTGUN RUSH 3 1 0
    17098 SHOTGUN SCRAMBLE 3 1 0
    17395 SHOTGUN RUSH 3 1 0
    17614 SHOTGUN SCRAMBLE 3 1 0
    17706 SHOTGUN SCRAMBLE 3 1 0
    17785 SHOTGUN RUSH 3 1 0
    18080 SHOTGUN PASS 2 0 1
    18198 SHOTGUN PASS 2 0 1
    18262 SHOTGUN PASS 2 0 1
    18382 SHOTGUN PASS 2 0 1
    18439 SHOTGUN PASS 2 0 1
    18756 SHOTGUN RUSH 2 1 0
    18865 SHOTGUN SCRAMBLE 2 1 0
    18927 SHOTGUN RUSH 2 1 0
    19352 SHOTGUN SCRAMBLE 2 1 0
    19549 SHOTGUN RUSH 2 1 0
    19550 SHOTGUN RUSH 2 1 0
    19620 SHOTGUN SCRAMBLE 2 1 0
    19740 SHOTGUN RUSH 2 1 0
    19796 UNDER CENTER RUSH 2 1 0
    19872 UNDER CENTER SCRAMBLE 2 1 0
    19998 SHOTGUN SCRAMBLE 2 1 0
    20020 SHOTGUN RUSH 2 1 0
    20021 SHOTGUN RUSH 2 1 0
    20022 SHOTGUN RUSH 2 1 0
    20061 SHOTGUN SCRAMBLE 2 1 0
    20081 SHOTGUN SCRAMBLE 2 1 0
    20344 SHOTGUN PASS 1 0 1
    20384 SHOTGUN PASS 1 0 1
    20529 SHOTGUN RUSH 1 1 0
    20749 SHOTGUN RUSH 1 1 0
    20912 SHOTGUN RUSH 1 1 0
    20940 SHOTGUN RUSH 1 1 0
    21141 SHOTGUN RUSH 1 1 0
    21145 SHOTGUN RUSH 1 1 0
    21329 SHOTGUN RUSH 1 1 0
    21373 UNDER CENTER RUSH 1 1 0
    21374 SHOTGUN RUSH 1 1 0
    21544 SHOTGUN SCRAMBLE 1 1 0
    21618 SHOTGUN RUSH 1 1 0
    21756 SHOTGUN RUSH 1 1 0
    21757 SHOTGUN RUSH 1 1 0
    22980 SHOTGUN PASS 0 0 1
    22982 SHOTGUN PASS 0 0 1
    22983 SHOTGUN PASS 0 0 1
    23092 SHOTGUN PASS 0 0 1
    23098 SHOTGUN PASS 0 0 1
    23099 SHOTGUN PASS 0 0 1
    23805 SHOTGUN PASS 0 0 1
    23806 SHOTGUN PASS 0 0 1
    23807 NO HUDDLE CLOCK STOP 0 0 0
    23810 SHOTGUN PASS 0 0 1
    23833 SHOTGUN PASS 0 0 1
    23834 SHOTGUN PASS 0 0 1
    23835 SHOTGUN PASS 0 0 1
    23903 NO HUDDLE SHOTGUN PASS 0 0 1
    24017 SHOTGUN PASS 0 0 1
    24021 UNDER CENTER PASS 0 0 1
    24222 SHOTGUN PASS 0 0 1
    24291 SHOTGUN PASS 0 0 1
    24320 SHOTGUN PASS 0 0 1
    24321 SHOTGUN PASS 0 0 1
    24645 SHOTGUN PASS 0 0 1
    24825 UNDER CENTER TWO-POINT CONVERSION 0 0 0
    24827 UNDER CENTER TWO-POINT CONVERSION 0 0 0
    25108 SHOTGUN PASS 0 0 1
    25148 UNDER CENTER TWO-POINT CONVERSION 0 0 0
    25149 UNDER CENTER TWO-POINT CONVERSION 0 0 0
    25206 SHOTGUN PASS 0 0 1
    25411 SHOTGUN PASS 0 0 1
    25999 SHOTGUN PASS 0 0 1
    26157 UNDER CENTER QB KNEEL 0 0 0
    26587 SHOTGUN PASS 0 0 1
    26726 SHOTGUN PASS 0 0 1
    26882 UNDER CENTER TWO-POINT CONVERSION 0 0 0
    26884 SHOTGUN PASS 0 0 1
    26964 SHOTGUN SACK 0 0 0
    27111 SHOTGUN PASS 0 0 1
    27263 SHOTGUN PASS 0 0 1
    27330 NO HUDDLE SHOTGUN PASS 0 0 1
    27331 SHOTGUN PASS 0 0 1
    27495 SHOTGUN PASS 0 0 1
    27541 SHOTGUN PASS 0 0 1
    27669 SHOTGUN PASS 0 0 1
    28242 SHOTGUN RUSH 0 1 0
    28534 SHOTGUN PASS 0 0 1
    28535 SHOTGUN PASS 0 0 1
    28540 SHOTGUN PASS 0 0 1
    28543 SHOTGUN PASS 0 0 1
    28544 SHOTGUN PASS 0 0 1
    28640 SHOTGUN PASS 0 0 1
    28641 SHOTGUN PASS 0 0 1
    28646 SHOTGUN PASS 0 0 1
    28653 SHOTGUN PASS 0 0 1
    28748 SHOTGUN SACK 0 0 0
    30975 UNDER CENTER TWO-POINT CONVERSION 0 0 0
    31409 UNDER CENTER QB KNEEL 0 0 0
    31410 UNDER CENTER QB KNEEL 0 0 0
    31417 SHOTGUN PASS 0 0 1
    31418 SHOTGUN PASS 0 0 1
    31421 SHOTGUN PASS 0 0 1
    31423 SHOTGUN PASS 0 0 1
    31433 SHOTGUN PASS 0 0 1
    31434 SHOTGUN PASS 0 0 1
    31435 SHOTGUN PASS 0 0 1
    31442 SHOTGUN PASS 0 0 1
    31443 SHOTGUN PASS 0 0 1
    31453 UNDER CENTER PASS 0 0 1
    31455 SHOTGUN PASS 0 0 1
    31461 SHOTGUN PASS 0 0 1
    31464 SHOTGUN PASS 0 0 1
    31651 UNDER CENTER QB KNEEL 0 0 0
    33726 SHOTGUN PASS 0 0 1
    33727 NO HUDDLE CLOCK STOP 0 0 0
    33735 SHOTGUN PASS 0 0 1
    33739 SHOTGUN PASS 0 0 1
    33743 SHOTGUN PASS 0 0 1
    33744 SHOTGUN PASS 0 0 1
    33745 NO HUDDLE SHOTGUN PASS 0 0 1
    33747 SHOTGUN PASS 0 0 1
    33748 SHOTGUN PASS 0 0 1
    33749 SHOTGUN PASS 0 0 1
    33757 SHOTGUN PASS 0 0 1
    33760 UNDER CENTER QB KNEEL 0 0 0
    33769 SHOTGUN PASS 0 0 1
    33775 SHOTGUN PASS 0 0 1
    33780 SHOTGUN PASS 0 0 1
    33783 SHOTGUN PASS 0 0 1
    33790 SHOTGUN PASS 0 0 1
    34387 SHOTGUN PASS 0 0 1
    34397 SHOTGUN PASS 0 0 1
    34402 SHOTGUN RUSH 0 1 0
    34408 SHOTGUN PASS 0 0 1
    34417 SHOTGUN PASS 0 0 1
    34425 SHOTGUN PASS 0 0 1
    34430 SHOTGUN PASS 0 0 1
    35765 SHOTGUN PASS 0 0 1
    35779 UNDER CENTER PASS 0 0 1
    35787 SHOTGUN PASS 0 0 1
    35792 SHOTGUN PASS 0 0 1
    35795 SHOTGUN PASS 0 0 1
    35796 SHOTGUN PASS 0 0 1
    35986 SHOTGUN PASS 0 0 1
    35987 SHOTGUN PASS 0 0 1
    35989 SHOTGUN PASS 0 0 1
    35990 UNDER CENTER PASS 0 0 1
    35996 SHOTGUN PASS 0 0 1
    36554 SHOTGUN PASS 0 0 1
    36560 SHOTGUN PASS 0 0 1
    36592 SHOTGUN PASS 0 0 1
    36659 NO HUDDLE SHOTGUN PASS 0 0 1
    36674 SHOTGUN PASS 0 0 1
    36689 SHOTGUN PASS 0 0 1
    36838 SHOTGUN PASS 0 0 1
    36854 SHOTGUN PASS 0 0 1
    37659 SHOTGUN PASS 0 0 1
    37661 SHOTGUN PASS 0 0 1
    37669 SHOTGUN PASS 0 0 1
    37670 SHOTGUN SACK 0 0 0
    37671 SHOTGUN PASS 0 0 1
    37672 SHOTGUN PASS 0 0 1
    37689 SHOTGUN PASS 0 0 1
    37692 SHOTGUN PASS 0 0 1
    37854 SHOTGUN PASS 0 0 1
    37855 SHOTGUN PASS 0 0 1
    37866 SHOTGUN PASS 0 0 1
    37874 SHOTGUN PASS 0 0 1
    37875 SHOTGUN PASS 0 0 1
    38922 SHOTGUN PASS 0 0 1
    38923 SHOTGUN PASS 0 0 1
    38927 SHOTGUN PASS 0 0 1
    38929 SHOTGUN PASS 0 0 1
    38933 SHOTGUN PASS 0 0 1
    38934 NO HUDDLE SHOTGUN PASS 0 0 1
    38935 SHOTGUN PASS 0 0 1
    38939 SHOTGUN PASS 0 0 1
    38944 SHOTGUN PASS 0 0 1
    38945 SHOTGUN RUSH 0 1 0
    38946 SHOTGUN PASS 0 0 1
    39091 SHOTGUN PASS 0 0 1
    39092 NO HUDDLE CLOCK STOP 0 0 0
    39094 NO HUDDLE SHOTGUN PASS 0 0 1
    39319 UNDER CENTER QB KNEEL 0 0 0
    39334 NO HUDDLE CLOCK STOP 0 0 0
    39341 SHOTGUN PASS 0 0 1
    39354 SHOTGUN PASS 0 0 1
    39449 UNDER CENTER TWO-POINT CONVERSION 0 0 0
    39450 SHOTGUN PASS 0 0 1
    39451 SHOTGUN PASS 0 0 1
    39888 SHOTGUN PASS 0 0 1
    39891 SHOTGUN PASS 0 0 1
    39894 SHOTGUN PASS 0 0 1
    39895 SHOTGUN PASS 0 0 1
    39901 SHOTGUN PASS 0 0 1
    40021 SHOTGUN PASS 0 0 1
    40023 SHOTGUN PASS 0 0 1
    40039 SHOTGUN PASS 0 0 1
    40044 SHOTGUN PASS 0 0 1
    40045 SHOTGUN PASS 0 0 1
    40046 SHOTGUN PASS 0 0 1
    40551 SHOTGUN SACK -1 0 0
    40952 SHOTGUN RUSH -1 1 0
    41018 SHOTGUN RUSH -1 1 0
    41063 SHOTGUN PASS -1 0 1
    41094 SHOTGUN PASS -1 0 1
    41108 SHOTGUN PASS -1 0 1
    41124 SHOTGUN PASS -1 0 1
    41170 SHOTGUN SACK -2 0 0
    41171 SHOTGUN SACK -2 0 0
    41188 SHOTGUN SACK -2 0 0
    41513 SHOTGUN PASS -2 0 1
    41520 SHOTGUN SACK -3 0 0
    41525 SHOTGUN SACK -3 0 0
    41526 SHOTGUN SACK -3 0 0
    41531 SHOTGUN SACK -3 0 0
    41552 SHOTGUN SACK -3 0 0
    41583 NO HUDDLE SHOTGUN RUSH -3 1 0
    41786 SHOTGUN SACK -4 0 0
    41812 SHOTGUN SACK -4 0 0
    41815 SHOTGUN SACK -4 0 0
    41900 SHOTGUN PASS -4 0 1
    41950 SHOTGUN SACK -5 0 0
    41968 SHOTGUN SACK -5 0 0
    41983 SHOTGUN SACK -5 0 0
    41987 SHOTGUN SACK -5 0 0
    41988 NO HUDDLE SHOTGUN SACK -5 0 0
    42001 SHOTGUN SACK -5 0 0
    42083 SHOTGUN SACK -6 0 0
    42084 SHOTGUN SACK -6 0 0
    42105 SHOTGUN SACK -6 0 0
    42159 SHOTGUN SACK -6 0 0
    42160 SHOTGUN SACK -6 0 0
    42231 SHOTGUN SACK -7 0 0
    42275 SHOTGUN SACK -7 0 0
    42286 SHOTGUN SACK -7 0 0
    42427 SHOTGUN SACK -8 0 0
    42435 SHOTGUN SACK -8 0 0
    42472 SHOTGUN SACK -9 0 0
    42492 SHOTGUN SACK -9 0 0
    42497 SHOTGUN SACK -9 0 0
    42512 SHOTGUN SACK -9 0 0
    42544 SHOTGUN SACK -9 0 0
    42549 SHOTGUN SACK -9 0 0
    42659 SHOTGUN SACK -10 0 0
    


```python
# Lamar Jackson stats 2021
qb_list = ['yards', 'is_rush', 'is_pass', 'is_touchdown', 'is_interception', 'is_fumble', 'is_sack']
lamar = big_truss[qb_list]
lamar.sum()
```




    yards              3676
    is_rush             130
    is_pass             392
    is_touchdown         23
    is_interception      15
    is_fumble            12
    is_sack              40
    dtype: int64




```python
# Lamar Jacksons Tendendcies 

qb_tendencies = ['pass_type', 'formation', 'play_type']
truss = big_truss[qb_tendencies]
big_truss['play_type'].value_counts()
```




    PASS                    392
    RUSH                     76
    SCRAMBLE                 54
    SACK                     40
    TWO-POINT CONVERSION      7
    QB KNEEL                  6
    CLOCK STOP                4
    FUMBLES                   1
    Name: play_type, dtype: int64




```python
# Lamar pass types

big_truss['pass_type'].value_counts()
```




    SHORT RIGHT     108
    SHORT LEFT      103
    SHORT MIDDLE    102
    DEEP RIGHT       33
    DEEP LEFT        25
    DEEP MIDDLE      21
    Name: pass_type, dtype: int64




```python
# The formation of lamar Jackson plays

big_truss['formation'].value_counts()
```




    SHOTGUN              521
    NO HUDDLE SHOTGUN     30
    UNDER CENTER          25
    NO HUDDLE              4
    Name: formation, dtype: int64




```python
# looking at Joe Burrows formation numbers
cool_joe['formation'].value_counts()
```




    SHOTGUN              461
    UNDER CENTER          97
    NO HUDDLE SHOTGUN     32
    NO HUDDLE              5
    Name: formation, dtype: int64




```python
big_truss['pass_type'].value_counts(normalize=True).mul(100).round(2).astype(str) + '%'
```




    SHORT RIGHT     27.55%
    SHORT LEFT      26.28%
    SHORT MIDDLE    26.02%
    DEEP RIGHT       8.42%
    DEEP LEFT        6.38%
    DEEP MIDDLE      5.36%
    Name: pass_type, dtype: object




```python
cool_joe['pass_type'].value_counts(normalize=True).mul(100).round(2).astype(str) + '%'
```




    SHORT RIGHT       31.06%
    SHORT LEFT        27.66%
    SHORT MIDDLE      22.65%
    DEEP RIGHT        10.02%
    DEEP LEFT          5.21%
    DEEP MIDDLE        3.21%
    RIGHT. PENALTY      0.2%
    Name: pass_type, dtype: object



# THE END

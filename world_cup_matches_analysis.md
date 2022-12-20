```python
import pandas as pd
import numpy as np
import warnings
warnings.filterwarnings("ignore")
import seaborn as sn
import matplotlib.pyplot as plt
sn.set(style="white", color_codes=True)
```


```python
wp = pd.read_csv('C:/Users/Mert/Downloads/world_cup_matches.csv', encoding='latin-1')
```


```python
wp.head(5)
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
      <th>team1</th>
      <th>team2</th>
      <th>possession team1</th>
      <th>possession team2</th>
      <th>possession in contest</th>
      <th>number of goals team1</th>
      <th>number of goals team2</th>
      <th>date</th>
      <th>hour</th>
      <th>category</th>
      <th>...</th>
      <th>penalties scored team1</th>
      <th>penalties scored team2</th>
      <th>goal preventions team1</th>
      <th>goal preventions team2</th>
      <th>own goals team1</th>
      <th>own goals team2</th>
      <th>forced turnovers team1</th>
      <th>forced turnovers team2</th>
      <th>defensive pressures applied team1</th>
      <th>defensive pressures applied team2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>QATAR</td>
      <td>ECUADOR</td>
      <td>42%</td>
      <td>50%</td>
      <td>8%</td>
      <td>0</td>
      <td>2</td>
      <td>20 NOV 2022</td>
      <td>17 : 00</td>
      <td>Group A</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>6</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>52</td>
      <td>72</td>
      <td>256</td>
      <td>279</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ENGLAND</td>
      <td>IRAN</td>
      <td>72%</td>
      <td>19%</td>
      <td>9%</td>
      <td>6</td>
      <td>2</td>
      <td>21 NOV 2022</td>
      <td>14 : 00</td>
      <td>Group B</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>8</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>63</td>
      <td>72</td>
      <td>139</td>
      <td>416</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SENEGAL</td>
      <td>NETHERLANDS</td>
      <td>44%</td>
      <td>45%</td>
      <td>11%</td>
      <td>0</td>
      <td>2</td>
      <td>21 NOV 2022</td>
      <td>17 : 00</td>
      <td>Group A</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>63</td>
      <td>73</td>
      <td>263</td>
      <td>251</td>
    </tr>
    <tr>
      <th>3</th>
      <td>UNITED STATES</td>
      <td>WALES</td>
      <td>51%</td>
      <td>39%</td>
      <td>10%</td>
      <td>1</td>
      <td>1</td>
      <td>21 NOV 2022</td>
      <td>20 : 00</td>
      <td>Group B</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>7</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>81</td>
      <td>72</td>
      <td>242</td>
      <td>292</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ARGENTINA</td>
      <td>SAUDI ARABIA</td>
      <td>64%</td>
      <td>24%</td>
      <td>12%</td>
      <td>1</td>
      <td>2</td>
      <td>22 NOV 2022</td>
      <td>11 : 00</td>
      <td>Group C</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>65</td>
      <td>80</td>
      <td>163</td>
      <td>361</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 88 columns</p>
</div>




```python
for col in wp.columns:                   #to see whole column name
    print(col)
```

    team1
    team2
    possession team1
    possession team2
    possession in contest
    number of goals team1
    number of goals team2
    date
    hour
    category
    total attempts team1
    total attempts team2
    conceded team1
    conceded team2
    goal inside the penalty area team1
    goal inside the penalty area team2
    goal outside the penalty area team1
    goal outside the penalty area team2
    assists team1
    assists team2
    on target attempts team1
    on target attempts team2
    off target attempts team1
    off target attempts team2
    attempts inside the penalty area team1
    attempts inside the penalty area  team2
    attempts outside the penalty area  team1
    attempts outside the penalty area  team2
    left channel team1
    left channel team2
    left inside channel team1
    left inside channel team2
    central channel team1
    central channel team2
    right inside channel team1
    right inside channel team2
    right channel team1
    right channel team2
    total offers to receive team1
    total offers to receive team2
    inbehind offers to receive team1
    inbehind offers to receive team2
    inbetween offers to receive team1
    inbetween offers to receive team2
    infront offers to receive team1
    infront offers to receive team2
    receptions between midfield and defensive lines team1
    receptions between midfield and defensive lines team2
    attempted line breaks team1
    attempted line breaks team2
    completed line breaksteam1
    completed line breaks team2
    attempted defensive line breaks team1
    attempted defensive line breaks team2
    completed defensive line breaksteam1
    completed defensive line breaks team2
    yellow cards team1
    yellow cards team2
    red cards team1
    red cards team2
    fouls against team1
    fouls against team2
    offsides team1
    offsides team2
    passes team1
    passes team2
    passes completed team1
    passes completed team2
    crosses team1
    crosses team2
    crosses completed team1
    crosses completed team2
    switches of play completed team1
    switches of play completed team2
    corners team1
    corners team2
    free kicks team1
    free kicks team2
    penalties scored team1
    penalties scored team2
    goal preventions team1
    goal preventions team2
    own goals team1
    own goals team2
    forced turnovers team1
    forced turnovers team2
    defensive pressures applied team1
    defensive pressures applied team2
    


```python
wp['team1'].value_counts()
```




    ARGENTINA         5
    CROATIA           4
    FRANCE            4
    NETHERLANDS       4
    ENGLAND           4
    PORTUGAL          3
    JAPAN             3
    MOROCCO           3
    BRAZIL            3
    QATAR             2
    KOREA REPUBLIC    2
    CAMEROON          2
    POLAND            2
    TUNISIA           2
    WALES             2
    BELGIUM           2
    SPAIN             2
    URUGUAY           1
    IRAN              1
    GHANA             1
    COSTA RICA        1
    CANADA            1
    SAUDI ARABIA      1
    AUSTRALIA         1
    SENEGAL           1
    ECUADOR           1
    SWITZERLAND       1
    UNITED STATES     1
    DENMARK           1
    MEXICO            1
    GERMANY           1
    SERBIA            1
    Name: team1, dtype: int64




```python
wp.drop_duplicates()
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
      <th>team1</th>
      <th>team2</th>
      <th>possession team1</th>
      <th>possession team2</th>
      <th>possession in contest</th>
      <th>number of goals team1</th>
      <th>number of goals team2</th>
      <th>date</th>
      <th>hour</th>
      <th>category</th>
      <th>...</th>
      <th>penalties scored team1</th>
      <th>penalties scored team2</th>
      <th>goal preventions team1</th>
      <th>goal preventions team2</th>
      <th>own goals team1</th>
      <th>own goals team2</th>
      <th>forced turnovers team1</th>
      <th>forced turnovers team2</th>
      <th>defensive pressures applied team1</th>
      <th>defensive pressures applied team2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>QATAR</td>
      <td>ECUADOR</td>
      <td>42%</td>
      <td>50%</td>
      <td>8%</td>
      <td>0</td>
      <td>2</td>
      <td>20 NOV 2022</td>
      <td>17 : 00</td>
      <td>Group A</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>6</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>52</td>
      <td>72</td>
      <td>256</td>
      <td>279</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ENGLAND</td>
      <td>IRAN</td>
      <td>72%</td>
      <td>19%</td>
      <td>9%</td>
      <td>6</td>
      <td>2</td>
      <td>21 NOV 2022</td>
      <td>14 : 00</td>
      <td>Group B</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>8</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>63</td>
      <td>72</td>
      <td>139</td>
      <td>416</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SENEGAL</td>
      <td>NETHERLANDS</td>
      <td>44%</td>
      <td>45%</td>
      <td>11%</td>
      <td>0</td>
      <td>2</td>
      <td>21 NOV 2022</td>
      <td>17 : 00</td>
      <td>Group A</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>63</td>
      <td>73</td>
      <td>263</td>
      <td>251</td>
    </tr>
    <tr>
      <th>3</th>
      <td>UNITED STATES</td>
      <td>WALES</td>
      <td>51%</td>
      <td>39%</td>
      <td>10%</td>
      <td>1</td>
      <td>1</td>
      <td>21 NOV 2022</td>
      <td>20 : 00</td>
      <td>Group B</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>7</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>81</td>
      <td>72</td>
      <td>242</td>
      <td>292</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ARGENTINA</td>
      <td>SAUDI ARABIA</td>
      <td>64%</td>
      <td>24%</td>
      <td>12%</td>
      <td>1</td>
      <td>2</td>
      <td>22 NOV 2022</td>
      <td>11 : 00</td>
      <td>Group C</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>65</td>
      <td>80</td>
      <td>163</td>
      <td>361</td>
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
      <th>59</th>
      <td>ENGLAND</td>
      <td>FRANCE</td>
      <td>54%</td>
      <td>36%</td>
      <td>10%</td>
      <td>1</td>
      <td>2</td>
      <td>10 DEC 2022</td>
      <td>20 : 00</td>
      <td>Quarter-final</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>9</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>49</td>
      <td>54</td>
      <td>193</td>
      <td>308</td>
    </tr>
    <tr>
      <th>60</th>
      <td>ARGENTINA</td>
      <td>CROATIA</td>
      <td>34%</td>
      <td>54%</td>
      <td>12%</td>
      <td>3</td>
      <td>0</td>
      <td>13 DEC 2022</td>
      <td>20 : 00</td>
      <td>Semi-final</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>12</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>85</td>
      <td>63</td>
      <td>321</td>
      <td>260</td>
    </tr>
    <tr>
      <th>61</th>
      <td>FRANCE</td>
      <td>MOROCCO</td>
      <td>34%</td>
      <td>55%</td>
      <td>11%</td>
      <td>2</td>
      <td>0</td>
      <td>14 DEC 2022</td>
      <td>20 : 00</td>
      <td>Semi-final</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>72</td>
      <td>47</td>
      <td>328</td>
      <td>218</td>
    </tr>
    <tr>
      <th>62</th>
      <td>CROATIA</td>
      <td>MOROCCO</td>
      <td>45%</td>
      <td>45%</td>
      <td>10%</td>
      <td>2</td>
      <td>1</td>
      <td>17 DEC 2022</td>
      <td>16 : 00</td>
      <td>Play-off for third place</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>7</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>75</td>
      <td>72</td>
      <td>288</td>
      <td>277</td>
    </tr>
    <tr>
      <th>63</th>
      <td>ARGENTINA</td>
      <td>FRANCE</td>
      <td>46%</td>
      <td>40%</td>
      <td>14%</td>
      <td>3</td>
      <td>3</td>
      <td>18 DEC 2022</td>
      <td>16 : 00</td>
      <td>Final</td>
      <td>...</td>
      <td>1</td>
      <td>2</td>
      <td>11</td>
      <td>21</td>
      <td>0</td>
      <td>0</td>
      <td>87</td>
      <td>104</td>
      <td>280</td>
      <td>409</td>
    </tr>
  </tbody>
</table>
<p>64 rows × 88 columns</p>
</div>




```python
wp['team1'].value_counts()
```




    ARGENTINA         5
    CROATIA           4
    FRANCE            4
    NETHERLANDS       4
    ENGLAND           4
    PORTUGAL          3
    JAPAN             3
    MOROCCO           3
    BRAZIL            3
    QATAR             2
    KOREA REPUBLIC    2
    CAMEROON          2
    POLAND            2
    TUNISIA           2
    WALES             2
    BELGIUM           2
    SPAIN             2
    URUGUAY           1
    IRAN              1
    GHANA             1
    COSTA RICA        1
    CANADA            1
    SAUDI ARABIA      1
    AUSTRALIA         1
    SENEGAL           1
    ECUADOR           1
    SWITZERLAND       1
    UNITED STATES     1
    DENMARK           1
    MEXICO            1
    GERMANY           1
    SERBIA            1
    Name: team1, dtype: int64




```python
wp.dropna()
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
      <th>team1</th>
      <th>team2</th>
      <th>possession team1</th>
      <th>possession team2</th>
      <th>possession in contest</th>
      <th>number of goals team1</th>
      <th>number of goals team2</th>
      <th>date</th>
      <th>hour</th>
      <th>category</th>
      <th>...</th>
      <th>penalties scored team1</th>
      <th>penalties scored team2</th>
      <th>goal preventions team1</th>
      <th>goal preventions team2</th>
      <th>own goals team1</th>
      <th>own goals team2</th>
      <th>forced turnovers team1</th>
      <th>forced turnovers team2</th>
      <th>defensive pressures applied team1</th>
      <th>defensive pressures applied team2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>QATAR</td>
      <td>ECUADOR</td>
      <td>42%</td>
      <td>50%</td>
      <td>8%</td>
      <td>0</td>
      <td>2</td>
      <td>20 NOV 2022</td>
      <td>17 : 00</td>
      <td>Group A</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>6</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>52</td>
      <td>72</td>
      <td>256</td>
      <td>279</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ENGLAND</td>
      <td>IRAN</td>
      <td>72%</td>
      <td>19%</td>
      <td>9%</td>
      <td>6</td>
      <td>2</td>
      <td>21 NOV 2022</td>
      <td>14 : 00</td>
      <td>Group B</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>8</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>63</td>
      <td>72</td>
      <td>139</td>
      <td>416</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SENEGAL</td>
      <td>NETHERLANDS</td>
      <td>44%</td>
      <td>45%</td>
      <td>11%</td>
      <td>0</td>
      <td>2</td>
      <td>21 NOV 2022</td>
      <td>17 : 00</td>
      <td>Group A</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>63</td>
      <td>73</td>
      <td>263</td>
      <td>251</td>
    </tr>
    <tr>
      <th>3</th>
      <td>UNITED STATES</td>
      <td>WALES</td>
      <td>51%</td>
      <td>39%</td>
      <td>10%</td>
      <td>1</td>
      <td>1</td>
      <td>21 NOV 2022</td>
      <td>20 : 00</td>
      <td>Group B</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>7</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>81</td>
      <td>72</td>
      <td>242</td>
      <td>292</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ARGENTINA</td>
      <td>SAUDI ARABIA</td>
      <td>64%</td>
      <td>24%</td>
      <td>12%</td>
      <td>1</td>
      <td>2</td>
      <td>22 NOV 2022</td>
      <td>11 : 00</td>
      <td>Group C</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>65</td>
      <td>80</td>
      <td>163</td>
      <td>361</td>
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
      <th>59</th>
      <td>ENGLAND</td>
      <td>FRANCE</td>
      <td>54%</td>
      <td>36%</td>
      <td>10%</td>
      <td>1</td>
      <td>2</td>
      <td>10 DEC 2022</td>
      <td>20 : 00</td>
      <td>Quarter-final</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>9</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>49</td>
      <td>54</td>
      <td>193</td>
      <td>308</td>
    </tr>
    <tr>
      <th>60</th>
      <td>ARGENTINA</td>
      <td>CROATIA</td>
      <td>34%</td>
      <td>54%</td>
      <td>12%</td>
      <td>3</td>
      <td>0</td>
      <td>13 DEC 2022</td>
      <td>20 : 00</td>
      <td>Semi-final</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>12</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>85</td>
      <td>63</td>
      <td>321</td>
      <td>260</td>
    </tr>
    <tr>
      <th>61</th>
      <td>FRANCE</td>
      <td>MOROCCO</td>
      <td>34%</td>
      <td>55%</td>
      <td>11%</td>
      <td>2</td>
      <td>0</td>
      <td>14 DEC 2022</td>
      <td>20 : 00</td>
      <td>Semi-final</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>72</td>
      <td>47</td>
      <td>328</td>
      <td>218</td>
    </tr>
    <tr>
      <th>62</th>
      <td>CROATIA</td>
      <td>MOROCCO</td>
      <td>45%</td>
      <td>45%</td>
      <td>10%</td>
      <td>2</td>
      <td>1</td>
      <td>17 DEC 2022</td>
      <td>16 : 00</td>
      <td>Play-off for third place</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>7</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>75</td>
      <td>72</td>
      <td>288</td>
      <td>277</td>
    </tr>
    <tr>
      <th>63</th>
      <td>ARGENTINA</td>
      <td>FRANCE</td>
      <td>46%</td>
      <td>40%</td>
      <td>14%</td>
      <td>3</td>
      <td>3</td>
      <td>18 DEC 2022</td>
      <td>16 : 00</td>
      <td>Final</td>
      <td>...</td>
      <td>1</td>
      <td>2</td>
      <td>11</td>
      <td>21</td>
      <td>0</td>
      <td>0</td>
      <td>87</td>
      <td>104</td>
      <td>280</td>
      <td>409</td>
    </tr>
  </tbody>
</table>
<p>64 rows × 88 columns</p>
</div>




```python
wp.columns = wp.columns.str.replace(' ', '')
```


```python
wp.head(2)
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
      <th>team1</th>
      <th>team2</th>
      <th>possessionteam1</th>
      <th>possessionteam2</th>
      <th>possessionincontest</th>
      <th>numberofgoalsteam1</th>
      <th>numberofgoalsteam2</th>
      <th>date</th>
      <th>hour</th>
      <th>category</th>
      <th>...</th>
      <th>penaltiesscoredteam1</th>
      <th>penaltiesscoredteam2</th>
      <th>goalpreventionsteam1</th>
      <th>goalpreventionsteam2</th>
      <th>owngoalsteam1</th>
      <th>owngoalsteam2</th>
      <th>forcedturnoversteam1</th>
      <th>forcedturnoversteam2</th>
      <th>defensivepressuresappliedteam1</th>
      <th>defensivepressuresappliedteam2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>QATAR</td>
      <td>ECUADOR</td>
      <td>42%</td>
      <td>50%</td>
      <td>8%</td>
      <td>0</td>
      <td>2</td>
      <td>20 NOV 2022</td>
      <td>17 : 00</td>
      <td>Group A</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>6</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>52</td>
      <td>72</td>
      <td>256</td>
      <td>279</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ENGLAND</td>
      <td>IRAN</td>
      <td>72%</td>
      <td>19%</td>
      <td>9%</td>
      <td>6</td>
      <td>2</td>
      <td>21 NOV 2022</td>
      <td>14 : 00</td>
      <td>Group B</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>8</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>63</td>
      <td>72</td>
      <td>139</td>
      <td>416</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 88 columns</p>
</div>




```python
wp.plot(kind="scatter", x="numberofgoalsteam1", y="numberofgoalsteam2")
```

    *c* argument looks like a single numeric RGB or RGBA sequence, which should be avoided as value-mapping will have precedence in case its length matches with *x* & *y*.  Please use the *color* keyword-argument or provide a 2D array with a single row if you intend to specify the same RGB or RGBA value for all points.
    




    <AxesSubplot:xlabel='numberofgoalsteam1', ylabel='numberofgoalsteam2'>




    
![png](output_10_2.png)
    



```python
sn.jointplot(x="numberofgoalsteam1", y="numberofgoalsteam2", data=wp, size=5)
```




    <seaborn.axisgrid.JointGrid at 0x2b95f47e7c0>




    
![png](output_11_1.png)
    



```python
sn.boxplot(x="offsidesteam1", y="offsidesteam2", data=wp)

```




    <AxesSubplot:xlabel='offsidesteam1', ylabel='offsidesteam2'>




    
![png](output_12_1.png)
    



```python
sn.violinplot(x="penaltiesscoredteam1", y="penaltiesscoredteam2", data=wp, size=6)
plt.title("penalties scored")
```




    Text(0.5, 1.0, 'penalties scored')




    
![png](output_13_1.png)
    



```python
sn.FacetGrid(wp, hue="penaltiesscoredteam1", size=6) \
   .map(sn.kdeplot, "penaltiesscoredteam2") \
   .add_legend()
```




    <seaborn.axisgrid.FacetGrid at 0x2b95fff2490>




    
![png](output_14_1.png)
    



```python
sn.barplot(x='penaltiesscoredteam1', y='penaltiesscoredteam2', data=wp)
```




    <AxesSubplot:xlabel='penaltiesscoredteam1', ylabel='penaltiesscoredteam2'>




    
![png](output_15_1.png)
    



```python
sn.barplot(x='penaltiesscoredteam1', y='penaltiesscoredteam2', hue='possessionincontest', data=wp)
```




    <AxesSubplot:xlabel='penaltiesscoredteam1', ylabel='penaltiesscoredteam2'>




    
![png](output_16_1.png)
    



```python

```


```python

```

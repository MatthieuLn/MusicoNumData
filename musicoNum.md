# Notebook pour le blog de musicologie numérique

Vous trouverez ici la reproduction de mes essais de code. Vous constaterez ainsi la facilité de partager ces informations.

Dans la première partie de code ci-dessous, j'importe les librairies nécessaires à la confection de notre analyse de données. Ensuite, je définis mon *dataframe* (df) comme étant le contenu d'une base de données au format CSV préparée en amont.


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("Desktop/Analyse_bdd/BDD_Test.csv", sep=";", index_col=0)
df
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
      <th>long</th>
      <th>larg</th>
      <th>haut</th>
      <th>nbr_cor</th>
      <th>nom_ver</th>
      <th>chev_mob</th>
      <th>Chev_im</th>
      <th>pas_chev</th>
    </tr>
    <tr>
      <th>id</th>
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
      <th>JP.KT.2</th>
      <td>1760</td>
      <td>250</td>
      <td>180</td>
      <td>13</td>
      <td>Koto</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>JP.KT.3</th>
      <td>1730</td>
      <td>260</td>
      <td>90</td>
      <td>13</td>
      <td>Koto</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>CN.GQ.15</th>
      <td>1150</td>
      <td>190</td>
      <td>120</td>
      <td>7</td>
      <td>Guqin</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>JP.NGK.3</th>
      <td>1100</td>
      <td>115</td>
      <td>90</td>
      <td>2</td>
      <td>Nigenkin</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>CN.YQ.2</th>
      <td>663</td>
      <td>238</td>
      <td>39</td>
      <td>38</td>
      <td>Yangqin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>JP.GoK.1</th>
      <td>1091</td>
      <td>126</td>
      <td>37</td>
      <td>5</td>
      <td>Gokin</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>JP.IGK.2</th>
      <td>1092</td>
      <td>107</td>
      <td>17</td>
      <td>1</td>
      <td>Ichigenkin</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>CN.GQ.19</th>
      <td>1240</td>
      <td>190</td>
      <td>105</td>
      <td>7</td>
      <td>Guqin</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>CN.YQ.4</th>
      <td>700</td>
      <td>250</td>
      <td>50</td>
      <td>28</td>
      <td>Yangqin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>CN.GQ.8</th>
      <td>1220</td>
      <td>204</td>
      <td>100</td>
      <td>7</td>
      <td>Guqin</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



La fonction ci-dessous est une description statistique des différents paramètres de la base de données. 


```python
df.describe()
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
      <th>long</th>
      <th>larg</th>
      <th>haut</th>
      <th>nbr_cor</th>
      <th>chev_mob</th>
      <th>Chev_im</th>
      <th>pas_chev</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>10.000000</td>
      <td>10.000000</td>
      <td>10.000000</td>
      <td>10.00000</td>
      <td>10.000000</td>
      <td>10.000000</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1174.600000</td>
      <td>193.000000</td>
      <td>82.800000</td>
      <td>12.10000</td>
      <td>0.200000</td>
      <td>0.200000</td>
      <td>0.600000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>359.700863</td>
      <td>58.802872</td>
      <td>48.471756</td>
      <td>11.92057</td>
      <td>0.421637</td>
      <td>0.421637</td>
      <td>0.516398</td>
    </tr>
    <tr>
      <th>min</th>
      <td>663.000000</td>
      <td>107.000000</td>
      <td>17.000000</td>
      <td>1.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1091.250000</td>
      <td>142.000000</td>
      <td>41.750000</td>
      <td>5.50000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1125.000000</td>
      <td>197.000000</td>
      <td>90.000000</td>
      <td>7.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1235.000000</td>
      <td>247.000000</td>
      <td>103.750000</td>
      <td>13.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1760.000000</td>
      <td>260.000000</td>
      <td>180.000000</td>
      <td>38.00000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



Nous pouvons ensuite faire un graphique du nombre de corde par spécimen identifié par un code (qui n'est pas le code définitif).


```python
df.plot.bar( y="nbr_cor", xlabel='identifiant', ylabel='nombre de cordes')
```




    <Axes: xlabel='identifiant', ylabel='nombre de cordes'>




    
![png](output_5_1.png)
    



```python

```

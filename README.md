# Proyecto-de-programacion
Trabajo de programación del índice de marginalización de México para el curso propedéutico de la Maestría en Ciencia de Datos. En esta actividad, hicimos uso de la Base de Datos por Municipio 2020 del índice de marginación en México. A lo largo del desarrollo del trabajo, se contestaron interrogantes y se creó código y gráficos relacionados con el tema.

Primero, comenzamos por importar las librerías que se usarán para el análisis de esta base de datos:

```python
import pandas as pd      #Libreria de pandas para el manejo de los dataframes
import matplotlib.ticker as mtick    #Para agregar unos detalles a las graficas
```

Tras esto, procedemos a importar la base de datos en un dataframe que estaremos utilizando durante el análisis:

```python
path_datos = "http://www.conapo.gob.mx/work/models/CONAPO/Marginacion/Datos_Abiertos/Municipio/IMM_2020.xls"
df = pd.read_excel(path_datos, sheet_name="IMM_2020")   
df
```
La siguiente tabla es el resultado de aplicar el método *describe()* al dataframe:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CVE_ENT</th>
      <th>CVE_MUN</th>
      <th>POB_TOT</th>
      <th>ANALF</th>
      <th>SBASC</th>
      <th>OVSDE</th>
      <th>OVSEE</th>
      <th>OVSAE</th>
      <th>OVPT</th>
      <th>VHAC</th>
      <th>PL.5000</th>
      <th>PO2SM</th>
      <th>IM_2020</th>
      <th>IMN_2020</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2.469000e+03</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
      <td>2469.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>19.215472</td>
      <td>19324.164844</td>
      <td>5.103849e+04</td>
      <td>10.164466</td>
      <td>45.853026</td>
      <td>3.159963</td>
      <td>1.500793</td>
      <td>6.118145</td>
      <td>7.987232</td>
      <td>26.566286</td>
      <td>69.900469</td>
      <td>82.143854</td>
      <td>53.955581</td>
      <td>0.844869</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.367340</td>
      <td>7382.892458</td>
      <td>1.469907e+05</td>
      <td>7.633633</td>
      <td>13.981594</td>
      <td>5.289299</td>
      <td>2.769167</td>
      <td>9.245995</td>
      <td>8.973591</td>
      <td>10.586540</td>
      <td>35.267726</td>
      <td>11.830444</td>
      <td>3.904590</td>
      <td>0.061140</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1001.000000</td>
      <td>8.100000e+01</td>
      <td>0.353446</td>
      <td>5.535137</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.950392</td>
      <td>0.000000</td>
      <td>28.453113</td>
      <td>21.406635</td>
      <td>0.335198</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>14.000000</td>
      <td>14079.000000</td>
      <td>4.489000e+03</td>
      <td>4.427755</td>
      <td>35.737568</td>
      <td>0.651869</td>
      <td>0.366077</td>
      <td>0.878499</td>
      <td>1.654653</td>
      <td>18.725100</td>
      <td>40.129696</td>
      <td>74.615600</td>
      <td>51.844432</td>
      <td>0.811812</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>20.000000</td>
      <td>20226.000000</td>
      <td>1.355200e+04</td>
      <td>8.202762</td>
      <td>46.339439</td>
      <td>1.428250</td>
      <td>0.828157</td>
      <td>2.452316</td>
      <td>4.714141</td>
      <td>25.000000</td>
      <td>100.000000</td>
      <td>84.643266</td>
      <td>54.423506</td>
      <td>0.852196</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>24.000000</td>
      <td>24027.000000</td>
      <td>3.528400e+04</td>
      <td>13.787294</td>
      <td>55.856378</td>
      <td>3.342618</td>
      <td>1.678328</td>
      <td>7.285869</td>
      <td>11.029646</td>
      <td>32.820816</td>
      <td>100.000000</td>
      <td>91.620112</td>
      <td>56.696126</td>
      <td>0.887782</td>
    </tr>
    <tr>
      <th>max</th>
      <td>32.000000</td>
      <td>32058.000000</td>
      <td>1.922523e+06</td>
      <td>53.071253</td>
      <td>88.328076</td>
      <td>64.450424</td>
      <td>53.065463</td>
      <td>81.788441</td>
      <td>68.149764</td>
      <td>69.564018</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>62.397145</td>
      <td>0.977052</td>
    </tr>
  </tbody>
</table>

Algo que podemos apreciar rápidamente de la tabla es que, a pesar de que la media del porcentaje de Población de 15 años o más sin educación básica (SBASC) es de 45.853026%, la media del porcentaje de Población de 15 años o más analfabeta (ANALF) es tan solo de 10.164466%. Esto nos ilustra que, aunque hay una gran cantidad de personas que no cuentan con estudios de nivel básico, todavía han aprendido a leer y escribir por otros medios.


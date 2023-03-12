# Gerando coordenadas a partir dos municípios 

- Importando pacotes e ler o dataframe

```
pip install geopy geopandas
import pandas as pd
import numpy as np
import geopandas as gpds 
```
```
nome_do_dataframe = pd.read_csv(r"aqui_colocar_o_caminho_de_onde_esta_o_arquivo.csv", encoding='utf-8')
print(nome_do_dataframe)
```

- Importar a API de georeferenciamento que vamos usar, eu escolhi a Nominatim, mas tem outras como Google Maps e Bing Maps

```
from geopy.geocoders import Nominatim
```

- Podemos procurar as coordenadas de um endereço ou município, aqui eu vou usar município

```
gpds.tools.geocode('Maceió', provider='Nominatim', user_agent="myGeocoder")
```
- E a saída é essa: 

<div align="center">
<img src="C:\Users\mecoa\Desktop\1.png" width="200px" />
</div>

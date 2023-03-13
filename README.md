# CEPE
Coordenadas com geopy 

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

- Importar a API de georeferenciamento que vamos usar, eu escolhi a Nominatim, mas tem outras como Google Maps e Bing Maps.

```
from geopy.geocoders import Nominatim
```

- Podemos procurar as coordenadas de um endereço ou município, aqui eu vou usar município.
(Na documentação do Nominatim, tem o exemplo se usar - user_agent="my-application", mas isso deu um HTTP errors, 
dessa forma utilizei user_agent="myGeocoder")

```
gpds.tools.geocode('Maceió', provider='Nominatim', user_agent="myGeocoder")
```
- E a saída é essa:

![1](https://user-images.githubusercontent.com/113151407/224518833-45122536-3a7e-434f-b547-e0945982ae31.png)

- Porém o meu dataframe tem 1071 linhas e quero fazer todos os municípios de uma vez, e para isso tenho que
colocar um delimitador de tempo para acessar a API pois há restrições e pode cair 

```
from geopy.extra.rate_limiter import RateLimiter
geocode = RateLimiter(locator.geocode, min_delay_seconds=1)
```
- Agora é só repetir o código mas no lugar da string 'Maceió' vou colocar 
a coluna que eu quero que ele pegue as coordenadas.

```
gpds.tools.geocode(nome_do_dataframe['nome_da_coluna'], provider='Nominatim', user_agent="myGeocoder")
```
![2](https://user-images.githubusercontent.com/113151407/224519047-c722bf8c-fabf-43e7-928f-52bc8fb65519.png)

- E para finalizar quero criar uma nova coluna no meu dataframe com as coordenadas que foram geradas; 
- Então crio uma variável com o nome da nova coluna que quero + o código anterior + a coluna de dados com as infos das coordenadas

```
nome_do_dataframe['coordenadas'] = gpds.tools.geocode(nome_do_dataframe['nome_da_coluna'], 
provider='Nominatim', user_agent="myGeocoder")["geometry"]
nome_do_dataframe
```
- E essa é a saída das coordenadas já no dataframe original. 

![3](https://user-images.githubusercontent.com/113151407/224519257-0b8b078a-6f52-4a16-850d-d6566f592877.png)

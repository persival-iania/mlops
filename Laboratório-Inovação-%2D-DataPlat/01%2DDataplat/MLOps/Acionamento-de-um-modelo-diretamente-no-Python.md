#Acionamento modelos em Python

## Requisitos

Para que você acione modelos diretamente via Python, a partir de qualquer execução, você vai precisar de:
- a URI onde o modelo está hospedado (isto pode ser obtivo com o ML engineer)
- um *token* gerado no Databricks para acesso ao ambiente (qualquer admin do Databricks consegue gerar)

# Código de acionamento 

import os
import requests
import numpy as np
import pandas as pd
import json

def create_tf_serving_json(data):
return {'inputs': {name: data[name].tolist() for name in data.keys()} if isinstance(data, dict) else data.tolist()}

def score model(dataset):
 url = 'https://adb-622288559698745.5.azuredatabricks.net/model/Modelo_Teste/1/invocations'
 headers = {'Authorization': f'Bearer {os.environ.get("**DATABRICKS_TOKEN**")}', 'Content-Type': 'application/json'}

 ds_dict = dataset.to_dict(orient='split') if isinstance(dataset, pd.DataFrame) else create_tf_serving_json(dataset)
 data JSON = json.dumps(ds_dict, allow_nan=True)
 response = requests. Request(method='POST', headers=headers, url=url, data=data JSON)
 if response.status_code != 200:
   raise Exception(f'Request failed with status {response.status_code}, {response. Text}')
 return response.json()

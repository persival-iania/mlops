

Para obter as métricas de modelo no Azure Databricks através do Data Factory, você pode usar a API de Metrics do Databricks para coletar as métricas de treinamento do modelo. Em seguida, você pode enviar as métricas para o Data Factory usando a API REST do Data Factory.

Para isso, você pode seguir os seguintes passos:

1. Configure o ambiente de trabalho do Databricks no Azure.
2. Crie um modelo de treinamento no Databricks.
3. Defina as métricas de treinamento no modelo. Por exemplo, você pode definir as métricas de precisão, recall e F1-score.
4. Use a API de Metrics do Databricks para coletar as métricas de treinamento do modelo.
5. Envie as métricas para o Data Factory usando a API REST do Data Factory.

O código em Python para obter as métricas do modelo e enviar para o Data Factory pode ser semelhante ao seguinte:

```python
import requests
import json
import os

# define o token de acesso ao Data Factory
access_token = os.environ.get('ACCESS_TOKEN')

# define as credenciais do ambiente de trabalho do Databricks
databricks_workspace_url = 'https://<databricks-instance>.cloud.databricks.com'
databricks_token = '<databricks-token>'

# define as configurações de coleta de métricas do modelo
model_run_id = '<model-run-id>'
model_metrics = ['precision', 'recall', 'f1-score']

# coleta as métricas do modelo usando a API de Metrics do Databricks
metrics_url = f'{databricks_workspace_url}/api/2.0/mlflow/runs/get-metric-history?run_uuid={model_run_id}&key={",".join(model_metrics)}'
metrics_headers = {'Authorization': f'Bearer {databricks_token}'}
metrics_response = requests.get(metrics_url, headers=metrics_headers)

# envia as métricas para o Data Factory usando a API REST do Data Factory
data_factory_url = '<data-factory-url>/api/v1/metrics'
data_factory_headers = {'Authorization': f'Bearer {access_token}', 'Content-Type': 'application/json'}
data_factory_payload = {'run_id': model_run_id, 'metrics': metrics_response.json()}
data_factory_response = requests.post(data_factory_url, headers=data_factory_headers, data=json.dumps(data_factory_payload))

# verifica se a operação foi bem-sucedida
if data_factory_response.status_code == 200:
    print('Métricas enviadas com sucesso para o Data Factory.')
else:
    print('Falha ao enviar métricas para o Data Factory.')
```

Certifique-se de substituir as informações de credenciais e configurações do modelo com as informações relevantes para o seu ambiente. Além disso, certifique-se de que as APIs do Databricks e do Data Factory estejam habilitadas e configuradas corretamente.
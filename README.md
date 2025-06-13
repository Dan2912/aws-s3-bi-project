# Projeto de Análise Financeira de Transações de Cartão no Power BI

Este projeto tem como objetivo construir uma solução completa para análise de dados financeiros de transações de cartão, integrando **Google Cloud Storage (GCS)**, Data Warehouse (DW) e Power BI para geração de relatórios e dashboards intuitivos.

---

## Arquitetura do Projeto

O projeto foi planejado seguindo uma arquitetura bem definida para garantir escalabilidade, segurança e eficiência no processamento dos dados.

Você pode visualizar o desenho da arquitetura detalhada neste diagrama:  
[Diagrama da Arquitetura no diagrams.net](https://app.diagrams.net/?src=about#G1ya-97xG5Cm4EcOYc4H5meehXzDbrsGBn#%7B%22pageId%22%3A%223tIZE2UBRQzZcbUsq0wZ%22%7D)

---

## Etapas do Projeto

1. **Criação do Bucket no Google Cloud Storage e Configuração IAM**  
   - Configuração do bucket GCS para armazenamento seguro dos arquivos de transações.  
   - Definição de permissões e papéis (roles) via IAM para controle de acesso.

2. **Upload dos Arquivos para o Bucket GCS via Google Colab**  
   - Script Python utilizando a biblioteca `google-cloud-storage` para importar arquivos locais e enviá-los para o bucket GCS.  

### Exemplo de código para upload:

```python
from google.cloud import storage
import os

# Defina o caminho do arquivo JSON de credenciais da conta de serviço do Google Cloud
os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "/path/para/sua/conta-servico.json"

# Inicializa o cliente do Google Cloud Storage
client = storage.Client()

bucket_name = 'projetos-bi-01'
pasta_destino = 'pasta/'

# Arquivo local que será enviado
arquivo_local = '/content/transacoes_02.csv'
nome_arquivo_no_bucket = pasta_destino + 'transacoes1.csv'

# Referência ao bucket
bucket = client.bucket(bucket_name)

# Cria um blob no bucket com o nome desejado
blob = bucket.blob(nome_arquivo_no_bucket)

# Upload do arquivo local para o bucket
blob.upload_from_filename(arquivo_local)

print(f"✅ Arquivo {arquivo_local} enviado para gs://{bucket_name}/{nome_arquivo_no_bucket}")

   print("Upload concluído com sucesso!")


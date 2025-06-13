# Projeto de Análise Financeira de Transações de Cartão no Power BI

Este projeto tem como objetivo construir uma solução completa para análise de dados financeiros de transações de cartão, integrando AWS S3, Data Warehouse (DW) e Power BI para geração de relatórios e dashboards intuitivos.

---

## Arquitetura do Projeto

O projeto foi planejado seguindo uma arquitetura bem definida para garantir escalabilidade, segurança e eficiência no processamento dos dados.

Você pode visualizar o desenho da arquitetura detalhada neste diagrama:  
[Diagrama da Arquitetura no diagrams.net](https://app.diagrams.net/?src=about#G1ya-97xG5Cm4EcOYc4H5meehXzDbrsGBn#%7B%22pageId%22%3A%223tIZE2UBRQzZcbUsq0wZ%22%7D)

---

## Etapas do Projeto

1. **Criação do Bucket S3 e Configuração IAM**  
   - Configuração do bucket S3 na AWS para armazenamento seguro dos arquivos de transações.  
   - Definição de políticas de segurança via IAM para controle de acesso.

2. **Upload dos Arquivos para S3 via Google Colab**  
   - Script Python usando a biblioteca `boto3` para importar arquivos locais e enviá-los para o bucket S3.  
   - Exemplo de código para upload:

   ```python
   import os
   import boto3

   # Configura as credenciais AWS via variáveis de ambiente (NUNCA deixe chaves hardcoded em produção)
   os.environ["AWS_ACCESS_KEY_ID"] = "sua-chave"
   os.environ["AWS_SECRET_ACCESS_KEY"] = "sua-chave"

   # Cria cliente S3
   s3 = boto3.client('s3', region_name='us-east-1')

   bucket_name = 'projetos-bi-01'
   arquivo_local = '/content/transacoes_02.csv'
   arquivo_no_s3 = 'pasta/transacoes1.csv'

   # Upload do arquivo para o bucket S3
   s3.upload_file(arquivo_local, bucket_name, arquivo_no_s3)

   print("Upload concluído com sucesso!")


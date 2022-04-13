## Docker Desktop
O ambiente designado para desenvolver a solução foi pre-configurado com o Airfow e o Spark em uma imagem docker. 

Para executar este ambiente será necessário instalar em seu equipamento o Docker Desktop, disponível para download no seguinte link:

[Download Docker Desktop](https://www.docker.com/products/docker-desktop)

Após instalar o docker será possível subir o ambiente utilizando a seguinte linha de comando na raíz desse repositorio (onde encontra-se o arquivo `docker-compose.yaml`):

<pre><code>docker-compose up</code></pre>

Ao executar o comando acima, pode ser requerido a permissão de acesso aos seguintes diretórios:

- ./datalake
- ./dags
- ./logs
- ./plugins

Se estiver utilizando Windows uma mensagem pop-up como a seguinte pode aparecer multiplas vezes na primeira execução:

![Docker Permission](/_img/docker_permission.png?raw=true "Docker Permission")

Caso ocorra, basta clicar na opção: **Share it**.

## Apache Airflow
Ao executar o comando __docker-compose__ algumas mensagens de log aparecerão e o ambiente estará pronto para uso quando a saída do log estiver como na seguinte imagem:

![Docker Compose Logs](/_img/docker_compose_log.png?raw=true "Docker Compose Logs")

A interface visual do Apache Airflow estará acessível no seguinte endereço:

http://localhost:8080

E poderá ser acessada através das seguintes credenciais:

- login: **airflow**
- password: **airflow**

Uma dag de exemplo (sample.py) foi disponibilizada neste repositório para auxiliar no início do desenvolvimento do pipeline.

![Airflow Interface](/_img/airflow.png?raw=true "Airflow Interface")

## Apache Spark
O Apache Spark (versão 3.1.1) está disponível na imagem docker junto com o Airflow, você poderá acessá-lo através do Spark Session no Python, exemplo:
<pre><code>
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .master("local[*]") \
    .appName("airflow_app") \
    .config('spark.executor.memory', '6g') \
    .config('spark.driver.memory', '6g') \
    .config("spark.driver.maxResultSize", "1048MB") \
    .config("spark.port.maxRetries", "100") \
    .getOrCreate()
</code></pre>

## DBT


## Ambiente de desenvolvimento

Para a realização desse projeto, foi utilizada a estrutura de *clusters* apresentada durante o curso. 

A etapa de instalação e configuração dos softwares em ambiente Windows está descrita [aqui](link).
 

### 1. **Criação dos diretórios**


No terminal, em `~$/home/danielle`,  criar um diretório chamado _treinamentos_ com o comando `mkdir treinamentos` e em seguida acessar essa pasta com`cd treinamentos.`


### 2. **Baixar o conteúdo do cluster**

Utilizar o arquivo disponibilizado pelo professor: 

```console
git clone https://github.com/rodrigo-reboucas/docker-bigdata.git desafio 
```
Criar uma pasta para guardar os arquivos .yml, que nomeei como *arquivo referencia*.



### 3. **Baixar a pasta Elastic**

Dentro do diretorio *desafio*, realizar download da pasta Elastic disponível em: 

```console
https://github.com/daniellecd/projeto_semantix/blob/main/elastic/elastic.zip
```
Atualizar o conteúdo do arquivo yml, para que contenha as configurações do namenode, datanode, hive, kafka, spark e elastic em um mesmo arquivo. Disponibilizado nesse [link](https://github.com/daniellecd/projeto_semantix/blob/main/docker-compose.yml).

A seguir é apresentada a estrutura do diretório utilizado nesse projeto.

```~> desafio/
/desafio
|-- arquivos referencia
|-- data
	-- hadoop
	-- hbase
	-- hdfs
	-- hue
	-- jupyter
	-- kafka
	-- metabase
	-- mongo
	-- mysql
	-- nifi
	-- notebooks
	-- postgresql
	-- util
	-- zookeeper
|-- input
|-- pipeline
    -- logstash.conf
|-- settings
    -- elasticsearch.yml
    -- kibana.yml
    -- logstash.yml
|-- docker-compose.yml
 ```       

Nem todos os serviços serão utilizados nesse projeto. A ideia principal era utilizar os recursos que tivemos acesso ao longo do curso.

 ### 4. **Configurar o vm.max_map_count com no mínimo 262144**

Para realizar essa configuração, seguir as seguintes etapas:

* Digitar o comando `sudo vi /etc/sysctl.conf`

* `i`  _# para inserir_

* `CTRL+END`_# ir para o final_

* `vm.max_map_count=262144` _# colar esse parâmetro_

* `ESC`  _# para sair_

* `:wq`  _# para salvar e sair_

No terminal, usar o comando `grep vm.max_map_count /etc/sysctl.conf` para verificar se funcionou.

**Nota:** É necessário utilizar o comando `sudo sysctl -w vm.max_map_count=262144` ao iniciar o cluster para que o container (*elastic*) permaneça ativo.

### 5. **Baixar as imagens**

```console
docker-compose pull
```

### 6. **Iniciar todos os serviços**

```console
docker-compose up -d
```

### 7. **Configurar o jar do spark**

Serão necessárias duas configurações adicionais: uma para para aceitar o formato parquet em tabelas Hive e outra de conexão com elastic. Os links para downlod dos arquivos .jar 
estão apresentados abaixo:

* Parquet

```console
curl -O https://repo1.maven.org/maven2/com/twitter/parquet-hadoop-bundle/1.6.0/parquet-hadoop-bundle-1.6.0.jar
```

```console
docker cp parquet-hadoop-bundle-1.6.0.jar jupyter-spark:/opt/spark/jars
```
  
 * Elastic 
```console
curl -O https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch-hadoop/7.9.2/elasticsearch-hadoop-7.9.2.jar
```

```console
docker cp elasticsearch-hadoop-7.9.2.jar jupyter-spark:/opt/spark/jars
```
  
### 8. **Aquisição dos dados**

Criar uma pasta denominada _dados_ dentro da pasta _input._ Dentro da pasta _dados_ realizar os seguintes comandos:

```console
sudo curl -O https://mobileapps.saude.gov.br/esus-vepi/files/unAFkcaNDeXajurGB7LChj8SgQYS2ptm/04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar
```
``` console 
sudo unrar x 04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar
```

-   Se necessário, instalar um descompactador de arquivo: `sudo apt-get install unrar` e executar o seguinte comando: `sudo unrar x <nomedoarquivo>.rar`

### 9. **Enviar arquivos para o HDFS**
 
Para acessar o *namenode*, utilizar o comando `docker exec -it namenode bash`. Criar um diretório denominado covid, verificar a criação da pasta e enviar os arquivos obtidos na etapa anterior:


```console 
hdfs dfs -mkdir -p /user/danielle/covid
```

```console 
hdfs dfs -ls -R /user
```

```console
hdfs dfs -put /input/dados/*.csv /user/danielle/covid
```

**Nota**: O envio dos dados para o hdfs é o primeiro item da atividade proposta. A continuidade desse projeto será realizado em Spark e apresentado no formato de notebook (.ipynb)

------------
<h5 align="center"> Feito com ❤  by daniellecd
</h5>

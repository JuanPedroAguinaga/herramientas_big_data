# Entorno Docker con Hadoop, Spark y Hive

Se pesenta un entorno Docker con Hadoop (HDFS) y la implementación de:
* Spark
* Hive
* HBase
* MongoDB
* Neo4J
* Zeppelin
* Kafka


Es importante mencionar que el entorno completo consume muchos recursos de su equipo, motivo por el cuál, se propondrán ejercicios pero con ambientes reducidos, en función de las herramientas utilizadas.

Ejecute `docker network inspect` en la red (por ejemplo, `docker-hadoop-spark-hive_default`) para encontrar la IP en la que se publican las interfaces de hadoop. Acceda a estas interfaces con las siguientes URL:

Namenode: http://<IP_Anfitrion>:9870/dfshealth.html#tab-overview
Datanode: http://<IP_Anfitrion>:9864/
Spark master: http://<IP_Anfitrion>:8080/
Spark worker: http://<IP_Anfitrion>:8081/	
HBase Master-Status: http://<IP_Anfitrion>:16010
HBase Zookeeper_Dump: http://<IP_Anfitrion>:16010/zk.jsp
HBase Region_Server: http://<IP_Anfitrion>:16030
Zeppelin: http://<IP_Anfitrion>:8888
Neo4j: http://<IP_Anfitrion>:7474

Para implementar ejecute
```
  git clone https://github.com/lopezdar222/herramientas_big_data
  cd herramientas_big_data
  sudo docker-compose -f docker-compose-vX.yml up -d
```

## 1) HDFS

Se puede utilizar el entorno docker-compose-v1.yml

Copiar los archivos ubicados en la carpeta Datasets, dentro del contenedor "namenode"

```
  sudo docker exec -it namenode bash
  cd home
  mkdir Datasets
  exit
  sudo docker cp <path><archivo> namenode:/home/Datasets/<archivo>
```

Ubicarse en el contenedor "namenode"

```
  sudo docker exec -it namenode bash
```

Crear un directorio en HDFS llamado "/data".

```
  hdfs dfs -mkdir -p /data
```

Copiar los archivos csv provistos a HDFS:
```
  hdfs dfs -put /home/Datasets/* /data
```

Este proceso de creación de la carpeta data y copiado de los arhivos, debe poder ejecutarse desde un shell script.

## 2) Hive

Se puede utilizar el entorno docker-compose-v2.yml

Crear tablas en Hive, a partir de los csv ingestados en HDFS.

Para esto, se puede ubicar dentro del contenedor correspondiente al servidor de Hive, y ejecutar desdea allí los scripts necesarios

```
  sudo docker exec -it hive-server bash
  hive
```

Este proceso de creación las tablas debe poder ejecutarse desde un shell script.
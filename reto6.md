# bigdata_in_aws---telematics_challenges

## HIVE y SparkSQL, Gestión de Datos via SQL

### Permisos y Carga de Datos
1. Conceder permisos ejecutando: "hdfs dfs -chmod -R 777 /user/hadoop/datasets/onu/" (Para cargar los datos de la tabla HDI)
3. Iniciar Beeline y conectarse a Hive ejecutando: "beeline"
4. Dentro de Beeline, conectarse al servidor: !connect jdbc:hive2://localhost:10000

![ConexionAlServidor](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/conexion%20al%20servidor.png)


### Creación de la Base de Datos y Tabla HDI
1. Crear la base de datos ejecutando: "CREATE DATABASE IF NOT EXISTS usernamedb;"
2. Usar la base de datos creada: "USE usernamedb;"
3. Crear la tabla HDI:
```sql
CREATE TABLE IF NOT EXISTS HDI (
    id INT,
    country STRING,
    hdi FLOAT,
    lifeex INT,
    mysch INT,
    eysch INT,
    gni INT
)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```

![CreateTable_HDI](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/Create%20table%20HDI%20.png)


### Creación de la tabla EXPO
1. Crear la tabla HDI:
```sql
CREATE TABLE IF NOT EXISTS EXPO (
    country STRING,
    export FLOAT
)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```

![CreateTable_HDI](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/Creacion%20tabla%20expo.png)

### Cargar los datos en la tabla HDI y en la tabla EXPO que acabomos de crear

1. Cargar los datos en la tabla HDI: "LOAD DATA INPATH '/user/hadoop/datasets/onu/hdi-data.csv' INTO TABLE HDI;"

![CreateTable_HDI](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/Cargar%20datos%20a%20tabla%20HDI.png)

2. Cargar los datos en la tabla EXPO: "LOAD DATA INPATH '/user/hadoop/datasets/onu/export-data.csv' INTO TABLE EXPO;"

![CreateTable_HDI](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/cargar%20datos%20a%20tabla%20EXPO.png)


### Verificación de datos de la tabla HDI

1. Obtener los primeros 10 registros
```sql
SELECT * FROM HDI LIMIT 10;
```

![CreateTable_HDI](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/Cargar%20datos%20a%20tabla%20HDI%202.png)


### Verificación de datos de la tabla EXPO

1. Obtener los primeros 10 registros
```sql
SELECT * FROM EXPO LIMIT 10;
```

![CreateTable_HDI](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/Verificar%20datos%20en%20tabla%20expo.png)




# bigdata_in_aws---telematics_challenges

## 1. HDFS y S3

### Creación de Cluster Utilizando Amazon EMR
1. Creación del cluster.
![Custer](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/1.png)

2. Desactivar el "Bloqueo de acceso público".
3. Crear una regla de entrada en el grupo de seguridad del nodo (instancia) con puerto 22 y 0.0.0.0/0.
4. Ingreso al cluster mediante Hub y creación de usuario y contraseña.

![Hub](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/2.png)

### Corrección de Error en Servicios de Archivos

Los servicios de archivos tenían un error, el cual fue corregido de la siguiente manera:

#### Pasos para Corregir este Error:
![Error](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/file%20error.png)


1. Ingresar al nodo master del cluster por SSH.
2. Editar el archivo `/etc/hue/conf/hue.ini`.
   - Comando: `nano /etc/hue/conf/hue.ini`
3. Modificar la línea de código que contiene `webhdfs-url`, cambiando el puerto de 14000 a 9870.

Finalmente asi se debe de verse despues de la correccion:
![Correction](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/fixed%20file%20error.png)

### Creación de directorios para archivos .csv (export-data.csv y hdi-data.csv)

![Data](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/datasets%20y%20onu%20con%20.csv.png)

## Ejemplo de gti-data.csv
![Ejemplo](https://github.com/JuanJmf01/bigdata_in_aws---telematics_challenges/blob/main/Images/Ejemplo%20de%20archivo%20.csv.png)



---

## 2. HIVE y SparkSQL, Gestión de Datos via SQL

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

### Verificacion en Hub

![CreateTable_HDI]()



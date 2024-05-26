# bigdata_in_aws---telematics_challenges

## 1. HDFS y S3

### Creación de Cluster Utilizando Amazon EMR
1. Creación del cluster.

(Adjuntar foto de creación del cluster)

2. Desactivar el "Bloqueo de acceso público".
3. Crear una regla de entrada en el grupo de seguridad del nodo (instancia) con puerto 22 y 0.0.0.0/0.
4. Ingreso al cluster mediante Hub y creación de usuario y contraseña.

(Adjuntar foto de creación del cluster)

### Corrección de Error en Servicios de Archivos

Los servicios de archivos tenían un error, el cual fue corregido de la siguiente manera:

#### Pasos para Corregir el Error:
1. Ingresar al nodo master del cluster por SSH.
2. Editar el archivo `/etc/hue/conf/hue.ini`.
   - Comando: `nano /etc/hue/conf/hue.ini`
3. Modificar la línea de código que contiene `webhdfs-url`, cambiando el puerto de 14000 a 9870.

(Mostrar error)
(Mostrar corrección del error)

---

## 2. HIVE y SparkSQL, Gestión de Datos via SQL

### Permisos y Carga de Datos
1. Conceder permisos ejecutando: "hdfs dfs -chmod -R 777 /user/hadoop/datasets/onu/" (Para cargar los datos de la tabla HDI)
2. Iniciar Beeline y conectarse a Hive ejecutando: "beeline"
3. Dentro de Beeline, conectarse al servidor: !connect jdbc:hive2://localhost:10000

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

4. Cargar los datos en la tabla HDI: "LOAD DATA INPATH '/user/hadoop/datasets/onu/hdi-data.csv' INTO TABLE HDI;"

### Verificación de datos

1. Obtener los primeros 10 registros "SELECT * FROM HDI LIMIT 10;"
2. Consultar países con GNI mayor a 2000: 
```sql
SELECT h.country, h.gni, e.expct
FROM HDI h
JOIN EXPO e ON (h.country = e.country)
WHERE h.gni > 2000;
```



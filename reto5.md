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

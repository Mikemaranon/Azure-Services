# Solucion ETL para batch processing con Hadoop en ambiente Azure con los servicios HDInsight + Azure Data Lake Storage Gen 2 + HIVE+ SQL Database + Sqoo

### Lo primero que necesitamos hacer es crear un grupo de recursos nuevo:  
![image](https://github.com/user-attachments/assets/6aff2674-e8c8-4742-9828-13b3c2d39d33)  
### Las etiquetas las dejamos vacías y saltamos a la siguiente parte, luego le damos a crear  
![image](https://github.com/user-attachments/assets/ea327d10-dc49-4b80-b62a-ffe3df068b08)  
![image](https://github.com/user-attachments/assets/76ed1457-9b5f-430d-923e-62f944f3f4cf)  
### Tras esto volvemos al inicio y nos vamos a cuentas de almacenamiento, luego creamos una.  
![image](https://github.com/user-attachments/assets/cbccd3fe-a41f-4b89-bc71-720d88937a93)  
![image](https://github.com/user-attachments/assets/64dfb6b0-cff5-4c0d-8d57-e053d3dee315)  
### Nos vamos a "avanzado" y marcamos lo siguiente.  
![image](https://github.com/user-attachments/assets/768a08f9-8d88-4f30-bbb0-3ca6e2d31520)  
![image](https://github.com/user-attachments/assets/5c6dfc34-daa6-4d24-b513-9eb730226c9f)  
### Nos vamos a "redes" y marcamos lo siguiente.  
![image](https://github.com/user-attachments/assets/d96215a7-314e-45cf-9ee8-8518689164c7)  
![image](https://github.com/user-attachments/assets/3866f585-731e-4eb6-a3f0-8d4efb4e7684)  
### Nos vamos a "protección de datos" y lo dejamos en la configuración por defecto.  
![image](https://github.com/user-attachments/assets/28328f27-9f70-44ef-8602-36ce23127d36)  
![image](https://github.com/user-attachments/assets/39fa3cf3-3da5-45bf-a5f7-9e910a2a1b0a)  
### Nos vamos a "cifrado" y lo dejamos en la configuración por defecto.  
![image](https://github.com/user-attachments/assets/5abbaef5-8f70-4fa6-a1d4-57dde30c49c3)  
### Nos vamos a "Etiquetas" y lo dejamos en blanco. Revisamos y creamos.  
![image](https://github.com/user-attachments/assets/81b8479e-9c09-45ad-bd82-6b053742de29)  

# Crear servicio de SQL (Data destination)

### En la barra superior buscamos "SQL" y luego pulsamos en crear  
![image](https://github.com/user-attachments/assets/c90d90ff-298d-48f1-9ef2-41ad7b5d7f98)  
### Creando la base de datos, introducimos nombre y creamos nuevo servidor  
![image](https://github.com/user-attachments/assets/4a31c380-0ef5-4f48-9a58-ddf53a424229)  
![image](https://github.com/user-attachments/assets/3891c114-dc63-4dee-84b5-31f8478c493f)  
### Creamos el administrador que queramos con la contraseña (admin13, Mike1234)  
![image](https://github.com/user-attachments/assets/fd05cea0-160f-468f-8fc7-364a52c311bb)  
### En set admin, buscamos nuestro usuario  
![image](https://github.com/user-attachments/assets/7cc51921-cbd3-48ab-84ca-31e004dda39c)  
### Seleccionamos "implementación" y "Almacenamiento de copias de seguridad con redundancia local"    
### Hacemos click en "configurar base de datos"  
![image](https://github.com/user-attachments/assets/96f1a0f9-6d3d-4817-93cc-faf9bad15719)  
### ponemos la siguiente configuración:  
![image](https://github.com/user-attachments/assets/745bd422-c74d-4af7-9117-dae27f1eb6d3)  
![image](https://github.com/user-attachments/assets/285df139-8a22-421a-96b3-55c312414e27)  
![image](https://github.com/user-attachments/assets/4d4d424f-5dd4-4347-84ff-57907de145c4)  
### Saltamos a "redes" y dejamos todo en por defecto  
### Saltamos a "seguridad" y lo dejamos todo en por defecto  
### Saltamos a "configuración adicional" y lo dejamos en por defecto  
### Saltamos a "Etiquetas" y lo dejamos vacío  
### Saltamos a "Revisar y crear" y le damos a crear  
![image](https://github.com/user-attachments/assets/f25057ca-a7d1-4f48-95cf-efeeea0bc677)  
### Hacemos click en la base de datos y luego en "Editor de consultas"  
![image](https://github.com/user-attachments/assets/9c73a97e-a9ed-4fe8-9733-5c3ccc9c4271)  
### vemos que hay un error con nuestro correo, para solucionarlo nos vamos al servidor dentro del grupo de recursos  
### en la pestaña de "Seguridad" seleccionamos "Redes", luego hacemos click en "Redes seleccionadas"  
![image](https://github.com/user-attachments/assets/b62a1d4a-559b-4f9a-b1ea-7bc1fb914ddd)  
### En reglas del firewall, damos a añadir la dirección IPv4 del cliente  
![image](https://github.com/user-attachments/assets/fbc8b227-47a4-46e9-ac31-b508662e7cf8)  
![image](https://github.com/user-attachments/assets/c8c5671a-fc15-4b27-bc10-3ab5473694b7)  
### Ahora vemos que lo detecta sin problemas  
![image](https://github.com/user-attachments/assets/83cd4f60-3c25-435b-a07c-115540e98bbd)  

# Identidades Administradas
### Escribimos "Identidades Administradas" en la barra de búsqueda  
![image](https://github.com/user-attachments/assets/e375ca73-53c2-4cb6-94d7-3a993a9fd48c)  
### Elegimos la primera opción y luego damos click en "crear"  
![image](https://github.com/user-attachments/assets/843c746f-af99-4f33-80b5-1bf98bf3c5b6)  
### Introducimos las siguientes opciones  
![image](https://github.com/user-attachments/assets/63113b63-e615-42ba-8829-e65e285708ee)  
### Saltamos a la opción de "Revisar" y le damos a "crear"  
![image](https://github.com/user-attachments/assets/9c48af46-8c48-4ec3-b55b-c50d076d47b5)  
![image](https://github.com/user-attachments/assets/6d7f5f42-a904-4ba2-b41b-ce6f5c8686b1)  
### Una vez creado nos vamos a Home y buscamos storagep9  
![image](https://github.com/user-attachments/assets/de2dc415-4049-4338-8a92-dbb30ee9c5cb)  
### Seleccionamos Control de Acceso (IAM), le damos a "crear"  
![image](https://github.com/user-attachments/assets/d83a86ba-8994-4ffc-9b9d-4d32fdb7ae74)  
### Creamos uno que se llama Storage Blob Data Owner
![image](https://github.com/user-attachments/assets/197d0d6d-9c5e-4f9b-83e4-c2b1256edc6c)  
### Introducimos las siguientes  
![image](https://github.com/user-attachments/assets/7e6741a1-84cc-41f1-b0e1-c22a8a8c83e1)  
### dejamos las "Condiciones" en por defecto  
![image](https://github.com/user-attachments/assets/0b4ff0f7-cebf-4804-99ba-8b3ded0342b6)  
### Dejamos la revisión y asignación en por defecto y creamos
### Ahora nos vamos al servidor y seleccionamos Control de acceso (IAM), luego a "añadir"
![image](https://github.com/user-attachments/assets/5dc0fd8d-a42a-4350-afb2-2317815d68eb)
### establecemos la siguiente configuración
![image](https://github.com/user-attachments/assets/8335246a-59ff-4535-9f18-0996f670cad1)
### Siguiente y "Revisar y Asignar"

# HD Insight

### Escribimos en la barra de búsqueda "Clústeres de HD Insight" y creamos uno  
![image](https://github.com/user-attachments/assets/f1edbf44-6d73-4af1-8f71-ba4d5f04ee49)  
### Al seleccionar la subscripción, si nos dice que no está registrada le damos a registrar y seleccionamos aquí  
![image](https://github.com/user-attachments/assets/f312cd58-122d-4771-923c-bcdeb7a3bf91)  
### Hacemos click en "seleccionar tipo de cluster", luego seleccionamos "Interactive query"  
![image](https://github.com/user-attachments/assets/27b995a7-16b5-4415-b969-435e8b98be74)  
### Seleccionamos usuario y contraseña (admin13, Mike1234!!)  
![image](https://github.com/user-attachments/assets/d43eb755-54c8-476a-b922-3e77e5f1c5e9)  
### Hacemos click en "Siguiente: Almacenamiento"  
![image](https://github.com/user-attachments/assets/b75247fe-6ea7-46a6-b760-50f987daa1c4)  
![image](https://github.com/user-attachments/assets/f3d23b02-eefd-47bc-a5ee-dc9ee9221cef)  
### En redes dejamos la configuración por defecto  
![image](https://github.com/user-attachments/assets/4b9cdb22-6838-452d-8d5e-0a35835212d3)
### Le damos a crear  
![image](https://github.com/user-attachments/assets/df4071c1-ebfd-40ef-bd80-3cbc2f336932)  

### Ahora nos vamos a "storagep9" y nos ubicamos aquí  
![image](https://github.com/user-attachments/assets/2c5e78a0-1d66-41a5-a82d-573fd55731cc)  
### Agregamos directorio  
![image](https://github.com/user-attachments/assets/8603c4bd-1b2a-4cbd-9ebd-32ee153dd343)  
### Dentro del directorio creamos otro nuevo  
![image](https://github.com/user-attachments/assets/9cfd31d5-26b7-4c20-8251-67e306988320)  
### Ahora cargamos el csv llamado "simulated_flight_data_extensive.csv" en el segundo directorio  
![image](https://github.com/user-attachments/assets/ea8de4ee-fdc8-4c8e-b6d6-2337682595d6)  
![image](https://github.com/user-attachments/assets/331bbfdf-5d3b-4d66-8c70-bdac3a06f5b2)  
### Ahora nos vamos a Home y al cluster  
![image](https://github.com/user-attachments/assets/69f4d482-bde2-45a4-b2cb-330a59d07776)  
### Hacemos click en Ambari
![image](https://github.com/user-attachments/assets/4d5352fb-95ea-47e0-b31f-b2ecd8aff1b2)  
### Nos pedirá el usuario y la clave para entrar, luego accedemos
### Hacemos click en los 9 cuadrados agrupados que hay al lado del usuario y escogemos "Hive view 2.0"  
### Después de validar algunas cosas debería aparecer esto  
![image](https://github.com/user-attachments/assets/bc22c35a-5134-46a9-81d6-3cc5ae6f771c)  
### Vamos a introducir la siguiente query
``` SQL
DROP TABLE IF EXISTS flightdelay_raw;

CREATE EXTERNAL TABLE flightdelay_raw(
    year INT,
    month INT,
    day INT,
    airline STRING,
    flight_number STRING,
    origin_airport STRING,
    destination_airport STRING,
    departure_delay INT,
    arrival_delay INT,
    flight_duration INT
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
STORED AS TEXTFILE
LOCATION '/demo/FlightDelayData/InputData';


DROP TABLE IF EXISTS flightdelay;

CREATE TABLE flightdelay AS
SELECT 
    year,
    CONCAT(year, '-', month, '-', day) AS flight_date,
    airline AS airline,
    flight_number AS flight_num,
    origin_airport AS origin_airport_code,
    destination_airport AS dest_airport_code,
    departure_delay AS dep_delay,
    arrival_delay AS arr_delay,
    flight_duration AS duration
FROM 
    flightdelay_raw;
```  

![image](https://github.com/user-attachments/assets/a7737cda-140e-4702-884d-5ed77014ff70)  
### Nos vamos a tables para ver
![image](https://github.com/user-attachments/assets/825cc829-217e-4bf9-9a61-28b4f0585572)  
### Volvemos a querys y creamos nueva worksheet, vamos a hacer una consulta simple  
``` SQL
SELECT * FROM flightdelay limit 5;
```
### Este es el resultado  
![image](https://github.com/user-attachments/assets/d305b213-1b67-4fe1-b692-e5d0145bea45)  
![image](https://github.com/user-attachments/assets/4aec3fce-0da5-4ade-bc57-316e0e84628a)  
### Vamos a abrir un nuevo worksheet y ejecutamos el siguiente query
``` SQL
INSERT OVERWRITE DIRECTORY '/demo/FlightDelayData/output'
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
SELECT regexp_replace(origin_city_name, '''', ''),
    avg(weather_delay)
FROM flightdelay
WHERE weather_delay IS NOT NULL
GROUP BY origin_city_name;
```

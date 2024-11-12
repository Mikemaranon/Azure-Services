# Aquí desarrollaré la práctica 10
Las siguientes 10 preguntas pertenecen a la práctica 10 y serán desarrolladas en detalles en este repositorio:

### Pregunta 1. Selecciona todos los registros del año 2023 donde el vuelo fue retrasado más de 60 minutos. Muestra las columnas de fecha, aerolínea, número de vuelo y el retraso en minutos.  
``` SQL
SELECT 
    year, 
    flight_date, 
    airline, 
    flight_num, 
    dep_delay, 
    arr_delay
FROM 
    flightdelay
WHERE 
    year = 2023 
    AND (dep_delay > 60 OR arr_delay > 60);
```
![image](https://github.com/user-attachments/assets/9b90d296-6a51-4b51-bd89-d537a73802b0)

### Pregunta 2. Calcula el promedio de retraso en la llegada y en la salida para cada aerolínea. Ordena los resultados en orden descendente por el retraso promedio en la llegada.  
``` SQL
SELECT 
    airline, 
    AVG(dep_delay) AS avg_dep_delay, 
    AVG(arr_delay) AS avg_arr_delay
FROM 
    flightdelay
GROUP BY 
    airline
ORDER BY 
    avg_arr_delay DESC;

```
![image](https://github.com/user-attachments/assets/2a87ce12-54fe-44a6-a8b0-aab809ab4c96)

### Pregunta 3. ¿Cuáles son las cinco rutas más comunes (aeropuerto de origen y destino) en los datos? Incluye el conteo de vuelos para cada ruta.
``` SQL
SELECT 
    origin_airport_code, 
    dest_airport_code, 
    COUNT(*) AS flight_count
FROM 
    flightdelay
GROUP BY 
    origin_airport_code, dest_airport_code
ORDER BY 
    flight_count DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/aebb454b-6c5c-4de8-92db-5f60c8bc4cf2)

### Pregunta 4. Encuentra los tres aeropuertos de destino con el mayor promedio de retraso en la llegada. Muestra el nombre del aeropuerto, el número total de vuelos y el retraso promedio. 
``` SQL
SELECT 
    dest_airport_code, 
    COUNT(*) AS flight_count, 
    AVG(arr_delay) AS avg_arr_delay
FROM 
    flightdelay
GROUP BY 
    dest_airport_code
ORDER BY 
    avg_arr_delay DESC
LIMIT 3;
```
![image](https://github.com/user-attachments/assets/92efa078-6baf-43ac-9b05-9e3f38f4b510)

### Pregunta 5. Selecciona todos los vuelos de los fines de semana (sábado y domingo) con origen en un aeropuerto específico y cuyo retraso en salida o llegada haya sido superior a 30 minutos. 
``` SQL
SELECT 
    *
FROM 
    flightdelay
WHERE 
    (DAYOFWEEK(flight_date) = 7  -- Domingo
    OR DAYOFWEEK(flight_date) = 1) -- Sábado
    AND (dep_delay > 30 OR arr_delay > 30)
    AND origin_airport_code = 'LAX'; 
```
![image](https://github.com/user-attachments/assets/a63b4170-01e9-4913-b83e-30fb681a0476)

### Pregunta 6. Encuentra el promedio de retraso en los vuelos para cada mes y año. Crea una tabla con las columnas de año, mes y promedio de retraso en minutos. 
``` SQL
SELECT 
    year(flight_date) AS year, 
    month(flight_date) AS month, 
    AVG(dep_delay) AS avg_dep_delay, 
    AVG(arr_delay) AS avg_arr_delay
FROM 
    flightdelay
GROUP BY 
    year(flight_date), 
    month(flight_date)
ORDER BY 
    year, month;
```
![image](https://github.com/user-attachments/assets/f83520f8-95a8-436d-89a1-07793710b220)

### Pregunta 7. Crea una tabla llamada DelayedFlightsSummary que contenga un resumen de los vuelos con retraso superior a 45 minutos en la llegada o salida. La tabla debe incluir las siguientes columnas: año, mes, aerolínea, aeropuerto de origen, aeropuerto de destino, número total de vuelos retrasados y el retraso promedio en minutos para cada combinación.
``` SQL
CREATE TABLE DelayedFlightsSummary AS
SELECT 
    year(flight_date) AS year, 
    month(flight_date) AS month, 
    airline, 
    origin_airport_code, 
    dest_airport_code, 
    COUNT(*) AS total_delayed_flights, 
    AVG(CASE 
            WHEN dep_delay > 45 THEN dep_delay 
            WHEN arr_delay > 45 THEN arr_delay 
            ELSE 0 
        END) AS avg_delay_minutes
FROM 
    flightdelay
WHERE 
    dep_delay > 45 OR arr_delay > 45
GROUP BY 
    year(flight_date), 
    month(flight_date), 
    airline, 
    origin_airport_code, 
    dest_airport_code;
```
![image](https://github.com/user-attachments/assets/6ae5776b-d0d1-4eee-83ef-d130c0b1ac2b)

### Pregunta 8. Selecciona los vuelos con una duración (tiempo de vuelo) superior al promedio de duración de todos los vuelos en el mismo año. Muestra las columnas de aerolínea, origen, destino y duración del vuelo. 
``` SQL
SELECT 
    airline, 
    origin_airport_code, 
    dest_airport_code, 
    duration
FROM 
    flightdelay f1
WHERE 
    duration > (
        SELECT 
            AVG(duration)
        FROM 
            flightdelay f2
        WHERE 
            year(f1.flight_date) = year(f2.flight_date)
    );
```
![image](https://github.com/user-attachments/assets/9251a5df-1dde-4e66-81d7-a763ca39a332)

### Pregunta 9. Encuentra el porcentaje de vuelos de cada aerolínea que han tenido un retraso en la llegada superior a 30 minutos.
``` SQL
SELECT 
    airline, 
    (COUNT(CASE WHEN arr_delay > 30 THEN 1 END) / COUNT(*)) * 100 AS delay_percentage
FROM 
    flightdelay
GROUP BY 
    airline;
```
![image](https://github.com/user-attachments/assets/92bead12-7f52-467c-b232-60b266985696)

### Pregunta 10. Si tuvieras una tabla adicional de aeropuertos con columnas como airport_code y airport_name, escribe una consulta para unir esta tabla con los datos de vuelos y obtener el nombre del aeropuerto de origen y de destino en cada vuelo.
``` SQL
SELECT 
    f.airline, 
    f.flight_num, 
    f.flight_date, 
    a1.airport_name AS origin_airport_name, 
    a2.airport_name AS dest_airport_name, 
    f.dep_delay, 
    f.arr_delay, 
    f.duration
FROM 
    flightdelay f
JOIN 
    airports a1 ON f.origin_airport_code = a1.airport_code
JOIN 
    airports a2 ON f.dest_airport_code = a2.airport_code;
```

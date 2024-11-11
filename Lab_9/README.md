### Solucion ETL para batch processing con Hadoop en ambiente Azure con los servicios HDInsight + Azure Data Lake Storage Gen 2 + HIVE+ SQL Database + Sqoo

Lo primero que necesitamos hacer es crear un grupo de recursos nuevo:  
![image](https://github.com/user-attachments/assets/6aff2674-e8c8-4742-9828-13b3c2d39d33)  
Las etiquetas las dejamos vacías y saltamos a la siguiente parte, luego le damos a crear  
![image](https://github.com/user-attachments/assets/ea327d10-dc49-4b80-b62a-ffe3df068b08)  
![image](https://github.com/user-attachments/assets/76ed1457-9b5f-430d-923e-62f944f3f4cf)  
Tras esto volvemos al inicio y nos vamos a cuentas de almacenamiento, luego creamos una.  
![image](https://github.com/user-attachments/assets/cbccd3fe-a41f-4b89-bc71-720d88937a93)  
![image](https://github.com/user-attachments/assets/64dfb6b0-cff5-4c0d-8d57-e053d3dee315)  
Nos vamos a "avanzado" y marcamos lo siguiente.  
![image](https://github.com/user-attachments/assets/768a08f9-8d88-4f30-bbb0-3ca6e2d31520)  
![image](https://github.com/user-attachments/assets/5c6dfc34-daa6-4d24-b513-9eb730226c9f)  
Nos vamos a "redes" y marcamos lo siguiente.  
![image](https://github.com/user-attachments/assets/d96215a7-314e-45cf-9ee8-8518689164c7)  
![image](https://github.com/user-attachments/assets/3866f585-731e-4eb6-a3f0-8d4efb4e7684)  
Nos vamos a "protección de datos" y lo dejamos en la configuración por defecto.  
![image](https://github.com/user-attachments/assets/28328f27-9f70-44ef-8602-36ce23127d36)  
![image](https://github.com/user-attachments/assets/39fa3cf3-3da5-45bf-a5f7-9e910a2a1b0a)  
Nos vamos a "cifrado" y lo dejamos en la configuración por defecto.  
![image](https://github.com/user-attachments/assets/5abbaef5-8f70-4fa6-a1d4-57dde30c49c3)  
Nos vamos a "Etiquetas" y lo dejamos en blanco. Revisamos y creamos.  
![image](https://github.com/user-attachments/assets/81b8479e-9c09-45ad-bd82-6b053742de29)  

### Crear servicio de SQL (Data destination)

En la barra superior buscamos "SQL" y luego pulsamos en crear  
![image](https://github.com/user-attachments/assets/c90d90ff-298d-48f1-9ef2-41ad7b5d7f98)  
Creando la base de datos, introducimos nombre y creamos nuevo servidor  
![image](https://github.com/user-attachments/assets/4a31c380-0ef5-4f48-9a58-ddf53a424229)  
![image](https://github.com/user-attachments/assets/3891c114-dc63-4dee-84b5-31f8478c493f)  
creamos el administrador que queramos con la contraseña (admin13, Mike1234)  
![image](https://github.com/user-attachments/assets/fd05cea0-160f-468f-8fc7-364a52c311bb)  
En set admin, buscamos nuestro usuario  
![image](https://github.com/user-attachments/assets/7cc51921-cbd3-48ab-84ca-31e004dda39c)  
Seleccionamos "implementación" y "Almacenamiento de copias de seguridad con redundancia local"    
Hacemos click en "configurar base de datos"  
![image](https://github.com/user-attachments/assets/96f1a0f9-6d3d-4817-93cc-faf9bad15719)  
ponemos la siguiente configuración:  
![image](https://github.com/user-attachments/assets/745bd422-c74d-4af7-9117-dae27f1eb6d3)  
![image](https://github.com/user-attachments/assets/285df139-8a22-421a-96b3-55c312414e27)  
![image](https://github.com/user-attachments/assets/4d4d424f-5dd4-4347-84ff-57907de145c4)  
Saltamos a "redes" y dejamos todo en por defecto  
Saltamos a "seguridad" y lo dejamos todo en por defecto  
Saltamos a "configuración adicional" y lo dejamos en por defecto  
Saltamos a "Etiquetas" y lo dejamos vacío  
Saltamos a "Revisar y crear" y le damos a crear  








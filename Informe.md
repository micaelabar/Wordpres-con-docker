# Instalación del Subsistema de Windows para Linux (WSL) y Configuración de Ubuntu como Entorno de Desarrollo Web con Angular.

## 1. Tiempo de duración:
  El tiempo estimado para la realización de este proyecto es de 1 hora.
## 2. Fundamentos:
Este proyecto está basado en el uso de Docker para crear y administrar contenedores para ejecutar WordPress, una de las plataformas más populares para la creación de sitios web. Docker proporciona un entorno aislado y repetible para instalar y ejecutar aplicaciones como WordPress, lo que facilita la administración y el mantenimiento del entorno de desarrollo o producción.

### Fundamentos claves:
- Contenedores Docker: Son entornos ligeros y aislados que permiten ejecutar aplicaciones de manera consistente en cualquier entorno.
- WordPress: Sistema de gestión de contenido (CMS) para crear sitios web, blogs, y aplicaciones en línea.
- MySQL: Base de datos utilizada por WordPress para almacenar su contenido.
- phpMyAdmin: Herramienta para gestionar MySQL de manera fácil y visual.
## 3. Conocimientos previos:
Para llevar a cabo este proyecto, es recomendable tener conocimientos básicos de:
- Uso de la terminal: Manejo de comandos en la terminal de Linux (o cualquier sistema operativo que utilices).
- Docker: Conocer los comandos básicos para crear y gestionar contenedores.
- WordPress: Familiaridad básica con la configuración y administración de WordPress.
- Bases de datos MySQL: Conocimiento básico sobre la creación y administración de bases de datos.
## 5. Objetivos a alcanzar:
- Configurar un entorno de desarrollo para WordPress utilizando Docker.
- Instalar y configurar MySQL para gestionar la base de datos de WordPress.
- Instalar phpMyAdmin para la administración visual de MySQL.
- Asegurar la persistencia de datos a través de volúmenes de Docker.
- Crear una red personalizada de Docker para facilitar la comunicación entre los contenedores de WordPress, MySQL y phpMyAdmin.
 ## 6. Equipo necesario:
- Computadora personal con capacidad para ejecutar Docker (Linux, macOS o Windows).
- Docker instalado en el equipo.
- Conexión a internet para descargar imágenes de contenedores.
 ## 7. Material de apoyo:
- Documentación oficial de Docker: https://docs.docker.com/
- Documentación de WordPress: https://wordpress.org/support/
- phpMyAdmin: https://www.phpmyadmin.net/
## 8. Procedimiento:
### Paso 1: Crear una red personalizada de Docker
```
docker network create wordpress-net
````
## Evidencia:
<imag!![imagen 1](https://github.com/user-attachments/assets/add83a98-e42e-4fcd-abcc-36b3ce1c4479)

### Paso 2: Crear un volumen para MySQL
```
docker volume create wordpress-db-data
````
## Evidencia:
<imag!![imagen 2](https://github.com/user-attachments/assets/919f21aa-fd1a-445c-baf0-1cc2453b05ba)


### Paso 3: Crear el contenedor de MySQL.
````
docker run -d --name mysql-container \
  --network wordpress-net \
  -e MYSQL_ROOT_PASSWORD=rootpassword \
  -e MYSQL_DATABASE=wordpress \
  -e MYSQL_USER=wordpressuser \
  -e MYSQL_PASSWORD=wordpresspassword \
  -v wordpress-db-data:/var/lib/mysql \
  mysql:5.7
````
## Evidencia:
<imag!![imagen 3](https://github.com/user-attachments/assets/8c35ec19-d11f-406e-b36f-eeaa27d09565)

### Paso 4: Crear el contenedor de phpMyAdmin
````
docker run -d --name phpmyadmin-container \
  --network wordpress-net \
  -e PMA_HOST=mysql-container \
  -e PMA_PORT=3306 \
  -p 8080:80 \
  phpmyadmin/phpmyadmin
````
## Evidencia:
<imag!![imagen 4](https://github.com/user-attachments/assets/fec6ab9c-35bb-430a-a058-5ba8bc53eb14)

### Paso 5: Crear el contenedor de WordPress
````
docker run -d --name wordpress-container \
  --network wordpress-net \
  -e WORDPRESS_DB_HOST=mysql-container:3306 \
  -e WORDPRESS_DB_NAME=wordpress \
  -e WORDPRESS_DB_USER=wordpressuser \
  -e WORDPRESS_DB_PASSWORD=wordpresspassword \
  -p 8081:80 \
  wordpress
````
## Evidencia:
<imag!![imagen 5](https://github.com/user-attachments/assets/3b592fdc-d83f-45a0-90da-2f59d9e97840)

## 9. Resultados esperados:
- Un contenedor de WordPress accesible en http://localhost:8081.
- Un contenedor de phpMyAdmin accesible en http://localhost:8080 para gestionar la base de datos.
- La base de datos de WordPress debe estar configurada y operativa.
## Evidencia:
<imag!![resultados ](https://github.com/user-attachments/assets/fa22012d-df65-4976-9573-fb5a648a65bc)

<imag!![resultados](https://github.com/user-attachments/assets/ded455b7-8cfe-4c8e-9412-837f71a28dbd)

## 10. Conclusión:
En este proyecto, se ha logrado configurar un entorno de desarrollo para WordPress utilizando Docker, lo que ha permitido crear un sistema eficiente, aislado y fácil de gestionar. La utilización de contenedores ha proporcionado una solución escalable y replicable, facilitando tanto la implementación como el mantenimiento de los servicios involucrados, como MySQL y phpMyAdmin.

El uso de Docker para gestionar estos contenedores garantiza la persistencia de los datos a través de volúmenes y asegura que las configuraciones de los contenedores sean consistentes en diferentes entornos de desarrollo o producción. Además, la conexión entre WordPress, MySQL y phpMyAdmin ha sido exitosa gracias a la creación de una red personalizada que permite la comunicación entre los contenedores.

En conclusión, esta experiencia demuestra la potencia de Docker para administrar aplicaciones complejas como WordPress, ofreciendo una solución robusta, fácil de gestionar y altamente flexible para cualquier entorno de desarrollo web.
  ## 11. Bibliografía:
  - Docker Documentation: https://docs.docker.com/
  - WordPress Documentation: https://wordpress.org/support/
  - phpMyAdmin Documentation: https://www.phpmyadmin.net/

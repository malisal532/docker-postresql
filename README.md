# docker-postresql
# docker-postgresql
Configuración de PostgreSQL en Docker

Este documento explica cómo instalar y configurar PostgreSQL en un contenedor Docker paso a paso.

Requisitos previos

Tener Docker instalado.

Conocimientos básicos de PostgreSQL y Docker.

# 1. Verificar que Docker está instalado

Ejecuta el siguiente comando para comprobar la versión de Docker:

docker --version

Si aparece un mensaje con la versión de Docker, significa que está instalado correctamente.

# 2. Descargar la imagen de PostgreSQL

Para obtener la imagen oficial de PostgreSQL, ejecuta:

docker pull postgres

Esto descargará la imagen desde Docker Hub.

# 3. Crear y ejecutar un contenedor con PostgreSQL

Ejecuta el siguiente comando para iniciar un contenedor con PostgreSQL:

docker run --name mi_postgres \
    -e POSTGRES_USER=admin \
    -e POSTGRES_PASSWORD=admin123 \
    -e POSTGRES_DB=mi_base \
    -p 5432:5432 \
    -d postgres

Parámetros explicados:

--name mi_postgres → Nombre del contenedor.

-e POSTGRES_USER=admin → Usuario de la base de datos.

-e POSTGRES_PASSWORD=admin123 → Contraseña.

-e POSTGRES_DB=mi_base → Nombre de la base de datos.

-p 5432:5432 → Expone el puerto 5432.

-d postgres → Ejecuta el contenedor en segundo plano.

Para verificar que el contenedor está corriendo, usa:

docker ps

# 4. Conectarse a PostgreSQL dentro del contenedor

Para acceder a la base de datos dentro del contenedor, ejecuta:

docker exec -it mi_postgres psql -U admin -d mi_base

Si todo está bien, verás el prompt de PostgreSQL listo para ejecutar comandos.

# 5. Crear la tabla "Estudiante"

Dentro de la consola de PostgreSQL, ejecuta:

CREATE TABLE Estudiante (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    edad INT,
    correo VARCHAR(100) UNIQUE,
    fecha_registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Para confirmar que la tabla se creó correctamente, usa:

\d Estudiante

# 6. Insertar y consultar datos

Para insertar un nuevo estudiante:

INSERT INTO Estudiante (nombre, edad, correo)
VALUES ('Juan Pérez', 22, 'juanperez@gmail.com');

Para ver los datos almacenados:

SELECT * FROM Estudiante;

# 7. Salir y detener el contenedor

Para salir de PostgreSQL:

\q

Para detener el contenedor:

docker stop mi_postgres

Para iniciarlo nuevamente:

docker start mi_postgres

# Conclusión

Con estos pasos, ya tienes PostgreSQL corriendo en Docker con una base de datos funcional. Puedes modificar los datos, agregar más tablas y hacer consultas según sea necesario. 

# DevSec-Examen

### Paso 1: Crear carpeta del proyecto
Crear una nueva carpeta, por ejemplo llamada moodle-docker.

Entrar a la carpeta:

mkdir moodle-docker
cd moodle-docker

### Paso 2: Crear archivo docker-compose.yml
Dentro de la carpeta, crear un archivo llamado docker-compose.yml.

Agregar la configuración de servicios:

MariaDB como base de datos.

Moodle como aplicación web.

phpMyAdmin opcionalmente para administrar la base de datos.

Ejemplo de docker-compose.yml:

version: '3.7'

services:
  mariadb:
    image: mariadb:10.5
    restart: always
    container_name: moodle-db
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: moodle
      MYSQL_USER: moodleuser
      MYSQL_PASSWORD: moodlepassword
    volumes:
      - mariadb_data:/var/lib/mysql

  moodle:
    image: bitnami/moodle:latest
    restart: always
    container_name: moodle-app
    ports:
      - "8080:8080"
    environment:
      MOODLE_DATABASE_TYPE: mariadb
      MOODLE_DATABASE_HOST: mariadb
      MOODLE_DATABASE_PORT_NUMBER: 3306
      MOODLE_DATABASE_NAME: moodle
      MOODLE_DATABASE_USER: moodleuser
      MOODLE_DATABASE_PASSWORD: moodlepassword
    depends_on:
      - mariadb
    volumes:
      - moodle_data:/bitnami/moodle
      - moodledata_data:/bitnami/moodledata

volumes:
  mariadb_data:
  moodle_data:
  moodledata_data:
Paso 3: Levantar los contenedores
Ejecutar el comando:

docker-compose up -d
Verificar que los contenedores están corriendo:


docker ps
(Aquí seguro había una imagen del docker ps mostrando moodle y mariadb levantados.)

### Paso 4: Acceder a Moodle
Entrar a navegador y abrir:
http://localhost:8080

Deberías ver la pantalla de instalación de Moodle.

### Paso 5: Configurar Moodle
Seleccionar idioma (Español).

Continuar con la instalación.

Confirmar rutas y configuración de base de datos:

Tipo de base de datos: MariaDB

Host de base de datos: mariadb

Nombre de la base de datos: moodle

Usuario: moodleuser

Contraseña: moodlepassword

(Esto coincide con lo configurado en docker-compose.yml).

### Paso 6: Aceptar términos y continuar
Aceptar las licencias GPL de Moodle.

Confirmar que el sistema cumple con los requerimientos (PHP, extensiones, etc.).

### Paso 7: Crear administrador
Ingresar datos para el usuario administrador de Moodle:

Nombre, correo, contraseña segura, etc.

### Paso 8: Crear primer curso
Desde el panel de Moodle, crear un nuevo curso llamado, por ejemplo, "Curso 1".

### Paso 9: Agregar usuarios
Crear o registrar usuarios.

Asignar roles como profesor, estudiante, etc.

### Paso 10: Finalización
Moodle queda configurado y funcionando dentro de contenedores Docker.

Puedes gestionar Moodle desde tu navegador y administrar cursos, usuarios, etc.

# Instalación de Laravel con Docker

## Requisitos:

- **Docker** en su version mas reciente
- Base de datos **MySql 8.0**

## Pre-Instalación
- Dentro del archivo `.env` se encuentran dos variables a personalizar:
    - Variable para definir el tag del contenedor `TAG=PROD`
    - Variable para definir el puerto a usar `PORT=8000`
- Importar proyecto
    - Dentro de la carpeta `src` importar todos los archivos del proyecto
    - Modificar el archivo `src/.env`, ejemplo:
        - Nombre del proyecto: `APP_NAME=Laravel`
        - URL del proyecto: `APP_URL=www.google.com`
        - Mostrar errores (en producción, dejar en **false**): `APP_DEBUG=false`
        - Host de la base de datos: `DB_HOST=192.169.100.168`
        - Puerto de escucha de la base de datos: `DB_PORT=3306`
        - Nombre de la base de datos: `DB_DATABASE=laravel`
        - Usuario de la base de datos: `DB_USERNAME=root`
        - Contraseña de la base de datos: `DB_PASSWORD=123456`
> Nota: si el archivo no existe, copiar la información de `src/.env.example`

## Instalación

Construir la imagen del Proyecto
```sh
$ docker-compose build
```
Iniciar los contenedores
```sh
$ docker-compose up -d
```
> Nota: si el archivo no existe, copiar la información de `.env.example`

Instalar composer
```sh
$ docker-compose exec app composer install --ignore-platform-reqs
```
Generar key
```sh
$ docker-compose exec app php artisan key:generate
```
Generar Link para storage
```sh
$ docker-compose exec app php artisan storage:link
```
Configuración adicional
```sh
$ docker-compose exec app php artisan config:clear
$ docker-compose exec app php artisan cache:clear
$ docker-compose exec app php artisan view:clear
$ docker-compose exec app php artisan config:cache
```
> Nota: El propósito de estos comandos es limpiar cache

Instalar Node JS y compilar el proyecto a producción
```sh
$ docker-compose exec app npm install
$ docker-compose exec app npm run prod
```
> Nota: La versión de Node JS, es la versión LTS actual a la fecha de instalación

Dar permisos, **Fundamental**
```sh
$ docker-compose exec app chown -R www-data: /var/www/html
```
    
Ejecutar migración de la base de datos
```sh
$ docker-compose exec app php artisan migrate:fresh --seed
```
> Nota: En caso de requerir modificar credenciales dentro del archivo `src/.env`, solo se debe ejecutar, luego de aplicado los cambios, los comando contenidos en **Configuración adicional**
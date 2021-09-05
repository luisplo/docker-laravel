# Usando Docker con Laravel

## Detalles

- PHP 8
- Composer last version

## Instrucciones

> Nota: si la carpeta `laravel` no existe, crearla

- Dentro de la carpeta `laravel` importar el proyecto a usar, el proyecto ya debe estar compilado
- Dentro del archivo `.env`, cambiar la variable `TAG` por la versión de la imagen y `PORT` para el puerto que desea usar, ejemplo: `TAG=PROD`, el nombre de la imagen será: `laravel:PROD`
- Dentro de la carpeta `laravel` crear el archivo `.env` correspondiente a las variables usadas por laravel, allí  debe ir toda la informacion de credenciales

## Instalación

Los comandos a continuación son para inicializar los contenedores

```sh
docker-compose up -d
```

Inicializados los contenedores, continuar con la configuración del proyecto **Laravel**, el siguiente comando nos permite entrar al contenedor

```sh
docker-compose exec app /bin/bash
```

> Nota: si no se cuenta con un proyecto, usar `composer create-project laravel/laravel .` 

Dentro del contenedor

```sh
composer install
```

```sh
composer dump-autoload
```

```sh
php artisan key:generate
```

```sh
php artisan storage:link
```

```sh
php artisan config:cache
```

```sh
php artisan cache:clear
```

> Nota: si el proyecto es ejecuta en producción, usar la url configurada en el archivo `laravel/.env` seguido del puerto usado en el archivo `.env`

Verificar el despliegue en su navegador

```sh
127.0.0.1:8000
```

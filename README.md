# Laboratorio #3 - CRUD Laravel
**Alumno: Joseph Córdoba | Cédula: 8-1025-2381 | Grupo: 1GS131 | Profesora: Ingeniera Irina Fong**

<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

## Descripción
Este laboratorio tiene como objetivo practicar las bases del CRUD (Create, Read, Update y Delete) en el ambiente de Laravel.  

Se documenta el proceso completo de los comandos utilizados para la creacion de la base de datos hasta la ejecución final del sistema.

---

## Realización del Laboratorio
Como primer paso tenemos la ubicación del proyecto. Abrimos el CMD y lo ejecutamos como administrador y nos posicionamos sobre la siguiente carpeta:
```bash
cd C:\xampp\htdocs
```
En caso de tener una carpeta especifa donde se ubique el proyecto, debemos hacerlo de esta forma:
```bash
cd C:\xampp\htdocs\"Nombre de tu carpeta"
```
Luego de posicionarnos en la carpeta indicada corremos el siguiente comando:
```bash
laravel new Nombre_Archivo
```
Una vez configurado todo el nuevo archivo pasamos a verificar el archivo **.env** este de la siguiente manera:
```sql
APP_MAINTENANCE_DRIVER=file
# APP_MAINTENANCE_STORE=database

PHP_CLI_SERVER_WORKERS=4 <-- Importante eliminar el # que precede esta linea

BCRYPT_ROUNDS=12

LOG_CHANNEL=stack
LOG_STACK=single
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=crud_rapido
DB_USERNAME=root
DB_PASSWORD=
```
También se verifica que en el archivo **AppServiceProvider.php** ubicado en **app/Providers/AppServiceProvider.php** contengan las siguientes lines de codigo y agregarlas de ser necesario:
```javascript
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Support\Facades\Schema; <-- Agregar de no tenerla originalmente

class AppServiceProvider extends ServiceProvider
{
    /**
     * Register any application services.
     */
    public function register(): void
    {
        //
    }

    /**
     * Bootstrap any application services.
     */
    public function boot(): void
    {
        Schema::defaultStringLength(191); <-- Agregar de no tenerla originalmente
    }
}
```
Luego de toda esta verificación es hora de correr uno por uno los siguientes comandos en la terminal de nuestro Visual Studio Code, donde abrimos previamente nuestro nuevo archivo:
```bash
php artisan config:clear
php artisan cache:clear
php artisan config:cache
```
## Migraciones
Una vez completado los pasos anteriores ahora ejecutaremos el siguiente comando:
```bash
php artisan migrate
```
Una vez el sistema nos indica que todo esta correcto, pasamos a la creación de un Modelo junto con su migración:
```bash
php artisan make:model Product -m
```
Este comando nos genera lo siguiente:
- Modelo: app/Models/Product.php
- Migración: create_products_table

  
Y posteriormente ejecutamos la Migración:
```bash
php artisan migrate
```
Todo esto en conjunto nos genera la **Tabla Products.**
## Instalación del generador CRUD
Instalamos el paquete generador del CRUD con el siguiente comando:
```bash
composer require ibex/crud-generator --dev
```
Luego lo configuramos con el siguiente comando:
```bash
php artisan vendor:publish --tag=crud
```
Y ahora se le genera el CRUD a la tabla Products:
```bash
php artisan make:crud products
```
Durante la ejecución del comando se selecciona la opción de **Stack: Bootstrap.** Esto genera:
- Controlador (ProductController)
- Modelo (sobrescrito)
- Request (validaciones)
- Vistas (Blade)
- Layout base
## Configuración de rutas
Se agrega lo que haga falta en el archivo **web.php**, ubicado en: **routes/web.php**, lo siguiente:
```javascript
<?php

use Illuminate\Support\Facades\Route;
use Illuminate\Support\Facades\Auth;
use App\Http\Controllers\ProductController;

Route::get('/', function () {
    return view('welcome');
});

Auth::routes();

Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

Route::resource('products', ProductController::class);
Auth::routes();

Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');
```
Así habilitamos las funciones del CRUD:
- Crear
- Leer
- Actualizar
- Eliminar
## Ultimos Pasos
Ya habiendo realizado todo lo anterior, ahora actualizaremos las dependecias con el comando: 
```bash
composer dump-autoload
```
Instalamos la interfaz de usuario:
```bash
composer require laravel/ui --dev
```
Y luego creamos la interfaz con Bootstrap:
```bash
php artisan ui bootstrap
php artisan ui bootstrap --auth
```
Y finalmente instalamos las dependecias de Node.js:
```bash
npm install
```
Y levantamos el proyecto:
```bash
npm run build
```
## Resultados Finales

## Autor
Nombre: Joseph Córdoba
Grupo: 1GS131
Correo: josephcordoba2318@gmail.com
Correo Institucional: joseph.cordoba@utp.ac.pa
## Fecha de Ejecución
Miercoles 28 de Abril de 2026.

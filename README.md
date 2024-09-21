<hr />

<h1>Implementación Laravel 11 + Sail + Octane + Swoole + Supervisor</h1>
<h2>Instrucciones</h2>

#instalar octane
./vendor/bin/sail composer require laravel/octane

#iniciar octane | elegit swoole
./vendor/bin/sail artisan octane:install 


#en el archivo .env agregar al final

OCTANE_SERVER=swoole
OCTANE_HTTPS=false

#ejecutar 
./vendor/bin/sail artisan sail:publish




#en el archivo docker/8.3/supervisord.confd

[program:php]
#command=%(ENV_SUPERVISOR_PHP_COMMAND)s
command=/usr/bin/php -d variables_order=EGPCS /var/www/html/artisan octane:start --server=swoole --host=0.0.0.0 --port=8000 --watch

#ejecutar
./vendor/bin/sail npm install --save-dev chokidar

# en el archivo docker-compose.yml

ports:
            - '8080:80'
            - '${VITE_PORT:-5173}:${VITE_PORT:-5173}'
            - 8000:8000


#ejecutar 

./vendor/bin/sail down
./vendor/bin/sail build --no-cache
./vendor/bin/sail up -d
./vendor/bin/sail artisan octane:status


#referencias
https://www.youtube.com/watch?v=0KjyubRdtvA

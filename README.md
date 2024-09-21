<hr />

<h1>Implementación Laravel 11 + Sail + Octane + Swoole + Supervisor</h1>
<h2>Instrucciones</h2>



#instalar octane<br/>
./vendor/bin/sail composer require laravel/octane
<hr />
#iniciar octane | elegit swoole<br/>
./vendor/bin/sail artisan octane:install 
<hr />

#en el archivo .env agregar al final

OCTANE_SERVER=swoole<br/>
OCTANE_HTTPS=false

<hr/>

#ejecutar <br/>
./vendor/bin/sail artisan sail:publish

<hr/>


#en el archivo docker/8.3/supervisord.confd<br/>

[program:php]
#command=%(ENV_SUPERVISOR_PHP_COMMAND)s
command=/usr/bin/php -d variables_order=EGPCS /var/www/html/artisan octane:start --server=swoole --host=0.0.0.0 --port=8000 --watch
<hr />

#ejecutar<br/>
./vendor/bin/sail npm install --save-dev chokidar

# en el archivo docker-compose.yml <br/>

ports:
            - '8080:80'
            - '${VITE_PORT:-5173}:${VITE_PORT:-5173}'
            - 8000:8000

<hr/>
#ejecutar <br/> 

./vendor/bin/sail down <br/>
./vendor/bin/sail build --no-cache <br/>
./vendor/bin/sail up -d <br/>
./vendor/bin/sail artisan octane:status <br/>

<hr/>
#referencias <br/>
https://www.youtube.com/watch?v=0KjyubRdtvA
<br />
https://www.digitalocean.com/community/tutorials/how-to-allow-remote-access-to-mysql

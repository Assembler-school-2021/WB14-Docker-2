# WB14-Docker-2

> Pregunta 1 : ahora ya tienes toda la información para hacer el contenedor de docker. Deberás 
> - descomentar la parte wordpres_container
> - mapear la información necesaria en formato yaml
> - borrar el mapping de mysql al exterior.
> - crear una carpeta para la información de la base de datos.


docker-compose.yml (con fichero y con variables de entorno):
```
  version: '3.1'
	
	services:
	
        mysql_container:
	    image: mysql:5.7 
	#    ports:
	#      - 3306:3306
	    environment:
	      MYSQL_ROOT_PASSWORD: wordpress
	    volumes:
	      - dbdata
	
	  wordpress_containter:
	    image: wordpress
	    ports:
	      - 8080:80
	#    environment:
	#      - WORDPRESS_DB_HOST=mysql_container
	#      - WORDPRESS_DB_PASSWORD=wordpress
	#      - WORDPRESS_DB_USER=root
	    env_file:
	      - .env.wp
	    depends_on:
	      - mysql_container
	
	volumes:
	  dbdata:
```
.env.wp:
```
	WORDPRESS_DB_HOST=mysql_container
	WORDPRESS_DB_PASSWORD=wordpress
	WORDPRESS_DB_USER=root
```

> Pregunta 2 : Prueba a buildear esta config con otro tag. Después ejecuta el contenedor. Cuando termines inspecciona el tamaño de las imagenes. Cuanto tamaño hay de diferencia?

De 303Mb a 7.5Mb

## Swarm
```
docker swarm init --advertise-addr=95.217.218.168 --data-path-addr=95.217.218.168
Swarm initialized: current node (rvhoou99kgu617kscq3ev3ky0) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3s5znt5apj4cgx8pkcfqzt4k9u65s1eipugp4oiuu667lo2kr8-d37t8qunuvtb4vz0fdga559ci 95.217.218.168:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

> Pregunta 3: dirigete a la pestaña App templates. Verás que tiene plantillas de ejemplo, escoge wordpress y customízala. Crea un subdominio nuevo en cloudflare para este stack que apunte igual a la IP del master donde está traefik. En este punto debes tener todos los conocimientos necesarios para lanzar el stack y que funcione. Recuerda que traefik enruta usando labels.

> Pregunta 4 : cuando todo funcione, busca la forma de escalar los frontales de wordpress a 2 instancias y comprueba que repartes la carga.

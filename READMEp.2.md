## Docker compose con cliente
Para configurar un servidor junto a un cliente tendremos que añadir al codigo anterior de docker compose esta parte:

  cliente:
    container_name: asir_cliente
    image: alpine
    tty: true
    stdin_open: true
    networks:
      bind9_subnet1:
        ipv4_address: 172.28.5.2

Despues de levantar los dos contenedores y comprobar que los dos están enganchados en una misma red, abriremos una terminal en el contenedor del cliente para instalar las herramientas de bind.

## abrir terminal en el cliente

Como el cliente usa una imagen alpine, tendremos que usar el comando:
    $ docker exec -it [nombre.contenedor] sh
Cuando la tengamos abierta, usaremos este comando:
    $ apk add --no-cache bind-tools
Puede haber fallos a la hora de intalar las herramientas. Para solucioanarlo borraremos el apartado de dns del cliente y volveremos a lanzar los contenedores. Cuando volvamos a intentar descargar las bind-tools, ya nos dejará. Luego tendremos que configurar la red de forma manual, por lo que tendremos que lanzar este comando dentro de la terminal del cliente:
    $ echo "newserver 172.28.5.1" >> etc/resolv.conf

## abrir terminal en el servidor dns

Vamos a intalar ping en el servidor dns para comprobar su conexión con la red y con el cliente, por lo tanto abrimos una terminal.
    $docker exec -it [nombre.contenedor] bash
Lanzaremos los siguientes comandos, a parte de ping, también instalaremos las dnsutils
    $ apt update
    $ apt install -y dnsutils    
    $ apt-get install -y iputils-ping
Luego se comprueba con ping y con dig las conexiones y ya estaría hecho.

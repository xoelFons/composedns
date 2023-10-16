bind9: Nombre del servicio. En este caso, se refiere a un servidor DNS BIND9.

image: Especifica la imagen de Docker que se utilizará para crear el contenedor del servicio. En este caso, se está utilizando la imagen "internetsystemsconsortium/bind9:9.16", que es una imagen de BIND9 en la versión 9.16.

container_name: Define el nombre del contenedor creado a partir de esta imagen. En este caso, el nombre del contenedor se establece como "asir2_bind9".

restart: Indica que el contenedor debe reiniciarse automáticamente en caso de un fallo o cuando Docker se inicia. El valor "always" significa que Docker intentará reiniciar el contenedor siempre que sea necesario.

ports: Aquí se especifican los puertos que se deben mapear desde el contenedor al host. En este caso, el servicio BIND9 escuchará en el puerto 53 tanto para TCP como para UDP. Esto es típico para un servidor DNS.

networks: Define la red a la que pertenece este servicio. En este caso, el servicio se conecta a una red llamada "bind9_subnet_asir" con una dirección IPv4 específica de 172.28.5.1. Esta red parece ser una red personalizada definida en otro lugar del archivo Docker Compose.

volumes: Especifica los volúmenes de Docker que se montan en el contenedor. En este caso, se están montando dos volúmenes. El primero, ./conf, se monta en "/etc/bind" dentro del contenedor y se utiliza para configurar el servidor DNS BIND9. El segundo, ./lib, se monta en "/var/lib/bind" y se utiliza para almacenar datos persistentes.

environment: Define variables de entorno que se establecen en el contenedor. En este caso, se configura la zona horaria (TZ) del contenedor como "Europe/Paris". Esto establecerá la zona horaria del contenedor en la zona horaria de París.

networks: Fuera del servicio, se define la red llamada "bind9_subnet_asir" con la opción "external: true". Esto indica que la red se crea fuera de este archivo Docker Compose y se está utilizando como una red externa.

En resumen, este fragmento de Docker Compose define un servicio de servidor DNS BIND9 que se ejecuta en un contenedor Docker, con configuraciones específicas para los puertos, volúmenes, variables de entorno y redes. Además, se conecta a una red personalizada llamada "bind9_subnet_asir".

## Pruebas

Para poder hacer pruebas necesitamos instalar dig en el contenedor.

Nos metemos dentro del contenedor 
$ docker exec -it [nombre contenedor] bash
**Attach shell**

$ apt update
$ apt install -y dnsutils
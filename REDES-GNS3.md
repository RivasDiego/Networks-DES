# Configuración Inicial
PC
---
El *default Gateway* siempre se configura en las PC y es **igual** a la ip del router al que estan conectadas.
### Comando para definir la IP y el Gateway

        ip [LA DIRECCION IP] [LA DIRECCION GATEWAY]

Ejemplo (Utilizano una direccion subred 190.50.70.0):  

        ip 190.50.70.1 190.50.70.2

_Siempre guardar con el comando **save**_



Router
---
Para acceder a la terminal de configuracion se utiliza el comando

        configure terminal

        conf t

Desde aqui, se puede acceder a las interfaces para poder configurarlas con el comando

        interface [NOMBRE DE LA INTERFAZ] [NUMERO DE LA INTERFAZ]
Ejemplos:

        interface fastethernet 0/0
        interface gigabitEthernet 1/0

        int f0/0
        int g1/0

---

Con este comando se configura la ip del router, es necesario incluir la mascara 

        ip address [IP] [MASCARA]
Ejemplo:

        ip address 190.50.70.2 255.255.255.0
        ip address 10.10.10.1 255.0.0.0
        
        ip add 190.50.70.2 255.255.255.0
        ip add 10.10.10.1 255.0.0.0

---
Es necesario agrerar el siguiente comando para levantar la interfaz

        no shutdown

        no shut

Nos salimos de ambas terminales con ***end***. Y como buena practica, es recomendado guardar cada cambio despues de hacerlo con el comando ***wr***. También es posible saltar de una interfaz a otra dentro de la terminal.

En este momento, ya se pueden probar las conexiones directas. Usamos la terminal del dispositivo base e introducimos el siguiente comando:

        ping [IP DESTINO]
Por ejemplo, desde la terminal de una PC a un router:
        
        ping 190.50.70.2
Y desde la terminal de un router a la interfaz de otro:

        ping 10.10.10.2
Es recomendable probar las conexiones de los routers, para verificar que puedan enviar todos los paquetes antes de establecer las rutas.
# Configuracion de las rutas
## Rutas estaticas
Para este algoritmo de enrutamiento, es necesaria la configuracion manual en cada dispositivo, definiendo los destinos y las interfaces a utilizar.  

Se utiliza la direccion IP indentificadora de la red, la mascara y la interfaz por la cual se va a llegar a la IP de destino. El comando (desde la consola de configuracion del router) es el siguiente:

        ip route [DIRECCION IP DE RED] [MASCARA] [INTERFAZ DESTINO]
Por ejemplo;

        ip route 190.50.102.0 255.255.255.0 10.10.10.4

Podremos verificar todas las rutas establecidas con el comando

        do show ip route static
Para guardar y salir, se sigue la buena practica de ***end*** y ***wr***.

## RIP || Protocolo de Información de Encaminamiento (Routing Information Protocol)
Este algoritmo es configura las rutas de manera dinamica, lo que significa que la configuración es más sencilla y más rápida. Es de tipo vector distancia. Usaremos el siguiente comando para acceder a la terminal de configuración de las rutas rip del router (luego de acceder a la terminal de configuración general con *conf t*):

        router rip

Se tiene que especificar la version con la que trabajara el protocolo, con 

        version [VERSION]
        version 2       // Usaremos la version 2

Y ahora empezamos la configuracion, con el siguiente comando, daremos a conocer cuales son las redes propias del router que estamos configurando. Recordar que es importante usar siempre la direccion de red para esto, puesto que es la que representa todo el segmento:

        network [IP DE RED]

        network 190.50.70.0
        network 10.10.10.0

        net 190.50.70.0
        net 10.10.10.0

Se tienen que agregar todos los segmentos de red que esten conectados con el router que estamos configurando, esto significa que se añaden las conexiones entre routers.   

Ahora le indicamos al router que no queremos que exista una auto suma de rutas, sino que las deje como estan configuradas desde un inicio.

        no auto-summary

        no au

Por ultimo, configuramos la interfaz que determinaremos como pasiva. Estas interfaces son las que no van a cambiar, y siempre van a mantener la misma configuracion de la red o subred a la que estamos conectados. 

        passive-interface [INTERFAZ DEL ROUTER]
        
        passive-interface g3/0
        passive-interface f0/0
        
        pas g3/0
        pas f0/0



Despues de configurar esta ultima parte guardamos y salimos con ***end*** y ***wr***.  
En dado caso querramos confirmar las rutas rip configuradas (Luego de trabajar en al menos dos routers), accedemos a la terminal de configuracion y colocamos:
        
        do show ip route rip

## OSPF || Abrir el camino más corto primero (Open Shortest Path First)

Este protocolo, igual que el anterior, es dinamico, por lo que es mas sencillo de configurar. Ahora bien, a diferencia del protocolo RIP, este es de tipo link-state (O estado de enlace). Para que este tipo de protocolo, los router envian un paquete "Hello" cada cierto tiempo (Que puede ser determinado por el usuario) para revisar el estado de todos los enlaces. Este protocolo también establece un DR (Designated Router) que es el encargado de manejar la tabla de direcciones de area y un BDR (Backup Designated Router) que es quien toma el rol del DR si este llega a fallar.

Antes de empezar con los comandos, es necesario entender el concepto de *Wildcard Mask*. Esta mascara es un identificador de la parte de red con la que se esta trabajando e indica al router el rango de la red que se va a utilizar en la tabla de direcciones en la tabla de enrutamiento. Para esto, **utilizamos el octeto 255.255.255.255 y le restamos la mascara o submascara** respectivamente. 

        Wilcard con clases

        255.255.255.255 -
        255.255.255. 0  =    //Clase C
        _________________
         0 . 0 . 0 .255      // Esta es una wildcard de la clase C

        Wilcard con VLSM
        
        255.255.255.255 -
        255.255.248. 0  =    // Mascara variable
        _________________
         0 . 0 . 7 .255      // WILDCARD

Manejando el concepto, podemos empezar con las configuraciones. Al igual que rip, accedemos a la configuracion especifica del protocolo

        router ospf 1
A cada router, se le asigna un id de router que se utilizara cuando se requiera informacion sobre el. Estos id siguen la nomenclatura *n.n.n.n*.
        
        router-id [n.n.n.n]

        router-id 1.1.1.1
        router-id 2.2.2.2  // OJO -> NO ES UNA IP

Luego de asignar el id, procedemos a agregar las redes a las que el router esta conectado, como hicimos con RIP, pero ahora añadimos la wildcard de la red y un campo extra que es el area, que se puede definir el area como el grupo de trabajo al que pertenece el router. Esto nos permite establecer diferentes grupos de trabajo, facilitando y amplificando la organizacion del mismo.

        network [IP DE RED] [WILDCARD] area [AREA]

        network 190.50.70.0 0.0.0.255 area 0
        network 10.10.10.0 255.255.255.0 area 0

        net 190.50.70.0 0.0.0.255 area 0
        net 10.10.10.0 255.255.255.0 area 0

Siempre recordar salir y guardar con ***end*** y ***wr*** despues de terminal toda la configuracion.  
Para revisar todas las conexiones, utilizamos

        show ip ospf neighbor
        show ip ospf neighbor database // Para ver la tabla de direcciones en ese router

## NAT || Traducción de direcciones de red (Network Address Translation)

Es un mecanismo utilizado por routers IP para cambiar paquetes entre dos redes que asignan mutuamente direcciones incompatibles. Consiste en convertir, en tiempo real, las direcciones utilizadas en los paquetes transportados. Exites tres tipos, estaticos, dinamicos y de sobrecarga.  

La estatica es que a una direccion interna, privada, le asignamos una direccion publica. Las dinamicas es en las que tenemos direcciones tanto privadas como publicas y hacemos que las rutas publicas trabajen con privadas y las privadas con publicas si es necesario. Por ultimo tenemos la de sobrecarga, que es directamente poder tener muchas direcciones privadas en una red interna, y solo una direccion publica.

![](https://i.imgur.com/fXk9B0k.png)

![](https://i.imgur.com/SmYEGYT.png)

Utilizaremos un nuevo componente del GNS3, el que esta indicado como NAT.   

Accedemos a la configuracion del router que queremos establecer como traductor, accedemos a la interfaz conectada a la NAT y asignamos una ip. Esta IP viene dada por el DHCP.

        config t

        ip add dhcp

        no shut

Ahora  configuramos de la interfaz conectada a la subred y en la configuracion general establecemos el pool de direcciones

        service dhcp

        ip dhcp pool [NOMBRE]

Luego se agrega la subnet

        network [IP] [MASCARA]

        network 192.60.24.0 255.255.255.0
        net 192.60.24.0 255.255.255.0

Se establece una ip fija

        default-router [IP]

        default-router 192.60.24.1

Y se espedifica el servidor dns, usualmente usamos el *8.8.8.8*, pero si existe un DNS interno, ese es el que se utiliza

        dns-server [Default DNS serever]

        dns-server 8.8.8.8

Cuando se tengan multiples subredes por las cuales el router puede establecer una conexion, es necesario establecer la interfaz de salida (La que se conecta directamente con NAT) y las de entrada (Las interfaces de las subredes). Esto se hace en la configuracion de cada interfaz en especifico

        ip nat outside    // Para la de salida

        ip nat inside     // Para las de entrada

Tambien es necesario declarar las listas de acceso, cual es el rango de ip con las que podremos salir y con cuales no. Para esto, desde la configuracion general del router, escribimos

        access-list [LISTA] permit ip [IP DE SUBRED] [WILDCARD] any

        access-list 100 permit ip [190.50.70.0 0.0.0.255 any

Y configuramos la sobrecarga del NAT

        ip nat inside source list [LISTA] interface [INTERFAZ DE SALIDA] overload

        ip nat inside source list 100 interface g1/0 overload

Salimos y guardamos. Para comprobar si todo funciona, vamos a las PC. Y estas deberian ser capaces de establecer una IP sin asignarselas estaticas. Lo hacemos con el comando

        ip dhcp

Y hacemos ping al servidor del dns o internet.

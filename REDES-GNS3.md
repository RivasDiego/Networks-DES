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
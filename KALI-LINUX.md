# Comandos en KALI-LINUX

## Ping - Send ICMP ECHO_REQUEST to network hosts

    ping    [ -LRUbdfnqrvVaAB]  destination
            [ -c count] 
            [ -i interval] 
            [ -l preload] 
            [ -p pattern] 
            [ -s packetsize] 
            [ -t ttl] 
            [ -w deadline] 
            [ -F flowlabel] 
            [ -I interface] 
            [ -M hint] 
            [ -Q tos] 
            [ -S sndbuf] 
            [ -T timestamp option] 
            [ -W timeout] 
            [ hop ...] 
El protocolo de mensajes de control de Internet (Internet Control Message Protocol, ICMP) es parte del conjunto de protocolos IP. Es utilizado para enviar mensajes de error e información operativa indicando, por ejemplo, que un host no puede ser localizado o que un servicio que se ha solicitado no está disponible.

**ping** utiliza un ECHO_REQUEST obligatorio del protocolo ICMP que envia a un host o a un gateway para obtener una respuesta. Es posible identificar un host con una direccion DNS, para así poder obtener una dirección IPV4 explícita de dicho host.

## Nmap - Network exploration tool and security / port scanner
**Nmap** ("Network Mapper") es una herramienta gratis de código abierto utilizada en descubriimiento de redes y auditorias de seguridad.  

Muchos sistemas y administradores de red también la encuentran útil para tareas como un inventario de red, manejar actualizaciones calendarizadas de servicios y monitorear hosts o el tiempo que un servicio lleva encendido.   

Al ejecutarse sobre una direccion IP que actua como host, **nmap** revela los puertos que estan abiertos, junto con los protocolos utilizados en dichos puertos.

    nmap    [Scan Type...]  {target specification} 
            [Options] 

## Wireshark
## Hydra
## John

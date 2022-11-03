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

    TARGET SPECIFICATION:
        -iL <inputfilename>: Input from list of hosts/networks
        -iR <num hosts>: Choose random targets
        --exclude <host1[,host2][,host3],...>: Exclude hosts/networks
        --excludefile <exclude_file>: Exclude list from file
    HOST DISCOVERY:
        -sL: List Scan - simply list targets to scan
        -sn: Ping Scan - disable port scan
    PORT SPECIFICATION AND SCAN ORDER:
        -sU: UDP Scan
        -sN/sF/sX: TCP Null, FIN, and Xmas scans
        -p <port ranges>: Only scan specified ports
            Ex: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
    SERVICE/VERSION DETECTION:
        -sV: Probe open ports to determine service/version info
        --version-intensity <level>: Set from 0 (light) to 9 (try all probes)
        --version-light: Limit to most likely probes (intensity 2)
        --version-all: Try every single probe (intensity 9)
        --version-trace: Show detailed version scan activity (for debugging)
    OS DETECTION:
        -O: Enable OS detection
    OUTPUT:
        -v: Increase verbosity level (use -vv or more for greater effect)
        -d: Increase debugging level (use -dd or more for greater effect)
        --reason: Display the reason a port is in a particular state
        --open: Only show open (or possibly open) ports

## Spiderfoot
## Wireshark
## Hydra
## John

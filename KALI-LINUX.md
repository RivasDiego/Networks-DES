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
La inteligencia de fuentes abiertas (open-source intelligence, o su acrónimo OSINT) es una metodología multifactorial de recolección, análisis y toma de decisiones sobre datos de fuentes disponibles de forma pública para ser utilizados en un contexto de inteligencia. En este tipo de investigación se utilizan fuentes públicas para la obtención de datos.

**Spiderfoot** es una colección de herramientas que optimizan la búsqueda de información en las fuentes públicas de internet. Se puede acceder desde la línea de comandos con
        
    spiderfoot 
        options:
            -h, --help            show this help message and exit
            -d, --debug           Enable debug output.
            -l IP:port            IP and port to listen on.
            -m mod1,mod2,...      Modules to enable.
            -M, --modules         List available modules.
            -C scanID, --correlate scanID
                                  Run correlation rules against a scan ID.
            -s TARGET             Target for the scan.
            -t type1,type2,...    Event types to collect (modules selected
                                  automatically).
            -u {all,footprint,investigate,passive}
                                  Select modules automatically by use case
            -T, --types           List available event types.
            -o {tab,csv,json}     Output format. Tab is default.
            -H                    Don't print field headers, just data.
            -n                    Strip newlines from data.
            -r                    Include the source data field in tab/csv output.
            -S LENGTH             Maximum data length to display. By default, all
                                  data is shown.
            -D DELIMITER          Delimiter to use for CSV output. Default is ,.
            -f                    Filter out other event types that weren't requested
                                  with -t.
            -F type1,type2,...    Show only a set of event types, comma-separated.
            -x                    STRICT MODE. Will only enable modules that can
                                  directly consume your target, and if -t was
                                  specified only those events will be consumed by
                                  modules. This overrides -t and -m options.
            -q                    Disable logging. This will also hide errors!
            -V, --version         Display the version of SpiderFoot and exit.
            -max-threads MAX_THREADS
                                  Max number of modules to run concurrently.

La opción **_-l_** es requerida para establecer un puerto inicial en donde las herramientas serán utilizadas. Pero también cuenta con una interfaz gráfica que se puede acceder desde el puerto en inicial.

## Wireshark
## Hydra
## John

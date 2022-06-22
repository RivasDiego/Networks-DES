# Comandos para la máquina virtual de Ubuntu

Comandos para escribir/leer archivos
---

        cat [archivo] // Lee el archivo

        cat > [archivo] // Crea el archivo y guarda el texto en él

        echo '{string}' > [archivo]   // Escribir
        echo [archivo]                // Leer

        touch [archivo]                     // Solo creación de archivos
        touch [archivo] [archivo] [archivo]

        > [archivo]  // Crear archivo 

        more [archivo]   //Leer archivo

        ls              // Lista los archivos

        nano [archivo]
        vimo [archivo]      //Ambos son editores de texto dentro de la terminal

Comandos de administración: 
---
        
        cd [ruta]                           // Cambiar de directorio
        mv [archivo] [ruta o archivo]       // Mover archivo a la ruta
        cp [archivo] [ruta o archivo]       // Copiar archivo a la ruta
        rm [archivo]                        // Eliminar archivo
        ps          // visualizar el estado de un proceso
        top         // ver las tareas del sistema que se ejecutan en tiempo real.
        kill        // Terminar un proceso específico
Modificar permisos
---

        chmod [tipo de permiso]  [Archivo carpeta]

| Número | Tipo de permiso  |
|:-------------------:|---|
| 0 | Sin Permisos| 
| 1 | Ejecución| 
| 2 | Escritura| 
| 3 | Lectura y escritura| 
| 4 | Lectura| 
| 5 | Lectura y ejecución| 
| 6 | Lectura y escritura| 
| 7 | Lectura, escritura y ejecución| 

Se juntan el tipo de permiso que le queremos dar al tipo de usuario:

| Propietario | Usuario Admin | Demas Usuarios | Descripción |
| :---: | :---: | :---: | ---|
| X   |  X  |  X  |     
| 7   |  7  |  7  | Permiso total para todos los usuarios |
|7|5|5| Propietario tiene permiso total, pero admin y los demas solo pueden Leer y ejecutar  |

Comandos para instalaciones
---
        
        sudo apt install [paquete] // Instalar la aplicacion/paquete especificado
        sudo apt update // Actualizar los paquetes del sistema


Otros comandos 
---

        date        // Fecha
        cal         // Muestra calendario (Necesita instalarse)
        uptime      // información sobre el tiempo que una máquina o servidor lleva activo
        w           // uptime con más info
        whoami      // Nombre asociado al usuario
        uname -a    // información del sistema operativo
        man [comando]                  // Manual de comando
        tar                            // Comando para archivos comprimidos
        sudo                           // Permisos de admin (Usar al principio del comando)
        pwd                            // muestra la ruta absoluta del directorio en el que se encuentra
        grep -i [palabra] [archivo]    // buscar una palabra en un archivo de texto 
        history                        // Historial de comandos
        find . -name [nombre]          // Buscar los archivos con el nombre especificado


        ***RUTAS***
        /proc/cpuinfo    // Información del procesador
        /proc/meminfo    // Información de memoria

Comandos de inicio y apagado
---

        Halt: Detiene todos los procesos y apaga el equipo.
        Shutdown –r [minutes]  // número de minutos en el que se reiniciará el equipo.
        shutdown –h now        // apaga el equipo saltándose la espera programada.
        shutdown –r now        // reinicia el equipo saltándose la espera programada



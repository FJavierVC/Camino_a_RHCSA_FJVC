# Herramientas Escenciales de gestion de archivos
Linux es un sistema operativo orientado a archivos, lo cual implica que para su gestion, la actividad del administrador del sistema puede ser rastrada.
En este capitulo se abordaran habilidades para la gestion de archivos. Como estan organizados los file system y como trabajar con archivos y directorios.

## Trabajando con la jerarquia de los File system
La mayoria de las distros de linux cuentan con directorios default. Saber manejarlos es indispensable para ser un Sysadmin.
El capitulo hablara de como usarlos y entender su jerarquia.

### Filesstem Hierarchy Standar FHS
Define la disposición de los file system de linux, puede ser consultada en `man 7 file-hierarchy`. Muestra los file systems mas significanes.

### Directorios importantes

- `/` Directorio del root.
- `/boot` Contiene todas los archivos y directorios que son necesarios para que bootee linux
- `/dev` Contiene **Device files** que se utilizan para acceder a discos fisicos. Necesario durante el booteo.
- `/etc` Contiene archivos de configuracion que el sistema utiliza para que programas y servicios funcionen.
- `/home` Directorios personales del usuario local
- `/media, /mnt` Contiene directorios que se utilizan para montar dispositivos en el **file systems tree**.
- `/opt` Se utiliza para paquetes opcionales
- `/proc` Utilizada por el file system proc. Es una estructura que da acceso a la informacion del kernel.
- `/root` Indica el directorio Home del usuario **root**
- `/run` Incluye procesos e informacion especifica de usuarios desde la ultima vez que se booteo
- `/srv` Se usa para datos por servicios como NFS, FTP y HTTP
- `/sys` Usado como una interfaz  para diferentes dispositivos de hardware que son gestionados por el kernel de linux y procesos asociados.
- `/tmp` Contiene archivos temporales que seran eliminados sin algun warning durante el boot.
- `/var` Incluye archivos que pueden ser cambiados en tamaño dinamicamente, tales como log files, correos y spool files

### Mounts
Para comprender la organizacion de los file systems de linux, es indispensable entender el concepto de montaje. Un **"mount"** es una conexión entre un dispositovo y un directorio. 
Un file system de linux esta presentado por una jerarquia, con el **root directory** como el punto de inicio.

Cuando se realiza el proceso de montage, un dispositivo queda ligado a un directorio, de esta forma, posdterior a un montaje exitoso el mismo directorio da acceso al contenido del dispositivo.

Hacer el montaje de dispositos es lo que hace a linux un sistema flexible. hacer el montage en un solo dispositivo trae muchos problemas, seguir esta practica lleva consigo ventajas como:

- Permite que actividades que se llevan a cabo en otras areas del sistema corran libremente.
- Permite distinguir entre diversas areas del sistema, aislando servicios y configuraciones de seguridad.
- Permite crear de manera dinamica almacenamiento adicional, si se llena un dispositivo con file systems que almacena todo, impide esta actividad.

Se puede organizar los file systems en diversos dispositivos, tal como una particion y volumenes logicos. Para configurar un dispositivo como un montage dedicado, se necesita ser capaz de usar ciertas opciones de montage especificas. Algunos directorios son montados comunmente en dispositivos dedicados como pueden ser:

- `/boot` Este directorio normalmente esta en un dispositivo separado, debido a que requiere informacion escencial de la computadora para bootear. De esta forma, el directorio root `/` usualmente esta en un LVM Logical Volume Manager, del cual Linux no puede bootear de manera predeterminada. El kernel y archivos asociados necesitan estar alojados de manera independiente en un dispositivo /boot dedicado.
- `/boot/EFI` Si el sistema utiliza Extensible Firmwre Interface (EFI) para bootear, necesita un dispositivo dedicado de montage, dando acceso a todos los archivos requeridos en una etapa temprana del proceso de booteo. 
- `/var` Este directorio esta alojado en un dispositivo dedicado debido a su crecimiento acelerado y dinamico. Cada log file esta escrito en `/var/log`, manejandolo de manera separada puedes asegurarte de que no llene el espacio de tu servidor.
- `/home` Este se maneja en un dispositivo dedicado debido a razones de seguridad.
<<<<<<< HEAD
- `/usr` este directorio solo contiene archivos del sistema operativo, normalmente usuarios estandar no necesitan tener acceso a este directorio, debido a esto debe estar en un dispositivo dedicado.
=======




Algunos servidores manejar directorios que estan montados en particiones dedicadas u otros volumenes. Es a criterio del aministrador la forma en que se van a montar los directorios.

Para tener una vista general de todos los puntos de montaje podemos utilizar el comando **`mount`** el cual funciona para dar la informaicion alojada en `/proc/mounts` donde el kernel mantiene los datos de los puntos de montaje actuales. Además, muestra las interfaces del kernel.

- `df -Th` Este comando fue diseñado para mostrar el espacio libre que queda en cada dispositivo montado, incluye la mayotria de los sistemas.
- `findmnt` muestra los montajes y su relacion con otros existentes. El comando `mount` puede ser un tanto abrumador debido a su salida, es por eso que usamos este.

>>>>>>> a227631da79ae34bb737b84021347f5fccdf7a44

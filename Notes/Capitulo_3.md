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
- `/usr` este directorio solo contiene archivos del sistema operativo, normalmente usuarios estandar no necesitan tener acceso a este directorio, debido a esto debe estar en un dispositivo dedicado.



Algunos servidores manejar directorios que estan montados en particiones dedicadas u otros volumenes. Es a criterio del aministrador la forma en que se van a montar los directorios.

Para tener una vista general de todos los puntos de montaje podemos utilizar el comando **`mount`** el cual funciona para dar la informaicion alojada en `/proc/mounts` donde el kernel mantiene los datos de los puntos de montaje actuales. Además, muestra las interfaces del kernel.

- `df -Th` Este comando fue diseñado para mostrar el espacio libre que queda en cada dispositivo montado, incluye la mayotria de los sistemas.
- `findmnt` muestra los montajes y su relacion con otros existentes. El comando `mount` puede ser un tanto abrumador debido a su salida, es por eso que usamos este.

cuando utilizamos el comando `df -hT` obtendemos un output como este
```
student@localhost:~$ df -hT
Filesystem            Type      Size  Used Avail Use% Mounted on
/dev/mapper/rhel-root xfs        38G  5.7G   32G  16% /
devtmpfs              devtmpfs  4.0M     0  4.0M   0% /dev
tmpfs                 tmpfs     1.8G   84K  1.8G   1% /dev/shm
tmpfs                 tmpfs     705M   12M  694M   2% /run
tmpfs                 tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
/dev/mapper/rhel-home xfs        19G  407M   18G   3% /home
/dev/sda2             xfs       959M  331M  629M  35% /boot
tmpfs                 tmpfs     353M  132K  353M   1% /run/user/1000
/dev/sr0              iso9660   817M  817M     0 100% /run/media/student/RHEL-10-0-BaseOS-x86_64

```

Podemos visualizar que nos arroja 7 columnas con informacion de interes.

- **Filesystem**
Muestra el nombre del archivo del dispositivo que interactua con el disco del dispositvo usado. El dispositivo real dentro de la salida comienzan con /dev. Tambien se pueden observar dispositivos tmpfs, son dispostivos de kernel que son usados para crear archivos del sistema temporales en RAM.
- **Type**
El tipo de filesystem que se creo para montar el dispositivo
- **Size**
El tamaño del dispositivo montado
- **Used**
La cantidad de espacio en disco que el dispositivo tiene en uso
- **Avail**
La cantidad de espacio en disco que esta libre
- **Use%**
El porcentage de espacio libre
- **Mounted on**
El directorio en donde actualmente esta montado el dispositivo

Nota importante, la informacion desplecada con el comando reporta el tamaño en kibibytes, si usamos la opcion `-m` veremos que la informacion de desplega en mebibytes y usando `-h` nos da informacion legible para los humanos en formato Jib, MiB, GiB, TiB, o PiB/

## Manejo de archivos

Algunas de las tareas que tiene que realizar un administrador de sistemas linux son:
- Trabajar con wildcards
- Manejar y trabajar con directorios
- Trabajar con rutas relativas y absolutas
- Escuchar archivos y directorios
- Copiar archivos y directorios
- Mover archivos y directorios
- Eliminar archivos y directorios

Ahora veremos como realizar estas acciones:

### Trabajar con wildcards
Trabajar con wildcars hace la vida del administrador mas sencilla, se trata de una caracteriztica de shell que te permite referirte a multiples archivos de una manera mas facil.

`*` Referencia a un ilimitado numero de caracteres. por ejemplo `ls *`, muestra todos los archivos en el directorio actual, menos los que cuentan con un nombre que comience con un punto (`.`).
`?` Se usa para referirse a un caracter especifico, que puede ser cualquier caracter. `ls c?t`  en este ejemplo podria referise tanto a `cat` como a `cut`.
`[auo]` Refiere a un caracter que deberia ser seleccionado de un rango que esta especificado entre corchetes. `ls c[auo]t` de esta forma podrian acer match `cat`,`cau` y `cot` 

### Manejar y trabajar con directorios
Para utilizar linux, utilizamos directorios que en ocasiones tambien llamamos folders. Es indispensable saber moverse entre ellos, para darle una estructura de jerarquía.
#### Rutas Relativas y Absolutas
Las **rutas absolutas** son rutas completas que hacen referencia a un archivo o directorio con el que se desea trabajar. Dicha ruta **path** inicia con la carpeta "root", seguida de todos los subdirectorios hasta llegar al archivo o carpeta. No importa en que parte se ejecute, los nombres de archivo absolutos o rutas absolutas siempre van a funcionar.
Un ejemplo de un "absulute filename" es `/home/lisa/file1`.

Las **rutas relativas** se ejecutan en el directorio actual en el que estemos parados, tal como lo muestra el comando `pwd`.

Ejemplo de comandos con rutas relativas y absolutas
- `-cp /home/lisa/file1 /home/lara` Como usa rutas absolutas, funcionara siempre, ejecutandolo donde sea que estemos parados.
- `cp lisa/file1 lara` Asumiento de nuestro directorio actual es **/home** al ejecutar este comando podemos ejecutarlo sin referenciar al directorio padre `/home`, debido a que tanto el archivo fuente como el destino se referencian como ruta relativa. Sin embargo, es un riesgo hacerlo así, pues si no existe el directorio **/lara**, el comando `cp` creara un archivo llamado **lara**.
Para asegurarnos que cree el archivo dentro del directorio y si no existe nos mande el STDERR usariamos el comando `cp lisa/dile1 lara/`.
- Imaginemos que estamos en **home/lisa**, podemos usar `cp file1 ../lara`, vemos que en este ejemplo el destino tiene "**..**" lo cual le da la indicacion de escalar a un directorio padre antes de crear el archivo.


Nota, al igual que con los comandos, podemos usar la tecla TAB para autocompletar los filename de los path, y así ahorrar tiempo de escritura o de busqueda.

### Listar Archivos y Directorios
Cuando trabajamos con directorios dentro de linux, es importante saber listarlos y su contenido, para eso podemos usar el comando `ls`. Si se usa sin argumentos, simplemente nos listara los archivos o directorios que se encuentran dentro de la ruta en la que estamos parados.
El comando `ls` puede combinarse con multiples argumentos para obtener salidas interesantes, segun nuestras necesidades.

- `ls -l` Lista el contenido del directorio actual, incluyendo la informacion de cada uno, como la fecha de creacion y los permisos.
- `ls -a` Lista todo el contenido del directorio, incluyendo aquellos que estan ocultos (Aquellos que comience con `.`)
- `ls lrt` la opcion **t** ordena los archivos segun su fecha de creacion o modificacion. La opcion **r** pondra al top de la lista el mas reciente.
- `ls -d` Muestra los nombres de los directorios que coincidan con el wildcard que usemos en combinacion.
- `ls -R` Muestra el contenido del directorio actual, asi como el contenido de los subdirectorios.


### Copiar archivos y directorios
El copiado se realiza con el comando `cp`, para copiar algun archivo simplemente tenemos que seguir esta logica: `cp /<path_archivo_original> /<path_archivo_destino>`.
Tambien podemos copiar el contenido de un directorio completo, con subdirectorios incluidos, para ello, tenemos que usar el argumento `-R`
Al utilizar el argumento `-a`, copiaremos los archivos y directorios respetando los privilegios que ya tenia configurado previamente, asi como todas sus otras propiedades.
Cuando queremos tratar con archivos ocultos, el comando cp necesita ser configurado o bien, a;adir informacion extra.

- `cp /directorio/.* /tmp` Este comando movera todo aquello que comience con un punto al directorio /tmp.

- `cp -a /directorio/ .` Este comando copia el directorio completo incluyendo su contenido al directorio actual en el que estamos.

- `cp -a /somedir> . .` copia los arcivos, regulares y ocultos al directorio acual

### Moviendo directorios y archivos
Para mover archivos de un path a otro, usaremos el comando `mv` el cuae remueve el archivo de su directorio actual y lo pegara en el nuevo. Tambien podemos usar este comando para renombrar archivos o directorios.
Ejemplo:
`mv myfile /tmp` Este comando movera el archivo myfile que se aloja en el directorio actual al directorio /tmp.

`mkdir somefiles; mv somefiles /tmp` Este comando sirve para crear un directorio y posteriormente moverlo a una ruta especificada. Funcionaria incluso si el directorio cuenta con archivos.

`mv myfile mynewfile` Asi podemos usar el comando **mv** para renombrar un archivo.

### Borrando Archivos y Directorios
Para borrar archivos y directorios usamos el comando `rm`. Se puede utilizar en archivos simples, si queremos eliminar un directorio que contiene archivos dentro, debemos usar el argumento **-r**.

`Nota, dentro de RHEL al utilizar el comando **rm** saldra una leyenda que nos pide ejecutar el comando con privilegios root, esto es debido a que esta definido como un alias **rm -i**, siempre se puede cambiar esta configuracion usando la opcion **-f** o removiendo el alias del directorio **/root/.bashrc**.`

### Usando Enlances
Los enlaces en linux funcionan como los alias, sin embargo, en este caso estan casados a un archivo. Hay links simbolicos y hard links. Para entenderlos es necesario conocer como los file system de linux usa los **inodos** para los sistemas de administrador (file system administration).

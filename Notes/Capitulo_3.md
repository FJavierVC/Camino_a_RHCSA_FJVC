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
- `dev` Contiene **Device files** que se utilizan para acceder a discos fisicos. Necesario durante el booteo.
- `etc` Contiene archivos de configuracion que el sistema utiliza para que programas y servicios funcionen.
- `home` Directorios personales del usuario local
- `media, /mnt` Contiene directorios que se utilizan para montar dispositivos en el **file systems tree**.
- `opt` Se utiliza para paquetes opcionales
- `proc`  
# Fundamentos Básicos de Linux
## Variables de Entorno
Al trabajar en linux, podemos crear nuestro propio ambiente de desarrollo a modo de que este fuencione justo de la manera en que nosotros necesitamos. 
El ambiente consiste en variables que pueden ser definidas por el usuario, como por ejemplo **$PATH**.
Exiten muchas otras variables, tales como **$LANG** **$SHELL** **$SESSION_MANAGER** etc.
Dichas variables varian en el valor de las mismas, segun las necesidades de cada usuario y la ventaja de trabajar con variables para scripts y programas es que el programa solo se preocupa de usar el nombre de la variable, sin prestar real interes en el contenido, pues como dijimos antes, este va a diferir.

Si precionamos en comando **env** en nuestra terminal, seremos capaces de observar las variables que estan seteadas en nuestro entorno en este preciso momento.

`student@localhost:/etc$ env`

Para definir una variable, solo es necesario escribir el nombre que llevara, seguida de un signo de igual "=" y el valor que le vamos a asignar:

`MAIL=/var/spool/mail/student`

y para leer el contenido de una variable, es suficiente con hacerlo con un **echo**:

`student@localhost:/etc$ echo $PATH
/home/student/.local/bin:/home/student/bin:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin`

## Reconociendo la configuracion de los archivos de entorno

Cuando un usuario se loggea, un entorno es creado de manera automatica. Condifuracion que esta seteada en los siguientes archivos de configuracion:

`/etc/profile` Es el archivo generico que es procesado cuando cualquier usuario inicia sesion

`/etc/bashrc`  Se procesa cuando se inicia una subshell

`~/.bash_profile` En este archivo, se pueden definir las variables para el inicio de sesion de un usuario especifico

`~/.bashrc` En este se pueden definir las variables de subshell para un usuario especifico.

### Diferencia entre Login shell y subshell

Un login shell es la shell que se inicia cuando entras formalmente al sistema como usuario.
Un subshell es una shell hija que nace dentro de otra shell que ya estaba abierta.

La diferencia importante no es solo “otra terminal”, sino cómo fue iniciada y qué configuración carga.



## Buscando ayuda
Al momento de querer utilizar los comandos de cualquier distribucion, nos daremos cuenta de que existen cientos de ellos con diversas variantes, atributos y opciones. Es aquí cuando el comando **man** aparece, pues se convierte en el mejor recurso para obtener ayuda sobre sintaxis y el uso de comandos.
Además de permitir desplegar una lista corta de comandos usando **command --help**.

### Help
La forma mas rápida de aprender a usar el atributo **--help**. No solo se desplegara un resumen del comando, sino tambien las opciones que se pueden agregar. Hay que tomar en cuenta que no existe una manera estricta de usar los atributos, pueden ser usados en el orden que se desee.

### Usando man
Las paginas de man describen de manera exacta como usar un comando. Algunas de las claves esenciales para usar **man** son:
**Note** >> La parte mas importante de una pagina del manual es la final, en ella se encuentran dos importantes secciones, ejemplos y la seccion "See Also"

- **G** para moverte al final de la pagina lo mas rapido posible
- **/example** para buscar la pagina del manual donde se muestren ejemplos de uso del comando

#### Encontrando la pagina correcta del manual
**apropos** o **man -k** son utiles para encontrar informacion especifica en las paginas del manual.
Para usarlo de manera correcta, usaremos  **man -k** seguido de la palabra que estamos buscando en la base de datos del manual.

En ocasiones, al usar este comando, encontraremos demasiada información, podemos ser más especificos, agregando filtros con el comando **grep**, teniendo en mente que que realmente conocemos lo que estamos buscando.

Las paginas **man** estan categorizadas de la siguiente forma:
- Programas ejecutables o comandos shell
- Convenciones y formatos de archivos 
- Comandos para administracion del sistema

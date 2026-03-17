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

`/etc/profile`
`/etc/bashrc`
`~/.bash_profile`
`~/.bashrc`

# 🐧 Fundamentos Básicos de Linux

---

## 🌎 Variables de Entorno

Al trabajar en Linux, podemos crear nuestro propio ambiente de desarrollo de modo que funcione justo de la manera en que nosotros necesitamos.

El entorno consiste en variables que pueden ser definidas por el usuario, como por ejemplo **`$PATH`**.

Existen muchas otras variables, tales como **`$LANG`**, **`$SHELL`**, **`$SESSION_MANAGER`**, etc.

Dichas variables cambian en su valor según las necesidades de cada usuario, y la ventaja de trabajar con variables en scripts y programas es que estos solo se preocupan por usar el nombre de la variable, sin prestar demasiado interés en su contenido, ya que, como dijimos antes, este puede diferir entre usuarios o sistemas.

Si ejecutamos el comando **`env`** en nuestra terminal, seremos capaces de observar las variables que están seteadas en nuestro entorno en ese preciso momento.

```bash
student@localhost:/etc$ env
```

Para definir una variable, solo es necesario escribir el nombre que llevará, seguido de un signo igual `=` y el valor que le vamos a asignar:

```bash
MAIL=/var/spool/mail/student
```

Y para leer el contenido de una variable, es suficiente con usar **`echo`**:

```bash
student@localhost:/etc$ echo $PATH
/home/student/.local/bin:/home/student/bin:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin
```

### 💡 Nota importante

No toda variable creada automáticamente se convierte en una variable de entorno disponible para procesos hijos.  
Para que una variable forme parte del entorno, normalmente debe exportarse con `export`.

Ejemplo:

```bash
NOMBRE="Francisco"
export CIUDAD="Puebla"
```

- `NOMBRE` → variable de shell
- `CIUDAD` → variable de entorno

---

## 📂 Reconociendo la configuración de los archivos de entorno

Cuando un usuario inicia sesión, un entorno es creado de manera automática.  
Dicha configuración se apoya en varios archivos importantes:

### Archivos principales

- **`/etc/profile`**  
  Es el archivo genérico que es procesado cuando cualquier usuario inicia sesión.

- **`/etc/bashrc`**  
  Se procesa cuando se inicia una subshell.

- **`~/.bash_profile`**  
  En este archivo se pueden definir variables y configuraciones para el inicio de sesión de un usuario específico.

- **`~/.bashrc`**  
  En este archivo se pueden definir variables y configuraciones de subshell para un usuario específico.

---

## 🔄 Diferencia entre Login Shell y Subshell

Un **login shell** es la shell que se inicia cuando entras formalmente al sistema como usuario.

Un **subshell** es una shell hija que nace dentro de otra shell que ya estaba abierta.

La diferencia importante no es solo que sea “otra terminal”, sino **cómo fue iniciada** y **qué configuración carga**.

### ✅ Login Shell

Se utiliza al iniciar sesión de forma real en el sistema, por ejemplo:

- al entrar por consola
- al conectarte por SSH
- al iniciar sesión en un TTY

Normalmente carga archivos como:

- `/etc/profile`
- `~/.bash_profile`
- `~/.profile`

### ✅ Subshell

Se crea desde una shell que ya estaba activa, por ejemplo al ejecutar:

```bash
bash
```

o al lanzar una shell hija dentro de otra sesión.

Normalmente una subshell interactiva de Bash carga:

- `~/.bashrc`

### 🧠 Idea clave

- **Login shell** → representa la entrada inicial del usuario al sistema.
- **Subshell** → representa una shell secundaria creada dentro de otra sesión ya existente.

### 📌 Ejemplo práctico

Si entras por SSH:

```bash
ssh usuario@servidor
```

normalmente llegas a un **login shell**.

Si ya estando dentro ejecutas:

```bash
bash
```

abres una **subshell**.

Si sales con:

```bash
exit
```

regresas a la shell anterior.

---

## 🆘 Buscando ayuda

Al momento de querer utilizar los comandos de cualquier distribución, nos daremos cuenta de que existen cientos de ellos con diversas variantes, atributos y opciones.

Es aquí cuando el comando **`man`** aparece, pues se convierte en el mejor recurso para obtener ayuda sobre sintaxis y uso de comandos.

Además, también es posible desplegar una ayuda resumida con:

```bash
comando --help
```

---

## ⚡ Help

La forma más rápida de obtener ayuda sobre un comando es usando el atributo **`--help`**.

No solo se desplegará un resumen del comando, sino también las opciones que se le pueden agregar.

Hay que tomar en cuenta que no siempre existe una forma estricta única de usar los atributos; en muchos casos pueden escribirse en distinto orden, siempre que la sintaxis del comando lo permita.

---

## 📖 Usando `man`

Las páginas de `man` describen de manera más exacta cómo usar un comando.

Algunas claves esenciales para usar **`man`** son:

> **Note:** La parte más importante de una página del manual suele estar hacia el final, donde muchas veces se encuentran dos secciones muy útiles: **ejemplos** y **See Also**.

- **`G`** para moverte al final de la página lo más rápido posible
- **`/example`** para buscar dentro de la página del manual donde se muestren ejemplos de uso del comando

---

### 🔎 Encontrando la página correcta del manual

**`apropos`** o **`man -k`** son útiles para encontrar información específica en la base de datos de páginas del manual.

Para usarlos correctamente, escribimos **`man -k`** seguido de la palabra que estamos buscando:

```bash
man -k password
```

En ocasiones, al usar este comando, encontraremos demasiada información.  
Podemos ser más específicos agregando filtros con el comando **`grep`**, siempre que tengamos una idea más clara de lo que estamos buscando.

Las páginas `man` están categorizadas de la siguiente forma:

- **1** → Programas ejecutables o comandos shell
- **5** → Convenciones y formatos de archivos
- **8** → Comandos para administración del sistema

De esta manera, podemos usar `grep` sabiamente. Por ejemplo, si queremos encontrar algo sobre **passwords** y sabemos que tiene que ver con configuración de archivos, podemos limitar la búsqueda así:

```bash
man -k password | grep 5
```

### ⚠️ Tener en cuenta

La base de datos de `man` debe estar actualizada.  
Para hacer la actualización manual, solo debemos ejecutar el comando **`mandb`** como administrador y sin argumentos.

```bash
sudo mandb
```

---

## 📚 Info

Además de la información que podemos encontrar en `man`, algunos comandos cuentan con documentación extra. Muchas veces esta puede consultarse desde el apartado **See Also** del propio `man`.

Los comandos **`pinfo`** o **`info`** nos permiten acceder a esta documentación más extendida, la cual suele estar alojada como un manual **Texinfo**.

- **`pinfo`** es más fácil de usar por su estilo de listas o menús.
- **`info`** es la herramienta estándar que comúnmente ya viene disponible o puede instalarse fácilmente.

La línea superior nos indicará en qué parte del documento `info` estamos posicionados.  
Hay que poner especial atención a los indicadores:

- **Up**
- **Next**
- **Previous**

Estos indican cómo navegar dentro de la jerarquía del documento.

Su estructura es jerárquica, muy parecida a una página web:

- presionar **`n`** para ir a la siguiente página
- presionar **`p`** para la anterior
- presionar **`u`** para subir en la jerarquía

---

### ⚠️ Incidente: paquete `pinfo` no disponible

Al intentar instalar `pinfo` mediante `dnf`, el sistema devolvió:

```bash
Error: Unable to find a match: pinfo
```

**Análisis:**

- En instalaciones minimalistas de RHEL, `pinfo` no es un paquete base.
- No se recomienda perder tiempo en el examen buscando repositorios externos (como EPEL) si existe una herramienta nativa equivalente.

**Solución (Best Practice RHCSA):**

Usar el visor de documentación estándar **`info`**, el cual ya fue instalado previamente en el ejercicio.

✅ En contexto RHCSA, esta decisión es mejor porque evita depender de repositorios adicionales y se apega más al entorno real del examen.

---

## 📁 `/usr/share/doc` Documentation file

Como tercera opción de documentación, podemos dirigirnos a la ruta **`/usr/share/doc`**, donde en ocasiones se copia información útil de servicios, paquetes y sistemas más complejos.

Esta ruta puede contener:

- archivos `README`
- ejemplos de configuración
- notas del desarrollador
- documentación adicional de paquetes instalados

Ejemplo:

```bash
ls /usr/share/doc
```

### 💡 Observación

No todos los paquetes incluyen la misma cantidad de documentación, pero cuando existe, esta carpeta puede ser muy útil para encontrar ejemplos reales o detalles adicionales sobre el funcionamiento de un servicio.

---

## ✅ Resumen rápido

En esta sección repasé tres ideas importantes:

1. Las **variables de entorno** permiten personalizar el comportamiento del sistema, scripts y programas.
2. Los archivos como **`/etc/profile`**, **`~/.bash_profile`** y **`~/.bashrc`** ayudan a definir cómo se construye el entorno del usuario.
3. Linux ofrece varias formas de buscar ayuda y documentación:
   - `--help`
   - `man`
   - `info`
   - `/usr/share/doc`

📝 Conocer estas herramientas es clave para trabajar con mayor autonomía en Linux y resolver dudas rápidamente, especialmente en preparación para RHCSA.


## Exam Preparation Tasks

### Define Key Terms

- **Shell**
  
  Es descrito como el entorno donde los usuarios y administradores introducen comandos que son ejecutados por el sistema operativo.
- **Bash**
  
  Tipo de shell, es el interprete entre el usuario y el sistema operativo
- **Internal command**
  
  Tipos de comandos pre establecidos en el sistema, son parte del mismo shell. Entre ellos se encuentran comandos como `type`, `pwd`, `cd`
- **External command**
  
  Tipos de comandos establecidos segun la distro o por usuarios externos, estos normalmente tienen su propia ruta, visible desde `$PATH`
- **`$PATH`**
  
  Variable de entorno que actua como mapa para que el shell encuentre programas ejecutables
- **STDIN**
  
  Entrada generica de informacion al shell, normalmente la entrada del teclado
- **STDOUT**
  
  Salida estandar de la ejecucion de un comando, cuando este se realiza de manera exitosa.
- **STDERR**
  
  Salida de error al ejecutar un comando, este describe el tipo de error
- **Redirection**
  
  Manera de redirigir tanto la entreada, salida normal o de error de un comando, usando > >> o |
- **File descriptor**
  
  0, 1 o 2, dependiendo del tipo de salida que busquemos, siendo 0 la entrada, 1 salida de comando.
- **Device file**

  Archivo que se encarga de la comunicacion entre la terminal y el hardware, hace la traduccion de comandos a bits y biceversa.

- **Pipe**

Es una forma de redirigir el output de un comando para utilizarlo posteriormente con otro, puede entenderse como la concatenacion de stdout con un nuevo comando.

- **Environment**

Es la manera en que estan configuradas las variables de entorno de un ambiente linux, segun las necesidades del usuario.
- **Variable**

Asignación de un valor, comando o funciona una palabra en especifico para su uso posterior, permitiendo acceder a dico valor desde cualquier parte del sistema, esto cuando se configuran como variables de entorno.

- **Login shell**

Es el primer shell al que entras al hacer un login, permite correr scripts, comandos, etc.
- **Subshell**

Es la shell que se abre al ejecutar comandos desde una shell principal o una login shell.

---

## Review Questions

- What is a variable?

Es una palabra o conjunto de caracteres que reciben un valor dinamico.

- Which command enables you to find the correct man page based on keyword usage?

`man -k keyword`

- Which file do you need to change if you want a variable to be set for user **bob** when this user logs in?

`vim.bashrc`

- When analyzing how to use a command, you read that the documentation is maintained with the **Texinfo** system. How can you read the information?

Podemos utilizar el comando `pinfo` si esta disponible, en caso contrario, usariamos solo `info` seguido del comando a revisar.

- What is the name of the file where Bash stores its history?

`.bash_history`

- Which command enables you to update the database that contains man keywords?

`mandb`

- How can you undo the last modification you have applied in Vim?

`u`

- What can you add to a command to make sure that it does not show an error message, assuming that you do not care about the information in the error messages either?

`2>`

- How do you read the current contents of the `$PATH` variable?

`echo $PATH`

- How do you repeat the last command you used that contains the string `dog` somewhere in the command?

`!dog`
---

## Lab 2.1

1. Modify your shell environment so that on every subshell that is started, a variable is set. The name of the variable should be `COLOR`, and the value should be set to `red`. Verify that it is working.

2. Use the appropriate tools to find the command that you can use to change a user password. Do you need root permissions to use this command?

3. From your home directory, type the command `ls -al wergihl *` and ensure that both errors and regular output are redirected to a file with the name `/tmp/lsoutput`.
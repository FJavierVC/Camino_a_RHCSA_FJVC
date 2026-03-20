# Exam Preparation Tasks

## Define Key Terms

- **Shell**
  
  Es descrito como el entorno donde los usuarios y administradores introducen comandos que son ejecutados por el sistema operativo.
- **Bash**
  
  Tipo de shell, es el interprete entre el usuario y el sistema operativo
- **Internal command**
  
  Tipos de comandos pre establecidos en el sistema, son parte del mismo shell. Entre ellos se encuentran comandos como `alias`, `pwd`, `cd`
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
  
  0, 1 o 2, dependiendo del tipo de salida que busquemos, siendo 0 la entrada, 1 salida de comando y el 2 el error.
- **Device file**

  Archivo que se encarga de la comunicacion entre la terminal y el hardware, hace la exposicion de comandos a bits y biceversa.

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

`~bob/.bashrc`

- When analyzing how to use a command, you read that the documentation is maintained with the **Texinfo** system. How can you read the information?

Podemos utilizar el comando `pinfo` si esta disponible, en caso contrario, usariamos solo `info` seguido del comando a revisar.

- What is the name of the file where Bash stores its history?

`.bash_history`

- Which command enables you to update the database that contains man keywords?

`mandb`

- How can you undo the last modification you have applied in Vim?

`u`

- What can you add to a command to make sure that it does not show an error message, assuming that you do not care about the information in the error messages either?

`2> /dev/null`

- How do you read the current contents of the `$PATH` variable?

`echo $PATH`

- How do you repeat the last command you used that contains the string `dog` somewhere in the command?

`!dog`
---

## Lab 2.1

1. Modify your shell environment so that on every subshell that is started, a variable is set. The name of the variable should be `COLOR`, and the value should be set to `red`. Verify that it is working.
```
student@localhost:~$ env | grep COLOR=red
COLOR=red
student@localhost:~$ cat .bashrc
# .bashrc
export COLOR=red

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

# User specific environment
if ! [[ "$PATH" =~ "$HOME/.local/bin:$HOME/bin:" ]]; then
    PATH="$HOME/.local/bin:$HOME/bin:$PATH"
fi
export PATH

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
if [ -d ~/.bashrc.d ]; then
    for rc in ~/.bashrc.d/*; do
        if [ -f "$rc" ]; then
            . "$rc"
        fi
    done
fi
unset rc
student@localhost:~$ cat .bashrc | grep COLOR 
COLOR=red
student@localhost:~$ cat .bashrc | grep COLOR
```
2. Use the appropriate tools to find the command that you can use to change a user password. Do you need root permissions to use this command?

Para hacer cambio de contraseña a cualquier usuario, si, si se necesitan permisos de administrador, pero cualquier usuario puede cambiar su propia contraseña sin ser root.
```
student@localhost:~$ man -k change user password | grep "change user password"
chage (1)            - change user password expiry information
passwd (1)           - change user password
student@localhost:~$ man passwd | sed -n '/DESCRIPTION/,/OPTIONS/p' > Desc.txt && cat Desc.txt
DESCRIPTION
       The passwd command changes passwords for user accounts. A normal user may only change the password for their own account, while the superuser may change the password for any account.  passwd also changes the account or
       associated password validity period.
```
> Nota: Se utilizó sed -n '/DESCRIPTION/,/OPTIONS/p' porque grep solo muestra la línea coincidente, mientras que sed permite extraer un rango completo de texto.

3. From your home directory, type the command `ls -al wergihl *` and ensure that both errors and regular output are redirected to a file with the name `/tmp/lsoutput`.
```
student@localhost:~$ ls -al wergihl * > /tmp/lsoutput 2>&1
student@localhost:~$ cat /tmp/lsoutput 
ls: cannot access 'wergihl': No such file or directory
-rw-r--r--. 1 student student 1193 Mar 19 17:50 1
-rw-r--r--. 1 student student    0 Mar 19 17:35 Desc
-rw-r--r--. 1 student student 2623 Mar 19 17:37 Desc.txt
-rw-r--r--. 1 student student   80 Mar 10 23:33 output
-rw-r--r--. 1 student student   46 Mar 11 17:50 testfile

Desktop:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..

Documents:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..

Downloads:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..

Music:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..

Pictures:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..

Public:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..

Templates:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..

Videos:
total 4
drwxr-xr-x.  2 student student    6 Mar  2 00:37 .
drwx------. 14 student student 4096 Mar 19 17:50 ..
```
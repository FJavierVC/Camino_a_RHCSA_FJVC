# Capítulo 2 | Ejercicio 2-6: Gestión de Variables y Entorno de Shell

## Objetivo
Comprender la persistencia de variables de entorno y la configuración del archivo de inicio de Bash (`.bashrc`).

---

### 1. Variables Temporales y Localización
En este paso, observamos cómo cambian las variables en la sesión actual y cómo afectan a otros comandos.

*   **Verificar idioma actual:**
    ```bash
    'student@localhost:~$ echo $LANG
    en_US.UTF-8
    ```
*   **Consultar ayuda (aparecerá en el idioma de $LANG):**
    ```bash
    'student@localhost:~$ ls --help 
    Usage: ls [OPTION]... [FILE]...
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

    Mandatory arguments to long options are mandatory for short options too.
    -a, --all                  do not ignore entries starting with .
    -A, --almost-all           do not list implied . and ..
        --author               with -l, print the author of each file
    -b, --escape               print C-style escapes for nongraphic characters
        --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                                e.g., '--block-size=M'; see SIZE format below
    .
    .
    .
    ```
*   **Cambiar idioma temporalmente:**
    ```bash
    'student@localhost:~$ ls --help 
    Modo de empleo: ls [OPCIÓN]... [FICHERO]...
    Muestra información acerca de los FICHEROs (del directorio actual por defecto).
    Ordena las entradas alfabéticamente si no se especifica ninguna de las
    opciones -cftuvSUX ni --sort.

    Los argumentos obligatorios para las opciones largas son también obligatorios
    para las opciones cortas.
    -a, --all                  no oculta las entradas que comienzan con .
    -A, --almost-all           no muestra las entradas . y .. implícitas
        --author               con -l, imprime el autor de cada fichero
    -b, --escape               imprime escapes en estilo C para los caracteres no
                                gráficos
        --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                                e.g., '--block-size=M'; see SIZE format below
    .
    .
    .
    ```
    > **Nota:** Este cambio solo afecta a la terminal activa. Si cierras la sesión (`exit`), el cambio se pierde.

---

### 2. Persistencia de Variables con `.bashrc`
Para que una variable esté disponible siempre, debemos editar el archivo de configuración del usuario.

*   **Abrir configuración de Bash:**
    ```bash
    'vim ~/.bashrc'
    '# .bashrc

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

    ```

*   **Añadir la variable:**
    Al final del archivo, agregamos la siguiente línea (se recomienda `export` para que sea variable de entorno):
    ```bash
    'vim ~/.bashrc'
    '# .bashrc

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
    export COLOR=red
    ```

---

### 3. Verificación de Persistencia
A diferencia de la variable `LANG` anterior, esta debe sobrevivir al cierre de la terminal.

1. Cerrar la terminal actual y abrir una nueva.
2. **Validar la variable:**
    ```bash
    'student@localhost:~$ echo $COLOR
    red

    ```

---

## Conceptos Clave para el RHCSA
*   **`~/.bashrc`**: Se ejecuta para shells que no son de login (como abrir una terminal en el escritorio).
*   **`export`**: Es fundamental. Sin `export`, la variable es local; con `export`, los procesos hijos (scripts, programas) pueden verla.
*   **`source ~/.bashrc`**: Alternativa para aplicar cambios sin tener que cerrar y abrir la terminal.

#### Encontrando la pagina correcta del manual
**apropos** o **man -k** son utiles para encontrar informacion especifica en las paginas del manual.
Para usarlo de manera correcta, usaremos  **man -k** seguido de la palabra que estamos buscando en la base de datos del manual.

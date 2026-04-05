# Trabajando con archivos

Abrir una terminal shell como un usuario ordinario.

## Verificar directorio actual

Ejecutar el comando:

```bash
pwd
```

Salida esperada:

```bash
student@localhost:~$ pwd
/home/student
```

---

## Crear directorios

Crear los directorios `newfiles` y `oldfiles`:

```bash
mkdir newfiles oldfiles
```

---

## Listar contenido

Listar los archivos y directorios del directorio actual:

```bash
ls
```

Ejemplo de salida:

```bash
student@localhost:~$ ls
Desc  Desc.txt  Desktop  Documents  Downloads  Music  newfiles  oldfiles  Pictures  Public  Templates  Videos
```

---

## Crear archivos

Crear dos archivos dentro del directorio `newfiles`:

- Un archivo oculto (`.hidden`)
- Un archivo visible (`unhidden`)

```bash
touch newfiles/.hidden newfiles/unhidden
```

---

## Copiar archivos

Copiar todo el contenido del directorio `newfiles` hacia `oldfiles`, incluyendo archivos ocultos y preservando atributos:

```bash
cp -a newfiles/. oldfiles/
```

---

## Verificar contenido copiado

Listar el contenido del directorio `oldfiles`, incluyendo archivos ocultos:

```bash
ls -a oldfiles
```

Salida esperada:

```bash
.  ..  .hidden  unhidden
```

---

## Notas importantes

- `.` representa el contenido de un directorio.
- `-a` en `cp` permite copiar archivos ocultos y preservar permisos.
- `ls -a` muestra archivos ocultos (los que comienzan con `.`).
- Usar `newfiles/.` garantiza que se copien todos los archivos, incluidos los ocultos.
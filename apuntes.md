# Introducción a la Terminal y Línea de Comandos

## Primeros pasos

## Empezando a correr

### Redirecciones: cómo funciona la shell

stdin, stdout, stderr se relacionan con los file descriptors 0, 1, 2

Redireccionamiento de stdout a un archivo,

```bash
ls -l /bin/usr > ls-output.txt
```

Esta linea de comando redirecciona la salida de ls a un archivo llamado ls-output.txt, que se reescribe cada vez que se ejecuta.

Si queremos que la salida se agregue al archivo, en vez de reescribirlo, usamos el operador `>>`

```bash
ls -l /bin/usr >> ls-output.txt
```

Redireccion de errores a un archivo

```bash
ls -l /bin/usr 2> ls-error.txt
```

En este caso, es necesario anteponer el numero de file descriptor a redireccionar. En este caso, el 2 corresponde a stderr.

En ocasiones nos puede interesar guardar tanto la salida como los errores en un mismo archivo. Para esto, usamos el operador `2>&1`

```bash
ls -l /bin/usr > ls-output.txt 2>&1
```

### Redirecciones: pipe operator

## Utilidades de la terminal

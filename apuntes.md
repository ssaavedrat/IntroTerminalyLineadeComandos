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

`cat` es un comando usado para concatenar archivos y mostrarlos en la salida estandar. Si le pasamos un archivo como argumento, lo muestra en la salida estandar. Si no le pasamos argumentos, lee de la entrada estandar.

```bash
cat file.txt
```

Si pasamos dos archivos como argumentos, los concatena y muestra el resultado en la salida estandar.

```bash
cat file1.txt file2.txt
```

si queremos guardar el resultado de la concatenacion en un archivo con tee

```bash
cat file1.txt file2.txt | tee file3.txt
```

`sort` puede ser utilizado en el pipe para ordenar la salida de ls

```bash
ls -l /bin/usr | sort | tee ls-sorted.txt
```

Extras, `cowsay` y `lolcat`. Cowsay es un programa que muestra un mensaje en un globo de dialogo de una vaca. Lolcat es un programa que muestra un mensaje con colores.

```bash
cowsay "Hola mundo" | lolcat
```

Esto generará la combinación de ambos, es decir, una vaca colorida.

### Encadenando comandos: Operadores de control

Los operadores de control son símbolos reservados por la terminal que nos permiten encadenar comandos.

Usamos el operador `;` para ejecutar comandos en secuencia.

```bash
ls; echo "Hola mundo"; cal
```

Lo anterior, ejecuta los comandos en secuencia, uno tras otro.

Usamos el operador `&` para ejecutar comandos en paralelo (asíncrono).

```bash
ls & echo "Hola mundo" & cal
```

Usamos el operador `&&` para ejecutar comandos en secuencia, pero solo si el comando anterior se ejecutó correctamente.

```bash
cd dsjfajsdfijd && echo "Hola mundo" && cal
```

si la carpeta no existe, el comando `echo` y `cal` no se ejecutarán.

Usamos el operador `||` para ejecutar comandos en secuencia, pero solo si el comando anterior NO se ejecutó correctamente.

```bash
cd dsjfajsdfijd || echo "Hola mundo" || cal
```

aquí si la carpeta no existe, el comando `echo` se ejecutará.

Por último, podemos combinar los operadores de control para crear secuencias más complejas.

En el siguiente ejemplo, si olvidamos el nombre del operador de cambio de directorio, podemos usar el operador `||` para ejecutar el comando `cd` solo si el comando `changedir` no existe. Luego, podemos usar el operador `&&` para crear la carpeta `test` solo si el comando `cd` se ejecutó correctamente.

```bash
changedir miCarpeta || cd miCarpeta && mkdir test
```

## Utilidades de la terminal

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

### Cómo se manejan los permisos

Cuando usamos el comando

```bash
ls -l
```

nos muestra una lista de archivos y directorios con sus permisos. Por ejemplo

```bash
-rw-r--r-- 1 user user  0 Dec  21 11:25 file.txt
```

El primer caracter indica el tipo de archivo. Los tipos son:

* `-` archivo regular
* `d` directorio
* `l` link simbólico
* `b` archivo de bloque (raro en carpetas de usuario guarda información de hardware)

Los siguientes 9 caracteres indican los permisos. Estos se dividen en 3 grupos de 3 caracteres cada uno. 

* El primer grupo indica los permisos del usuario que creó el archivo (User). 
* El segundo grupo indica los permisos del grupo al que pertenece el archivo (Group). 
* El tercer grupo indica los permisos del resto de los usuarios (World).

Los permisos pueden ser de lectura `r`, escritura `w` o ejecución `x`. Si el permiso no está activado, se muestra un `-` en su lugar.

Se utiliza codificación octal para representar los permisos. Cada grupo de 3 caracteres se representa con un número de 0 a 7. 

Por ejemplo, el permiso `rwx = 111` se representa con el número 7, el permiso `rw- = 110` se representa con el número 6, el permiso `r-x = 101` se representa con el número 5, y así sucesivamente.

### Modificando permisos en la terminal

#### Cambiar permisos a un archivo

Usando chmod de manera simbólica

```bash
chmod [simboloDelUsuario][operador][permiso] [archivoParaCambiarSusPermisos]
```

La otra forma es usar la codificación octal

```bash
chmod [permisoEnOctal] [archivoParaCambiarSusPermisos]
```

Por ejemplo, para darle permisos de lectura y escritura al usuario que creó el archivo, y quitarle permisos de lectura y escritura al grupo y al resto de los usuarios, usamos

```bash
chmod u=rw,g-rw,o-rw archivo.txt
```

#### Gestionar usuarios

Podemos obtener el nombre del usuario actual con el comando `whoami`

```bash
whoami
```

Cuando ejecutamos `ls -l` podemos observar en la tercera columna el nombre del usuario que creó el archivo. En la cuarta columna podemos observar el nombre del grupo al que pertenece el archivo.

```bash
-rw-r--r-- 1 user user  0 Dec  21 11:25 archivo.txt
```

Para cambiar de usuario utilizamos el comando `su`

```bash
su [nombreDeUsuario]
```

Un caso especial es usar su con el nombre de usuario `root`. El usuario root es el usuario administrador del sistema. Este usuario tiene permisos para hacer cualquier cosa en el sistema. Por lo tanto, es recomendable usarlo con cuidado.

```bash
su root
```

Alternativamente, se accede con `sudo su`.

#### ¿Qué hacer en caso de olvidar una contraseña?

Si estás usando Windows Subsystem for Linux (wsl) y se te olvidó la contraseña del root. Sigue estos pasos:

* Abre el cmd de windows y ejecuta este comando `wsl --user root`. Esto hará que se inicie en la terminal wsl con el usuario root.
* Luego ejecuta el comando `passwd root` el cual te permitirá cambiar la contraseña del usuario root.

Ya con esto puedes volver a la terminal de wsl y volver a ejecutar el comando `su root`.

#### Cambiar de dueño

Para cambiar el dueño de un archivo usamos el comando `chown`

```bash
chown [nuevoDueño] [archivo]
```

### Variables de Entorno

Las variables de entorno son útiles cuando necesitamos que cierta información prevalezca para poder trabajar más rápido o necesitamos guardar información para no tener que recordarla constantemente.

Podemos listar las variables de entorno con el comando `env`

```bash
env
```

En cambio si quieremos listar una en específico usamos `echo`, seguido del nombre de la variable antecedido por el signo `$`

```bash
echo $PATH
```

#### ¿Cómo crear variables de entorno?

Para crear una variable de entorno nos dirigimos al archivo `.bashrc` que se encuentra en la carpeta de nuestro usuario. El archivo está oculto, por lo que debemos usar el comando `ls -la` para poder verlo.

Al editar el archivo podemos agregar una variable de entorno, por ejemplo,

```bash
SALUDO_AMISTOSO = "Hola mundo"
```

Y luego llamarlo desde la terminal con `echo`

```bash
echo $SALUDO_AMISTOSO
```

También es posible crear nuevos alias para comandos que usamos frecuentemente. Por ejemplo, si queremos crear un alias para el comando `ls -la` podemos agregar la siguiente línea al archivo `.bashrc`

```bash
alias l="ls -la"
```

Luego, podemos usar el comando `l` para ejecutar `ls -la`

### Comandos de Búsqueda

Podemos buscar programas con el comando `which`

```bash
which cowsay
```

Para buscar archivos, utilizamos el comando `find`

```bash
find [directorio] [opciones]
```

Podemos buscar archivos por nombre y utilizando wildcards. Por ejemplo, buscar todos los archivos con extensión `.txt` en desde el directorio actual

```bash
find ./ -name *.txt
```

Podemos buscar por tipo de archivo. `d` para directorios, `f` para archivos regulares, `l` para links simbólicos. Por ejemplo, buscar todos los directorios en el directorio actual

```bash
find ./ -type d
```

Podemos buscar por tamaño de archivo. Para ello, utilizamos los prefijos `k` para kilobytes, `M` para megabytes, `G` para gigabytes. Como los tamaños de archivos son variables usamos los operadores `+` para mayor que, `-` para menor que.

Por ejemplo, buscar todos los archivos mayores a 1MB en el directorio actual

```bash
find ./ -size +1M
```

Para buscar vacíos usamos la opción `-empty`

```bash
find ./ -empty
```

Para limitar la búsqueda a un número de niveles de profundidad usamos la opción `-maxdepth` o `-mindepth`, cuando nos queremos saltar níveles de profundidad. Por ejemplo, para buscar en el directorio actual y en un nivel de profundidad

```bash 
find ./ -maxdepth 1
```

Todos estos comandos de búsqueda pueden ser combinados. Además su salida puede ser entregada a `less` para poder verla de manera más cómoda.

```bash
find ./ -name *.txt -type f -size +1M | less
```

### Usando el comando grep

GREP: **G**lobal **R**egular **E**xpression **P**rint

El comando grep nos permite buscar patrones en archivos o en la salida de otros comandos.

```bash
grep [opciones] [expresión regular] [archivo]
```

Por ejemplo, para buscar la palabra `The` en el archivo `file.txt`

```bash
grep The file.txt
```

#### Opciones del comando grep

Podemos ignorar mayúsculas y minúsculas con la opción `-i`

```bash
grep -i The file.txt
```

Para contar el número de ocurrencias usamos la opción `-c`

```bash
grep -c The file.txt
```

Para excluir archivos usamos la opción `-v`

```bash
grep -v The file.txt
```

Podemos limitar el número de ocurrencias con la opción `-m`

```bash
grep -m 2 The file.txt
```

## Utilidades de la terminal

### Utilidades de Red

El comando ifconfig nos permite ver la configuración de red de nuestra computadora

```bash
ifconfig
```

El comando ping nos permite verificar la conectividad con un host

```bash
ping [host]
```

El comando `curl` nos permite hacer peticiones http para obtener el contenido de una página web / archivo en la web.

```bash
curl [url]
```

Usamos el comando `wget` para descargar archivos de la web directamente a la computadora.

```bash
wget [url]
```

El comando traceroute nos permite ver la ruta que toma un paquete para llegar a un host.

```bash
traceroute [host]
```

Con el comando `netstat -i` podemos ver las interfaces de red de nuestra computadora.

```bash
netstat -i
```

### Comprimiendo Archivos Tar y Zip

### Usando el comando tar

El comando `tar` nos permite comprimir y descomprimir archivos. Para comprimir archivos usamos la opción `-c` agregamos `-f` para indicar el nombre del archivo de salida y agregamos `-v` (verbose) para ver el progreso de la compresión.

```bash
tar -cvf [nombreDelArchivo.tar] [archivos]
```

Adicionalmente, podemos usar la opción `-z` para comprimir con gzip.

```bash
tar -cvzf [nombreDelArchivo.tar.gz] [archivos]
```

Para descomprimir usamos la opción `-x`

```bash
tar -xvf [nombreDelArchivo.tar] [archivos]
```

### Usando el comando zip

El comando `zip` nos permite comprimir y descomprimir archivos. Para comprimir archivos usamos la opción `-r` para comprimir recursivamente (carpeta y archivos).

```bash
zip -r [nombreDelArchivo.zip] [archivos]
```

Para descomprimir simplemente usamos el comando `unzip`

```bash
unzip [nombreDelArchivo.zip]
```
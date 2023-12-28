# Introducción a la Terminal y Línea de Comandos

## Primeros pasos

### ¿Qué es la terminal?

La terminal es una interfaz de texto que nos permite interactuar con el sistema operativo. En este caso, nos referimos a la terminal de Linux.

### Aprendiendo a caminar en la terminal

#### Sistema de carpetas 

El sistema de carpetas de Linux es similar al de Windows. La carpeta raíz es `/`. Las carpetas de usuario se encuentran en `/home`. La carpeta de usuario actual se representa con `~`. La carpeta de usuario actual se puede obtener con el comando `pwd` (print working directory).

```bash
pwd
```

#### Navegando entre carpetas

Para navegar entre carpetas usamos el comando `cd` (change directory). Por ejemplo, para ir a la carpeta de usuario actual usamos la virgulilla `~`.

```bash
cd ~
```

El punto y doble punto se utilizan para referirse a la carpeta actual y a la carpeta padre, respectivamente.

```bash
cd ..
```

Para ir a la carpeta raíz usamos la barra `/`.

```bash
cd /
```

#### Listando archivos y carpetas

Para listar archivos y carpetas usamos el comando `ls` (list). Por ejemplo, para listar los archivos y carpetas de la carpeta actual usamos

```bash
ls
```

Para obtener más información sobre los archivos y carpetas usamos la opción `-l` (long).

```bash
ls -l
```

Si queremos listar de forma más amigable, usamos la opción `-h` (human readable).

```bash
ls -lh
```

#### Comando file

El comando `file` nos permite obtener información sobre un archivo. Por ejemplo, para obtener información sobre el archivo `file.txt` usamos

```bash
file file.txt
```

### Manipulando archivos y carpetas

#### Comando mkdir

El comando `mkdir` (make directory) nos permite crear carpetas. Por ejemplo, para crear una carpeta llamada `test` usamos

```bash
mkdir test
```

Podemos crear múltiples carpetas a la vez. Por ejemplo, para crear las carpetas `test1`, `test2` y `test3` usamos

```bash
mkdir test1 test2 test3
```

#### Comando touch

El comando `touch` nos permite crear archivos. Por ejemplo, para crear un archivo llamado `file.txt` usamos

```bash
touch file.txt
```

Podemos crear múltiples archivos a la vez. Por ejemplo, para crear los archivos `file1.txt`, `file2.txt` y `file3.txt` usamos

```bash
touch file1.txt file2.txt file3.txt
```

#### Comando cp

El comando `cp` (copy) nos permite copiar archivos y carpetas. Por ejemplo, para copiar el archivo `file.txt` a la carpeta `test` usamos

```bash
cp file.txt test
```

cp permite cambiar el nombre de un archivo o carpeta. Por ejemplo, para copiar el archivo `file.txt` a la carpeta `test` con el nombre `file2.txt` usamos

```bash
cp file.txt test/file2.txt
```

#### Comando mv

El comando `mv` (move) nos permite mover carpetas. Por ejemplo, para mover el directorio `test` a la carpeta `test2` usamos

```bash
mv test test2
```

#### Comando rm

El comando `rm` (remove) nos permite eliminar archivos y carpetas. Por ejemplo, para eliminar el archivo `file.txt` usamos

```bash
rm file.txt
```

Ahora si queremos eliminar la carpeta `test2` usamos la opción `-r` (recursive) para eliminar de forma recursiva (archivos y carpeta).

```bash
rm -r test2
```

El archivo rm tiene las opciones, `-f` (force) para forzar la eliminación y `-i` (interactive) para preguntar antes de eliminar.

### Explorando el contenido de nuestros archivos

#### Comandos head y tail

El comando `head` nos permite ver las primeras líneas de un archivo. Por ejemplo, para ver las primeras 5 líneas del archivo `file.txt` usamos

```bash
head -n 5 file.txt
```

El comando `tail` nos permite ver las últimas líneas de un archivo. Por ejemplo, para ver las últimas 5 líneas del archivo `file.txt` usamos

```bash
tail -n 5 file.txt
```

La cantidad por defecto de líneas es 10. Por lo tanto, podemos omitir el parámetro `-n` en ambos comandos.

#### Comando Less

El comando `less` nos permite ver el contenido de un archivo de forma interactiva. Por ejemplo, para ver el contenido del archivo `file.txt` usamos

```bash
less file.txt
```

Para navegar por el archivo usamos las flechas del teclado. Para salir presionamos la tecla `q`. Para buscar una palabra usamos `/` seguido de la palabra a buscar. Para buscar la siguiente ocurrencia usamos `n`.

### ¿Qué es un comando?

Un comando es un mensaje enviado al ordenador que provoca una respuesta en este sistema y se comporta como una orden, pues informa al dispositivo informático que debe ejecutar una acción según la indicación enviada.

Un comando puede ser:
* Un programa ejecutable
* Un comando de utilidad de la shell. Ejemplo: `cd`
* Una función de la shell. Ejemplo: `mkdir`
* Un alias. Ejemplo: `ls`

#### Comando type

El comando `type` nos permite saber qué tipo de comando estamos ejecutando. Por ejemplo, para saber qué tipo de comando es `ls` usamos

```bash
type ls
```

#### Comando alias

El comando `alias` nos permite crear alias para comandos. Por ejemplo, para crear un alias para el comando `ls -lh` usamos

```bash
alias l="ls -lh"
```

Ahora podemos usar el comando `l` para ejecutar `ls -lh`

```bash
l
```

#### Comando help

El comando `help` nos permite obtener ayuda sobre un comando.

#### Comando man

El comando `man` permite acceder al manual de un comando (mayor información).

#### Comando info

El comando `info` permite acceder a la información de un comando (menor información).

#### Comando whatis

El comando `whatis` nos permite obtener una descripción de un comando.

### Wildcards

Los wildcards son caracteres especiales que nos permiten seleccionar archivos y carpetas de forma más eficiente.

Se pueden usar con los comandos de manipulación de archivos `ls`, `cp`, `mv` y `rm`.

#### Tipos de wildcards

* `*` (asterisco): representa cualquier cantidad de caracteres.
* `?` (signo de interrogación): representa un solo caracter.
* `[]` (corchetes): representa un rango o conjunto de caracteres.

#### Ejemplos de uso

Para listar todos los archivos de texto de la carpeta actual usamos

```bash
ls *.txt
```

Para listar todos los archivos de texto que empiezan con la letra `f` usamos

```bash
ls f*.txt
```

Si queremos buscar archivos que empiecen con `photo_` pero queremos seleccionar todas las fotos con nombre `photo_1`, `photo_2`, `photo_3`, etc. Podemos usar el wildcard `?` para seleccionar un solo caracter.

```bash
ls photo_?.jpg
```

Si queremos buscar archivos que empiezan con la letra `C` o la letra `D` usamos el wildcard `[]` para seleccionar un rango de caracteres.

```bash	
ls [CD]*
```

Si quieremos buscar archivos en un rango de números usamos el wildcard `[]`. Por ejemplo, para fotografías del año 2019 a 2021 usamos

```bash
ls photo_[2019-2021]*.jpg
```

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

#### Usando el comando tar

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

#### Usando el comando zip

El comando `zip` nos permite comprimir y descomprimir archivos. Para comprimir archivos usamos la opción `-r` para comprimir recursivamente (carpeta y archivos).

```bash
zip -r [nombreDelArchivo.zip] [archivos]
```

Para descomprimir simplemente usamos el comando `unzip`

```bash
unzip [nombreDelArchivo.zip]
```

### Manejo de Procesos

#### Comando ps

El comando `ps` nos permite ver los procesos que se están ejecutando en nuestra computadora.

```bash
ps
```

#### Comando Kill

El comando `kill` nos permite terminar procesos. Para ello, debemos conocer el id del proceso que queremos terminar. Para obtener el id de un proceso usamos el comando `ps`, obtenemos su id y luego lo pasamos como argumento al comando `kill`.

```bash
kill [idDelProceso]
```

#### Comando top

El comando `top` nos permite ver los procesos que se están ejecutando en nuestra computadora. Además, nos permite ver el uso de recursos de cada proceso.

```bash
top
```

Podemos ver opciones de top presionando la tecla `h`.

#### Comando htop

El comando `htop` es similar al comando `top`, pero con una interfaz más amigable.

```bash
htop
```

### Procesos en foreground y background

Cuando ejecutamos un comando en la terminal, este se ejecuta en foreground. Esto significa que la terminal queda bloqueada hasta que el comando termine de ejecutarse.

Cuando un proceso está en ejecución sin que sea mostrado en la terminal se dice que se está ejecutando en el background. 

A modo de ejemplo, usaremos el comando `cat > file.txt` para escribir en un archivo. Este comando nos permite escribir en un archivo desde la terminal. Ahora utilizaremos `CTRL + Z` para detener el proceso. 

Luego, usaremos el comando `jobs` para ver los procesos que se están ejecutando en background. 

```bash	
jobs
```

Para traer el proceso suspendido al foreground usamos el comando `fg` seguido del número de proceso que queremos traer al foreground.

```bash
fg [numeroDeProceso]
```

#### Otras formas de enviar al background

Podemos enviar un proceso al background agregando el símbolo `&` al final del comando.

```bash
cat > file.txt &
```

Podemos enviar un proceso al background después de haberlo ejecutado. Por ejemplo, podemos ejecutar la interfaz gráfica de chrome con

```bash
google-chrome-stable
```

Luego usamos el comando `CTRL + Z` para detener el proceso y luego usamos el comando `bg` seguido del número de proceso que queremos enviar al background.

```bash
bg [numeroDeProceso]
```

Esto nos permite seguir usando la terminal mientras el proceso se ejecuta en background con normalidad.

### Editores de Texto en la Terminal

Existen 3 editores de texto en la terminal que son muy populares. Estos son `nano`, `vim` y `emacs`.

#### Editor vim

Para abrir un archivo escribimos 

```bash
vim [nombreDelArchivo]
```

Para empezar a escribir presionamos la tecla `i`. Para salir del modo de escritura (inserción) presionamos la tecla `ESC`. Para guardar los cambios presionamos `:w` y para salir presionamos `:q`. Para guardar y salir presionamos `:wq`.

En el modo normal podemos usar `dd` para borrar una línea, `yy` para copiar una línea, `p` para pegar una línea, `u` para deshacer, `CTRL + R` para rehacer. 

En el modo normal `/` nos permite buscar una palabra al igual que en `less`.

### Personalizar la terminal

1. Instalar Tilix

    ```bash
    sudo apt install tilix
    ```

2. Instalar ZSH

    ```bash
    sudo apt install zsh
    ```

3. Instalar Oh My ZSH

4. Personalizar funcionalidades y colores

5. Usar power level
   1. Instalar powerlevel10k
   2. Instalar fonts
   3. Configurar powerlevel10k
      1. Para recongifurar `p10k configure`

## Recursos

* Linux basics for Hackers
* The Linux Command Line
* Grep (O'Reilly)
* Regular Expressions (O'Reilly)
* Linux Pocket Guide (O'Reilly)
* Vi and Vim Editors Pocket Reference (O'Reilly)

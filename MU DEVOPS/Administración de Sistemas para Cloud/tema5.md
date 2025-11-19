Tema 5

Administración básica de sistema operativo en Linux

Administración de Sistemas en la Cloud

Índice

[Esquema 3](#_Toc76983243)

[Ideas clave 4](#_Toc76983244)

[5.1. Introducción y objetivos 4](#_Toc76983245)

[5.2. Sistema de archivos 4](#_Toc76983246)

[5.3. Usuarios y grupos 12](#_Toc76983247)

[5.4. Procesos y servicios 18](#_Toc76983248)

[5.5. Herramientas de sistema 24](#_Toc76983249)

[5.6. Referencias bibliográficas 37](#_Toc76983250)

[A fondo 38](#_Toc76983251)

[Test 39](#_Toc76983252)

Esquema

![Interfaz de usuario gráfica, Texto, Correo electrónico  Descripción generada automáticamente](data:image/jpeg;base64...)

Ideas clave

5.1. Introducción y objetivos

Este tema presentará algunos de los conceptos básicos de la administración de sistemas Linux: sistemas de archivos, usuarios, grupos, etc. Es probable que cualquier instalación de *software* requiera modificaciones y tareas sobre estos objetos. La soltura con la línea de comandos será de ayuda para poder entender los ejemplos de este tema.

Los **objetivos** que se pretenden conseguir son:

* Conocer los fundamentos de los conceptos básicos de Linux que aparecen de manera recurrente en muchas tareas administrativas.
* Aprender a manipular los objetos del sistema operativo para automatizar tareas sobre estos.

A continuación, en el vídeo *Administración de usuarios y procesos en Linux*, se verá una demostración de creación, mantenimiento y borrado de usuarios, asignación de permisos.

![](data:image/jpeg;base64...)

5.2. Sistema de archivos

Se suele decir que cualquier cosa en Linux es un archivo. Los **archivos** normales no son más que un tipo más de archivo y los **directorios** son archivos que contienen los nombres de otros archivos. El comando pwd ofrece información sobre el directorio actual en la consola. El comando cd permite cambiar de directorio.

~$ pwd

/home/ubuntu

~$ cd /var/log

/var/log$

Árbol de directorios

El directorio raíz se identifica por la barra oblicua (/). Este directorio es la base del árbol de directorios. Al contrario que Windows, todo el sistema operativo de **Linux depende de un único árbol.** No hay unidades de disco C: o D:, como en Windows. En Linux, todas las particiones, unidades y almacenamiento se alojan en algún punto bajo la raíz /. El almacenamiento y las unidades externas se «montan» en un directorio. Este directorio aparece como una carpeta más del árbol. Por ejemplo, la ruta /media suele alojan las unidades del CD (disco duro) y las unidades de USB externas, una vez montadas.

El directorio raíz es el inicio de cualquier ruta, o *path*, absoluta. Es posible cambiar de directorio usando **rutas absolutas** desde cualquier directorio. Por ejemplo, cd /var/log funcionará aunque la consola se encuentre en /home/ubuntu. Las **rutas relativas,** sin embargo, no parten de la raíz, sino del directorio en el que se encuentra la consola en ese momento. Si el directorio actual es /var, tanto cd /var/log como cd log cambiarán al mismo directorio. El símbolo «..» (dos puntos) denota el directorio padre al actual, mientras que «.» (un punto) denota al directorio actual. Ambos pueden usarse en rutas relativas.

~ $ cd /var/log

/var/log $ cd log

-bash: cd: log: No such file or directory

/var/log $ cd ..

/var $ cd log

/var/log $ cd ./cups

/var/log/cups $

La mayoría de las distribuciones de Linux siguen un **mismo esquema** de árbol de directorios. Aunque hay diferencias, rutas como /bin, /boot, /etc, /home o /tmp son prácticamente una constante en cualquier Linux. La Tabla 1 lista los directorios habituales de la raíz y su contenido.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 1. Directorios habituales de Linux. Fuente: elaboración propia.

Para examinar el contenido de los directorios, se puede usar el ya conocido comando ls. Ejecutando ls -la en la *home* de un usuario, se obtiene la siguiente información (Figura 1).

![](data:image/png;base64...)

Figura 1. Comando ls en la *home* del usuario. Fuente: elaboración propia.

Tipos de archivos

Los ficheros que comienzan con un punto son archivos ocultos. El comando ls no lo muestra por defecto, a menos que se invoque con el modificador -a. Son archivos normales a todos los efectos. Es habitual que las configuraciones específicas de ciertas aplicaciones se guarden como archivos ocultos en la *home*. Por ejemplo, .viminfo son detalles de vim, mientras que .python\_history guarda el histórico de la *shell* de Python.

La primera columna de detalles muestra información sobre el tipo de archivo y los permisos. El primer carácter de la columna indica el tipo de archivo. La mayoría de los archivos de la Tabla 2 tiene el *flag* de tipo vacío, con un guion (-). Esto significa que son archivos normales. La d significa que son directorios, mientras que la l significa que el archivo es un enlace a otro archivo. La c y la b denotan dispositivos de bloque y de carácter, respectivamente, como los mostrados en la Figura 2. Otros tipos de archivos son los *sockets* (s, también en la Figura 2) y las tuberías (p, de *pipe*).

![](data:image/png;base64...)

Figura 2. Dispositivos como archivos en /dev y *sockets* en /var/run. Fuente: elaboración propia.

Sistema de permisos

Los permisos del archivo se indican con los últimos nueve caracteres de la primera columna. En Linux, los permisos se usan para determinar de qué acceso disponen los usuarios y grupos sobre un archivo. El control de permisos sobre archivos y aplicaciones es crítico para la seguridad y el correcto funcionamiento de un *host*. Un permiso erróneo puede suponer un agujero de seguridad (por ejemplo, si todas las subcarpetas de /home permiten lectura al resto de usuarios en un servidor de FTP) o impedir que un servicio funcione correctamente (por ejemplo, si un servidor Nginx se ejecuta con el usuario www-data, pero la carpeta de archivos estáticos solo permite acceso al usuario root). Los tres permisos principales son:

* Lectura, indicado con el flag r.
* Escritura/edición, indicado con el flag w.
* Ejecución, indicado con el flag x.

![Interfaz de usuario gráfica, Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 3. Columna de tipo de archivo y permisos y su representación binaria y octal. Fuente: elaboración propia.

Como su propio nombre indica, el *flag* de lectura permite leer o ver un archivo normal o leer los nombres, pero no los detalles, del contenido de un directorio. El *flag* de escritura permite hacer cambios sobre un archivo o, si se trata de un directorio, permite crear, borrar y renombrar los ficheros del directorio. El *flag* de ejecución permite, efectivamente, la ejecución de un archivo. Los binarios de /bin deben tener el *flag* activo para que se puedan ejecutar. Un *script*, aunque sea un fichero de texto, puede tener el *flag* activo para poder ejecutarlo. Si el *flag* de ejecución se activa en un directorio, es posible «entrar» dentro del directorio usando el comando cd.

Los *flags* están agrupados en **tres clases:** usuario, grupo y otros. Los permisos de usuario aplican al usuario propietario del grupo. Los permisos de grupo describen los permisos que reciben los usuarios miembros del grupo propietario del archivo. El concepto de grupo propietario puede parecer chocante, pero está muy extendido en entornos Linux. La última clase describe los permisos de cualquier otro usuario.

El formato de los *flags* no es arbitrario, ya que se corresponde con la **representación binaria,** de forma que cada *flag* es un *bit*. Si el permiso está activo, el *bit* estará a uno. Una presentación muy habitual de los permisos es agrupar los tres *bits* de cada clase y mostrar la representación octal de esos *bits*. Así, según muestra la Figura 3, si los tres *flags* están activos, la representación octal de 111 es 7, mientras que, si solo los *flags* de lectura y ejecución están activos, la representación octal de 101 es 5.

Este formato es muy útil para modificar la configuración de permisos de un archivo. El comando que permite cambiar los permisos es chmod y acepta dos sintaxis:

* Clase|activar/desactivar|permiso.
* Representación binaria.

Por ejemplo, dado un archivo con permisos rw-rwx---, es posible activar la ejecución para el usuario propietario, desactivar la ejecución para el grupo y activar la lectura para el resto con los dos comandos siguientes:

chmod u+x,g-x,o+r file

chmod 764 file

En el primer comando, cada permiso individual se activa o desactiva para cada clase. En el segundo comando, se usa la representación binaria de los *flags* para definir todos los permisos de una sola vez. La Figura 4 muestra los permisos antes y después de la ejecución de chmod.

![A screen shot of a clock  Description automatically generated](data:image/png;base64...)

Figura 4. Cambio de permisos en un archivo. Fuente: elaboración propia.

La Tabla 2 muestra algunos ejemplos de permisos junto a su representación en octal.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 2. Ejemplos de permisos habituales en formato octal. Fuente: elaboración propia.

Enlaces

El fichero de la Figura 1con el *flag* l es un enlace*.* Hay dos tipos de enlaces: enlaces fuertes y enlaces débiles o simbólicos. Los **enlaces fuertes,** o *hard links*, son referencias reales al archivo. Si se borran todos los enlaces fuertes a un archivo, el archivo se borra también. Un enlace fuerte solo se puede crear en la misma partición que el archivo al que referencia.

Los **enlaces simbólicos** se pueden borrar sin afectar al fichero al que referencian. Es habitual que los archivos binarios tengan enlaces simbólicos, para poder acceder a ellos con varios nombres o para poder cambiar la versión de un binario sin cambiar el nombre con el que se accede. Por ejemplo, la Figura 5 muestra los ejecutables de Python en la carpeta /usr/bin. La versión instalada de Python es la 3.6, tal como se indica en el binario python3.6. Sin embargo, es posible ejecutarlo tanto con python como con python3. Una actualización a Python 3.8 cambiaría estos enlaces simbólicos, para que apunten al nuevo binario, pero manteniendo los nombres python y python3.

![A screen shot of a monitor  Description automatically generated](data:image/png;base64...)

Figura 5. Enlaces simbólicos. Fuente: elaboración propia.

Los enlaces se crean con el comando ln. Los enlaces serán fuertes por defecto y simbólicos con el *flag* -s. La manera más sencilla de crear un enlace simbólico en la ruta actual es simplemente indicando la ruta del archivo enlazado (ver Figura 6).

![A screen shot of a computer  Description automatically generated](data:image/png;base64...)

Figura 6. Creación de enlace simbólico. Fuente: elaboración propia.

5.3. Usuarios y grupos

Linux es un sistema operativo **multiusuario** (Matotek et al., 2017). Esto significa que permite el inicio de sesión de múltiples usuarios simultáneamente, ya sea por la línea de comandos o en una sesión de escritorio. También hay usuarios específicos para ciertos componentes del sistema operativo. Por ejemplo, el servidor web Nginx suele ejecutarse bajo el usuario nginx o el usuario www-data, según cómo se haya instalado el paquete.

Linux también tiene el concepto de **grupo.** Los usuarios pueden pertenecer a uno o más grupos y suelen agregarse a grupos para dar permisos de acceso a ciertos recursos. Por ejemplo, una carpeta compartida ofrecida en un servidor FTP puede dar acceso a un grupo concreto. Los miembros de ese grupo podrán leer los ficheros, facilitando la labor administrativa.

Por regla general, al crear un usuario, se crea una capeta *home*, típicamente debajo de la ruta /home. Esta carpeta ofrece un lugar en el que los usuarios pueden guardar sus ficheros, además de ser la ubicación por defecto que muchas aplicaciones usan para guardar las configuraciones específicas de cada usuario. Por ejemplo, las claves para las conexiones SSH se guardan en la carpeta ~/.ssh y el histórico de Bash se guarda en ~/.bash\_profile. Efectivamente, el símbolo «~» hace referencia a la carpeta *home* de un usuario, con independencia de la ruta absoluta de la misma. Un usuario Ubuntuque tenga su carpeta en /home/ubuntu podría crear un archivo tanto con touch ~/new\_file como con touch /home/ubuntu/new\_file.

Sudo

El comando sudo permite la ejecución de comandos administrativos a usuarios distintos de root. Las ventajas de Sudo son:

* Incrementa la seguridad.
* Permite más granularidad en el control de comandos administrativos.
* Incorpora auditoría de ejecución.
* Algunas distribuciones deshabilitan el usuario root, por lo que Sudo es la única opción.

Los comandos de creación y modificación de usuarios son ejemplos de comandos administrativos que solo el usuario root puede ejecutar. Las distribuciones que deshabilitan el usuario root habilitan el comando Sudo para todos los comandos para un usuario normal: Ubuntu lo habilita para el usuario que se crea durante la instalación y, en Amazon Linux, es el usuario ec2-user el que tiene permisos.

Para modificar permisos de Sudo, hay que editar el fichero /etc/sudoers con el comando especial visudo. Este comando también necesita privilegios, así que habría que ejecutarlo con sudo visudo. Se abrirá el editor del sistema y se comprobará la sintaxis del fichero. Un fichero /etc/sudoers erróneo impedirá que se puedan ejecutar comandos administrativos y, por tanto, ni siquiera se podrá ejecutar sudo visudo para arreglar el fichero.

Según el contenido de /etc/sudoers de la Figura 7, hay dos formas de dar permisos de Sudo a un usuario:

* Añadiendo el usuario individualmente con una línea nueva, por ejemplo, ubuntu ALL=(ALL:ALL) ALL.
* Añadir el usuario como miembro de un grupo con permisos, como los grupos admin o sudo.

La sintaxis del fichero se puede consultar con man sudoers.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 7. Editor nano tras ejecutar sudo visudo. Fuente: elaboración propia.

Administración de usuarios

El comando useradd permite crear usuarios nuevos. Durante la creación, se especifican el nombre, la descripción (con el *flag* -c), la *shell* por defecto del usuario (con -s) y si se desea crear la *home* del usuario (con -m). El usuario estará desactivado y sin contraseña, que habrá que añadir con el comando passwd. La Figura 8 muestra la creación de un usuario nuevo, la fijación de la contraseña y el inicio de sesión con este nuevo usuario.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 8. Creación de usuario con useradd. Fuente: elaboración propia.

La información del nuevo usuario se almacena en dos ficheros, /etc/passwd y /etc/shadow (Frampton, s. f.). El primero contiene detalles del usuario: nombre de usuario, ID, ID de grupo, ruta de la *home* y ruta de la *shell* por defecto, entre otros.

Los ID son identificadores numéricos. Las utilidades de administración permiten que los usuarios trabajen con nombres de usuario y de grupo, aunque internamente el sistema trabaje con esos identificadores. La ruta de la *home* puede ser inválida (por ejemplo, /nonexistent) si el usuario no dispone de ella. De la misma manera, la ruta de la *shell* puede apuntar a /usr/sbin/nologin: esta es una *shell* especial que impide el inicio de sesión, pero registra el intento de inicio de sesión en los *logs*. Un usuario puede no recibir una *shell* en algunos casos. Un servidor FTP, por ejemplo, puede ofrecer acceso a sus usuarios exclusivamente por FTP, pero no por *shell* (se podría deshabilitar el acceso por SSH completamente, pero esto cierra la puerta al acceso de administradores).

![](data:image/png;base64...)

Figura 9. Fichero /etc/passwd. Fuente: elaboración propia.

El fichero /etc/passwd también contiene la contraseña, aunque, en el ejemplo de la Figura 9, todos los usuarios contienen una x en el campo reservado para la misma. Originalmente, las contraseñas se alojaban en ese campo como un *hash* unidireccional, pero este mecanismo era susceptible a ataques de fuerza bruta, especialmente si el fichero era robado, lo que no era imposible, porque el fichero debía ser legible por todos los usuarios.

Para intentar reducir el riesgo, las contraseñas se movieron a un segundo fichero, /etc/shadow, con un *hash* más complejo. Este fichero, además, solo es legible por el usuario root. La Figura 10 muestra el fichero /etc/shadow del mismo sistema que el fichero /etc/passwd de la Figura 9. Solo los usuarios ubuntu y ubuntu\_new tienen contraseña.

![A screenshot of a computer  Description automatically generated](data:image/png;base64...)

Figura 10. Fichero /etc/shadow. Fuente: elaboración propia.

Administración de grupos

En Linux, cada usuario debe pertenecer al menos a un grupo. La mayoría de las distribuciones crean un nuevo grupo para cada nuevo usuario. Solo este usuario pertenecerá a este grupo, que será el grupo primario del usuario. Los demás grupos de los que sea miembro serán grupos suplementarios. El comando id muestra tanto el ID del usuario como los grupos a los que pertenece. En el siguiente ejemplo, el usuario ubuntu pertenece a ubuntu como grupo principal y a los grupos cdrom y sudo, entre otros, como suplementarios.

$ id ubuntu

uid=1000(ubuntu) gid=1000(ubuntu)

groups=1000(ubuntu),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)

Los grupos suplementarios pueden definirse durante la creación del usuario:

$ sudo useradd -m -G sudo,cdrom ubuntu\_sudo

$ id ubuntu\_sudo

uid=1002(ubuntu\_sudo) gid=1002(ubuntu\_sudo)

groups=1002(ubuntu\_sudo),24(cdrom),27(sudo)

También es posible modificar la membresía de grupos una vez creado el usuario con usermod.

$ sudo usermod -a -G plugdev ubuntu\_sudo

$ id ubuntu\_sudo

uid=1002(ubuntu\_sudo) gid=1002(ubuntu\_sudo)

groups=1002(ubuntu\_sudo),24(cdrom),27(sudo),46(plugdev)

El comando groupadd permite crear grupos, mientras que groupdel los borra.

$ sudo groupadd new\_group

$ sudo usermod -a -G new\_group ubuntu\_sudo

$ id ubuntu\_sudo

uid=1002(ubuntu\_sudo) gid=1002(ubuntu\_sudo)

groups=1002(ubuntu\_sudo),24(cdrom),27(sudo),46(plugdev),1003(new\_group)

$ sudo groupdel new\_group

5.4. Procesos y servicios

Al igual que otros sistemas operativos, en Linux existe el concepto de servicio, también llamado *daemon*. Los **servicios** son procesos que no terminan inmediatamente tras la ejecución, como el comando pwd, sino que se ejecutan continuamente, ofreciendo ciertas funcionalidades al sistema operativo o a los usuarios. Algunos ejemplos de servicios son, por ejemplo, el *daemon* de SSH, cuyo proceso se llama sshd, o el servidor web Apache, cuyo proceso es httpd. El comando ps aux muestra todos los procesos en ejecución, tanto servicios como otros procesos.

![A screen shot of a computer  Description automatically generated](data:image/png;base64...)

Figura 11. Comando ps aux. Fuente: elaboración propia.

La lista en la Figura 11 muestra los procesos ordenados por PID, de *process* ID. El PID se usa para controlar e identificar procesos. El proceso con PID 1, /sbin/init, es el primer proceso que arranca y el que se encarga de arrancar otros procesos. El proceso init era originalmente parte del sistema System-V. La mayoría de las distribuciones usan **Systemd** como gestor de arranque de procesos; en esos casos, el proceso con el PID 1 será /sbin/systemd. Ubuntu ha conservado el nombre del proceso init, aunque utiliza Systemd (Ubuntu usó [Upstart](http://upstart.ubuntu.com/) como gestor hasta la versión 16.04).

El comando top es una herramienta de monitorización interactiva que muestra los procesos en funcionamiento en el equipo. Al contrario que ps, top se actualiza cada pocos segundos. Por defecto, top ordena los procesos por el uso instantáneo del CPU, por lo que los primeros procesos de la lista son los que más cargan el equipo.

![A screenshot of a computer  Description automatically generated](data:image/png;base64...)Figura 12. Comando top durante una ejecución de apt-get update. Fuente: elaboración propia.

Los procesos pueden terminar por sí mismos si terminan su cometido o si sufren un error que provoque que se cierren con un código de salida diferente de 0. En algunos casos, no obstante, es necesario detener los procesos antes de tiempo. La familia de comandos de kill facilitan la tarea de enviar «señales»a los procesos (Van Vugt, 2015). Algunas señales pueden ser ignoradas y, en todo caso, el *software* tiene que estar preparado para atenderlas. Las principales señales se muestran en la Tabla 3.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 3. Señales habituales. Fuente: elaboración propia.

El comando kill envía una señal a un proceso a partir del PID. Es necesario conocer el PID, que es fácil de obtener a partir de ps. Por ejemplo, en la Figura 13, se muestra el PID de un proceso top al que se envía la señal SIGKILL.

![A close up of a screen  Description automatically generated](data:image/png;base64...)

Figura 13. Comando kill sobre un proceso top. Fuente: elaboración propia.

Se puede hacer uso de la sustitución al vuelo de comandos de Bash para obtener el PID del proceso con pidof e insertarlo en kill en una sola línea:

$ sudo kill -9 `pidof top`

El comando killall es un poco más cómodo de usar para un usuario, ya que permite especificar el nombre del proceso. Como su nombre indica, killall terminará todos los procesos con ese nombre. También permite especificar un usuario, por lo que terminará los procesos de ese usuario. Si el usuario ha iniciado una sesión interactiva, killall terminará también el proceso de consola y, por tanto, terminará la sesión del usuario.

$ killall -u username

$ killall -r httpd

Finalmente, pkill permite terminar procesos con el nombre del proceso. Es también capaz de terminar los procesos hijos de un proceso padre con el *flag* -P.

$ pkill -P pid

Los servicios se pueden administrar como procesos con el comando kill, pero es posible usar la funcionalidad de Systemd para obtener más información. La utilidad systemctl permite arrancar, parar, recargar y obtener información de los servicios arrancados con Systemd. Por ejemplo, para el servicio de SSH, systemctl muestra la información que se encuentra en la Figura 14.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 14. Información del servicio SSH con systemctl. Fuente: elaboración propia.

El campo *loaded*, en la segunda línea, indica el fichero utilizado para arrancar el servicio. Este *unit file* no es el binario como tal, sino un fichero de configuración de Systemd que indica, entre otras cosas, condiciones de ejecución, la ruta al binario con los *flags* necesarios para el arranque y ficheros con variables de entorno. El fichero de Systemd de sshd se muestra a continuación.

$ cat /lib/systemd/system/ssh.service

[Unit]

Description=OpenBSD Secure Shell server

After=network.target auditd.service

ConditionPathExists=!/etc/ssh/sshd\_not\_to\_be\_run

[Service]

EnvironmentFile=-/etc/default/ssh

ExecStartPre=/usr/sbin/sshd -t

ExecStart=/usr/sbin/sshd -D $SSHD\_OPTS

ExecReload=/usr/sbin/sshd -t

ExecReload=/bin/kill -HUP $MAINPID

KillMode=process

Restart=on-failure

RestartPreventExitStatus=255

Type=notify

RuntimeDirectory=sshd

RuntimeDirectoryMode=0755

[Install]

WantedBy=multi-user.target

Alias=sshd.service

Estos ficheros son editables por un administrador y es posible definir ficheros propios para configurar aplicaciones propias como servicios.

La información provista por systemctl va más allá. Indica también el estado del servicio, active (running) en este caso. El estado puede ser inactive (dead) si se ha parado el servicio o failed, con el código de salida, si el proceso terminó de manera abrupta. Además, las últimas líneas del fichero de *log* se incluyen en la salida de systemctl status, lo que puede ser útil si el proceso ha detectado un error antes de detenerse.

Además de ofrecer información, systemctl permite arrancar y parar los servicios con systemctl start y systemctl stop. La Figura 15 muestra ejemplos de ambos comandos. Es necesario identificar el servicio con el nombre y el servicio no siempre tiene el mismo nombre que el proceso que ejecuta. Es posible listar todos los servicios en ejecución filtrando la salida de systemctl con grep running, como en la Figura 16, o todos los servicios habilitados (que pueden no estar en ejecución si se han parado manualmente o si han fallado) con grep enabled.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 15. Arranque y parada de servicios con systemctl. Fuente: elaboración propia.

![A close up of a screen  Description automatically generated](data:image/png;base64...)

Figura 16. Servicios en ejecución con systemctl. Fuente: elaboración propia.

5.5. Herramientas de sistema

Una tarea habitual de los administradores es controlar el rendimiento del sistema. Algunos de los parámetros habituales son el uso del CPU, memoria, uso de *swap* y espacio libre del disco duro. Las siguientes secciones presentan algunas herramientas de Linux para monitorizar estas métricas.

*Top*

El comando top muestra los comandos con más uso del CPU, ordenados en orden descendente de uso, junto con otras métricas, como uso de memoria, *swap*, etc. La pantalla de *top* se actualiza cada cinco segundos, por defecto, y tendrá un aspecto similar a la Figura 17.

![A close up of a screen  Description automatically generated](data:image/png;base64...)

Figura 17. Comando top en un sistema de escritorio. Fuente: elaboración propia.

Las primeras líneas muestran un resumen de información del sistema, en este orden:

* Hora actual, *uptime* del sistema, número de usuarios que han iniciado sesión y la carga media del CPU durante el último minuto, últimos cinco minutos y últimos quince minutos.
* Número total de procesos y el número en cada estado.
* Uso del CPU y porcentaje del CPU dedicado a procesos de usuario, a procesos del núcleo del sistema y sin uso.
* Uso de memoria física: total, libre y en uso, en *bytes*.
* Uso de memoria virtual: espacio total de *swap*, libre y en uso.

A continuación, la tabla lista los procesos, ordenados por uso de CPU. Es posible cambiar los campos que se muestran, el orden y los campos de resumen. Por ejemplo, para ordenar los procesos por uso de memoria, habría que pulsar f para entrar en el menú de la Figura 18, seleccionar %MEM, pulsar s para ordenar por ese campo y pulsar q para volver a la pantalla de top. También se podrían añadir nuevas columnas, seleccionándolas y pulsando d.

![Interfaz de usuario gráfica, Texto  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 18. Configuración de columnas de top. Fuente: elaboración propia.

La Tabla 4 lista los campos habituales de top y su descripción.

![Interfaz de usuario gráfica, Texto, Aplicación, Correo electrónico  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 4. Columnas habituales de top. Fuente: elaboración propia.

*Uptime*

El comando uptime muestra por consola un resumen del estado del sistema: la hora actual, el tiempo que el sistema ha estado arrancado, el número de usuarios conectados y el uso medio del CPU en el último minuto, últimos cinco minutos y últimos quince minutos.

$ uptime

23:32:56 up 37 min, 2 users, load average: 0.00, 0.00, 0.05

*Vmstat*

El comando vmstat ofrece un resumen de métricas de rendimiento en intervalos definidos por el usuario. En vez de actualizar los valores en la consola, como top, imprime los valores de las métricas en una línea periódicamente. El ejemplo de la Figura 19 imprime las métricas cada cinco segundos, hasta un máximo de ocho. Las columnas están organizadas en categorías. La descripción de cada columna se detalla en la Tabla 6.

![A screen shot of a computer  Description automatically generated](data:image/png;base64...)

Figura 19. Comando vmstat. Fuente: elaboración propia.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 5. Columnas de vmstat. Fuente: elaboración propia.

*Df*

El comando df muestra el espacio disponible en los sistemas de ficheros montados. En la Figura 20 se muestra la salida de df en una instalación de Ubuntu con escritorio. El modificador -h imprime los valores en unidades más legibles para un usuario, como KB, MB, etc.

![A screen shot of a computer  Description automatically generated](data:image/png;base64...)

Figura 20. Comando df -h. Fuente. Elaboración propia.

Directorio /proc

En la sección del sistema de ficheros, se mencionó que el directorio /proc es un directorio especial, ya que contiene archivos con información del sistema operativo. De hecho, no solo se puede obtener información, sino que es posible cambiar los parámetros del núcleo de Linux editando los archivos contenidos de /proc, modificando así el comportamiento del sistema.

El sistema de archivos /proc no es un directorio real en el disco duro, sino una colección de estructuras de datos en la memoria, administrada por el núcleo, que aparece como un conjunto de directorios y archivos. El propósito de /proc (también llamado **sistema de archivos de procesos**) es ofrecer acceso a la información sobre el sistema operativo y sobre todos los procesos que se encuentran en ejecución.

Los archivos de /proc son accesibles, como cualquier otro, pero es necesario conocer el significado y la sintaxis de ellos para interpretar la información. Por ejemplo, los comandos cat o less mostrarán el contenido de los archivos y ls muestra una lista con los archivos disponibles.

![A close up of a screen  Description automatically generated](data:image/png;base64...)

Figura 21. Listado de archivos de /proc. Fuente: elaboración propia.

El primer conjunto de directorios (indicado por el *flag* d en la salida de ls -l /proc o en diferente color en la Figura 21) representa los procesos que se ejecutan actualmente en su sistema. Cada directorio que corresponde a un proceso tiene el PID como nombre. Los archivos de cada directorio contienen información sobre el proceso: el binario, la línea de comandos con la que se ha ejecutado, las variables de entorno, uso de memoria, etc. La Figura 22 muestra algunos de estos ficheros para el proceso de un servidor FTP.

![A screenshot of a computer  Description automatically generated](data:image/png;base64...)

Figura 22. Detalles del proceso del servidor FTP. Fuente: elaboración propia.

Otro archivo interesante es /proc/cpuinfo. Este contiene las características de los procesadores del equipo: fabricante, modelo, conjuntos de instrucciones, frecuencia, etc.

# cat /proc/cpuinfo

processor : 0

vendor\_id : GenuineIntel

cpu family : 6

model : 158

model name : Intel(R) Core(TM) i7-7820HQ CPU @ 2.90GHz

stepping : 9

cpu MHz : 2903.998

cache size : 8192 KB

physical id : 0

siblings : 1

core id : 0

cpu cores : 1

apicid : 0

initial apicid : 0

fpu : yes

fpu\_exception : yes

cpuid level : 22

wp : yes

flags : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 syscall nx rdtscp lm constant\_tsc rep\_good nopl xtopology nonstop\_tsc cpuid pni pclmulqdq monitor ssse3 cx16 sse4\_1 sse4\_2 x2apic movbe popcnt aes xsave avx rdrand hypervisor lahf\_lm abm 3dnowprefetch pti avx2 rdseed clflushopt

bugs : cpu\_meltdown spectre\_v1 spectre\_v2 spec\_store\_bypass

bogomips : 5807.99

clflush size : 64

cache\_alignment : 64

address sizes : 39 bits physical, 48 bits virtual

power management:

La Tabla 6 describe algunos de los archivos y directorios de /proc.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 6. Algunos ficheros y directorios de /proc. Fuente: elaboración propia.

Programación de tareas

Ciertos programas de Linux no están pensados para ejecutarse continuamente como un servicio, pero es necesario ejecutarlos en un instante futuro dado o periódicamente. Algunas de estas tareas pueden ser copia de seguridad, análisis de *logs* o descarga de grandes ficheros (por ejemplo, ficheros de actualización o sincronización de *mirrors*) en horario nocturno.

El comando **at** programa comandos para su ejecución en un momento dado. El servicio atd se encarga de ejecutar los comandos programados con at. Estos trabajos se ejecutarán en el momento indicado, tras lo cual at los borrará de la lista. Los pasos para programar un trabajo son los siguientes:

* Ejecutar at <tiempo>. El formato para indicar el instante es muy versátil y acepta formatos como:
  + at 21:30.
  + at now.
  + at now + 15 minutes.
  + at now + 4 hours.
  + at noon.
  + at now next hour (dentro de 60 minutos).
  + at now next day (a la misma hora del día siguiente).
  + at 17:00 tomorrow.
  + at 3:00 Jan 18, 2021.
* Se abrirá una *shell* de at en la que se introducen los comandos, uno por línea.
* Para cerrar la consola de at, hay que pulsar Ctrl+D, una vez escritos los comandos.

![A screenshot of a computer screen  Description automatically generated](data:image/png;base64...)

Figura 23. Programación de comandos con at. Fuente: elaboración propia.

La Figura 23 muestra cómo se añaden dos comandos para su ejecución a las 3:00 a. m. del día siguiente. La lista de trabajos programados se puede consultar con atq y se pueden borrar con atrm <id>.

$ atq

3 Mon May 11 03:00:00 2020 a root

2 Sun May 10 21:31:00 2020 a root

Este comando no permite, sin embargo, programar tareas que se ejecuten periódicamente de manera automática. Para ello, se puede usar el servicio **cron** y el comando **crontab**. *Cron* no permite trabajos con más de un comando, pero siempre se puede escribir un *script* con los comandos necesarios. El servicio comprueba los trabajos disponibles cada minuto y ejecuta los que deban ejecutarse en ese momento.

Los pasos para programar un trabajo de cron son:

* Preparar el *script* o el comando que se ejecutará.
* Preparar un archivo de texto con la programación y el comando. El archivo puede contener más de una tarea, cada una con su programación.
* Ejecutar crontab <fichero> para confirmar la definición.
* Confirmar que el trabajo está definido con crontab -l.

El formato de definición de tareas es el siguiente:

5 0 \* \* \* ps aux > /tmp/$(date +%Y%M%d$h%m)-ps.log

Las cinco primeras columnas de la línea definen la programación: cada campo representa una unidad temporal y el valor indica en qué momento se «activa» ese campo. Cada campo puede contener un número, una lista de números separadas por comas, una pareja de números con un guion representando un intervalo o un asterisco, que indica todos los valores posibles. La Tabla 7 lista la unidad y los posibles valores de cada campo.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 7. Campos de la programación de cron. Fuente: elaboración propia.

Este sistema puede parecer complicado, así que la Tabla 8 tiene ejemplos de cómo interpretar la sintaxis.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 8. Ejemplos de cron. Fuente: elaboración propia.

Cuando un usuario ejecuta crontab -l, el comando solo muestra los trabajos programados por él mismo. Por ejemplo, si el usuario root define el trabajo del ejemplo, su listado de trabajo sería el siguiente:

$ crontab -l

5 0 \* \* \* ps aux > /tmp/$(date +%Y%M%d$h%m)-ps.log

Es decir, exactamente el contenido del fichero con el que se ha definido el trabajo. Sin embargo, el fichero /etc/crontab contiene la programación de trabajos de sistema. Por ejemplo, en un equipo Ubuntu, el fichero /etc/crontab por defecto contiene lo siguiente:

$ cat /etc/crontab

SHELL=/bin/sh

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user command

17 \* \* \* \* root cd / && run-parts --report /etc/cron.hourly

25 6 \* \* \* root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )

47 6 \* \* 7 root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )

52 6 1 \* \* root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )

Además de unas variables de entorno que se aplicarán a cada uno de los trabajos, el fichero contiene cuatro trabajos, que corresponden con tareas horarias, diarias, semanales y mensuales. El comando run-parts ejecutará los *scripts* contenidos en cada una de las carpetas /etc/cron.\*, siguiendo la programación del fichero crontab. Los servicios de sistema pueden aprovechar esta funcionalidad para añadir *scripts* recurrentes en estas carpetas y así delegar la ejecución periódica a cron. Por ejemplo, en la Figura 24, se muestran las tareas diarias. Una de ellas, /etc/cron.daily/passwd, crea copias de seguridad de los ficheros de las cuentas de usuario y grupo en la carpeta /var/backup.

![A screen shot of a computer  Description automatically generated](data:image/png;base64...)

Figura 24. Tareas diarias en /etc/cron.daily. Fuente: elaboración propia.

5.6. Referencias bibliográficas

Frampton, S. (s. f.). 6.6. Linux Password & Shadow File Formats. En *Linux Administration Made Easy*.

<https://www.tldp.org/LDP/lame/LAME/linux-admin-made-easy/shadow-file-formats.html>

Matotek, D., Turnbull, J. y Lieverdink, P. (2017). *Pro Linux System Administration: Learn to Build Systems for Your Business Using Free and Open Source Software* (2. ª ed.). Apress.

Página de Upstart (<http://upstart.ubuntu.com/>).

Van Vugt, S. (2015). *Beginning the Linux Command Line* (2. ª ed.). Apress.

A fondo

*Rethinking PID 1*

Pid Eins. (s. f.). *Rethinking PID 1.* <http://0pointer.de/blog/projects/systemd.html>

Este artículo ofrece una crítica al porqué de Systemd. Es muy técnico, pero la lectura abarca conceptos complejos con un enfoque manejable, incluso para administradores con poca experiencia en Linux.

*Kill Signals and Commands*

Linux.org. (s. f.). *Kill Signals and Commands*. <https://www.linux.org/threads/kill-signals-and-commands-revised.11625/>

Este corto artículo repasa las señales disponibles en Linux, su significado y las diferentes formas de utilizarlas. Es más una guía de uso que un artículo, ya que es eminentemente práctico.

*Filesystem Hierarchy Standard*

LSB Workgroup, The Linux Foundation. (2015). *Filesystem Hierarchy Standard*. <https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html>

El estándar del árbol de directorio de Linux, editado por un grupo de trabajo específico, es una lectura densa y solo recomendable para desarrolladores del *kernel* y afines. No obstante, los capítulos de introducción sirven de pistas para entender el porqué de esta arquitectura, antes de entrar en los detalles profundos del diseño y la implementación.

Test

1. ¿Qué comando sirve para solicitar una terminación programada de un proceso?

A. kill -15 <pid>.

B. kill -9 <pid>.

C. kill -15 <nombre>.

D. Ninguna de las anteriores.

1. ¿Qué tipos de permisos tendrá un archivo normal tras configurarlo con chmod 777 filename?

A. Lectura y escritura para el usuario propietario, nada más.

B. Lectura, escritura y ejecución para cualquier usuario del sistema.

C. Lectura para cualquier usuario, escritura y ejecución para el propietario.

D. Ninguna de las anteriores.

1. ¿Qué comando permitenaveriguar el PID de un proceso?

A. pidof.

B. ps.

C. top.

D. Todos los anteriores.

1. ¿Qué relación hay entre usuarios y grupos?

A. Los usuarios pueden pertenecer a un único grupo.

B. Los usuarios pertenecen al menos a un grupo principal y a cero o más grupos suplementarios.

C. Los usuarios pueden no pertenecer a un grupo o pueden pertenecer a uno o más grupos.

D. Los grupos puede agrupar otros grupos, pero no usuarios.

1. ¿Qué opción del comando systemctl reinicia un servicio?

A. restart.

B. stop.

C. status.

D. start.

1. ¿Qué fichero aloja las contraseñas de los usuarios en texto plano?

A. /etc/passwd.

B. /etc/shadow.

C. Todos los anteriores.

D. Ninguno de los anteriores.

1. ¿Cuál es el resultado de ejecutar ln -s /usr/bin/python3.6 ~/python?

A. Aparece un enlace simbólico al binario de Python en la *home* del usuario con el nombre python.

B. Aparece un enlace simbólico al binario de Python en la *home* del usuario con el nombre python3.6.

C. Aparece un enlace fuerte al binario de Python en la *home* del usuario con el nombre python.

D. Aparece un enlace simbólico al binario de Python en la raíz del árbol de directorios con el nombre python.

1. ¿Qué comandos permiten crear, modificar y borrar usuarios?

A. usercreate, usermodify y userdelete.

B. usercreate, usermod y deluser.

C. useradd, moduser y rmuser.

D. useradd, usermod y userdel.

1. ¿Por qué visudo ha de ejecutarse con sudo?

A. Por convenio.

B. No es necesario.

C. Porque es un comando privilegiado.

D. Puede no usarse si no se edita el fichero.

1. ¿Qué *flag* denota un archivo oculto?

A. d.

B. l.

C. Ninguno.

D. s.
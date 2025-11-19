Tema nº 4

Packer: compilación

de imágenes

Herramientas DevOps

Índice

[Esquema 3](#_Toc52771670)

[Ideas clave 4](#_Toc52771671)

[4.1. Introducción y objetivos 4](#_Toc52771672)

[4.2. Casos de uso 4](#_Toc52771673)

[4.3 Instalación 6](#_Toc52771674)

[4.4. Conceptos y nomenclaturas 8](#_Toc52771675)

[4.5. Comandos 10](#_Toc52771676)

[4.6 Templates 15](#_Toc52771677)

[4.7 Configuración de templates 24](#_Toc52771678)

[4.8. Trabajo con Packer 25](#_Toc52771679)

[4.9 Conclusiones 26](#_Toc52771680)

[4.10 Referencias bibliográficas 28](#_Toc52771681)

[A fondo 29](#_Toc52771682)

[Actividades 31](#_Toc52771683)

[Test 32](#_Toc52771684)

Esquema

![](data:image/png;base64...)

Ideas clave

4.1. Introducción y objetivos

Packer es una **herramienta que se utiliza para generar imágenes**. Las imágenes son un fichero binario que determina los contenidos iniciales (en disco) de una máquina virtual u otros entornos. Las imágenes contienen todos los elementos que les componen al momento de su creación, si bien casi todos los proveedores en la nube pueden proporcionar contenido extra después.

Packer facilita la creación de imágenes y automatización del proceso, lo que la convierte en una herramienta muy útil para DevOps. Además de automatizar el proceso, Packer **permite crear la misma imagen para distintos proveedores *cloud****,* lo que reduce el «*vendor lock-in*», y facilita el cambio de proveedor en la nube en el futuro.

4.2. Casos de uso

Packer se centra en la creación de imágenes. Sin embargo, debido a su facilidad para crear imágenes de forma rápida y reproducible establece varios **casos de uso diferentes.**

* **Aceleración de los despliegues.** Debido a que crea imágenes con la mayoría del software preinstalado, se aceleran los despliegues de nuevos entornos o la creación de nuevas instancias.

Esto permite, por una parte, disminuir el tiempo que tardamos en autoescalar, y por otra, acelerar las pruebas de integración por el rápido despliegue del entorno de pruebas.

* **Infraestructura inmutable.** Las operaciones de nuestros automatismos pueden situarse en dos fases durante el despliegue de una instancia o máquina virtual. Una de las fases es la preparación de la imagen, la otra es la configuración de la instancia.

Habitualmente, los errores que acontecen durante la creación de la imagen son menos urgentes ya que en el peor de los casos podemos utilizar la imagen anterior si la tenemos almacenada. Si una instancia falla por cualquier motivo es muy fácil desplegar otra que tome el relevo y destruir o guardar la anterior dependiendo de si queremos investigar que ocurrió.

* **Integración continua.** Packer es liviano, portátil y se controla por línea de comandos. Esto la convierte en la herramienta perfecta para ponerla en el canal de entrega continua. Packer se puede usar para generar nuevas imágenes de máquina para múltiples plataformas en cada cambio a Chef/Puppet.

Como parte de este canal o *pipeline*, las imágenes recién creadas pueden luego lanzarse y probarse, para verificar que los cambios en la infraestructura funcionan. Si las pruebas pasan, puedes estar seguro de que la imagen funcionará cuando se implemente. Esto brinda un nuevo nivel de estabilidad y capacidad de prueba a los cambios de infraestructura.

* **Entornos de desarrollo locales.** Packer ayuda a mantener el desarrollo, la puesta en escena y la producción de la forma más similar posible. Packer se puede utilizar para generar imágenes para múltiples plataformas al mismo tiempo. Un ejemplo clásico es crear imágenes tanto para el proveedor de *cloud* (AWS, Azure, Google, etc.) como para VirtualBox o VMware.

Esto permite utilizar una máquina virtual local para el desarrollo con una imagen igual o muy similar a la de producción. Si asociamos este hecho con el caso de uso anterior, veremos que se puede obtener un sistema bastante “elegante” para entornos de trabajo consistentes, desde el desarrollo y hasta producción.

* **Creación de *appliance*s.** Dado que Packer crea imágenes consistentes para múltiples plataformas en paralelo, es una herramienta perfecta para crear dispositivos y demos de productos desechables. A medida que tu software cambia, puedes crear dispositivos de forma automática con el software preinstalado.

Por tanto, podemos decir que puede utilizarse tanto para compartir demos como para crear una nueva oferta como **«*appliance*»** de un servicio tradicionalmente SaaS (software como servicio). Esto es frecuentemente un requisito de negocio, ya que permite vender a entornos que no pueden utilizar servicios en la nube.

4.3 Instalación

Packer primero debe instalarse en la máquina en la que deseas ejecutarlo. Para facilitar la instalación, Packer se distribuye como un paquete binario para todas las plataformas y arquitecturas compatibles. Es posible compilar Packer desde el código fuente ya que es código abierto, pero no es lo recomendado.

* **Windows**

Si utilizas Chocolatey, simplemente ejecuta:

choco install packer

Suele tener la última versión.

* **macOS**

Si utilizas Homebrew, puedes simplemente ejecutar:

$ brew install packer

* **Desde fichero compilado (Linux y los anteriores)**

Para instalar Packer, primero encuentra el paquete apropiado para tu sistema y descárgalo. Packer está empaquetado como un archivo ZIP.

A continuación, descomprime el paquete descargado en el directorio donde se instalará Packer. En los sistemas Unix, ~ /bin/packer o /usr/local/packer generalmente son buenos, dependiendo de si deseas restringir la instalación solo a tu usuario o instalarla en todo el sistema. En sistemas Windows, puedes colocarlo donde desees.

Después de descomprimir el paquete, el directorio debe contener un único programa binario llamado Packer. El último paso para la instalación es asegurarse de que el directorio donde se ha instalado Packer esté en la PATH.

**MacOS y Linux**

Consulta la siguiente página para obtener instrucciones sobre cómo configurar PATH https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux- unix

**Windows**

La siguiente página contiene instrucciones para configurar PATH en Windows: https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on- windows

Comprueba la instalación

Para comprobar que está correctamente instalado, ejecuta el comando packer. La salida debe ser algo similar a lo que figura a continuación:

$ packer

usage: packer [‐‐version] [‐‐help] <command> [<args>]

Available commands are:

build build image(s) from template

fix fixes templates from old versions of packer inspect see components of a template

push push template files to a Packer build service validate check that a template is valid

version Prints the Packer version

Comprueba la versión instalada. Esta guía debería ser compatible con versiones superiores a 1.0 pero es conveniente utilizar una de las últimas versiones a no ser que requieras algo más antiguo por algún motivo.

4.4. Conceptos y nomenclaturas

Antes de empezar con Packer es conveniente revisar los conceptos principales. Esta no es una herramienta compleja ya que tiene un único propósito: crear imágenes. Para describir cómo queremos que sean las imágenes utilizaremos uno o varios de estos conceptos.

* ***Artifacts***: los artefactos son el resultado de una compilación o ejecución única, y generalmente son un conjunto de ID o archivos que representan una imagen de la máquina. Cada constructor (*builder*) produce un solo artefacto. Como ejemplo, en el caso del constructor de Amazon EC2, el artefacto es un conjunto de AMI (uno por región). Las AMI son identificadores únicos para las imágenes. Para el constructor VMware, el artefacto es un directorio de archivos que incluye la máquina virtual creada. En general, los artefactos son las imágenes y otras salidas deseadas de Packer.
* ***Builds*:** las compilaciones son una tarea única que finalmente produce una imagen, normalmente para una sola plataforma. Varias versiones se ejecutan en paralelo. En general, cuando se ejecuta Packer se realizarán una serie de compilaciones independientes en paralelo, que pueden requerir múltiples pasos.
* ***Builder*:** los constructores son componentes de Packer que pueden crear una imagen de máquina para una plataforma específica. Los constructores leen una configuración y la usan para ejecutar y generar una imagen de máquina. Un constructor se invoca como parte de una compilación (*build*) para crear las imágenes deseadas. Los constructores de ejemplo incluyen a VirtualBox, VMware y Amazon EC2; y se pueden crear y agregar a Packer mediante complementos externos.
* ***Commands***: los comandos son subcomandos para el programa Packer que realizan algún trabajo. Un ejemplo de comando es *build,* que se llama ejecutando packer build. Como hemos dicho anteriormente, Packer incluye una serie comandos que definen su interfaz de línea de comandos.
* ***Provisioners***: los aprovisionadores son componentes de Packer que instalan y configuran el software dentro de una máquina en funcionamiento antes de que esta se convierta en una imagen estática. Su trabajo principal es el de lograr que la imagen contenga el software deseado. Los proveedores de ejemplo incluyen scripts de Shell, Chef, Puppet, etc. De este trabajo que realizan los *provisioners* surgirán las ventajas de rendimiento (si se han hecho instalaciones costosas) o el código que hará que la instancia se configure así misma de forma automática.
* ***Post-processors***: los posprocesadores son componentes de Packer que toman el resultado de un constructor u otro posprocesador y lo procesan para crear un nuevo artefacto. Como ejemplos de posprocesadores podemos nombrar la compresión de artefactos mediante compress, subir dicha compresión a un servidor para almacenarla mediante *upload*, etc.
* ***Templates****:* los templates son archivos JSON que definen una o más compilaciones (*builds*) configurando todos los componentes de Packer como los aprovisionadores y los compiladores. Packer puede leer una *template* y usar su información para crear múltiples imágenes de máquina en paralelo.

Un ejemplo de template es el siguiente:

{

"builders": [

{

"type": "amazon‐ebs", "access\_key": "...",

"secret\_key": "...", "region": "us‐east‐1", "source\_ami": "ami‐fce3c696", "instance\_type": "t2.micro", "ssh\_username": "ubuntu",

"ami\_name": "packer {{timestamp}}"

}

],

"provisioners": [

{

"type": "shell",

"script": "setup\_things.sh"

}

]

}

4.5. Comandos

Antes de describir más a fondo a las *templates* conviene familiarizarse con los subcomandos de Packer. Estos se controlan a través de una interfaz de línea de comandos. Toda la interacción se realiza mediante el comando packer. Al igual que muchas otras herramientas de línea de comandos, la herramienta packer necesita un subcomando para ejecutarse, y ese subcomando también puede tener opciones adicionales. Los subcomandos se ejecutan con packer SUBCOMMAND, donde «SUBCOMMAND» es el comando real que desea ejecutar.

Si ejecutamos Packer vemos los subcomandos disponibles:

$ packer

Usage: packer [‐‐version] [‐‐help] <command> [<args>]

Available commands are:

build build image(s) from template

fix fixes templates from old versions of packer inspect see components of a template

push push a template and supporting files to a Packer build service

validate check that a template is valid

version Prints the Packer version

Como es habitual en muchos comandos, usar ‐h en alguno de los subcomandos trae la ayuda de ese subcomando:

$ packer build ‐h

Usage: packer build [options] TEMPLATE

Will execute multiple builds in parallel as defined in the template. The various artifacts created by the template will be outputted.

Options:

‐color=false Disable color output (on by default)

‐debug Debug mode enabled for builds

‐except=foo,bar,baz Build all builds other than these

‐only=foo,bar,baz Build only the specified builds

‐force Force a build to continue if artifacts exist, deletes existing artifacts

‐machine‐readable Machine‐readable output

‐on‐error=[cleanup|abort|ask] If the build fails do: clean up (default), abort, or ask

‐parallel=false Disable parallelization (on by default)

‐var 'key=value' Variable for templates, can be used multiple times.

‐var‐file=path JSON file containing user variables.

Output para *scripts*

Por defecto, Packer se ejecuta de una forma muy cómoda para los usuarios; utiliza un buen formato (espaciado) y colores. Además, admite una configuración de salida totalmente legible por máquina, lo que permite usar Packer en entornos automatizados, algo que resulta esencial en una herramienta DevOps.

El formato de salida es compatible con comandos clásicos de UNIX como awk / sed / grep / cut / etc. Para habilitar la salida de máquina, simplemente hay que usar el flag ‐ machine‐readable. Por ejemplo, el subcomando version devolverá algo similar a esto:

$ packer -machine-readable version

1586421620,,version,1.5.5

1586421620,,version-prelease,

1586421620,,version-commit,0b7dd74+CHANGES

1586421620,,ui,say,Packer v1.5.5

Formato de la salida para scripts

El formato legible por máquina es un formato de texto delimitado por comas, orientado a la línea. Esto hace que sea más conveniente de analizar usando herramientas estándar de Unix como awk o grep, además de los lenguajes de programación completos como Ruby o Python.

El formato es:

fecha,compilación,tipo,datos

A continuación, una breve explicación de cada uno de ellos:

* fecha. La fecha es un *«timestamp»* de Unix partiendo de UTC. Es decir, el número de segundos desde EPOC.
* compilación. La compilación indica cuál de las compilaciones que puedan estar ejecutándose en paralelo está generando el mensaje. El campo está vacío si es un mensaje global como en el ejemplo anterior.
* tipo. El tipo de mensaje suele indicar el formato de los datos que siguen a continuación y el tipo de evento que ha ocurrido.
* datos. Los datos son una lista de valores separados por comas. Los tipos y cantidad vienen determinados por el tipo anterior. Las comas en los datos se reemplazan por %!. Los saltos de línea por \n o \r, dependiendo de su formato original.

El subcomando build

El comando de packer build toma una *template* y ejecuta todas las compilaciones dentro de ella para generar un conjunto de artefactos. Las diversas construcciones especificadas dentro de una template se ejecutan en paralelo, a menos que se especifique lo contrario; y los artefactos que se crean se mostrarán al final de la compilación.

Algunas opciones relevantes son:

* ‐debug: deshabilita la paralelización y muestra más información para depurar. En muchos casos los constructores van parando y tienes que pulsar para continuar, para que puedas inspeccionar los pasos intermedios (como la máquina virtual antes de que se genere la imagen). Es útil si la imagen no funciona como se esperaba.
* ‐only=compilacion: construye solo las compilaciones indicadas (separadas por comas). Esto es muy útil cuando añadimos nuevos aprovisionadores y queremos probarlos hasta que funcionen correctamente.
* ‐except=compilacion: construye todas las compilaciones salvo los indicados (separados por comas).
* **‐on‐error={opcion}:** por defecto la opción es cleanup, pero otros valores son abort, ask. El valor por defecto es el recomendado para entornos de integración continua pero cuando estamos depurando o probando localmente puede ser útil poner ask o abort para poder inspeccionar los ficheros temporales.

El subcomando *validate*

El comando packer validate se usa para validar la sintaxis y la configuración de una *template*. El comando devolverá un estado de salida cero en caso de éxito y un estado de salida distinto de cero en caso de error. Además, si una *template* no se valida, se generará un mensaje de error. Este comando resulta útil para hacer comprobaciones rápidas de una *template* y encontrar pequeños defectos sin ejecutar. También resulta de interés en entornos de integración continua para hacer una primera prueba sin llegar a generar nada a modo de test unitario.

El subcomando inspect

El comando de packer inspect toma una *template* y genera los diversos componentes que la definen. Esto puede ayudarte a aprender rápidamente sobre estas sin tener que sumergirte en el JSON. El comando te dirá cosas como qué variables acepta la *template,* los constructores y proveedores que define, y el orden en que se ejecutarán. Es útil cuando se tienen múltiples *templates* de Packer en una empresa y no recordamos los párametros o proveedores que tenía una *template* en particular. Es recomendable utilizarlo antes de empezar a leer la *template* para tener una visión general.

Otros comandos

El subcomando fix permite migrar templates antiguas para ser compatibles con nuevas versiones. Si comenzamos a utilizar Packer recientemente no es tan necesario, ya que los templates no cambian tanto como antes, pero es útil saber que existe.

El subcomando push ya no es útil ya que la web Atlas va a cerrar en poco tiempo. La alternativa es crear la imagen directamente en la nube que queramos (AMI en AWS por ejemplo) o utilizar un posprocesador para subir la imagen generada a un servicio de almacenamiento como puede ser S3.

4.6 Templates

Las *templates* o plantillas son el principal componente de Packer con el que vamos a interactuar. Son archivos JSON que configuran los diversos componentes de Packer para crear una o más imágenes de máquina. Tanto usuarios como programas pueden leer, escribir y editar fácilmente las *templates*. Esto tiene el beneficio de poder no solo crear y modificar templates a mano, sino también escribir *scripts* para crear o modificar templates dinámicamente. Debido a que son archivos de texto, son muy convenientes porque pueden subirse a repositorios de versiones y trabajar con ellos con un sistema de integración continua si los modificamos a menudo, o al menos conservar un histórico de versiones. Por último diremos que las *templates*  son usadas por comandos como packer build, que ya vimos anteriormente.

Estructura de una *template*

Es un objeto JSON que tiene un conjunto de claves que configura varios componentes de Packer.

(Las claves disponibles dentro de una *template* se enumeran a continuación.)

Solo los builders son requeridos, las claves restantes son opcionales.

Sección *builders*

La sección builders de una *template* es requerida, y es la base de la *template* de Packer. Se compone de una lista con los constructores que queremos que Packer use para generar nuestros artefactos.

La documentación de Packer contiene una lista de todos los constructores, aunque en este tema hablaremos de los más comunes. <https://www.packer.io/docs/builders/index.html>

Los constructores son los responsables de crear máquinas y generar imágenes de ellas para diversas plataformas. Por ejemplo, hay constructores independientes para EC2, VMware, VirtualBox, etc. Packer viene con muchos constructores por defecto, y también se puede ampliar esta lista para agregar constructores nuevos.

Primero veremos las características principales de un constructor y luego veremos las opciones de algunos como ejemplo.

En una template, una **sección de definiciones de constructores** es algo similar a esto:

{

"builders": [

{

"type": "amazon‐ebs",

"access\_key": "...",

"secret\_key": "..."

}

]

}

Cada uno de los *builders* contiene una definición que se corresponde con una compilación (build) específica. La definición de un *build* requiere al menos una clave type que configura qué tipo de constructor se usará para la imagen y definirá el resto de parámetros aceptados y requeridos. En el ejemplo anterior, vemos que amazon‐ebs acepta dos parámetros, access\_key y secret\_key. Estos parámetros los usaran los constructores para poder crear los artefactos.

Cada build en Packer tiene un nombre. Por defecto el nombre es el type, pero podemos definir un nombre específico mediante la clave name. Esto es útil cuando queremos crear varias imágenes con el mismo builder, por ejemplo, cuando subimos la misma imagen a varias cuentas que no se comparten.

Otra clave importante es comunicator. Un comunicador es el mecanismo utilizado para conectarse dentro del builder y poder configurar elementos dentro de la máquina virtual. También hemos de decir que los aprovisionadores lo utilizan para conectar. Dependiendo del builder, el valor por defecto será uno u otro. Los más comunes son:

* ssh: Se utilizará una conexión SSH para conectar con la máquina. Es el valor por defecto más común y el más usado para máquinas Linux.
* winrm: Se utilizará una conexión WinRM. Es la más utilizada para máquinas Windows.

También existe un comunicador none que se puede usar si no vamos a conectar con la máquina. Algunos builders tienen comunicadores especiales, pero en muchos casos ya vienen configurados por defecto y no les tenemos que prestar atención.

Tanto ssh como winrm tiene múltiples opciones que se pueden utilizar, siendo los más comunes las credenciales para conectar con la máquina y, en algunos casos, la configuración de un bastión de salto por si tenemos restricciones para conectar a la máquina directamente.

Sección provisioners

La sección de aprovisionadores **contiene una lista de todos los aprovisionadores que Packer usará para instalar y configurar la máquina**. Son opcionales, aunque altamente utilizados y es poco común que no estén.

Estos se ejecutan en el orden en el que están definidos. Un ejemplo de **definición de aprovisonador** es este:

{

"provisioners": [

{

"type": "shell",

"script": "install.sh"

}

]

}

La sección provisioners incluye una lista de cada uno de los aprovisionadores. Cada aprovisionador es un objeto JSON con al menos la clave type. Habitualmente se usan más claves para configurar el aprovisionador.

Otro parámetro común es only, que recibe una lista con los builds sobre los que aplica el aprovisionador (el nombre o el tipo). Es frecuente tener alguna pequeña diferencia en la imagen base utilizada por cada build o algún requisito especial de alguno de los entornos. Por ejemplo, los servidores desde los que bajar paquetes podrían ser distintos si tenemos una caché local.

Otra clave común es override. Esta recibe un objeto que contiene como claves los diferentes builds y permite realizar pequeños cambios en los entornos. Es particularmente común en los primeros aprovisionadores ya que las imágenes base pueden ser distintas y se requieren algunos pasos para hacerlas más parecidas.

Una última clave común es pause\_before, que recibe un *string* con una definición de tiempo. Un caso de ejemplo es esperar a que un servicio recién instalado arranque completamente. Habitualmente se expresa en segundos, por ejemplo:

{

"type": "shell",

"script": "install.sh",

"pause\_before": "30s"

}

Aprovisionadores comunes

Veremos a continuación un resumen de los aprovisionadores más comunes:

* file: permite añadir ficheros. Muy utilizado para subir ficheros de configuración y para indicar la versión del software que se quiere utilizar. Se pueden subir ficheros individuales o directorios. En caso de que desees subir ficheros generados durante la ejecución de Packer, créalos en un directorio temporal y sube los contenidos del directorio.

Un ejemplo:

{

"type": "file",

"source": "custom.conf",

"destination": "/etc/nginx/conf.d/custom.conf"

}

* shell: permite ejecutar scripts en la máquina que se está creando. Se puede ejecutar una lista de comandos con la opción inline, un script con script o varios scripts con scripts.

Un ejemplo de varios aprovisionadores comunes incluyendo uno ejecutado con sudo

sería:

{

"provisioners": [

{

"type": "shell",

"inline": [

"sudo apt‐get install ‐y git",

"ssh‐keyscan github.com >> ~/.ssh/known\_hosts",

"git clone git@github.com:exampleorg/myprivaterepo.git"

]

},

{

"type": "shell",

"script": "install.sh",

"execute\_command": "echo 'packer' | sudo ‐S sh ‐c '{{ .Vars }} {{ .Path }}'",

"pause\_before": "30s"

},

{

"type": "shell",

"script": "configure.sh"

}

]

}

Para más opciones y casos comunes puedes revisar la siguiente documentación: [https://www.packer.io/docs/provisioners/shell.html](http://www.packer.io/docs/provisioners/shell.html)

* **shell‐local**: permite ejecutar un comando en la máquina local, en lugar de en la máquina que se está creando. Es particularmente útil para crear pequeños ficheros locales o modificar y comprimir algo de contenido antes de enviarlo.
* powershell: sus casos de uso son similares a los de Shell pero para Windows.
* windows‐restart: es bastante frecuente tener que reiniciar Windows para aplicar algún cambio y terminar alguna instalación. Este aprovisionador se encarga de ello.
* Muchos sistemas de gestión de la configuración como Ansible, Chef, Puppet, Salt y Converge tienen aprovisionadores para Packer. Esto permite utilizar las herramientas si los *scripts* empiezan a ser muy complicados, para hacer más fácil la reusabilidad o, si ya tenemos las configuraciones creadas, nos permite reusarlas. Esta situación es muy frecuente cuando migramos algunos sistemas de configuración, durante el despliegue, a imágenes inmutables.

Sección *post‐processors*

La sección de posprocesador dentro de una *template* configura cualquier procesamiento posterior que se realice a las imágenes creadas por los constructores. Algunos ejemplos de posprocesamiento serían la compresión de archivos o la subida de artefactos a servicios de almacenamiento.

**Los posprocesadores son opcionales**. Por lo tanto, si no se definen dentro de una *template*, no se realizará el procesamiento posterior de la imagen. El artefacto resultante de una construcción es solo la imagen generada por el constructor. En algunos casos los posprocesadores no son tan comunes, pero para sistemas de virtualización locales como VMWare y Virtualbox son de gran utilidad para almacenar la imagen y comprimirla.

Un ejemplo de configuración de postprocesado sería:

{

"post‐processors": [

"compress"

]

}

Si necesitamos pasar parámetros al posprocesador, en lugar de indicar type como cadena de texto podemos poner un objeto como ponemos a continuación:

{

"post‐processors": [

{

"type": "compress",

"format": "tar.gz"

}

]

}

Los coprocesadores no ejecutan en un orden definido. Para poner más de un posprocesador donde cada uno ejecuta un paso para generar el artefacto final, es necesario utilizar un posprocesador de lista. Esto se hace sustituyendo el posprocesador individual con una lista de los posprocesadores en orden de ejecución. Los resultados intermedios son ignorados. Un ejemplo de este caso de uso es:

{

"post‐processors": [

[

"compress",

{

"type": "upload",

"endpoint": "http://storage.unir.net"

}

]

]

}

Es decir, si queremos almacenar artefactos en dos lugares distintos, usaremos dos posprocesadores en la lista de post‐processors. Si lo que queremos es comprimir y luego subir a un único lugar, usaremos un único elemento de tipo lista en la sección que incluirá dos posprocesadores dentro como en el ejemplo anterior.

Una opción muy común es only. Esta opción permite solo aplicar un postprocessor sobre unos constructores específicos. Por ejemplo, podemos solo subir las imágenes de VirtualBox e ignorar las AMI generadas para AWS.

{

"type": "upload",

"endpoint": "http://storage.unir.net",

"only": [

"virtualbox‐iso"

]

}

Otra opción que resulta muy útil en algunos casos es keep\_input\_artifact, que por defecto está desactivada. Si indicamos true nos permitirá almacenar la entrada de un posprocesador. Por ejemplo, se puede usar para guardar una copia local del artefacto que se sube mediante un posprocesador de subida como vagrant‐cloud, googlecompute‐ export o shell‐local. shell‐local.

Tiene múltiples usos, pero uno habitual es el de subir la imagen a un servidor ftp local o para hacer una copia a un directorio remoto montado en el sistema de ficheros.

Secciones variables

La sección variables permite aumentar la portabilidad de las *templates* y mantener credenciales fuera de estas (y de nuestro sistema de control de versiones). Un ejemplo es:

{

"variables": {

"aws\_access\_key": "{{ env `AWS\_ACCESS\_KEY` }}",

"aws\_secret\_key": ""

},

"builders": [

{

"type": "amazon‐ebs",

"access\_key": "{{user `aws\_access\_key`}}",

"secret\_key": "{{user `aws\_secret\_key`}}"

// ...

}

]

}

En este ejemplo una de las variables viene por defecto del entorno (mediante env) mientras que solo la otra está definida. Veremos cómo funciona la parametrización de *templates* en la siguiente sección, pero podemos ver que usan {{ }} para delimitar donde aplican.

Para pasar las variables a Packer, se utiliza el parámetro ‐var al llamar a packer build. Un ejemplo sería packer build ‐var 'aws\_access\_key=foo' ‐var 'aws\_secret\_key=bar' packer‐env.json. Las variables también se pueden pasar desde un fichero mediante ‐var‐file.

Para más información, accede al siguiente link: [https://www.packer.io/docs/templates/user-variables.html](http://www.packer.io/docs/templates/user-variables.html)

4.7 Configuración de templates

Las *templates* **se pueden configurar usando interpolación de variables y otras funciones**. Esto permite que las templates sean más sencillas de mantener y que tengan muchas más capacidades.

La sintaxis utilizada para esto son las **llaves dobles** {{ }}. Las funciones se llaman poniéndolas entre llaves {{ timestamp }}. Las variables se prefijan por . y en mayúsculas, por ejemplo: {{ .Variable }} La función user permite acceder a las variables de entrada definidas en la sección variables.

En la siguiente fuente podrás ver más funciones soportadas <https://www.packer.io/docs/templates/engine.html#functions>

Las más frecuentes son:

* template\_dir: devuelve el directorio del template.
* timestamp: muestra el tiempo actual, como un *timestamp* de Unix.
* isotime: muestra la fecha actual con el formado dado.
* uuid: es un ID aleatorio con el formato de UUID, lo que hace prácticamente imposible una colisión.
* user: sustituye por una variable de usuario
* build\_name: es el nombre del build que está ejecutándose.
* clean\_ami\_name: limpia el nombre de caracteres ilegales en AMI
* lean\_image\_name: limpia el nombre de caracteres ilegales en Google Compute y otras nubes.

Se puede acceder a las variables de entrada mediante user. Además de las variables de entrada, Packer incluye muchas más variables que se obtienen durante la ejecución. Los constructores, aprovisionadores y otros componentes pueden proveer variables adicionales.

4.8. Trabajo con Packer

Packer es una herramienta con un caso de uso muy concreto pero muy potente. Para crear *templates*, lo ideal es empezar con un constructor concreto y configurarlo hasta que genere una imagen sin configurar. Si es necesario, podemos probar los posprocesadores y comprobar si funcionan. Durante el resto del desarrollo podemos comentarlos para que no se apliquen, de modo que sea más sencillo y rápido iterar, y ya los tendremos hechos y probados. Una vez hecho esto, empezaremos a crear los aprovisionadores. Si ya tenemos creados los *scripts* el proceso será sencillo. Si no tenemos *scripts* ni otro sistema de configuración como Ansible, debemos empezar por ahí. Una opción es ejecutar packer build ‐‐debug y parar antes del bloque de aprovisionamiento. Una vez hecho esto, nos podemos conectar a la máquina e interactivamente probar los comandos hasta confeccionar el *script* que deseamos.

Para mantener y gestionar *templates*, los comandos packer validate y packer inspect son muy útiles para entender y revisar el template sin necesidad de hacer una compilación, lo que ahorra mucho tiempo. El parámetro ‐debug es extremadamente útil si hemos hecho cambios y no han funcionado correctamente.

Una buena práctica, si mantenemos imágenes con constructores de varios tipos, es añadir un constructor que podamos ejecutar localmente lo que nos permitirá trabajar más rápido y nos reportará un menor coste. Esto no siempre es posible y el coste de mantenimiento se puede disparar si el entorno local es completamente distinto.

La herramienta packer se acopla muy bien con nuestro sistema de integración continua. Un ejemplo de ello sería crear una imagen, que desplegaremos en nuestro sistema de producción, después desplegarla y ejecutar nuestros *tests* de regresión contra esa instancia. Esto nos permitirá detectar no solo errores de código, sino también errores de configuración y posibles regresiones de paquetes en nuestra distribución.

4.9 Conclusiones

Las imágenes de la máquina «precocidas» tienen muchas ventajas, pero la mayoría no ha podido beneficiarse de ellas por la dificultad que presentaban a la hora de crearlas y gestionarlas. Tampoco había herramientas para automatizar la creación de imágenes de máquina o tenían una curva de aprendizaje demasiado alta. El resultado es que, antes de Packer, la creación de imágenes de máquinas amenazaba la agilidad de los equipos de operaciones y, por lo tanto, no se utilizaba, a pesar de los enormes beneficios que reportan.

Packer ha cambiado este paradigma: es fácil de usar y automatiza la creación de cualquier tipo de imagen de máquina. Dentro de sus capacidades también se incluye la gestión de la configuración, ya que fomenta el uso de un marco como Chef, Puppet o Ansible para instalar y configurar el software dentro de las imágenes.

En otras palabras: Packer trae imágenes «precocinadas» a la era moderna, desbloqueando el potencial que aún estaba sin explotar y creando nuevas oportunidades.

Las ventajas más destacadas de Packer son:

» **Implementación de infraestructura súper rápida.**

Las imágenes de empaquetador permiten ejecutar máquinas completamente aprovisionadas y configuradas en cuestión de segundos, en lugar de varios minutos u horas. Esto no solo beneficia la producción, sino también el desarrollo, ya que las máquinas virtuales de desarrollo también se pueden iniciar en segundos, sin esperar un tiempo de aprovisionamiento típicamente mucho más largo.

» **Portabilidad de proveedores múltiples**.

Debido a que Packer crea imágenes idénticas para múltiples plataformas, puede ejecutar la producción en AWS, puesta en escena/QA en una nube privada como OpenStack y desarrollo en soluciones de virtualización de escritorio como VMware o VirtualBox. Cada entorno ejecuta una imagen de máquina idéntica, brindando la máxima portabilidad.

» **Estabilidad mejorada.**

Packer instala y configura todo el software para una máquina en el momento en que se construye la imagen. Si hay errores en estos *scripts*, se detectarán de forma inmediata, en lugar de varios minutos después del lanzamiento.

» **Mayor capacidad de prueba**. Después de construir una imagen de máquina, la imagen de la máquina puede iniciarse rápidamente y ser probada para verificar que todo funcione. Si todo ha ido bien, puedes estar seguro de que cualquier otra máquina lanzada desde esa imagen funcionará correctamente.

4.10 Referencias bibliográficas

Turnbull, J. (2017). *The Packer Book.* Turnbull Press.

HashiCorp. (s. f.). Documentation. Packer by HashiCorp.

Recuperado el 5 de enero de 2020 de: <https://www.packer.io/docs>

A fondo

*Creación de imagen de Packer con Ubuntu 20.04 para nubes privadas*

Automating Ubuntu 20.04 installs with Packer

<https://nickcharlton.net/posts/automating-ubuntu-2004-installs-with-packer.html>

Ubuntu ha cambiado en su versión 20.04 el instalador dejando de ser el mismo de Debian. Esto permite ficheros de Packer para nube privada algo más sencillos. Este recurso es un buen ejemplo para aprender más sobre esto.

*Creación de una imagen de Packer con Debian*

Unnatended install for Debian <https://www.packer.io/guides/automatic-operating-system-installs/preseed_ubuntu/>

Un ejemplo con una explicación sobre como usar Preseed files. Es un patrón muy utilizado en Debian, Ubuntu antes de 20.04 y similar a otras distribuciones. Es una lectura interesante.

*Creación de imágenes para varias nubes*

Parallel Builds <https://www.packer.io/intro/getting-started/parallel-builds/>

Packer como hemos visto permite construir en paralelo mediante varios builders. En este recurso, podemos ver un ejemplo práctico de creación de una imagen igual en varias nubes distintas en paralelo. Es un buen ejemplo si necesitamos distribuir appliances para varias nubes.

*The Packer Book*

The Packer Book <https://packerbook.com/>

Probablemente el siguiente punto a leer después de haber estudiado completamente la documentación oficial. Combina bien con un libro del mismo autor sobre Terraform. Probablemente lo más destacable sería estudiar y entender los capítulos sobre integración continua y integración con sistemas con configuración. Es útil si queremos extender Packer también.

Test

1. ¿Qué es Packer?
   1. Una herramienta de despliegue de infraestructura
   2. Una herramienta de monitorización
   3. Una metodología de componentes inmutables
   4. \*Una herramienta de creación de imagenes (Packer es una herramienta para la creación de imágenes Open Source que soporta múltiples nubes y sistemas de virtualización)
2. ¿Es posible crear una imagen para varias nubes con Packer?
   1. No, ya que Packer solo soporta un sistema de virtualización
   2. Sí, pero siempre mediante distintos ficheros de Template
   3. Sí, usando los provisioner
   4. \*Si, usando los *builders* (Los *builders* definen donde se va a crear la imagen y es posible especificar más de uno)
3. ¿Soporta Packer las variables?
   1. \*Si, existe una sección de variables en el fichero de *template* (Las variables en *packer* se declaran en la sección variables del fichero de *template* en formato *json*)
   2. No, Packer no puede parametrizarse
   3. Sí, se puede poner cualquier variable que deseemos sin declararla
   4. No, ya que Packer varía en cada ejecución
4. ¿Qué son los *comunicators*?
   1. \*C y D son correctas (Los communicators son diferentes formas de que los provisioners se conecten durante la creación de imagen y se especifican en el builder)
   2. Depende del contexto, pero no son un concepto de Packer
   3. Definen la forma en la que los *provisioners* se pueden conectar
   4. Se definen asociados a un *builder*
5. ¿Qué hace el flag -parallel?
   1. \*Permite que cada builder se ejecute en paralelo, pero los provisioners se ejecutaran en orden (Por defecto los builders se ejecutan en paralelo y este flag hace que se ejecuten en serie. Los provisioners siempre se ejecutan en serie)
   2. Permite que los *provisioners* se ejecuten en paralelo
   3. Permite que tanto los *builders* como los *provisioners* se ejecuten en paralelo
   4. Activa el flag parallel ya que el valor por defecto es false
6. ¿Que hace el flag -only?
   1. Hace que solo se ejecute uno de los *provisioners*
   2. Hace que solo se ejecute uno de los *post-processors*
   3. \*Hace que solo se ejecute uno de los *builders* (El flag only afecta a los builders y permite varios valores separados por comas)
   4. Solo puede recibir un único valor
7. La opción -on-error…:
   1. Con el valor *abort* permite que cuando haya un error podamos mirar los ficheros temporales
   2. Con el valor *ask* nos pregunta que queremos hacer
   3. Con el valor *cleanup* limpia todos los datos temporales
   4. \*Todas las otras respuestas son correctas (La opción -on-error puede tomar los valores cleanup, abort y ask)
8. Las variables en Packer se pasan mediante:
   1. \*La B y la C (Tanto -var como -var-file estan soportadas en Packer)
   2. El parámetro -var
   3. El parámetro -var-file, dando un json con las variables
   4. El parámetro -with
9. Si queremos cambiar un fichero además de enviarlo podemos...:
   1. Ejecutar un provisioner local-shell para cambiarlo y luego subirlo con file
   2. Ejecutar un provisioner file y luego cambiarlo en el sistema de destino con shell
   3. Ejecutar un sistema de configuración tipo Ansible, Chef o Puppet
   4. \*Todas las otras respuestas son correctas (Las anteriores opciones permiten modificar el fichero y que acabe en el sistema de destino)
10. Las variables en Packer...:
    1. Solo las variables de entorno están disponibles
    2. Solo las variables de línea de comando están disponibles
    3. Los *providers* no pueden proveer variables adicionales
    4. \*Ninguna de las otras respuestas es correcta (Existen muchos tipos de variables como las provistas por los *providers,* las de línea de comandos, las de entorno y además muchas incluidas por Packer por defecto)
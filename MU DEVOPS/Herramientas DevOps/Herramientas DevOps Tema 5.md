Tema nº 5

Terraform: Infraestructura como código

Herramientas DevOps

Índice

[Esquema 3](#_Toc40557936)

[Ideas clave 4](#_Toc40557937)

[5.1. Introducción y objetivos 4](#_Toc40557938)

[5.2. ¿Qué es Terraform? 4](#_Toc40557939)

[5.3 Configuración y guía de ejemplo 10](#_Toc40557940)

[5.4 Primer despliegue de infraestructura 12](#_Toc40557941)

[5.5 Cambios en la infraestructura 19](#_Toc40557942)

[5.6. Conclusiones 28](#_Toc40557943)

[5.7. Referencias bibliográficas 29](#_Toc40557944)

[A fondo 30](#_Toc40557945)

[Actividades 32](#_Toc40557946)

[Test 33](#_Toc40557947)

Esquema

![](data:image/png;base64...)

Ideas clave

5.1. Introducción y objetivos

Terraform es una herramienta utilizada para gestionar despliegues en diferentes entornos. Su foco no es el ciclo de vida del código de una aplicación individual, sino de toda la infraestructura alrededor de ella.

En este tema se pretenden conseguir los siguientes objetivos:

* Conocer y explorar la herramienta Terraform;
* Completar la instalación y configuración de Terraform;
* Realizar el primer despliegue de Terraform;
* Aprender a cómo aplicar cambios sobre la infraestructura.

En el tema siguiente profundizaremos en las funciones más avanzadas de Terraform para coordinar despliegues más complejos y conocer sus definiciones de una forma más académica.

5.2. ¿Qué es Terraform?

Terraform es una herramienta que se utiliza para la construcción, el cambio y el versionado de infraestructura, de manera segura y eficiente. Esta puede administrar tanto servicios existentes como nubes públicas o soluciones internas personalizadas.

Los archivos de configuración indican a Terraform cuáles son los componentes necesarios para el despliegue desde una única aplicación o bien, desde el centro de datos completo. Terraform genera un plan de ejecución con una descripción completa sobre aquello que hará para alcanzar el estado deseado, y a continuación lo ejecuta para que la infraestructura descrita pueda ser construida. Terraform tiene la capacidad de determinar qué ha cambiado, a medida que las modificaciones tienen lugar, y además, elaborar planes de ejecución incrementales para que posteriormente se ejecuten.

La infraestructura que Terraform puede administrar incluye componentes de bajo nivel como instancias de cómputo, almacenamiento y redes, así como componentes de alto nivel tales como entradas de DNS, funciones de SaaS, etc. Como sabemos, es posible gestionar el propio código de una aplicación, pero el ciclo de vida del código de una aplicación suele ser más complejo y por ello es conveniente usar otras herramientas además de Terraform.

Características clave de Terraform

Veremos a continuación las características fundamentales que hacen de Terraform una herramienta altamente eficaz:

* **Infraestructura como código.** La infraestructura se describe utilizando una sintaxis de configuración de alto nivel. Esto permite que un plano (*blueprint*) del centro de datos pueda ser versionado y tratado como cualquier otro código. Además, la infraestructura se puede compartir y reutilizar.
* **Planificación de la ejecución.** En el paso de «planificación» Terraform genera un plan de ejecución. Este plan muestra qué hará Terraform cuando ejecute la llamada a apply. De esta manera es posible anticipar cualquier movimiento inesperado mientras Terraform manipula la infraestructura.
* **Grafo de recursos.** Terraform crea un grafo de todos los recursos y paraleliza la creación y modificación de cualquier recurso no dependiente. Por eso podemos decir que Terraform construye la infraestructura de la manera más eficiente posible, a la vez que ofrece una visión de las dependencias en su infraestructura.
* **Automatización de cambios.** Es posible añadir conjuntos de cambios complejos a la infraestructura sin apenas realizar trabajo manual. Esto es debido al plan de ejecución y el grafo de recursos que hemos visto antes, que aportan información exacta sobre qué cambiará Terraform y en qué orden lo hará. Como es de esperar, esto evita errores humanos y agiliza el trabajo de forma considerable.

Casos de uso

Terraform tiene muchos casos de uso. Debido a su naturaleza extensible, se puede utilizar Terraform para manipular muchos recursos. Resulta importante juzgar para cuales casos de uso conviene usar Terraform dependiendo de la escala, la frecuencia de cambio y el tiempo que nos llevará documentar la configuración frente a la opción de automatizarla.

* **Aplicaciones multicapa.** Un patrón muy común es la arquitectura *N-tier*. La arquitectura de 2 niveles más común es un conjunto de servidores web que utilizan un nivel de base de datos. Se agregan niveles adicionales para los servidores API, almacenamiento en caché de servidores, servidores de trabajo asíncrono, etc.

**El motivo por el cual se utiliza este patrón** **es que los niveles se pueden escalar de forma independiente, característica que permite hacer frente a la separación de intereses** (del inglés *separation of concerns*). Además, las arquitecturas multicapa suelen ser muy sencillas de entender porque las capas generan un orden natural y ayudan a entender las dependencias.

Terraform es una buena herramienta para administrar estas infraestructuras: cada nivel puede ser descrito como una colección de recursos, y las dependencias entre cada nivel se pueden gestionar de forma automática. Terraform asegurará que el nivel de la base de datos esté disponible antes de que los servidores web se inicien y, a su vez, que los equilibradores de carga conozcan los nodos web. Cada nivel puede ser escalado con Terraform de forma sencilla, modificando un valor de configuración de recuento único o, creando desde Terraform, entornos de escalado automático. Debido a que la creación y el aprovisionamiento de recursos está codificado y automatizado, la escala elástica con carga se vuelve trivial.

* **Autoservicio de clusters.** A medida que una organización adquiere un mayor tamaño, los equipos de operaciones experimentan un enorme desafío a la hora de administrar la infraestructura.

Con el fin de facilitar la gestión de tareas del área de operaciones, lo más acertado es crear una infraestructura **«autoservicio»**. De esta forma, los equipos podrán administrar su propia infraestructura a través del uso de herramientas proporcionadas por el equipo de operaciones. Terraform permite que la construcción y el escalado de un servicio pueda ser codificado en una configuración. Es posible compartir estas configuraciones dentro de una organización, y ello hace que los equipos de clientes puedan usar la configuración como una caja negra y se valgan de Terraform para administrar sus servicios.

Este tipo de caso de uso **funciona muy bien con arquitecturas de microservicios,** donde las capas de caché y la persistencia están distribuidas y gestionadas por equipos pequeños. Resulta de vital importancia respetar las buenas prácticas y ayudar a crear y mantener esas piezas.

* **Entornos desechables.** En casi toda organización constituye una práctica común contar con un entorno de producción y otro de preproducción o control de calidad. Estos últimos son clones más pequeños del entorno de producción, y se utilizan para estudiar y analizar el comportamiento de las aplicaciones antes de que pasen a producción.

Según el entorno de producción se hace más grande y complejo, aumenta la complejidad para mantener los entornos de preproducción sincronizados. Entender las diferencias entre los entornos de producción y preproducción también se vuelve esencial. Terraform resulta útil en estos casos para que, una vez codificado el entorno de producción, pueda compartirse con QA, preproducción o desarrollo. Estas configuraciones se pueden usar para desplegar rápidamente nuevos entornos de prueba y eliminarlos fácilmente cuando ya no hacen falta. Se pueden crear entornos específicos para medir la *performance* de grandes cambios antes de pasar a producción o incluso a preproducción. Terraform ayuda a mantener entornos paralelos, que se pueden crear y destruir elásticamente.

* **Redes definidas por software.** La red definida por software (SDN) es cada vez más frecuente, especialmente en entornos *cloud,* pero también en *datacenters* y nubes privadas, ya que proporciona más control a operaciones y desarrollo; y permite a la red soportar mejor las aplicaciones que se ejecutan en la parte superior. Es común que en la mayor parte de las SDN las implementaciones tengan, por una parte, una capa de control y por la otra, una capa de infraestructura.

Terraform se puede utilizar para codificar la configuración de redes definidas por software. Esta definición puede ser utilizada por Terraform para configurar y modificar automáticamente las propiedades de los objetos mediante la interfaz con la capa de control. Como es de esperar, también permite que la configuración sea versionada y puedan realizarse los cambios pertinentes para implementar la automatización. Tal es el caso de AWS VPC, una de las implementaciones SDN más populares entre los usuarios, que puede ser configurada por Terraform.

En algunos casos estas redes pueden ser parte esencial de los entornos de preproducción y producción, pero en otros casos pueden describir otras partes compartidas y de infraestructura.

* **Aprovisionamiento de Programadores de recursos.** La asignación estática de aplicaciones a máquinas representa un verdadero desafío en infraestructuras a gran escala. Para dar solución a este problema, existen planificadores como Kubernetes, Mesos y YARN. Estos se utilizan para programar dinámicamente contenedores Docker, Hadoop, Spark y muchos otros programas y herramientas.

Esto permite que Terraform se use en capas: para configurar la infraestructura física y aprovisionar entornos como Kubernetes o Mesos y luego desplegar parte de la infraestructura en ellos. Dependiendo de la nube, desplegar Kubernetes mediante Terraform puede ser una buena decisión. Veremos más sobre Kubernetes y Docker en la asignatura Contenedores de este Máster.

* **Despliegue multinube**. La estrategia de diseminar la infraestructura a través de múltiples nubes con el fin de aumentar la tolerancia a los fallos resulta muy atractiva. El hecho de utilizar únicamente una región o un proveedor de nube, hace que la tolerancia a los fallos esté limitada por la disponibilidad de ese proveedor. Por tanto, tener una implementación de múltiples nubes permite una recuperación más elegante de la pérdida de una región o proveedor completo.

También nos permite evitar el temido *«vendor lock-in»* por estar atados a un único proveedor. Usar una herramienta como Terraform en lugar de otras específicas de *provider* como CloudFormation o Azure Resource Manager Templates nos permite desplegar recursos en otras nubes sin cambiar nuestro flujo de despliegue y gestión del cambio.

Las implementaciones en múltiples nubes pueden convertirse en un verdadero desafío debido a que muchas herramientas existentes para la gestión de la infraestructura son específicas de la nube. Sin embargo, Terraform facilita este trabajo, porque permite que a través de una única configuración se pueda para administrar a múltiples proveedores, y también gestionar dependencias entre nubes. Esta característica de Terraform simplifica en gran medida la gestión y la orquestación, y ayuda al departamento de operaciones en la construcción de infraestructuras de nubes múltiples a gran escala.

Usos con otras herramientas

**Terraform no controla la configuración dentro de las propias máquinas.** Por ello es conveniente combinarlo con herramientas (gestores de la configuración) como Chef, Puppet y Ansible para configurar el software de las propias máquinas virtuales.

Mencionaremos brevemente cómo lanzar dichas herramientas desde Terraform, ya que son ampliamente utilizadas y hablaremos de ellas en detalle en el Máster.

Para gestionar entornos con multitud de contenedores en máquinas virtuales se hace necesario aprovisionar entornos como Kubernetes, Spark o Mesos (gestores de contenedores y entornos de ejecución), Terraform es, sin dudas, una buena herramienta para aprovisionar estos entornos.

5.3 Configuración y guía de ejemplo

Terraform es una herramienta compleja con muchas funcionalidades y posibles configuraciones.

En la siguiente sección haremos un ejemplo básico de configuración y despliegue en AWS. Para ello, usaremos la cuenta que se ha creado anteriormente en el Máster. **Algunos de los ejemplos despliegan recursos, por lo que recomendamos eliminarlos después de usarlos y comprobar que no quede nada para que no consuman demasiados recursos gratuitos.**

Instalación de Terraform

Terraform consiste en un binario que ejecuta la tarea y, una vez terminado, detiene la ejecución. Terraform no requiere de un servidor para mantener y gestionar los cambios, siendo muy sencillo de mantener.

Para usos de mayor escala, es interesante usarlo desde servidores, pero para los objetivos de este curso lo ejecutaremos localmente. Terraform se distribuye como un paquete binario para todas las plataformas y arquitecturas compatibles.

A la hora de instalar Terraform, **es necesario que busques el paquete adecuado para tu sistema operativo antes de realizar la descarga**. Verás que Terraform está empaquetado como un archivo .zip; una vez lo descargues, deberás descomprimir, el paquete. Cualquier otro archivo en el paquete que no sea el binario llamado Terraform puede ser eliminado, y esto no afectará al funcionamiento de Terraform.

Es posible que haya métodos alternativos para instalarlo dependiendo de la plataforma, como Chocolatey (Windows), Homebrew (MacOS), Apt-Get (Debian) o Yum (Fedora). Es más sencillo utilizar estos sistemas, pero comprueba la versión antes de instalarlo. La versión utilizada en esta guía es la 0.11.

Hay una nueva versión de Terraform que aún no es estable (la 0.12) que ofrece varios cambios importantes a la herramienta. La mayoría de los conceptos no cambian, pero sí algunos casos de la sintaxis de los ficheros de configuración y la integración con los *providers*. Iremos mencionando algunos de estos cambios cuando ocurran, pero no afectan demasiado al uso diario de la herramienta.

El último paso en la instalación es asegurarte de que el binario terraform esté disponible en la PATH. Esto depende de la plataforma.

Otra alternativa es usar Docker para desplegar. Hablaremos más de Docker durante el Máster, pero su uso es más avanzado y algo más complicado, así que no recomendamos usarlo para seguir este tutorial.

Verificación de la instalación

Una vez hayas instalado Terraform, deberás verificar que la instalación ha funcionado correctamente abriendo una nueva sesión de terminal para comprobar que Terraform está disponible. Al hacer la ejecución deberías ver resultados similares a estos:

$ terraform

Usage: terraform [‐‐version] [‐‐help] <command> [args]

The available commands for execution are listed below.

The most common, useful commands are shown first, followed by less common or more advanced commands. If you're just getting started with Terraform, stick with the common commands. For the

other commands, please read the help and docs before usage.

Common commands:

apply Builds or changes infrastructure

console Interactive console for Terraform interpolations # ...

Si el entorno PATH no se ha configurado correctamente, aparecerá un error que indica que Terraform no se pudo encontrar. En ese caso, regresa y asegúrate de que la RUTA variable contiene el directorio donde se instaló Terraform.

5.4 Primer despliegue de infraestructura

Una vez instalado Terraform, debemos comprobar que funciona correctamente, y por tanto, haremos un primer despliegue de infraestructura. Construiremos infraestructura en AWS (ya deberíamos tener una cuenta para esta nube), pero debes saber que Terraform puede administrar muchos proveedores. En caso de que aún no tengas una cuenta de AWS, este es un buen momento de que crees una. Solo vamos a utilizar los recursos de AWS que califiquen como *«free tier»*, ya que estos podrás utilizarlos sin coste durante el primer año. En cualquier caso, comprueba lo que se va a desplegar y no olvides eliminarlo.

Configuración

Cuando hablamos de la **configuración Terraform,** nos referimos alconjunto de archivos que se utilizan para describir la infraestructura en dicha herramienta. Con el objeto de iniciar una única instancia de AWS EC2, a continuación, vamos a escribir nuestra primera configuración. El formato de los archivos de configuración lo describiremos en más detalle después, pero esto nos sirve como una primera aproximación.

Ten en cuenta que los archivos de configuración también pueden ser JSON, pero recomendamos usar JSON (únicamente) cuando la configuración sea generada por una máquina.

Vamos a guardar loscontenidos en un archivo llamado example.tf. Por favor, verifica que no existan otros archivos \*.tf en tu ordenador, porque Terraform carga todos.

provider "aws" {

access\_key = "ACCESS\_KEY\_HERE"

secret\_key = "SECRET\_KEY\_HERE"

region = "us-east-1"

}

resource "aws\_instance" "example" {

ami = "ami-2757f631"

instance\_type = "t2.micro"

}

**Importante:** Esta configuración que hemos visto, está pensada para funcionar en casi todas las cuentas EC2 con acceso a una VPC predeterminada. En caso de que tú estés usando una región que no sea us-este-1, deberás seleccionar un AMI en la región de tu preferencia, porque las ID de AMI son específicas de una región. Por ende, reemplaza ACCESS\_KEY\_HERE y SECRET\_KEY\_HERE con tu clave de acceso AWS y contraseña.

En este ejemplo estamos poniendo las credenciales directamente en el fichero. Es necesario aclarar que esto no es una buena práctica y resulta más conveniente pasar las credenciales de otra forma. Esta opción es mucho más “limpia” para situaciones en las que los archivos \*tf se registran con control de fuente o donde hay más de un usuario administrador. Más adelante haremos las credenciales parametrizables.

**Importante:** si por cualquier motivo omites las credenciales de AWS, lo que ocurrirá es que Terraform, de forma automática, intentará buscar las credenciales de API guardadas (por ejemplo, en ~ / .aws / credenciales) o las credenciales de perfil de instancia de IAM.

Si eliges que las credenciales de IAM queden fuera de la configuración de Terraform, consecuentemente esas credenciales permanecerán fuera del control de origen, y podrás usar diferentes credenciales de IAM para los usuarios sin que haga falta modificar los archivos de configuración. El fichero anterior es una configuración completa de Terraform que se puede aplicar directamente. A continuación, vamos a explicar la estructura.

Un proveedor es responsable de crear y gestionar recursos. Para la configuración del proveedor, utilizaremos el bloque de proveedor (*provider*), que en este caso es «aws». En la práctica, es muy frecuente que existan múltiples bloques de proveedores si la configuración de Terraform está compuesta de múltiples proveedores.

Además de los proveedores también tendremos recursos. Estos pueden ser un componente físico, como una instancia EC2, o también un recurso lógico como, por ejemplo, una aplicación Heroku.

También encontraremos un bloque de recursos (*resource*), que define un recurso dentro de la infraestructura. Este presenta dos cadenas antes de abrir el bloque: el tipo de recurso y el nombre del recurso. Si continuamos con nuestro ejemplo, el tipo de recurso es «aws\_instance» y el nombre es «example» (el prefijo del tipo se asigna al proveedor).

A modo de interpretación, vamos a decir que «aws\_instance» le indica de forma automática a Terraform que es administrado por el proveedor «aws». Por otra parte, veremos que, dentro del bloque de recursos, hay una configuración para el recurso, que depende de cada proveedor y recurso completo. Para nuestra instancia de EC2 especificamos un AMI para Ubuntu y solicitamos una instancia «t2.micro», a fin de utilizar las prestaciones gratuitas.

Inicialización

**terraform init** es el primer comando que utilizaremos para ejecutar una nueva configuración. También se usa después de actualizar una configuración existente desde el control de la versión. Este comando inicializa varias configuraciones locales y los datos que serán utilizados por el resto de los comandos.

Con el fin de admitir una gran cantidad de infraestructura y proveedores de servicios, Terraform utiliza una arquitectura basada en *plugins*. A partir de la versión 0.10.0, cada «provider» es un propio binario encapsulado, distribuido por separado de Terraform. El comando terraform init descarga e instala de forma automática el «Provider» binario para los proveedores en uso dentro de la configuración. En este caso, es solo el proveedor de AWS:

$ terraform init Initializing the backend...

Initializing provider plugins...

‐ downloading plugin for provider "aws"...

The following providers do not have any version constraints in configuration, so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking changes, it is recommended to add version = "..." constraints to the corresponding provider blocks in configuration, with the constraint strings suggested below.

\* provider.aws: version = "~> 1.0"

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform commands should now work.

If you ever set or change modules or backend configuration for Terraform, rerun this command to reinitialize your environment. If you forget, other commands will detect it and remind you to do so if necessary.

El complemento de proveedor aws se descarga e instala en un subdirectorio del directorio de trabajo actual, junto con otros archivos que sirven para mantener el estado. El resultado especifica qué versión del complemento se instaló y sugiere que se especifique esa versión en la configuración para garantizar que la ejecución de terraform init en el futuro instale una versión compatible. Este paso no es necesario para seguir la guía de inicio, ya que esta configuración se descartará al final. Sin embargo, es importante para entornos de producción, con el fin de hacer las configuraciones más repetibles. **Es aconsejable aumentar esta versión después de comprobar que el cambio es compatible.**

**Los providers requieren algunos cambios para la versión 0.12.** La forma recomendada para actualizar es subir a la última versión desde la 0.11 y posteriormente subir a la versión 0.12 o superiores de Terraform. Si estáis empezando un nuevo proyecto esto no debería ser un problema.

Aplicación de cambios

Ahora ejecutaremos terraform apply en el mismo directorio que el archivo example.tf que hemos creado anteriormente. Deberíamos ver una salida similar a la siguiente (aunque hemos truncado parte de la salida por motivos de extensión):

$ terraform apply # ...

+ aws\_instance.example

ami: "ami‐2757f631"

availability\_zone: "<computed>" ebs\_block\_device.#: "<computed>" ephemeral\_block\_device.#: "<computed>" instance\_state: "<computed>"

instance\_type: "t2.micro"

key\_name: "<computed>"

placement\_group: "<computed>"

private\_dns: "<computed>"

private\_ip: "<computed>"

public\_dns: "<computed>"

public\_ip: "<computed>" root\_block\_device.#: "<computed>" security\_groups.#: "<computed>"

source\_dest\_check: "true"

subnet\_id: "<computed>"

tenancy: "<computed>" vpc\_security\_group\_ids.#: "<computed>"

**Este resultado muestra el plan de ejecución**, que no es más que la descripción de las acciones que tomará Terraform con el objetivo de cambiar la infraestructura real, para que coincida con la configuración. Como podemos ver, hay una gran similitud entre el formato de salida y el formato de diferencias que generan otras herramientas, como Git. El signo + que aparece en el resultado, al lado de aws\_instance.example, implica que Terraform va a crear este recurso, y justo debajo indica los atributos que se establecerán. Si el valor visualizado es «<computed>», esto nos indica que el valor no se conocerá hasta que se cree el recurso. En esta etapa, es posible que haya un error de sintaxis en la configuración y la aplicación Terraform puede fallar. Por favor, lee el mensaje de error y corrige lo que haga falta.

Si todo ha ido bien y el plan se ha creado con éxito, Terraform se quedará en pausa y estará a la espera de la aprobación para poder reanudar su actividad. Si detectas que el plan no es correcto, o intuyes que es peligroso, es seguro abortar aquí. En nuestro caso, el plan no presenta ninguna anomalía, así que escribiremos **yes** en la confirmación y daremos continuidad a nuestra operación.

Ten en cuenta que la ejecución del plan suele tardar algunos minutos porque Terraform espera a que esté disponible la instancia de EC2:

# ...

aws\_instance.example: Creating...

ami: "" => "ami‐2757f631"

instance\_type: "" => "t2.micro" [...]

aws\_instance.example: Still creating... (10s elapsed) aws\_instance.example: Creation complete

Apply complete! Resources: 1 added, 0 changed, 0 destroyed. # ...

**¡Has terminado!** Ahora es momento deir a la consola de EC2 y ver la instancia creada. (¡No olvides comprobar la región que aparece en la configuración del proveedor!).

AQUI

Es importante que sepas que Terraform ha escrito datos en el archivo de estado terraform.tfstate. Ten en cuenta que **este archivo es sumamente relevante porque lleva a cabo un seguimiento de los ID de aquellos recursos que fueron creados para que la herramienta Terraform tenga conocimiento sobre lo que está gestionando. Por ello, deberás guardarlo y compartirlo con aquellas personas dentro de la organización que deban ejecutar Terraform.**

Si bien para compartir el estado automáticamente es recomendable configurar el estado remoto para trabajar con Terraform, esto no resulta necesario en casos que no revisten complejidad, como la guía de introducción que veremos a continuación.

Utilizaremos terraform show para ver el estado actual:

$ terraform show aws\_instance.example:

id = i‐32cf65a8

ami = ami‐2757f631

availability\_zone = us‐east‐1ª

instance\_state = running

instance\_type = t2.micro

private\_ip = 172.31.30.244

public\_dns = ec2‐52‐90‐212‐55.compute‐1.amazonaws.com

public\_ip = 52.90.212.55

subnet\_id = subnet‐1497024d

vpc\_security\_group\_ids.# = 1

vpc\_security\_group\_ids.3348721628 = sg‐67652003

Como se puede observar, mientras creábamos el recurso, hemos obtenido también información sobre las propiedades finales de dicho recurso. Los valores que hemos reunido también nos servirán a la hora de referenciar, en caso de que queramos configurar productos o recursos adicionales.

Aprovisionamiento

La instancia de EC2 que lanzamos en este momento se basa en el AMI dado, pero no tiene ningún software adicional instalado. De todas maneras, esto es todo lo que necesitas si estás ejecutando una infraestructura basada en imágenes (como la que hemos visto antes, cuando creamos imágenes con Packer, por ejemplo).

Aún así, algunas infraestructuras requieren adicionalmente un paso de inicialización o aprovisionamiento de software. **Terraform soporta «provisioners»** como veremos más adelante.

5.5 Cambios en la infraestructura

Acabamos de ver cómo podemos crear infraestructura en Terraform (en nuestro caso una instancia EC2). Ahora vamos a ver cómo modificar ese recurso y cómo Terraform nos ayudará a gestionar el cambio.

Terraform construye un plan de ejecución que **se encarga de modificar (únicamente) aquello que sea necesario para alcanzar el estado deseado.**

Cuando utilizas Terraform para modificar la infraestructura, tienes la capacidad para versionar sus configuraciones y además el estado, lo que te permite ver la evolución de la infraestructura a través del tiempo.

Cambios en la configuración

Modificaremos el AMI de nuestra instancia. Para ello, edita el aws\_instance.example en tu configuración con el siguiente cambio:

resource "aws\_instance" "example" {

ami = "ami‐b374d5a5"

instance\_type = "t2.micro"

}

Hemos cambiado el AMI de Ubuntu (el nombre de las imágenes para máquina virtual en Amazon) a otra con una versión diferente. Cuando quieras editar las configuraciones de Terraform deberás hacerlo de esta forma. Si deseas además eliminar recursos, puedes hacerlo libremente y Terraform sabrá hacer lo propio para destruirlos.

Aplicación de cambios

Ahora que hemos cambiado la configuración, vamos a ejecutar Terraform a fin de comprobar cómo se han aplicado estos cambios a los recursos existentes.

$ terraform apply # ...

‐/+ aws\_instance.example

ami: "ami‐2757f631" => "ami‐b374d5a5" (forces new resource)

availability\_zone: "us‐east‐1a" => "<computed>"

ebs\_block\_device.#: "0" => "<computed>"

ephemeral\_block\_device.#: "0" => "<computed>" instance\_state:

"running" => "<computed>"

instance\_type: "t2.micro" => "t2.micro"

private\_dns: "ip‐172‐31‐17‐94.ec2.internal" => "<computed>"

private\_ip: "172.31.17.94" =>

"<computed>"

public\_dns: "ec2‐54‐82‐183‐4.compute‐1.amazonaws.com" => "<computed>"

public\_ip: "54.82.183.4" => "<computed>"

subnet\_id: "subnet‐1497024d" => "<computed>"

vpc\_security\_group\_ids.#: "1" => "<computed>"

Vamos a analizar el fragmento anterior:

El prefijo - / + que aparece al comienzo nos indica que Terraform destruirá y recreará el recurso (no lo va a actualizar). Es cierto que, si bien en algunos casos los atributos pueden actualizarse *in situ* (estos están señalizados con el ~ prefijo), es necesaria una recreación si queremos cambiar el AMI para una instancia de EC2. La herramienta Terraform gestionará estos detalles y describirá en el plan de ejecución cómo va a hacerlo.

Además, el plan de ejecución muestra que el cambio de AMI no puede realizarse mediante un simple update y requiere que el recurso sea reemplazado. Teniendo en cuenta este dato, es un buen momento para reajustar los cambios que vayas a introducir y de esta forma puedes evitar la destrucción o creación de actualizaciones si estas no son aceptables en determinados casos (por ejemplo, los componentes con estado como son las bases de datos, que perderían la información).

Como puedes ver, antes proceder Terraform pedirá una confirmación/aprobación del plan de ejecución. Si quieres ejecutar los pasos planificados, indica Sí:

# ...

aws\_instance.example: Refreshing state... (ID: i‐64c268fe) aws\_instance.example: Destroying...

aws\_instance.example: Destruction complete aws\_instance.example: Creating...

|  |  |  |  |
| --- | --- | --- | --- |
| ami: | "" | => | "ami‐b374d5a5" |
| availability\_zone: | "" | => | "<computed>" |
| ebs\_block\_device.#: | "" | => | "<computed>" |
| ephemeral\_block\_device.#: | "" | => | "<computed>" |
| instance\_state: | "" | => | "<computed>" |
| instance\_type: | "" | => | "t2.micro" |
| key\_name: | "" | => | "<computed>" |
| placement\_group: | "" | => | "<computed>" |
| private\_dns: | "" | => | "<computed>" |
| private\_ip: | "" | => | "<computed>" |
| public\_dns: | "" | => | "<computed>" |
| public\_ip: | "" | => | "<computed>" |
| root\_block\_device.#: | "" | => | "<computed>" |
| security\_groups.#: | "" | => | "<computed>" |
| source\_dest\_check: | "" | => | "true" |
| subnet\_id: | "" | => | "<computed>" |
| tenancy: | "" | => | "<computed>" |
| vpc\_security\_group\_ids.#: | "" | => | "<computed>" |

aws\_instance.example: Still creating... (10s elapsed) aws\_instance.example: Still creating... (20s elapsed) aws\_instance.example: Creation complete

Apply complete! Resources: 1 added, 0 changed, 1 destroyed. # ...

AQUI

Tal y como se indicaba el plan de ejecución, el primer paso que ha dado Terraform es el de destruir la instancia existente y más tardíamente, ha creado una nueva en reemplazo de esta. Si quieres visualizar los nuevos valores asociados con esta instancia, utiliza show terraform.

Destrucción de la infraestructura

Antes hemos abordado cómo construir y cambiar la infraestructura. Antes de pasar a la creación de múltiples recursos y mostrar las dependencias, vamos a repasar cómo destruir completamente la infraestructura gestionada por Terraform.

**Si bien destruir la infraestructura es un evento raro en los entornos de producción, al usar** Terraform para crear entornos de desarrollo, pruebas, QA, etc., podrás realizar una destrucción automática de dichos entornos de forma muy práctica. El comando terraform destroy, te permitirá realizar esta tarea. Este es muy parecido al comando terraform apply, a diferencia de que se comporta como si todos los recursos hubieran sido eliminados de la configuración.

$ terraform destroy # ...

‐ aws\_instance.example

El prefijo – que aparece delante de aws\_instance.example indica que la instancia será destruida. Tal y como ocurre con terraform apply, primero veremos el plan de ejecución y luego deberemos dar una aprobación para que se ejecuten los cambios.

Si respondemos Sí, veremos los cambios aplicados:

# ...

aws\_instance.example: Destroying...

Apply complete! Resources: 0 added, 0 changed, 1 destroyed. # ...

Igualmente a lo que ocurre con apply, Terraform establece el orden en el que actuará y determina cuando destruirá los recursos. En el caso de ejemplo, como tenemos únicamente 1 recurso, el orden no afecta. Sin embargo, si tuviésemos un caso más complejo donde hubiese numerosos recursos, Terraform aplicaría un orden determinado con el objetivo de respetar las dependencias.

Dependencias de recursos

Ahora vamos a introducir dependencias de recursos, donde veremos una configuración con múltiples recursos por primera vez, pero, además, casos donde los recursos usan como parámetros la información de otros.

En el ejemplo con el que estamos trabajando tenemos un único recurso, pero en la práctica, la infraestructura suele tener un conjunto diverso y variado de recursos. Terraform permite que sus configuraciones contengan múltiples recursos, de distinto tipo, y a su vez, tipos de múltiples proveedores.

A continuación, veremos un ejemplo con múltiples recursos y abordaremos cómo hacer debemos hacer referencia a los atributos de otros recursos para poder configurar recursos.

Cómo asignar una IP elástica

AQUI

Con el fin de enriquecer nuestra configuración, asignaremos una IP elástica a la instancia de EC2. Para ello, vamos a Modificar el example.tf y agregaremos lo siguiente:

resource "aws\_eip" "ip" {

instance = "${aws\_instance.example.id}"

}

Esto es similar a lo que hemos hecho en el ejemplo anterior (cuando agregamos un recurso de instancia EC2), excepto que esta vez estamos construyendo un tipo de recurso «aws\_eip». Lo que hace este tipo de recuros es asignar y asociar una IP elástica a una instancia EC2. El único parámetro para aws\_eip es «instance», que es la instancia de EC2 para asignar la IP.

La *template* aplica interpolación con el objetivo de utilizar un atributo de la instancia EC2 que anteriormente desplegamos. La sintaxis para esta interpolación solicita el atributo «id» del recurso «aws\_instance.example».

La interpolación de variables ha cambiado levemente entre las versiones 0.11 y 0.12, y es un poco más sencilla de usar. Si queréis indagar más, podéis ver los detalles en la documentación de Terraform. Hay muchos ejemplos por internet en ambas versiones así que por un tiempo será necesario que conozcáis las diferencias para poder adaptar la sintaxis de una a otra. La herramienta de migración automática de Terraform corrige casi todos los usos.

Cómo aplicar cambios

Vamos a ejecutar el comando terraform apply para ver cómo Terraform aplica este cambio. El resultado que obtendrás debe ser similar a este:

$ terraform apply

+ aws\_eip.ip

allocation\_id: "<computed>" association\_id: "<computed>" domain: "<computed>"

instance: "${aws\_instance.example.id}" network\_interface: "<computed>"

private\_ip: "<computed>"

public\_ip: "<computed>"

+ aws\_instance.example

ami: "ami‐b374d5a5"

availability\_zone: "<computed>" ebs\_block\_device.#:

"<computed>" ephemeral\_block\_device.#: "<computed>"

instance\_state: "<computed>"

instance\_type: "t2.micro"

key\_name: "<computed>"

placement\_group: "<computed>"

private\_dns: "<computed>"

private\_ip: "<computed>"

public\_dns: "<computed>"

public\_ip: "<computed>" root\_block\_device.#:

"<computed>" security\_groups.#: "<computed>"

source\_dest\_check: "true"

subnet\_id: "<computed>"

tenancy: "<computed>" vpc\_security\_group\_ids.#:

"<computed>"

**Terraform creará dos recursos: la instancia y la elastic-IP**. En el valor de «instancia» para «aws\_eip», se puede ver que la interpolación en bruto está aún presente. El motivo por el que esto ocurre es que esta variable no se conocerá hasta que se cree «aws\_instance», que va a ser finalmente reemplazada durante la ejecución.

Como imaginarás, antes de proceder Terraform solicitará una aprobación. Para continuar, responde sí:

# ...

aws\_instance.example: Creating...

ami: "" => "ami‐b374d5a5"

instance\_type: "" => "t2.micro" [..]

aws\_instance.example: Still creating... (10s elapsed)

aws\_instance.example: Creation complete

aws\_eip.ip: Creating...

|  |  |  |  |
| --- | --- | --- | --- |
| allocation\_id:  association\_id: domain: | ""  ""  "" | =>  =>  => | "<computed>"  "<computed>" "<computed>" |
| instance: | "" | => | "i‐f3d77d69" |
| network\_interface: | "" | => | "<computed>" |
| private\_ip: | "" | => | "<computed>" |
| public\_ip: | "" | => | "<computed>" |

aws\_eip.ip: Creation complete

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

De acuerdo con lo que vemos en el fragmento anterior, Terraform ha creado la instancia EC2 previo a crear la Dirección IP elástica. Esto se debe a que la herramienta puede inferir una dependencia, y sabe que debe crear la instancia primero gracias a la expresión de interpolación que pasa la ID del EC2 instancia a la dirección IP elástica,

Dependencias implícitas y explícitas

Gracias al análisis de los atributos de los recursos que se utilizan en las expresiones de interpolación, **Terraform tiene la capacidad de inferir en qué ocasiones hay dependencias entre los recursos**. En el ejemplo que hemos visto recién, la expresión $ {aws\_instance.example.id} crea una dependencia implícita en *example* (una aws\_instance).

Con esta información sobre las dependencias Terraform se vale para determinar el orden correcto en el cual debe crear los diferentes recursos. Si analizamos nuestro caso veremos que Terraform establece que aws\_instance ha de crearse antes de aws\_eip. Estas dependencias implícitas a través de expresiones de interpolación representan la forma primordial para informar a Terraform sobre estas relaciones, y por ello es recomendable utilizarlas siempre que sea posible, porque reducirá de forma exponencial la redundancia y trabajo manual.

En algunos casos hay dependencias entre recursos que no resultan visibles para Terraform. El argumento depends\_on es aceptado por cualquier recurso y acepta una lista de recursos para crear dependencias explícitas.

Un buen ejemplo para utilizar el comando depends\_on es para declarar explícitamente una dependencia. Vamos a plantearnos el siguiente caso: una aplicación que ejecutaremos en nuestra instancia EC2 usará un *«bucket»* específico de Amazon S3, y dicha dependencia está configurada dentro del código de la aplicación. Debido a ello, no es visible para Terraform y podremos valernos de depends\_on para mostrar a Terraform esta dependencia.

# New resource for the S3 bucket our application will use.

resource "aws\_s3\_bucket" "example" {

# NOTE: S3 bucket names must be unique across \_all\_ AWS accounts, so

# this name must be changed before applying this example to avoid naming # conflicts.

bucket = "terraform\_getting\_started\_guide" acl = "private"

}

# Change the aws\_instance we declared earlier to now include "depends\_on"

resource "aws\_instance" "example" {

ami = "ami‐2757f631" instance\_type = "t2.micro"

# Tells Terraform that this EC2 instance must be created only after the # S3 bucket has been created.

depends\_on = ["aws\_s3\_bucket.example"]

}

Recursos no dependientes

Ahora añadiremos una nueva instancia EC2:

resource "aws\_instance" "another" {

ami = "ami‐b374d5a5"

instance\_type = "t2.micro"

}

Como esta nueva instancia no depende de ningún otro recurso, podemos crearla en paralelo con los otros recursos. Donde sea posible, Terraform realizará operaciones al mismo tiempo (en paralelo) para reducir el tiempo total requerido para aplicar los cambios.

En los siguientes ejemplos no utilizaremos esta segunda instancia, así que, eliminaremos este recurso de la configuración y volveremos a ejecutar Terraform para que se destruya.

5.6. Conclusiones

Terraform es una herramienta de código abierto creada por HashiCorp y escrita en el lenguaje de programación Go. El código Go compila en un solo binario (o más bien, un binario para cada uno de los sistemas operativos admitidos) llamado Terraform.

Como hemos visto en este tema, este binario nos permitirá implementar infraestructura desde un ordenador o servidor de compilación con mínima intervención manual y sin necesidad de incluir una infraestructura adicional. Eso es porque el binario terraform realiza llamadas API en su nombre a uno o más proveedores, como Amazon Web Services (AWS), Azure, Google Cloud, Digital Ocean, OpenStack, etc. Eso significa que Terraform aprovecha los proveedores de infraestructura que ya tiene para interactuar con infraestructura mediante APIs, por ejemplo, los mecanismos de autenticación que ya tiene por estar conectado a esos proveedores (con AWS utiliza las claves que ya tiene).

El código de Terraform tiene una sintaxis simple, característica que resulta muy agradecida para los usuarios. Además, permite implementar recursos interconectados en múltiples proveedores de la nube, así que podremos implementar infraestructura completa -servidores, bases de datos, equilibradores de carga (load balancers), topología de red, etc.- en los archivos de configuración de Terraform y asignar esos archivos al control de versiones. Sus comandos, como, por ejemplo, terraform apply, nos permitirán implementar esa infraestructura. La tarea que lleva a cabo el binario de Terraform es la de analizar el código, traducirlo en llamadas API a los proveedores de nube que se hayan especificado en el código, y, de la forma más eficientemente posible, realizar dichas llamadas a la API.

Cuando necesites realizar cambios en la infraestructura, en lugar de actualizar la infraestructura de forma manual en los servidores, puedes directamente realizar los cambios en los archivos de configuración de Terraform. Esos cambios se validarán mediante pruebas automáticas y revisiones de códigos, se confirmará el código actualizado control de versiones, y luego se ejecutará el comando terraform apply para que Terraform realice las llamadas API necesarias para implementar los cambios.

5.7. Referencias bibliográficas

Alvarado, G. (2019). Tutorial: *Infraestructura como código con Terraform*. Recuperado de <https://galvarado.com.mx/post/tutorial-infraestructura-como-c%C3%B3digo-con-terraform/>

Castillo Cotán, J. M. (2017). *Casos de uso — documentación de Terraform: Infraestructura como código - 3.0*. Recuperado de <https://terraform-infraestructura.readthedocs.io/es/latest/casosdeuso/>

Documentación oficial de Terraform: <https://www.terraform.io/docs/index.html>

A fondo

**Terraform: Up & Running: Writing Infrastructure as Code**

Terraform: Up & Running: Writing Infrastructure as Code por

Yevgeniy Brikman ISBN: 9781491977057

Buen libro si queremos complementar la documentación oficial de Terraform. Se centra mucho en AWS pero el conocimiento puede adaptarse a otros entornos

***Ejemplo de una arquitectura de dos capas***

Repositorio con un ejemplo de dos capas [*https://github.com/terraform-providers/terraform-provider-aws/tree/master/examples/two-tier*](https://github.com/terraform-providers/terraform-provider-aws/tree/master/examples/two-tier)

Un buen ejemplo de como se podría realizar un despliegue de una arquitectura de dos capas. Lo más interesante es como las conecta y el hecho de que incluye varias configuraciones adicionales de red lo que permite verlo como un ejemplo más completo de lo habitual.

Actividades

Trabajo/Lectura. Título de la actividad

Debemos especificar:

* **Objetivos** de la actividad (se recomienda la redacción directa, por ejemplo: con esta actividad vas a conseguir…; a través de esta actividad podrás…).
* **Descripción** de la actividad y **pautas** de elaboración.
* **Criterios de evaluación**.
* **Extensión** máxima de la actividad (nº páginas, nº diapositivas, etc.).

Si la actividad propuesta es de trabajo colaborativo, incluiremos también:

* **Organización del equipo**: estudiantes que lo componen y cómo se forman los grupos.
* **Herramientas y comunicación**: cuentas de correo corporativas de Office 365 (@comunidadunir.net), sala Connect, foro, Skype, otras.
* **Entrega**: un documento por alumno, un documento grupal, enlace a OneDrive, enlace a YouTube, otras.
* **Evaluación:** ¿nota mixta? (% trabajo de grupo e individual), rúbrica, permitida la opción de trabajo individual; indicaciones para convocatoria extraordinaria (individual/no se podrá presentar), otras.

Test

1. Terraform es una herramienta de ….:
   1. \*Infraestructura como código (Terraform es una herramienta de despliegue y configuración de infraestructura donde definimos la infraestructura de forma principalmente declarativa)
   2. Balanceo de carga
   3. Creación de imágenes inmutables
   4. Monitorización de sistemas
2. Las dependencias en Terraform …:
   1. Tienen que ser definidas explicitamente con depends\_on
   2. Solo se definen de forma implicita mediante referencias a variables
   3. \*Pueden ser definidas explicitamente o implicitamente (Terraform utiliza tanto dependencias explicitas como implicitas al decidir el orden de los despliegues)
   4. Solo se usan como documentación
3. Un caso de uso típico de Terraform es …:
   1. La configuración de un servidor desplegado con otra herramienta
   2. El despliegue de infraestructura física mediante netboot
   3. \*El despliegue de infraestructura virtual en una o varias nubes (Terraform permite desplegar muchos tipos de recursos, principalmente infraestructura virtual en diferentes nubes)
   4. El despliegue de infraestructura virtual pero siempre en una nube
4. Terraform interactúa con las redes ...:
   1. Ya que permite enrutar en tráfico entre piezas de la infraestructura a través de su binario al estar programado en Go
   2. \*Ya que puede configurar redes virtuales de varios proveedores de nubes (Terraform permite configurar redes virtuales en muchos proveedores como por ejemplo AWS VPC pero no permite enrutar tráfico ya que Terraform solo aplica durante el despliegue y configuración)
   3. Terraform no puede configurar redes
   4. A y B son correctas
5. Si queremos desplegar una máquina dejandola configurada con Terraform podemos:
   1. Crear una imagen ya configurada con Packer y desplegarla con Terraform
   2. \*Todas las otras respuestas son correctas (Existen diferentes técnicas para configurar máquinas virtuales con Terraform y todas las expresadas aquí son válidas)
   3. Aprovisionar la configuración con una de las integraciones de Terraform con Chef, Puppet o Ansible
   4. Usar scripts nativos de la nube como Cloud Init configurados desde Terraform
6. El recurso *aws\_eip* …:
   1. Despliega una máquina virtual con conexión IP
   2. No existe en el *provider* de aws
   3. \*Reserva una ip elástica (El recurso aws\_eip reserva una IP elástica, que es una IP que puede asignarse a una máquina y moverse posteriormente)
   4. Crea un pool de ips que auto escalan elásticamente
7. El comando *terraform show* ...:
   1. Refresca el estado con los recursos desplegados y muestra sus valores
   2. Refresca el estado con los recursos desplegados
   3. Muestra la versión de Terraform
   4. \*Muestra los valores del estado (El comando terraform show muestra los valores del estado que tenemos ahí pero no los refresca con el estado actual en la nube)
8. El comando *terraform apply* ...:
   1. Permite aplicar cambios de configuración a los componentes pero no puede crearlos ni eliminarlos
   2. \*Permite aplicar cambios de configuración, crear y eliminar componentes (*terraform apply* puede crear y eliminar componentes y en algunos casos cambiar la configuración de algunos ya existentes)
   3. Permite aplicar cambios de configuración y crear componentes pero no eliminarlos
   4. Permite crear y eliminar componentes pero no aplicar cambios de configuración
9. El comando *terraform init* ...:
   1. Realiza el primer despliegue de las configuraciones que tenemos
   2. Inicializa el proyecto actual y se asegura que tengamos las últimas versiones de los plugins
   3. Inicializa el proyecto actual, se asegura que tengamos las versiones apropiadas de los plugins y realiza el primer despliegue de las configuraciones que tenemos
   4. \*Inicializa el proyecto actual y se asegura que tengamos las versiones apropiadas de los plugins (terraform init descarga las versiones seleccionadas o las ultimas si no hemos elegido version pero no realiza acciones sobre la infraestructura)
10. Terraform esta escrito en ...:
    1. \*Go (Terraform esta escrito en el lenguaje de programación Go)
    2. Python
    3. Javascript
    4. Bash
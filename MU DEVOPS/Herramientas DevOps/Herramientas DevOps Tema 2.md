Tema nº 2

Componentes

de Aplicaciones

Herramientas DevOps

Índice

[Esquema 3](#_Toc40470454)

[Ideas clave 4](#_Toc40470455)

[2.1. Introducción y objetivos 4](#_Toc40470456)

[2.2. Tipos de componentes 4](#_Toc40470457)

[2.3. Computo 6](#_Toc40470458)

[2.4. Gestión del estado 12](#_Toc40470459)

[2.5. Conclusiones 23](#_Toc40470460)

[1.4. Referencias bibliográficas 24](#_Toc40470461)

[A fondo 25](#_Toc40470462)

[Actividades 27](#_Toc40470463)

[Test 28](#_Toc40470464)

Esquema

![](data:image/png;base64...)

Ideas clave

2.1. Introducción y objetivos

Las aplicaciones y entornos DevOps suelen estar compuestos de diferentes piezas o componentes que trabajan conjuntamente para resolver algún tipo de problema.

Cada uno de estos tipos de componentes o herramientas tiene características operacionales y una función específica en las diferentes aplicaciones. Para poder hablar de una arquitectura completa de una aplicación es necesario conocer los distintos componentes, sus diferencias (en ocasiones, sutiles) y las características que tienen para ser desplegados y mantenidos.

En este tema vamos a analizar los diferentes tipos de componentes y su impacto en un entorno DevOps. Los objetivos que se pretenden conseguir son:

* Reconocer los componentes con estado y sin estado, y considerar si un componente de cómputo debería tener estado o no.
* Conocer los distintos tipos de almacenamientos de la información y reconocer las características de estos.
* Describir las principales formas de desplegar código en entornos de nube y sus características, a fin de elegir la forma más adecuada para cada escenario.

2.2. Tipos de componentes

Existen muchos tipos de componentes que una aplicación puede utilizar para componer sus sistemas. En el caso de DevOps, hablaremos de un componente como una pieza desplegable, independientemente de que pudiera tener su propio ciclo de vida.

En ocasiones varios componentes compartirán su ciclo de vida, pero no es necesario que todos los componentes de una aplicación compartan el mismo ciclo de vida.

Para poder analizar los tipos de componentes, es importante atender a ciertas categorías, si tienen estado o no y si son frecuentemente reusables entre proyectos o no.

Componentes con y sin estado

Probablemente la pieza de información más relevante sobre un componente es si guarda estado o no. Un componente guarda estado cuando puede variar su respuesta una misma pregunta sin necesidad de que haya variado la respuesta de algunas de las peticiones a otros componentes.

Los componentes sin estado son fácilmente reemplazables ya que una copia idéntica del mismo componente debería poder responder a las peticiones idénticamente. Esto tiene amplias consecuencias operacionales que nos permite adoptar estrategias sencillas de balanceo de carga o reemplazar completamente un componente que esta funcionando incorrectamente con uno nuevo.

Sobre los componentes con estado es importante a su vez considerar dos subtipos, donde el estado puede ser reconstruido y donde el estado no puede ser reconstruido.

En realidad, esta dicotomía es un gradiente ya que parte de la pregunta es cuanto nos cuesta reconstruir la información. Es posible que sea imposible, que sea necesario volver a preguntar a nuestros clientes, que necesitemos recuperar otras copias o realizar costosos cómputos o por último que la información sea barata de replicar, pero solo perdamos unos pocos recursos sin afectar operacionalmente a la aplicación completa.

Frecuentemente, las bases de datos suelen guardar información que no es posible recuperar en general o solo parcialmente (desde un *backup*). Por otro lado, el almacenamiento de sesiones si las tenemos suele no ser reproducible y perderlo implica obligar a los usuarios a volver a introducir sus credenciales, pero no es tan valioso. Por último, una caché es por definición posible de ser recreada pero el coste podría o no impactar a la disponibilidad de la aplicación o a la experiencia de los usuarios.

Componentes reusables

Los componentes pueden o no ser reusables entre proyectos de la misma empresa o de otras empresas.

Cuando una componente puede definirse con una API reusable que es frecuentemente necesaria, podremos encontrar componentes en el mercado que podemos incluir en nuestra arquitectura de forma reusable.

Frecuentemente, habrá partes de la aplicación que son únicas de nuestra aplicación y sobre estos componentes habremos de programar nuestra lógica o bien configurar esa lógica si hemos encontrado una solución que nos permita reusar partes.

Las partes que más frecuentemente se reutilizan son las bases de datos y en general piezas con estado. La gestión de estado con alta eficiencia y fiabilidad es complicada lo que ha llevado a la creación de familias enteras de productos de almacenamiento de estado que veremos en este tema.

Esto no implica que todas las piezas reusables sean con estado. Por ejemplo, tenemos piezas como los CMS (por ejemplo, Wordpress o Drupal) que son piezas que gestionan la lógica de negocio, que pueden hacerse sin estado y que aun así son piezas reusables. Por supuesto, dependiendo de cuanto necesitemos personalizarlas podríamos desarrollar piezas de código completas.

Por el otro lado, incluso cuando creamos aplicaciones completas de cómputo, frecuentemente utilizamos librerías o *frameworks* que nos aligeran el trabajo y que son piezas reusables de cómputo, aunque en este caso se juntan con nuestro código en único componente desplegable.

Finalmente, existen piezas completamente reusables de cómputo como pueden ser herramientas para realizar Machine Learning y entrenar redes neuronales. Otros ejemplos son piezas de gestión de políticas de seguridad como Open Policy Agent (que se puede usar sin estado).

2.3. Cómputo

Los componentes de cómputo son algunos de los componentes más comunes y que más frecuentemente cambian en las aplicaciones.

La lógica de negocio suele cambiar más frecuentemente que otros componentes y es la parte que se desarrolla localmente en lugar de usar componentes puramente reusables, por ese motivo es importante desarrollar técnicas y adoptar practicas y herramientas que permitan la gestión de este tipo de componentes.

Tipos de cómputo y métricas

Cuando analizamos las necesidades de un componente de cómputo, las principales características son las necesidades de procesamiento (CPU), las de memoria volátil (RAM) y las de memoria más lenta pero grande (Disco).

Las necesidades de procesamiento (CPU) hace años que han dejado de crecer exponencialmente para crecer mucho más lentamente, lo que ha ocasionado que en ocasiones se hable simplemente del número de cores o vcpu que se le da al componente de cómputo.

La memoria RAM permite almacenar información de precálculo (ciertas cachés) así como información de las peticiones en curso. Si la información de precálculo acaba siendo demasiado grande o compleja de recalcular el componente puede empezar a comportarse como un componente con estado. Frecuentemente, la memoria se invertirá en guardar la información necesaria para calcular la peticiones o tareas en curso.

El disco no deja de ser un almacenamiento de memoria más a largo plazo. Suele sobrevivir a reinicios lo que lo hace conveniente para almacenar el estado del componente si lo tuviera o cachés y almacenamiento de cálculo que no se va a consumir simultáneamente y que se puede ir procesando secuencialmente.

Por último y aunque no es elemento de cómputo intrínsecamente, es importante considera que el objetivo de un componente de cómputo suele ser comunicar sus resultados. Esta comunicación ocasionalmente se realiza por disco (por ejemplo, generando un resultado y haciendo una copia de seguridad del disco) pero mucho más frecuentemente mediante la comunicación en red. Esto hace que las capacidades de red del componente de cómputo sean muy importantes de equilibrar para evitar que el cuello de botella sea la comunicación.

Una de las características principales de los componentes de cómputo si no tienen estado suele ser que en muchas ocasiones es posible paralelizar el trabajo más fácilmente que si tienen estado. Si el tipo de servicio que proveen es respuesta a peticiones, es posible utilizar los balanceadores de carga en frente de nuestros servicios para repartir la carga. Si obtienen tareas de una cola de tareas, la mayoría de ellas soportan más de un consumidor y podemos balancear la carga así. En nodos de cómputo de procesamiento de datos, es posible en ocasiones partir los datos en piezas que pueden ejecutarse en paralelo pudiendo analizar gran cantidad de datos usando técnicas como el famoso *MapReduce.*

Con todos estos componentes, existen diferentes formas de adquirir estos recursos que veremos a continuación. Las diferentes formas tienen consecuencias distintas en cómo se gestionan, pero todas ellas suelen tener las anteriores características implícitas o se requieren configurar.

Infraestructura como servicio, IaaS

Esta es la tecnología básica para obtener cómputo en la nube. En este caso lo que hacemos es obtener servidores, virtuales o no, como un servicio donde nosotros configuraremos sus funciones de cómputo.

En cierto sentido, incluso la infraestructura física trabaja en la misma abstracción, el servidor, aunque tendrá sus características concretas. En cierto sentido, si instalamos y configuramos una máquina física con una imagen básica estaríamos en el mismo estado que cuando un proveedor de nube (privada o pública) nos da una máquina virtual. La distinción es importante, pero en entornos DevOps se suele instalar algún tipo de orquestación incluso si trabajamos con equipos físicos como podrían ser algunas de las tecnologías de nube privada como Openstack y VMWare vCenter. Por este motivo, en este tema nos centraremos en estos casos de nube.

La práctica totalidad de servidores en la nube ofrecen este tipo de servicio como su servicio más fundamental y es ampliamente utilizado.

Cuando se inicializa un servidor, este llevara una instalación inicial que luego personalizaremos como necesitemos. Esta instalación inicial suele llamar la imagen de la máquina y puede contener la información que necesitemos. En esta asignatura hablaremos de Packer como una forma de genera estas imágenes.

Dependiendo de nuestro proveedor de este servicio, el tiempo de aprovisionamiento de la máquina podrá ir desde algo menos de un minuto a varias horas. A esto deberíamos sumarle el tiempo que necesitemos para configurar un nodo. La consecuencia de esto es que tendremos que trabajar en el tiempo de configuración y elegir un proveedor de nube rápido provisionando las máquinas si tenemos escenarios donde queremos autoescalar el servicio para adaptarnos a la demanda.

Sin considerar el coste de mantener y configurar este tipo de servicios, este suele ser la opción más económica si sacamos partido a los recursos que se nos ofrece.

Por otro lado, la máquina virtual incluye gran cantidad de recursos y, por ejemplo, habremos de pagar por la memoria o la CPU tanto si la usamos como si no. Este tipo de “fragmentación” del espacio sobrante puede llevar a subir los costes efectivos de esta solución. Esto implica que deberemos monitorizar el consumo tanto para detectar servidores colapsados como para detectar servidores poco ocupados que necesitan más trabajo o bien un tamaño menor.

Hablaremos de herramientas de monitorización en esta asignatura que nos pueden ayudar en estas tareas.

Plataforma como servicio, PaaS

Las plataformas como servicios frecuentemente se definen en base a una plataforma de ejecución que es capaz de tomar código y levantar procesos que se asemejan a servidores dependiendo del consumo que requiramos.

En este caso, la plataforma de ejecución suele conllevar restricciones importantes para que pueda tomar nuestro código y ejecutar y las aplicaciones suelen ser menos portables entre proveedores que con otras tecnologías. A cambio, este tipo de aplicaciones suelen traer herramientas sofisticadas de integración de nuestro código y de despliegue que pueden ayudar a reducir el esfuerzo en automatismos que debe realizar un equipo de DevOps. A cambio, este tipo de plataformas frecuentemente cobran el cómputo considerablemente más caro que otras soluciones y es un factor que tendremos que considera según vaya cambiando nuestra escala.

La solución más famosa de PaaS sería Heroku aunque las nubes suelen tener sus propias soluciones como AWS Beanstalk[[1]](#footnote-1), Google App Engine[[2]](#footnote-2) u otras.

Frecuentemente, las plataformas de PaaS ofrecen una autoescalabilidad fácil pero los nodos están restringidos a no tener ningún estado ya que no se gestionan individualmente.

Contenedores como servicio, CaaS

Las plataformas de contenedores como servicio son plataformas que permite ejecutar nuestros contenedores basados en las imágenes que nosotros generemos sin necesidad de gestionar los nodos de cómputo. Este tipo de plataformas está experimentando un gran crecimiento y hay un amplio ecosistema de herramientas que nos permiten generar a nosotros un CaaS, como podría ser Docker Swarm, Nomad o Kubernetes. Por otro lado, muchos proveedores de nube nos ofrecen un sistema como Kubernetes pero gestionado por ellos lo que se comporta como CaaS. Adicionalmente existen soluciones como AWS ECS [[3]](#footnote-3)que gestionan máquinas con contenedores automáticamente, soluciones como AWS Fargate[[4]](#footnote-4) o Azure Container Instances[[5]](#footnote-5) que no solo gestionan los contenedores, sino que no es necesario definir sobre que máquinas se van a ejecutar. En la actualidad, mucha de la actividad y uso se está realizando en torno a Kubernetes. Por tal motivo, estudiaremos en detalle este tipo de tecnologías en la asignatura de la máster dedicada a ello.

Funciones como servicio, FaaS

Las funciones como servicio son componentes de cómputo que se definen con una pieza de código o función que reacciona a un evento. En este paradigma, no se define un proceso que sirve peticiones u obtiene trabajo de una cola de mensajes, sino que la función es “ejecutada” cuando ocurre un evento, que podría ser una nueva petición o un nuevo mensaje en una cola de trabajo, y ejecuta hasta que el evento se completa y la ejecución de la función finaliza.

En cierto sentido, es si creáramos un servidor por cada tarea y lo destruyéramos cuando se completa la tarea. Frecuentemente, esas funciones ejecutan como contenedores efímeros como podría ser la principal implementación, AWS Lambda, aunque no todas las implementaciones utilizan contenedores como capa de abstracción como CloudFlare Worker[[6]](#footnote-6) que utilizan V8 context isolates, una tecnología basada en las máquinas virtuales de javascript. Un ejemplo de FaaS abierto que puede ejecutar sobre kubernetes es Knative[[7]](#footnote-7)

En el caso de FaaS existen varios impactos para DevOps que tenemos que considerar:

* **Cada función realizará una tarea relativamente pequeña**. Esto hace cada función sencilla pero la coordinación entre ellas y la arquitectura global puede ser complicada. Es importante tener una estrategia de compatibilidad entre las distintas funciones y una buena separación y coordinación de los despliegues al haber más piezas
* **Si no hay peticiones, no existe consumo**. Por este motivo las funciones o lambdas son muy utilizadas para peticiones infrecuentes y pueden conllevar un gran ahorro de recursos en estos casos.
* **La ejecución de una función implica arrancar un entorno**. Aunque esto es relativamente rápido es importante medir lo que se suele denominar como “Cold Start” o arranque en frio. Si la función se ha ejecutado recientemente, los proveedores suelen tener una caché de parte del arranque y las ejecuciones serán mucho más rápidas.
* **El coste de las ejecuciones** suele ser más elevado que la misma ejecución en un servidor o un contenedor siempre que ese contendor tenga una utilización alta.
* **La escalabilidad de las funciones** suele ser algo más rápido que la de máquinas virtuales o contenedores en muchos casos, aunque puede llevar a consumos muy elevados si no se controla correctamente por pequeños errores o *crawlers* remotos

Existen arquitecturas y proyectos completos que se empiezan a realizar con *Functions* o *Lambdas,* pero la mayoría no las usan exclusivamente. Sin embargo, estas funciones son extraordinariamente útiles para realizar automatizaciones alrededor del ecosistema DevOps. Por ejemplo, realizar *backups*, comprobaciones después de escalados, tareas recurrentes o pequeñas tareas muy esporádicas, pero importantes, que no encajan bien en otras piezas de la arquitectura. Es una herramienta importante, aunque ahora mismo no sea conveniente utilizarla exclusivamente.

2.4. Gestión del estado

La gestión del estado es una de las tareas más importantes y complicadas en aplicaciones DevOps. Mientras las aplicaciones sin estado suelen ser fáciles de escalar “horizontalmente”, es decir, añadir más piezas idénticas esto suele ser más complicado en la gestión del estado. En muchas ocasiones utilizaremos un escalado “vertical” es decir, aumentando las capacidades de cómputo y almacenamiento para almacenar y responder a consultas más rápidamente.

Existen componentes de gestión del estado con buenas capacidades de escalado horizontal y existen técnicas, como el *sharding*, que consiste en partir la información en bloques distintos y guardarlos en componentes distintos permitiéndonos escalar horizontalmente. A continuación, hablaremos de diferentes tipos componentes con estado y las principales consideraciones para elegir uno u otro y sus características.

Bases de datos

Las bases de datos son una categoría muy amplia de almacenes de datos. Existen varias clasificaciones distintas que afectan a cuál base de datos queremos elegir. A continuación, voy a detallar algunas formas posibles de clasificarlas para poder analizar mejor el problema. En muchas ocasiones la base de datos impacta fuertemente en el tipo de desarrollo que se va a realizar y en la velocidad y fiabilidad de este. Por este motivo, la elección de una base de datos suele resultar de un balance entre consideraciones de desarrollo (nos va a permitir desarrollar adecuadamente), de mantenibilidad (podemos y sabemos mantenerla) y de disponibilidad (va a ser estable en producción y nos va a permitir mantener el nivel de servicio requerido).

La primera clasificación se refiere al tipo de contendido y de consulta que vamos a realizar, considerando dos tipos, OLAP y Data Warehouse:

* **OLAP** (*On-Line Analytical Processing*) son bases de datos que se utilizan para dar servicio a los clientes en vivo respondiendo a preguntas, tradicionalmente sobre el estado actual y gestionando este estado. Son las bases de datos más utilizadas y la mayoría de las bases de datos SQL y muchas otras como las orientadas a documento o grafo frecuentemente se utilizan de esta forma. En estas bases de datos, es importante la velocidad de consulta y guardado y la integridad de los datos (véanse garantías como consistencia eventual y ACID).
* ***Data-Warehouse*** o almacenamiento de datos son bases de datos que se utilizan para almacenar datos históricos del progreso del sistema para un análisis posterior. En este tipo lo importante suele ser el coste de almacenamiento a largo plazo, la capacidad de consulta y agregación de grandes cantidades de datos y la capacidad de ingesta de grandes cantidades de datos en grupos (trabajos de backup diarios) o en vivo mediante un *stream*. No es tan importante el tiempo de respuesta de una escritura en concreto sino la velocidad del conjunto

La segunda de las clasificaciones es por tipo de interfaz exterior y “paradigma de datos” que exponen al desarrollador y operador. El paradigma más frecuente y utilizado es el relacional con el lenguaje SQL como el máximo exponente, pero desde hace unos años ha habido un movimiento para explorar otros paradigmas distintos, en ocasiones agrupados en torno al termino noSQL, pero que realmente son muy variados y merecen clasificaciones individuales:

* **SQL**: las bases de datos SQL son las más conocidas y utilizadas. Existen implementaciones de código abierto muy utilizadas como MySQL, PostreSQL o SQLite y otras de código privativo como Oracle DB extraordinariamente potentes. Son muy utilizadas en la industria. Su principal característica es la definición de esquemas basados en tablas y sus relaciones que permiten realizar consultas cruzadas bastante eficientemente. Debido a la madurez de las implementaciones, pueden ser aplicadas en muchos entornos
* **Orientadas a documentos:** las bases de datos orientadas a documentos almacenan un concepto de Documento y se basan principalmente en obtenerlo y procesarlo. En esta categoría entran desde bases de datos clave valor como Redis, bases de datos de documentos que permiten consultas más complejas como MongoDB o Couchbase y algunas bases de datos que veremos posteriormente de búsqueda como ElasticSearch.
* **Orientadas a grafo:** las bases de datos orientadas a grafo se basan en definir unas entidades o Nodos que se relacionan entre ellos mediante Vértices. La principal característica de estas bases de datos es que incluyen algoritmos para recorrer esas relaciones de formas potentes y con un rendimiento bueno.
* **Orientadas a columna:** las bases de datos orientadas a columna se basan principalmente en guardar documentos, pero el foco es en la especificación de las columnas y su almacenamiento conjunto. En lugar de guardar cada documento en un sitio, se guarda el valor de una columna para todos los documentos conjuntamente. Esto permite realizar agregaciones muy eficientemente y son muy utilizadas para *Data Warehouse* aunque no únicamente (frecuentemente utilizando familias de algoritmos como MapReduce). Obtener un documento completo suele ser algo más costoso, pero si los documentos contienen muchos campos y solo se van a utilizar algunos, el coste se reduce a diferencia de la mayoría de base de datos orientadas a documentos.

En general, la principal característica de las bases de datos es que los datos almacenados en ellas suelen tener valor. Por ese motivo al gestionar este tipo de componentes es esencial considerar la disponibilidad y tener un buen plan de recuperación frente a problemas.

* **Backups**: es esencial tener un sistema de backups con automatización para poder recuperarlos (no solo almacenar el backup, también un proceso para restaurarlo). Los backups permiten reducir la cantidad de datos perdidos en el caso de un incidente y aumentar la velocidad de restauración de servicio.
* **Migración de esquemas y datos:** es importante tener técnicas para el mantenimiento de los datos con las necesidades de la aplicación. Es frecuente que los datos deban cambiar de estructura, cambiarse esquemas, añadirse campos adicionales o migrar un tipo de organización a otra. Tener automatismos o al menos procesos para realizar estos cambios reduce drásticamente el número de desperfectos cuando estos cambios se necesitan.
* **Redundancia y alta disponibilidad:** la redundancia nos permite tener más de un componente idéntico disponible que puede reemplazar otro en caso de problema. Existen diferentes técnicas de redundancia y alta disponibilidad y algunas de ellas también permiten una escalabilidad horizontal. Las técnicas más frecuentes son el Activo-Pasivo, donde hay dos bases de datos con una funcionando (activa) y una segunda lista para trabajar con una copia idéntica de los datos si hubiera un problema. Activo-Activo permite a dos bases de datos estar trabajando simultáneamente repartiendo la carga. Esto solo aumentaría la redundancia es la caída de uno o varios nodos no hace la utilización subir por encima del 100%. En bases de datos puede ser complicado tener escrituras simultaneas en varios nodos por tener riesgo de pérdida de datos. Por esto existe otra técnica, Maestro-Esclavo o Replica Set donde uno de los nodos es el que gestiona las escrituras y el resto responden a las lecturas. Si los nodos de lectura pueden promocionar a un nodo de escritura cuando este se rompa, esto también ayudará a la disponibilidad. Una técnica que permite aumentar la disponibilidad de una forma indirecta es el *sharding*. Aunque el *sharding* no permite aumentar la disponibilidad total del sistema, puede disminuir el impacto de un problema. Si un *shard* no está disponible, puede ser posible servir los datos de los otros *shards* haciendo que el sistema esté solo parcialmente caído.

En cierto sentido, las siguientes categorías que veremos de almacenamiento también se consideran bases de datos en ocasiones y existen situaciones que una base de datos se puede clasificar de diferentes formas (por ejemplo, en ocasiones se utiliza Redis como una cola de mensajería o MongoDB como una caché).

A continuación, exploraremos otros tipos de almacenamiento centrándonos en que su caso de uso es suficientemente distinto como para que convenga analizarlas por separado.

Colas de mensajería

Las colas de mensajería se utilizan para distribuir mensajes entre diferentes componentes del sistema. Existen muchos tipos de colas de mensaje y diversas implementaciones. Estas en general permiten comunicar a un productor con uno o varios consumidores del mensaje. Una de las principales características de esta tecnología es que las peticiones son asíncronas, el productor envía el mensaje y el consumir puede recibirlo tiempo después. Esto permite aumentar la resistencia del sistema a picos de consumo ya que la cola de mensajes puede balancear la carga. Otra característica de las colas de mensajes es que permiten desacoplar las diferentes piezas del sistema. En cierto sentido, pueden actuar tanto como un balanceador de carga como un proxy reverso que en base a la petición determina quien debe atenderla.

Las colas de mensaje se consideran componentes con estado, ya que los mensajes que se están enviando pero que aún no se han recibido deben gestionarse dentro del servicio. Como el productor envía un mensaje, pero frecuentemente no se queda esperando a la respuesta, es importante que se controle si se pueden perder mensajes enviados y bajo que preceptos. Además, si no hay consumidores disponibles, un mensaje puede estar en la cola un tiempo largo y esto conllevaría un estado más grande.

Los principales patrones de consumo de las colas de mensajes son:

* **Colas de trabajo:** en estas se tiene un productor y varios consumidores. Todos los consumidores toman tareas de la misma cola y cada tarea o mensaje es consumida por solo uno de estos consumidores. Esta técnica permite distribuir la carga y atender a los mensajes rápidamente. Si uno de los consumidores falla, no se pierde el servicio solo se tardará más en atender un mensaje determinado.

![A picture containing clock  Description automatically generated](data:image/png;base64...)

Figura 1 Cola de mensajería en modo Cola de trabajo. Origen: documentación de RabbitMQ

* **Pub/Sub o publicación y suscripción: e**n este modelo, los mensajes se envían a un “tema” y los consumidores pueden apuntarse a uno o varios “temas” de donde recibirán todos los mensajes que lleguen. La principal diferencia con la cola de trabajo es que los mensajes que lleguen ahí se van a distribuir a todos los consumidores no solo a uno. Esto es un patrón apropiado para notificación de eventos ya que todos los que requieran actuar frente al evento pueden actuar cuando llegue el mensaje.

![A picture containing drawing, clock  Description automatically generated](data:image/png;base64...)

Figura 2 Representación de Pub/Sub o suscripción. Origen: documentación de RabbitMQ

* **Enrutado sofisticado:** muchos sistemas de mensajería permiten definir diferentes colas de mensajes dependiendo de características del mensaje. Esto permite realizar diferentes tipos de patrones más sofisticados.

![A picture containing text, clock  Description automatically generated](data:image/png;base64...)

Figura 3 Ejemplo de enrutado complejo basado en un tipo de mensaje. Origen: documentación de RabbitMQ

Por ejemplo, es posible repartir la carga entre diferentes colas de trabajo dependiendo de su urgencia. O es posible enviar solo los mensajes de error a una de las colas con más prioridad. También se puede usar para escuchar temas que no están predefinidos por el productor. Por ejemplo, frente a un event podría suscribirme a todos los eventos de urgencia alta mientras otro podría suscribirse a los eventos de un tipo en concreto sin importar su urgencia.

![A picture containing text, clock  Description automatically generated](data:image/png;base64...)

Figura 4 Ejemplo de enrutado complejo basado en patrones sobre el tipo de mensaje para varios temas. Origen: Documentación de RabbitMQ

* **Llamada a un procedimiento remoto:** esta técnica es menos usada ya que realmente implementa un protocolo de pregunta y respuesta tradicional donde el productor va a recibir una contestación del servicio consumidor. Para este tipo de casos de uso es más frecuente realize una llamada directa, pasando por un proxy reverse si es necesaria la flexibilidad. La principal desventaja de esto es que la petición no es asíncrona. Si el tiempo de respuesta es muy largo en la petición, es posible que queramos que la petición se realice de forma asíncrona. Para este tipo de problemas lo que haremos será crear una cola donde enviar las peticiones y una cola efímera para recibir la respuesta a ese único mensaje. De esta forma es posible enviar un sistema de pregunta respuesta asíncrono usado colas de mensajes.

![A close up of text on a black background  Description automatically generated](data:image/png;base64...)

Figura 5 Ejemplo de llamada a procedimiento remoto con respuesta usando colas de mensajes. Origen: Documentación de RabbitMQ

Las colas de mensajes son uno de los componentes con estado que, aunque son ampliamente utilizados, se tarda más de lo necesario en implementar. Muchos sistemas complejos comienzan desde el primer momento con una base de datos y acaban implementando algún tipo de sistema de trabajo asíncrona ad-hoc. Encontrar el momento idóneo para incluir una cola de mensajería en nuestra arquitectura es importante y puede evitar muchos problemas y tiempo de codificación, así como una mayor flexibilidad para adaptarse a los cambios de patrón de consumo de los mensajes.

Motores de búsqueda

Los motores de búsqueda son bases de datos especializadas en la búsqueda de información, frecuentemente de texto, aunque soportan búsquedas por campos en muchos casos. La búsqueda de consultas en documentos textuales tiene peculiaridades distintas a las de las consultas generales en las bases de datos. Mientras las consultas generales suelen ser precisas (o bien se cumple el criterio o no se cumple) y ordenadas por un criterio frecuentemente definido en la consulta (como puede ser ordenar por fecha), las búsquedas por texto suelen buscar por la aparición de ciertos términos, pero requieren de técnicas concretas. Por ejemplo, una búsqueda por dos términos frecuentemente será más probable que sea correcta si los términos están cerca uno de otro. Otra funcionalidad frecuente es la búsqueda de términos similares como plurales o en ocasiones sinónimos para ayudar a encontrar más documentos.

Existen varios tipos de motores de búsqueda tanto OpenSource como comerciales. En nuestro caso, hablaremos con más detalle de como usar uno de los más populares, ElasticSearch, en la sección aplicándolo a la creación de paneles de control y a la búsqueda de logs operativos en esta asignatura.

Cachés

Las cachés se utilizan para almacenar información que puede ser reconstruida a partir de otras fuentes para poder acceder a ella de una forma más rápida. Existen muchos tipos de componentes de caché y también es frecuente tener ciertas capas de caché internamente dentro de los componentes de cómputo.

Es importante tener presente una cosa, las cachés son extremadamente potentes si estamos resolviendo consultas idénticas frecuentemente, pero si los datos en los que se basan cambian podría quedarse obsoleta. Invalidar una caché que ha quedado obsoleta es un trabajo complicado de mantener en el tiempo y propenso a errores. Esto actúa limitando en los lugares en los que podemos utilizar cachés y la duración de estas.

Existen diferentes tipos de componentes de caché ya que se adaptan a diferentes dominios. A continuación, veremos algunos:

* **Caché respuesta completa**

Son cachés que se ponen delante de los servicios de cómputo y almacenan la respuesta completa a una petición por si esta pudiera repetirse.

Un ejemplo clásico son las páginas web públicas donde muchas páginas no son personalizadas o poco personalizadas y se envían a una gran cantidad de usuarios sin cambios. En estos casos una caché delante de nuestro servicio puede reducir mucho la carga que tienen que soportar los servidores. Un ejemplo de esta tecnología podría ser Varnish[[8]](#footnote-8) que es una caché Open Source muy utilizada en este dominio.

Un subtipo de estas cachés podrían ser los **CDN**[[9]](#footnote-9). Este tipo de cachés se suelen consumir como un servicio que no desplegamos, sino que está gestionado por otra empresa. Los CDN o redes de distribución de contenidos son sistemas que permiten almacenar o bien archivos estáticos o bien respuestas temporales a nuestros contenidos y replicarlos en múltiples regiones cerca de los usuarios. Se comportan como una caché que no solo reduce el número de peticiones recibidas por nuestros servicios, sino que además permiten responder más rápidamente ya que las peticiones tienen que viajar menos distancia en el caso de clientes lejanos. Algunos proveedores famosos de CDN podrían ser Akamai, CloudFlare of AWS CloudFront.

* **Cachés en memoria**

Este tipo de cachés son almacenamientos temporales en memoria que permiten un tipo de respuesta rápido. Normalmente son accedidos mediante un mecanismo de clave valor y permiten almacenar un dato por un tiempo limitado. Las dos más famosas son Memcachéd y Redis. Aunque Redis tiene bastante potencia y es utilizado para otros fines también.

Gestión de la configuración

La gestión de la configuración es una tarea complicada en sistemas con muchas piezas. La configuración consiste en las credenciales y la información de conexión entre las piezas, así como otra configuración que cambie como se va a ejecutar la funcionalidad como pueden ser opciones deshabilitadas en producción, distintas configuraciones de acceso al disco, un menor tamaño de cachés, etc.

La forma más frecuente de gestión de la configuración es mediante el aprovisionamiento. Cuando se provisionan nuevas versiones, la configuración es subida mediante ficheros de configuración, variables con entorno o ConfigMap de Kubernetes por ejemplo. En este sistema, la configuración esta almacenada en el sistema de aprovisionamiento y configuración que tengamos.

Esta técnica tiene como ventaja que no necesitamos tener un servicio adicional ejecutando para gestionar la producción y que los cambios de configuración siguen el mismo flujo de instalación de nuevas versiones lo cual incluye las validaciones y el flujo de despliegue.

La principal desventaja es que no permite desplegar la configuración fuera del ciclo de desarrollo y en ocasiones necesita poder configurarse. Un ejemplo típico son situaciones donde las direcciones de ciertos servicios o sus credenciales pueden cambiar en el tiempo fuera de la ventana de despliegue y por tanto es necesario cargar la configuración. Otro ejemplo frecuente son los secretos, que es conveniente controlar de forma distinta al código y que deben rotarse de forma automática.

Una de las principales soluciones Open Source para la gestión de secretos es Vault[[10]](#footnote-10). Para la gestión de configuraciones, aparte de muchas soluciones nativas de las diferentes nubes o la solución de Kubernetes mediante ConfigMap, es posible utilizar etcd[[11]](#footnote-11). Para tecnologías como Java es frecuente utilizar un Config Server, como podría ser el del framework Spring[[12]](#footnote-12).

Información de ejecución y sesión

La información de ejecución o sesión son las partes de información de una tarea de larga duración. El caso más frecuente es la información de sesión de un usuario que ha hecho *login* en nuestra aplicación y que puede tener algún tipo de información asociado a la sesión.

En muchas ocasiones, esta información puede solaparse y confundirse con las cachés. La principal característica es el impacto que tiene la pérdida de esta información. En el caso de las sesiones, si se pierde, es posible que no se pueda recuperar cierta información de la actividad del usuario como el hecho de que introdujo su contraseña. Esto podría forzar a hacer *login* otra vez, y por ello obliga a tratar este tipo de almacenamiento con técnicas algo distintas a las cachés puras.

Para almacenar este tipo de información, lo más frecuente es utilizar Redis o MongoDB, aunque en ocasiones se utilizan otros componentes como Memcachéd.

2.5. Conclusiones

En este tema hemos visto diferentes formas y perspectivas para analizar los componentes con un vocabulario que nos permitirá tener las nociones necesarias para analizar qué componentes son más idóneos en un proyecto y entender qué papel pueden jugar en una arquitectura más compleja.

Además, podremos reconocer un catálogo de problemas frecuentes que tienen componentes reusables que podemos adoptar. Esto nos ayudará a evaluar de una mejor manera las herramientas, y a saber buscar ciertos componentes más especializados cuando los necesitemos, en lugar de adoptar medidas parciales.

1.4. Referencias bibliográficas

* Stephens, R. (2015) *Beginning Software Engineering.* ISBN 9781118969168
* Silberschatz, A., Korth H., Sudarshan, S. (2010) *Database System Concepts Sixth.* McGraw-Hill. ISBN 0-07-352332-1
* Eric Redmond E., and Jim R. Wilson (2012) *Seven Databases in Seven Weeks: A Guide to Modern Databases and the NoSQL Movement.* ISBN 9781934356920
* Chodorow K., Bradshaw, S. (2019) *MongoDB: The Definitive Guide, 3rd Edition, Powerful and Scalable Data Storage.* O'Reilly Media. ISBN 9781491954461

A fondo

*MongoDB*

Documentación de MongoDB: <https://www.mongodb.com/>

MongoDB es una base de datos orientada a documentos muy popular y uno de los principales exponentes del movimiento NoSQL. Es interesante aprender un poco más de ella, especialmente de sus diferentes modos de despliegue y técnicas de escalabilidad horizontal.

Si queremos entrar en más detalle podemos estudiar la referencia bibliográfica: MongoDB: The Definitive Guide, 3rd Edition de O’Really

*RabbitMQ*

Documentación del sistema Open Source de colas de mensajería RabbitMQ <https://www.rabbitmq.com/>

Un buen sistema de mensajería con una gran documentación. Soporta muchos tipos diferentes de enrutado de mensaje y es una buena forma de entender diferentes patrones desde el punto de vista de un desarollador. Estudiarlo nos permitirá entender cuando puede ser posible proponer una cola de mensajes en general, aunque no sea esta implementación.

*Jepsen*

Website sobre sistemas distribuidos <https://jepsen.io/>

Si necesitamos una aplicación funcionado en sistemas distribuidos es interesante comprobar si ha sido evaluado.

Las evaluaciones son muy duras y exhaustivas y ningún sistema realmente pasa sin problemas, pero es bueno leer los tipos de problemas y consejos de configuración para entender las características operacionales del sistema que utilicemos. Principalmente publica sobre bases de datos.

AWS Lambda

AWS Lambda. Página web oficial.

<https://docs.aws.amazon.com/lambda/latest/dg/welcome.html>

Un buen recurso para aprender más sobre FaaS. Aunque hay mucho conocimiento específico de Lambda, los ejemplos y las primeras explicaciones permiten entender como se trabaja con lambdas, la estructura de los eventos, la firma de las funciones y este conocimiento es útil y bastante transferible.

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

1. CDN es

A. Caché Delivery Namespace, una tecnología que permite ofrecer namespaces B. Una tecnología de caché para almacenar resultados parciales por un tiempo corto

\*C. Una tecnología para servir contenido estático o cachéado desde múltiples localizaciones en el mundo (CDN significa Content Delivery Network, un tipo de solución que permite servir contenido, frecuentemente estático o cachéado, y que ofrece una red de servidores disponibles en todo el mundo para servir la información)

D. Un tipo de appliance que se despliega localmente

1. ¿Cuál es la principal desventaja de los sistemas de configuración dinámicos durante la ejecución?

A. Es imposible que pueden reaccionar a cambios de configuración fuera de la ventana de despliegues

\*B. Pueden convertirse es un punto de fallo único si no se gestiona cuidadosamente y requieren monitorización (Al ser un sistema de configuración dinámico durante la ejecución es posible cambiar el valor en cualquier momento no necesariamente durante el despliegue, aunque si no estuviera disponibles las aplicaciones podrían fallar al no obtener valores necesarios para su funcionamiento)

C. Siguen el mismo ciclo de vida de despliegue

D. B y C son correctas

1. ¿Cuáles son los dos patrones más frecuentes de las colas de mensajería?
   1. Pub/Sub y consistencia eventual
   2. ACID y colas de trabajo
   3. \*Pub/Sub y colas de trabajo (ACID es un tipo de garantía de las bases de datos y Consistencia eventual también. Pub/Sub y las colas de trabajo son patrones de consumo en las colas de mensajería)
   4. ACID y consistencia eventual
2. Las bases de datos OLAP son:
   1. \*Bases de datos que responden a peticiones en vivo sobre el estado actual (OLAP significa *Online Analytical Processing* y es una categoría de las bases de datos por su finalidad, no una forma de almacenar los datos y se basa en responder las peticiones rápidamente)
   2. Bases de datos para procesamiento masivo sobre información histórica
   3. Bases de datos principalmente NoSQL
   4. Bases de datos que almacenan datos organizándolos en el paradigma OLAP
3. ¿Cual es la principal diferencia entre las bases de datos orientadas a documento y a columna?
   1. Las bases de datos columnares almacenan cada columna junta en lugar de almacenar por filas
   2. Las bases de datos orientadas a documento permiten almacenar documentos con un número distinto de campos
   3. Las bases de datos columnares son muy utilizadas con tipos de algoritmos como *MapReduce*.
   4. \*Todas las respuestas anteriores son correctas (Estas bases de datos son dos tipos de bases de datos que almacenan los documentos complejos por columnas o bien como un documento frecuentemente compuesto)
4. ¿Son todos los componentes reusables con estado?
   1. Si, porque un componente reusable debe tener una lógica no especializada a nuestro problema y los componentes sin estado no se pueden configurar
   2. Si, porque los componentes reusables son bases de datos y cachés
   3. \*No, porque existen funcionalidades comunes frecuentes como pueden ser los proxies reversos o algoritmos de datos (Los proxies reversos o algoritmos de datos complejos como algunos de aprendizaje automático son ejemplos de componentes reusable con estado)
   4. No, porque todos los componentes deben ser sin estado sean reusables o no
5. FaaS es:
   1. Un tipo de base de datos con procedimientos almacenados
   2. \*Un tipo de despliegue de componentes de cómputo (Function as a Service es una técnica de desplegar funciones como nuestro pase de componente de cómputo)
   3. exclusiva de AWS con Lambda
   4. Un tipo de despliegue que nunca puede escalar hasta zero
6. ¿Cuáles de las siguientes son correctas?
   1. \*La B y la D (El escalado horizontal puede realizarse mediante técnicas como los Replica set y el escalado vertical consiste de dar más recursos a un componente)
   2. El escalado vertical, usando un componente con más recursos
   3. El escalado horizontal, solo disponible para componentes sin estado
   4. El escalado horizontal, por ejemplo, como Replica Sets para componentes con estado
7. ¿Cómo podemos repartir la carga entre varios nodos de cómputo para aumentar la capacidad del sistema?
   1. Con una cola de tareas
   2. Con un sistema Pub/Sub
   3. Con un balanceador de carga
   4. \*A y C son correctas (Pub/Sub permite repartir la carga entre varios nodos pero no aumenta la capacidad del sistema ya que todos ellos reciben el evento y este no se reparte)
8. ¿Cuáles son bases de datos persistentes?
   1. MongoDB, Spring Boot, Memcachéd
   2. MariaDB, PostgreSQL, Memcachéd
   3. \*MongoDB, PostgreSQL, MySQL (Ni Spring Boot ni Varnish son bases de datos. Memcachéd puede almacenar datos, pero al no poder persistirlos en disco no se utiliza como base de datos persistentes)
   4. PostgreSQL, IaaS, Varnish

1. <https://aws.amazon.com/elasticbeanstalk/> [↑](#footnote-ref-1)
2. <https://cloud.google.com/appengine>. Google App Engine empezó como PaaS pero esta lentamente moviéndose hacia el espacio de CaaS y es actualmente una solución híbrida. [↑](#footnote-ref-2)
3. <https://aws.amazon.com/ecs/> [↑](#footnote-ref-3)
4. <https://aws.amazon.com/fargate/> [↑](#footnote-ref-4)
5. <https://azure.microsoft.com/en-us/services/container-instances/#overview> [↑](#footnote-ref-5)
6. <https://workers.cloudflare.com/> [↑](#footnote-ref-6)
7. <https://knative.dev/> [↑](#footnote-ref-7)
8. https://varnish-caché.org/ [↑](#footnote-ref-8)
9. https://es.wikipedia.org/wiki/Red\_de\_distribuci%C3%B3n\_de\_contenidos [↑](#footnote-ref-9)
10. https://www.vaultproject.io/ [↑](#footnote-ref-10)
11. https://etcd.io/ [↑](#footnote-ref-11)
12. https://spring.io/guides/gs/centralized-configuration/ [↑](#footnote-ref-12)
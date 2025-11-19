Tema nº 3

Arquitectura de aplicaciones

Herramientas DevOps

Índice

[Esquema 3](#_Toc52771150)

[Ideas clave 4](#_Toc52771151)

[3.1. Introducción y objetivos 4](#_Toc52771152)

[3.2. Tipos de aplicaciones 4](#_Toc52771153)

[3.3. Tipos de arquitectura 8](#_Toc52771154)

[3.4. Aplicaciones monolíticas y appliances 9](#_Toc52771155)

[3.5. Aplicaciones multicapa 12](#_Toc52771156)

[3.6. Aplicaciones orientadas a microservicios 15](#_Toc52771157)

[3.7. Mallas de servicios: Service Mesh 17](#_Toc52771158)

[3.8. Conclusiones 19](#_Toc52771159)

[3.9. Referencias bibliográficas 19](#_Toc52771160)

[A fondo 21](#_Toc52771161)

[Actividades 23](#_Toc52771162)

[Test 24](#_Toc52771163)

Esquema

![](data:image/png;base64...)

Ideas clave

3.1. Introducción y objetivos

En esta lección vamos a hablar de los diferentes tipos de arquitectura, y sus componentes. Mencionaremos sus características y las consecuencias que acarrean a fin de poder elegir la opción que mejor se adapte a nuestras circunstancias.

Nos apoyaremos en el vocabulario de tipos de componentes que hemos estudiado en la lección anterior, lo que nos permitirá estudiar arquitecturas más complejas desde un punto de vista más abstracto.

Los objetivos que se pretenden conseguir en este tema son:

* Conocer diferentes tipos de «arquitecturas tipo» que nos permitan conocer distintas soluciones;
* Poder adaptar los patrones a nuestros problemas concretos;
* Entender distintos tipos de aplicaciones y sus consecuencias sobre el ciclo DevOps;
* Aprender a clasificar las aplicaciones considerando distintas facetas.

3.2. Tipos de aplicaciones

Existen diferentes tipos de aplicaciones y estás se relacionan entre ellas, dando lugar a situaciones complejas dentro de las empresas. Comenzaremos por establecer una distinción importante entre el tipo de aplicación, cómo y dónde se ejecuta nuestro código. Nuestra aplicación puede ejecutarse en un entorno bajo nuestro control o bien en un entorno no gestionado por nosotros. Esto dará lugar a diferentes patrones e impactará nuestro ciclo DevOps. Tenemos distintos extremos y la mayoría de las aplicaciones se encuentran en algún punto intermedio, con diferentes piezas en diversos lugares. Por ejemplo:

* Software que se esté ejecutando en hardware dedicado que solo se puede configurar una vez (microcontroladores, IoT, etc.)
* Aplicaciones que se estén ejecutando en equipos de clientes. *Appliances* que se ejecutan en un centro de datos de cliente, aplicaciones móviles, aplicaciones de escritorio, etc.
* Aplicaciones que se estén ejecutando en equipos de clientes, pero con control sobre qué versión se ejecuta (aplicaciones web de una única página, aplicaciones de escritorio que se actualizan automáticamente, librerías autogeneradas, etc.)
* Aplicaciones que componen un servicio que se da al cliente (páginas online, APIs automatizadas, terminales de punto de venta con un modelo SaaS, etc.)

Clasificación de los sistemas de acuerdo con la velocidad y coste de cambio

En general, debemos considerar dos facetas distintas para cada una de las diferentes piezas que componen nuestra aplicación:

* Control del lugar de ejecución, su entorno y dependencias

Es posible que podamos tener un control limitado (aplicaciones móviles que tienen que soportarse en muchos dispositivos distintos, aplicaciones web que tienen que ejecutarse en múltiples navegadores y tamaño de dispositivo) o un control alto como puede ser servidores gestionados por nosotros, o hardware diseñado y elegido por nuestra empresa.

* Capacidad para enviar actualizaciones y el coste de estas

Es probable que tengamos una capacidad limitada de enviar actualizaciones o una capacidad elevada. Por un lado, tenemos software que no puede cambiar fácilmente una vez liberado, como puede ser software embebido en hardware sin capacidad de actualizarse automáticamente o el software que antiguamente se liberaba en un CD para ordenadores sin internet. Por otro lado, tenemos situaciones en las que controlamos cuando liberar el software, como pueden ser aplicaciones en nuestros servidores con ventanas amplias de actualización o redundancia para poder hacer actualizaciones dinámicamente, o aplicaciones web que servimos en el momento.

A medio camino tenemos aplicaciones móviles que algunos usuarios actualizan, pero otros no, o aplicaciones de escritorio donde la actualización puede ser más o menos mala dependiendo de lo complicado que sea actualizar.

|  |  |  |
| --- | --- | --- |
|  | Difícil actualización | Fácil actualización |
| Entorno sin control | Librerías *open source*, aplicaciones de escritorio sin control sobre la actualización | Aplicaciones web servidas desde nuestros servidores |
| Entorno con control | Entornos embebidos sin conexión a internet | Software de servidor que se ejecute en nuestros propios servidores |

Es importante entender dónde se sitúan nuestras distintas piezas ya que esto influenciará nuestro ciclo DevOps. Por ejemplo, Microsoft no podía utilizar el mismo ciclo de desarrollo para Windows cuando tenía que imprimir CDs y enviar cajas a las tiendas. Recordemos que la mayoría de la gente no tenía internet de alta velocidad como ahora, que es posible obtener actualizaciones a través de internet. Otro ejemplo radica en la gestión de una aplicación móvil, donde los usuarios pueden decidir qué actualizar o qué no, en contraposición con una aplicación web donde nuestro servidor elige qué versión es enviada al usuario en un determinado momento.

Esta clasificación afecta al ciclo DevOps ya que impacta directamente a la velocidad máxima de iteración que tenemos al liberar nuevas versiones a los clientes, y por tanto, al valor de negocio. Si no podemos enviar nuevas actualizaciones más de una vez cada tres meses, aunque podamos hacer iteraciones internamente, la fecha de *release* influenciará nuestro ciclo de desarrollo.

Si somos capaces de liberar nuevas versiones con la frecuencia deseada, podemos optar por un ciclo con integración y despliegue totalmente continuo, donde cada cambio se libera a producción una vez que se han terminado sus pruebas de forma continua, liberándose múltiples versiones al día.

Es importante recordar que distintas partes de nuestra aplicación pueden tener restricciones diferentes, lo que nos dará lugar a un entorno híbrido, potencialmente con disferentes velocidades. Un ejemplo clásico de esto son las aplicaciones móviles con un *backend* controlado por el equipo de desarrolladores. En este caso, podremos liberar el *backend* tan frecuentemente como queramos, pero la actualización de la aplicación móvil depende del usuario y seguramente querremos que el *backend* soporte varias versiones antiguas de la aplicación. En esos casos seguramente liberemos el *backend* antes de la versión móvil (siendo compatible hacia atrás) e intentaremos que el protocolo sea muy adaptable para poder seguir liberando valor sin estar bloqueados por la aplicación móvil.

Aplicaciones de cliente: cliente ligero y cliente pesado

Una clasificación típica de aplicaciones de cliente es **cliente ligero o cliente pesado**.

Tradicionalmente, se conoce como cliente ligero a un ordenador liviano que se ha optimizado para establecer una conexión remota con un entorno informático basado en servidor. El servidor realiza la mayor parte del trabajo, y entre estas tareas se puede incluir iniciar programas de software, realizar cálculos y almacenar datos. Desde luego, esto contrasta con un cliente pesado o un ordenador convencional; el primero también está destinado a trabajar en un modelo cliente-servidor, pero tiene un poder de procesamiento local significativo, mientras que el segundo pretende realizar su función principalmente a nivel local.

Esta clasificación fue adoptada en las páginas web, donde si una página web se construía en el servidor y la mayoría de los cálculos se realizaban en el servidor entonces el navegador y la página actuaban como un cliente ligero.

Por el contrario, si el servidor expone una API sencilla y la mayoría de las funciones están en el cliente, en ocasiones se habla de un cliente pesado. Esto es frecuente en las aplicaciones móviles y en algunas aplicaciones de navegador (SPA[[1]](#footnote-1)) complejas. En cierto sentido, muchas aplicaciones con una construcción compleja en el servidor y una construcción compleja en el cliente rompen esta dicotomía. Una combinación de ambos estaría representada por una aplicación con *Machine Learning* ejecutándose en el servidor, y una aplicación compleja con estado en el navegador.

3.3. Tipos de arquitectura

La arquitectura de software se refiere a las **estructuras fundamentales de un sistema de software y la disciplina de crear tales estructuras y sistemas**. Cada estructura comprende elementos de software, relaciones entre ellos y propiedades de elementos y relaciones. La arquitectura de un sistema de software es una metáfora análoga a la arquitectura de un edificio. Funciona como un plan para el sistema y el proyecto en desarrollo, y establece las tareas necesarias que deben ser ejecutadas por los equipos de diseño.

A diferencia de lo que ocurre con la arquitectura de edificios, no existe una buena definición de las partes que la componen y muchas veces la definición de lo que compone una aplicación o su arquitectura son construcciones sociales, pero son muy útiles para entender y analizar el problema.

En general, **arquitectura se refiere a una noción definida de los aspectos más importantes del diseño interno de un sistema de software**. Una buena arquitectura es especialmente importante en el software, de lo contrario se volverá más lento y costoso agregar nuevas capacidades en el futuro.

La arquitectura suele referirse a:

* Un cuerpo de código que los desarrolladores consideran una sola unidad.
* Un grupo de funcionalidades que los clientes de la organización ven como una sola unidad.
* Una iniciativa que los inversores y accionistas ven como un presupuesto único.

En nuestro caso, nos centraremos en las diferentes partes desplegables de una aplicación y en cómo estas se relacionan entre sí. Nuestro objetivo es analizar la arquitectura y enfocarnos sobre los impactos que tiene para un ciclo DevOps.

Hablaremos sobre cómo se despliegan las partes con y sin estado; cómo se conectan las diferentes piezas; cómo impacta el fallo de una pieza al sistema global, como aumentar la disponibilidad de sistema, etc.

Por último, hay que mencionar que la arquitectura de una aplicación es cambiante (es posible iterar e ir transformándola) y no permite clasificarse completamente. En un sistema complejo, la arquitectura será única o parcialmente única. Aun así, hay ciertos patrones muy comunes que se ven con pequeñas variaciones en muchos proyectos o que son muy útiles para razonar sobre los diferentes balances y consecuencias de una implementación y que es imprescindible conocer.

Para poder considerar los tipos de arquitectura desde un punto de vista DevOps es importante conocer los tipos de componentes más comunes y como operarlos, para posteriormente ver como se organizan en tipos de arquitectura completas.

3.4. Aplicaciones monolíticas y *appliances*

Un sistema de software se llama "monolítico" si tiene una arquitectura en la que los aspectos funcionalmente distinguibles (por ejemplo, entrada y salida de datos, procesamiento de datos, manejo de errores y la interfaz de usuario) están juntos, en lugar de contener componentes arquitectónicamente separados.

Una aplicación monolítica es autónoma e independiente de otras aplicaciones informáticas. La filosofía de diseño es que la aplicación es responsable no solo de una tarea en particular, sino que puede realizar todos los pasos necesarios para completar una función en particular. Hoy en día, algunas aplicaciones de finanzas personales son monolíticas en el sentido de que ayudan al usuario a llevar a cabo una tarea completa, de extremo a extremo, y son silos de datos privados en lugar de partes de un sistema más grande de aplicaciones que trabajan juntas. Algunos procesadores de texto son aplicaciones monolíticas. Estas aplicaciones, a veces, están asociadas con computadoras mainframe.

Una segunda acepción de una aplicación monolítica, es una aplicación que está compuesta de una única capa de aplicación, frecuentemente apoyada de una base de datos que puede estar desplegada o no junto a ella. En nuestro caso esta definición la consideraremos como una aplicación con dos capas, y la veremos en la siguiente sección ya que tiene implicaciones diferentes a nivel de operaciones.

En nuestro caso, hablaremos de una aplicación monolítica cuando se compone de un único componente desplegable.

Una faceta importante es que el término arquitectura monolítica se usa en ocasiones para aplicaciones sin una arquitectura definida. Esto puede o no ocurrir cuando hay un único componente desplegable. Podría ocurrir que, dentro del componente, existe una división en diferentes capas y o algún tipo de arquitectura interna. Las aplicaciones monolíticas, si tienen que guardar un estado interno, tienen que gestionarlo en la misma pieza desplegable. Es muy frecuente que las aplicaciones en general requieran de algún tipo de estado o persistencia, la mayoría de las consideraciones a continuación emanan de esa característica. Si nuestra aplicación no tiene estado, se podría considerar como un componente de cómputo y hablaremos más delante de como operar con componentes de cómputo puro.

Desde el punto de vista DevOps, las aplicaciones monolíticas suelen tener características operacionales muy concretas.

Estado integrado

La primera, es que las arquitecturas monolíticas tienen el estado integrado en la aplicación. Esto implica que no es posible actualizar la parte de cómputo simplemente reemplazando la pieza de cómputo, sino que será necesario entrar dentro del componente para configurar una nueva versión. Esto puede ser sencillo (subir un binario nuevo en el caso de Go por ejemplo) o complejo, si tenemos que asegurarnos de que todas las dependencias estén correctamente instaladas como en el caso de lenguajes interpretados.

Actualización combinada

Otra característica es la complejidad y en muchos casos imposibilidad, de realizar actualizaciones sin cortar el servicio. Si no paramos el servicio, las actualizaciones pueden conllevar errores para las peticiones durante la actualización. Aunque hay técnicas para mitigar esto como levantar dentro del monolito dos veces el mismo proceso, son procesos delicados que implican un coste adicional para comprobar que funcionan correctamente con todas las actualizaciones.

Simplicidad de operaciones

A cambio, al ser un único componente que desplegar esto nos permite reducir mucho la necesidad de configurar la conexión entre diferentes componentes y hace mucho menos complicada la instalación manual del sistema.

Esta característica es frecuentemente utilizada cuando no vamos a ser nosotros los que despleguemos. Por este motivo muchas herramientas incluso cuando no han sido diseñadas con una arquitectura monolítica, se despliegan de forma monolítica cuando se distribuyen para ejecutar en centro de datos privados.

Por ejemplo, aunque GitHub no es ni mucho menos un monolítico en su versión SaaS, distribuyen una versión como monolito para instalar en entornos segregados donde GitHub no va a llevar las operaciones sino el cliente. En estos casos, la simplicidad en las operaciones compensa los problemas operativos.

Consejos de uso

Si utilizamos una arquitectura de despliegue monolítica hay algunas técnicas que podemos intentar aplicar:

* **Separar los datos de la aplicación todo lo que se pueda**

Deberíamos intentar, siempre que sea posible, separar el estado del cómputo, aunque sea dentro de un mismo componente desplegable. Esto lo podemos lograr usando una base de datos instalado en el mismo proceso, separando los datos de la aplicación. Otra técnica es montar un volumen de disco distinto al de la aplicación, separado que se pueda montar y desmontar, lo que nos permitiría migrar los datos de una instalación a otra. Además, esto facilita la realización de *backups* de ese volumen mediante *snapshots*.

* **Diseñar y comprobar periódicamente un plan de despliegue desde cero**

Aunque las actualizaciones frecuentes sean comúnmente de la aplicación sin desplegar, es importante poder desplegar la aplicación desde cero. Una buena práctica es recuperar las copias de seguridad de los datos sobre un despliegue nuevo y realizar pruebas sobre este. Eso nos asegura que el despliegue desde cero y la recuperación de datos funciona, aunque la aplicación donde se originaron los datos este dañada (potencialmente también en la copia de seguridad).

* **Practicar la respuesta ante cortes de servicio**

Aunque tengamos un servicio con ventanas naturales de parada de servicio (noches, fines de semana) es importante tener un método para declarar que el servicio esta caído. Esto es conveniente en todas las arquitecturas, pero es esencial en los despliegues monolíticos ya que las probabilidades de un corte total del servicio son mucho mayores.

Con estos consejos, podemos mitigar los problemas de este tipo de arquitecturas y usarlas cuando sean convenientes. Aun así, en general, optaremos por una arquitectura distinta si podemos. Existen formas sencillas de pasar de un despliegue en monolito a un despliegue multicapa simplemente separando la base de datos en un componente distinto. Desde el punto de vista de arquitectura de aplicación esto es frecuentemente considerado un monolito, pero desde el punto de vista operacional comparte muchas características con una arquitectura multicapa.

3.5. Aplicaciones multicapa

Las aplicaciones multicapa son aplicaciones compuestas por diferentes componentes que se llaman los unos a los otros de una forma lineal. Es decir, cada componente es llamado por el inmediatamente anterior y llama al posterior. En ocasiones se permite que un componente se “salte capas” y llame a otros componentes posteriores, pero nunca debería llamarse a capas anteriores. Las capas que podemos saltar se suelen denominar “Capas abiertas” y las que no “Capas cerradas”.

El ejemplo más clásico es una arquitectura de dos capas, una capa de aplicación y otra capa de almacenamiento de datos.

El código de la aplicación puede en ocasiones considerarse un monolito o no, dependiendo de la definición que se use y de la estructura interna. Este tipo de arquitecturas son muy conocidas y sencillas de mantener y si se tiene cuidado de que la capa de aplicación sea de computación pura y no se permite introducir estado de ningún tipo ahí, es posible desplegar la capa de aplicación múltiples veces para aumentar la escalabilidad horizontal.

Base de datos

Capa de aplicación

Balanceador de carga

Capa de aplicación

Este tipo de arquitecturas permiten combinar un desarrollo simple para equipos pequeños o poco experimentados, con una razonable escalabilidad.

Es importante notar que en este diagrama la base de datos sigue siendo un único componente. Deberíamos explorar alguna de las técnicas para componentes de base de datos que vimos en el tema anterior como puede ser un Activo-Pasivo, un Replica Set, etc.

Las arquitecturas multicapa suelen funcionar mejor cuando el propio software está diseñado internamente como multicapa, ya que permite juntar y separar las capas según sea necesario. El principal problema es que el código de cada una de las capas puede ir creciendo con partes no relacionadas y que frecuentemente una nueva funcionalidad, requiere cambios en todas las capas. Esto ocasiona problemas a la hora de coordinar a múltiples equipos que puedan estar realizando cambios muy frecuentes y si el aislamiento no es bueno entre el código de los diferentes equipos, problemas localizados pueden afectar al rendimiento de todo el sistema. Por ello cuando empezamos a implicar a varios equipos puede ser útil explorar otras arquitecturas entre equipos como pueden ser los microservicios.

3.6. Aplicaciones orientadas a microservicios

Los microservicios son un tipo de arquitectura que permite gestionar grandes aplicaciones con muchos equipos cooperando juntos de forma que se distribuye el trabajo entre diferentes equipos, y se crean capas de abstracción entre los equipos donde gestionan microservicios.

Las arquitecturas de microservicios han sido ampliamente utilizadas y han tenido un ciclo de optimismo en aquellos lugares donde se han utilizado. Aunque este tipo de arquitectura ha tenido mucho éxito, desafortunadamente ha sido aplicada también en sitios donde arquitecturas con una menor escala hubieran colaborado y actualmente hay debate sobre en qué entornos deberían utilizarse y cuando no.

Para comenzar, vamos a definir los puntos principales sobre una arquitectura orientada a microservicios:

* Divide las piezas en componentes llamados microservicios;
* Cada microservicio se comunica con otros microservicios mediante protocolos de petición y respuesta (como puede ser HTTP o gRPC) o mediante envío de mensajes;
* Los microservicios no deben acceder a bases de datos compartidas, sino que cada servicio gestiona su propio estado;
* No existe una exigencia de que cada microservicio esté formado por un único componente, pero si deben exponer una interfaz única como forma de exponer funcionalidad al sistema completo;
* Los microservicios deben ser resistentes a problemas en otros microservicios impactando el servicio global lo menos posible.

Probablemente, la consideración más importante es que los microservicios no significan que no tengamos más arquitectura que hacer, sino que a alto nivel solo trataremos con microservicios gestionados por distintos equipos que se comunican mediante protocolos sencillos; pero cada uno de estos microservicios tendrá una arquitectura concreta. Los microservicios más sencillos, sin estado, podrían estar compuestos de un único componente. Los microservicios con estado frecuentemente intentarán gestionar ese estado en un componente separado y tendrán al menos dos componentes. Es posible que un componente tenga una arquitectura compleja.

La principal ventaja de los microservicios es que disminuyen la necesidad de coordinación innecesaria por las operaciones entre los equipos que mantienen los microservicios. Será necesaria la coordinación para utilizar la documentación y consumir un servicio u otro o analizar casos de uso complejos, pero se evitarán las discusiones sobre si un cambio debiese o no ir en una *release* junto con otro cambio de otro equipo sobre el mismo componente.

La Ley de Conway[[2]](#footnote-2) indica que una arquitectura a gran escala seguirá los patrones de comunicación de una organización. Una de las principales características de las arquitecturas de microservicios es que requiere y fomenta equipos independientes que mantienen un sistema y son responsables de él. Esta forma de organizarse está muy alineada con los DevOps, donde los diferentes equipos llevan sus propias operaciones y cada microservicio se comporta como una mini-organización independiente con su propio equipo.

Sin embargo, si tenemos un único equipo de, por ejemplo, menos de ocho personas, el hecho de partir la aplicación en muchos componentes desplegables separadamente, no implica que estemos siguiendo una arquitectura de microservicios. Esto no significa que la división no pueda ser una buena idea, ya que una vez que tenemos las herramientas y automatismos, el coste de cada componente puede no ser tan grande y traernos beneficios, pero no obtendremos la mayoría de las ventajas que tienen las arquitecturas orientadas a microservicios.

Por último, los microservicios pueden conllevar un cierto nivel de duplicidad ya que se busca evitar dependencias entre diferentes equipos. La principal dependencia evitable es la lógica de comunicación entre los microservicios, por ejemplo, cómo se llaman los otros microservicios, cual es la política adecuada de reintentos y la latencia esperada, donde se deben reportar los problemas con ese servicio automáticamente, etc. A continuación, hablaremos de las mallas de servicio que ofrecen una solución a este tipo de problemas.

3.7. Mallas de servicios (Service Mesh)

Las mallas de servicios son un complemento y una herramienta frecuentemente utilizada junto con microservicios. En los microservicios, hemos visto que cada servicio puede llamar a otro mediante protocolos sencillos. Cuando la cantidad y la escala de los microservicios aumenta, puede ser conveniente generar patrones de comunicación entre los microservicios que nos permitan tener visibilidad sobre cómo se comportan y dotar de un poco más de inteligencia a la red.

Las mallas de servicio son una capa de infraestructura configurable que permite una comunicación rápida, con baja latencia y con capacidad de grandes cargas en gran cantidad de servicios.

La principal característica de las mallas de servicio es que cada servicio tiene una pieza junto a él que interpreta las llamadas a otros servicios del mesh e implementa la lógica que esté implementada para esa ruta. Inicialmente, algunas mallas implementaban esa lógica como librerías, pero con el tiempo la mayoría de las implementaciones generan un proxy reverso local para poder ser más interoperables con diferentes lenguajes.

Las mallas de servicio son muy frecuentemente utilizadas con despliegues de contenedores, aunque hay implementaciones sin contenedores.

Los principales componentes de una malla de servicios son

* **Marco de orquestación de servicios.** A medida que se agregan más servicios y componentes a la infraestructura de una aplicación, una herramienta separada para monitorear y administrar el conjunto de los componentes se vuelve esencial. Esta herramienta es frecuentemente Kubernetes que se estudiará en detalle en la asignatura de contenedores.
* **Servicios e instancias.** Una instancia es una copia única en ejecución de un microservicio. A veces la instancia es un componente único. Los clientes rara vez acceden a una instancia directamente; más bien acceden a un servicio, que es un conjunto de instancias idénticas que es escalable y tolerante a fallos.
* **Proxy sidecar.** Un proxy de sidecar se ejecuta junto con una sola instancia. El propósito del proxy de sidecar es enrutar, el tráfico desde y hacia el componente al que apoya. El sidecar se comunica con otros proxys de su mismo tipo y es administrado por el marco de orquestación. Muchas implementaciones de malla de servicio usan un proxy sidecar para interceptar y administrar todo el tráfico de entrada y salida a la instancia para asegurarse que siempre se está usando.
* **Servicio de descubrimiento**. Cuando una instancia necesita interactuar con un servicio diferente, necesita encontrar y descubrir una instancia saludable y disponible del otro servicio. Normalmente, la instancia realiza una búsqueda de DNS para este propósito. El marco de la orquestación de componentes mantiene una lista de instancias que están listas para recibir solicitudes y proporciona la interfaz para consultas DNS.
* **Balanceo de carga.** La mayoría de los *frameworks* de orquestación ya proporcionan balanceo de carga de capa 4 (capa de transporte). Una malla de servicio implementa un balanceo de carga de capa 7 (capa de aplicación) más sofisticado, con algoritmos más ricos y una gestión de tráfico más potente. Los parámetros de equilibrio de carga se pueden modificar a través de API, lo que hace posible orquestar implementaciones azul-verde o canarios[[3]](#footnote-3).
* **Cifrado.** La malla de servicios puede cifrar y descifrar solicitudes y respuestas, eliminando esa carga de cada uno de los servicios. La malla de servicio también puede mejorar el rendimiento al priorizar la reutilización de las conexiones existentes y persistentes, lo que reduce la necesidad de la creación computacionalmente costosa de otras nuevas (la mayoría de la criptografía para los protocolos como TLS consume muchos más recursos al inicializar la comunicación que para enviar tráfico). La implementación más común para encriptar el tráfico es el TLS mutuo (mTLS), donde una infraestructura de clave pública (PKI) genera y distribuye certificados y claves para el uso de los proxies sidecar.
* **Autenticación y autorización.** La malla de servicio puede autorizar y autenticar solicitudes realizadas desde fuera y dentro de la aplicación, enviando solo solicitudes validadas a instancias.
* **Soporte para el patrón del interruptor de circuito**. La malla de servicio puede admitir el patrón de interruptor, que aísla las instancias poco saludables, y luego las vuelve a colocar gradualmente en el grupo de instancias saludables si vuelven a funcionar.

No todas las implementaciones ofrecen todas las opciones enumeradas arriba, pero sí muchas similares, y brindan una visión de lo que suelen proporcionar. Algunas de las implementaciones de *Service Mesh* más populares son *Istio* o *Linkerd*.

3.8. Conclusiones

Es necesario comprender la arquitectura de una aplicación completa para desarrollar correctamente un ciclo DevOps. Las técnicas DevOps tienen un impacto en la arquitectura y ésta en las técnicas DevOps a utilizar, lo que implica que es necesario entender diferentes patrones de arquitectura, para saber analizar las necesidades operacionales de una aplicación.

En este tema hemos visto diferentes arquitecturas y sus patrones. También hemos estudiado diferentes tipos de aplicaciones para conocer qué necesidades e impactos tienen sobre la arquitectura.

El conocimiento de los potenciales de arquitecturas nos permite elegir la más idónea; por ejemplo, podemos evitar un monolito o segregar su estado si queremos alta disponibilidad. O bien, evitar seguir todas las restricciones de los microservicios en un sistema si tenemos una empresa pequeña que no va a crecer tan rápido, obviando algunos problemas de mantenibilidad que traen aparejados.

3.9. Referencias bibliográficas

* Richards, M. (2015) *Software Architecture Patterns.* O'Reilly Media, Inc. ISBN: 9781491924242
* Miranda, G. (2018) *The Service Mesh.* O'Reilly Media, Inc. ISBN: 9781492031314
* RedHat Inc. (s.f.) What's a service mesh? Recuperado el 20 de noviembre de 2020 de <https://www.redhat.com/en/topics/microservices/what-is-a-service-mesh>

A fondo

*Making Architecture matter*

Vide de Martin Fowler en 2015 <https://www.youtube.com/watch?v=DngAZyWMGR0>

He aquí una interesante reflexión de lo que significa la arquitectura una vez que se adoptan los preceptos ágiles. Explica alguna de las connotaciones que tiene la arquitectura y da varias reflexiones y definiciones que ayudarán a entender que debemos tener en cuenta cuando reflexionemos sobre las nuestras.

*What is a Service Mesh*

Articulo de Redhat sobre Service meshes <https://www.redhat.com/en/topics/microservices/what-is-a-service-mesh>

Este artículo entra en más detalles sobre los microservicios y nos permite conocer ciertos términos y empezar a explorar su uso y algunas de las implementaciones más populares como *Istio*.

*Fault Tolerance in a High Volume, Distributed System*

Articulo sobre tolerancia a errores en sistemas distribuidos <https://netflixtechblog.com/fault-tolerance-in-a-high-volume-distributed-system-91ab4faae74a>

Un artículo muy influyente sobre técnicas para mantener una alta disponibilidad en sistemas distribuidos con múltiples dependencias. Uno de los artículos que introducen muchas de las técnicas de Service Mesh en 2012.

*Microservicios*

Compendio de artículos y guías sobre los microservicios <https://martinfowler.com/articles/microservices.html>

Un compendio de artículos sobre los microservicios y un buen punto de partida para aprender más sobre ellos. Es interesante leer las diferentes facetas que se exploran al estudiar sobre los microservicios.

Test

1. El coste de actualizar afecta al ciclo DevOps y la arquitectura porque:
   1. Los errores afectan durante más tiempo, lo que implica que la arquitectura tiene que fomentar la predictibilidad.
   2. La reproducibilidad de los entornos se convierte en esencial ya que descubrir un problema después de liberar es muy costoso
   3. \*Todas las otras respuestas son correctas (Un alto coste de actualización intrínseco afecta a todas las fases DevOps y debe traducirse en una arquitectura adaptada al problema)
   4. No es tan fácil probar el valor de negocio de una actualización con los usuarios
2. Las aplicaciones de navegador son siempre de cliente pesado:
   1. No siempre, por ejemplo, las aplicaciones de una única página regidas por JavaScript (SPA) son de cliente ligero
   2. No, es posible que sean ejecutadas con un navegador ligero como puede ser Safari o Firefox
   3. \*No, las aplicaciones que no implementan la lógica en el navegador (poca cantidad de JavaScript) se asemejan filosóficamente a los denominados clientes ligeros quedando en un lugar intermedio (La clasificación de cliente ligero surge en un contexto distinto, pero, traduciéndola a la actualidad, un cliente en el cual cada página es solo de presentación y toda interacción resulta en una petición al servidor se asemeja a un cliente ligero).
   4. Si, los navegadores modernos son necesariamente pesados
3. Las aplicaciones monolíticas...:
   1. Frecuentemente tienen el estado integrado
   2. Es sencillo mantenerles operando sin cortes de servicio mientras actualizamos
   3. Es conveniente mantener los datos lo más segregados posible para la mantenibilidad a largo plazo
   4. \*A y C son correctos (En las aplicaciones monolíticas es difícil no tener cortes de servicio en todas las actualizaciones, aunque se puede mitigar su impacto con buenas prácticas para muchas de las actualizaciones)
4. Las aplicaciones multicapa...:
   1. \*Se componen de diferentes capas con un orden donde solo se puede llamar a capas posteriores (Las capas son llamadas desde capas anteriores y pueden llamar a capas posteriores, es decir, no pueden llamar a la anterior o anteriores y pueden estar desplegadas en componentes distintos)
   2. Se componen de un único componente con muchas capas y no pueden estar distribuidas entre varios componentes
   3. Se componen de diferentes capas donde todas pueden llamarse entre si
   4. Se componen de capas donde cada capa solo puede llamar a su capa anterior y posterior
5. La ley de Conway…:
   1. Postula que el consumo de energía por unidad de superficie en los procesadores se mantiene constante
   2. Postula que deberíamos organizar la arquitectura en microservicios para seguir la organización de empresas más común
   3. \*Postula que la arquitectura de un sistema en una organización sigue los patrones de comunicación de la organización (La ley de Conway postula que las conexiones entre componentes implican comunicación entre equipos, por tanto, las conexiones seguirán los patrones de comunicación de una organización)
   4. Postula que las arquitecturas de microservicios no pueden funcionar salvo en empresas con un solo equipo
6. Las mallas de servicios:
   1. No puede usarse en una arquitectura de capas
   2. Son un tipo de arquitectura opuesta a los microservicios
   3. Son un tipo de componente que se despliega separadamente al resto de componentes del sistema
   4. \*Es una técnica para gestionar la comunicación de componentes (La malla de servicios de una técnica de arquitectura que habilita un tipo de comunicación concreto para aumentar la comunicación, frecuentemente utilizado en sistemas de microservicios)
7. Las aplicaciones web servidas como SaaS son un ejemplo de:
   1. Aplicaciones difíciles de actualizar, ya que son muy propensas a romperse
   2. Aplicaciones con un entorno muy controlado
   3. \*Aplicaciones de fácil actualización, pero con un entorno sin control (En las aplicaciones web en general no controlamos la versión del navegador, pero al ejecutar desde nuestros servidores podemos controlar que versión servimos)
   4. Aplicaciones de fácil actualización y entorno con alto control
8. Los *appliances* que distribuimos a clientes son:
   1. Aplicaciones que frecuentemente son despliegues monolíticos para facilitar la forma de desplegar a los clientes
   2. \*Todas las respuestas son correctas (Los *appliances* son frecuentemente utilizados por clientes sin que tengamos acceso a su infraestructura, lo que influye en su facilidad para desplegar, pero en nuestro poco control sobre la actualización)
   3. Aplicaciones difíciles de actualizar ya que los clientes suelen tener control sobre el ciclo de actualizaciones
   4. Un tipo de aplicaciones compuestas por un único componente, frecuentemente desplegadas para realizar una función concreta en un *datacenter* físico o virtual
9. Las bases de datos:
   1. No pueden formar parte de una arquitectura de microservicios
   2. Son frecuentemente compartidas por varios microservicios
   3. \*Ninguna de las otras respuestas es correcta (Las bases de datos son una pieza de software reusable que puede ser un componente o parte de uno y como componente puede estar dentro de un microservicio, pero no compartido entre ellos)
   4. No pueden usarse en monolitos ya que las bases de datos son siempre un componente desplegable separado
10. Istio es…:
    1. Un balanceador de carga
    2. Un sistema de cache
    3. Una implementación de bases de datos NoSQL
    4. \*Una tecnología de Service Mesh (Istio es una de las implementaciones más populares de *Service Mesh* para *Kubernetes*)

1. Single Page Application o aplicación de una única página. Son aplicaciones de navegador que gestionan su estado completamente sin refrescos desde Javascript. Véase: <https://es.wikipedia.org/wiki/Single-page_application> [↑](#footnote-ref-1)
2. https://es.wikipedia.org/wiki/Ley\_de\_Conway [↑](#footnote-ref-2)
3. Los canarios o *canary deployments* es una técnica de despliegue que consiste en desplegar una nueva version de un componente y enruta un subconjunto del tráfico para comprobar si el tiempo de respuesta o tasa de errores cambia significativamente antes de comenzar a liberar una nueva version. [↑](#footnote-ref-3)
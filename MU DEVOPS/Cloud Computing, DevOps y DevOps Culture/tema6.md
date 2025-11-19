Tema 6

Cloud Computing

Cloud Computing, DevOps and DevOps Culture

Índice

[Esquema 3](#_Toc77150260)

[Ideas clave 4](#_Toc77150261)

[6.1. Introducción y objetivos 4](#_Toc77150262)

[6.2. Tipos de nube 6](#_Toc77150263)

[6.3. Niveles de servicio 8](#_Toc77150264)

[6.4. Proveedores de nube pública 10](#_Toc77150265)

[6.5. Aplicaciones móviles y nube 11](#_Toc77150266)

[6.6. Referencias bibliográficas 13](#_Toc77150267)

[A fondo 14](#_Toc77150268)

[Test 15](#_Toc77150269)

Esquema

![](data:image/jpeg;base64...)

Ideas clave

6.1. Introducción y objetivos

DevOps se originó en las, así llamadas, empresas «nacidas en la web» (empresas que se originaron en la Internet) como Etsy, Flickr y Netflix. Mientras estas empresas daban solución a los desafíos tecnológicos complejos de gran escala, tenían arquitecturas bastante simples (a diferencia de las grandes empresas que crecieron en torno a los sistemas heredados y/o a través de adquisiciones y fusiones), con sistemas de múltiples y complejas tecnologías que tenían que interactuar. Como puedes imaginar, en la actualidad todas las empresas de tecnología se enfrentan a nuevos retos y desafíos, como los modelos de entrega de aplicaciones móviles y de nube y las cadenas de suministro de software. En los siguientes apartados explicaremos algunos de estos retos y, sobre todo, veremos cómo puede ayudar DevOps a resolverlos con la ayuda del Cloud Computing.

Uno de los cambios más importantes que ha afectado a DevOps (y, de hecho, también lo ha ayudado a madurar) es el Cloud Computing (computación en la nube). La omnipresencia de la tecnología de nube privada (pública e híbrida) ha permitido a las organizaciones proveer entornos bajo demanda. En las organizaciones tradicionales, donde utilizan servidores físicos, solicitar un nuevo servidor es un proceso complejo, largo y tedioso. Puede tomar días o incluso semanas adquirir un nuevo servidor físico, instalar y configurar el sistema operativo (en siglas, OS) y configurar todo el software necesario para desplegar la aplicación. La virtualización y la nube ayudan a resolver ese problema en gran medida, y este hecho ha traído aparejado un enorme crecimiento en la escala en la que se utilizan los entornos para desplegar las aplicaciones. A raíz de este fenómeno, se ha hecho necesaria la automatización de las tareas de implementación de software, abordadas y resueltas por DevOps.

Al mismo tiempo, **la llegada de la nube facilita el despliegue continuo y proporciona un acceso más fácil a los entornos símiles a producción durante las etapas de desarrollo y pruebas del canal de entrega.** También ha llevado a un novedoso modelo de autoservicio para los desarrolladores, quienes normalmente trabajaban de forma separada en relación con operaciones. Con las tecnologías de nube, un desarrollador puede no solo realizar una construcción automática, sino también pedir el aprovisionamiento y configuración de un entorno de producción similar a la nube para desplegar la aplicación que está construyendo… ¡todo ello sin la intervención directa del equipo de operaciones! Ambas capacidades proporcionadas por la nube facilitan la adopción DevOps.

**El paradigma de la nube introduce un cambio en la visualización del sistema y los datos que son propiedad de una empresa.** Además, el uso compartido de servicios o recursos tales como el almacenamiento, hardware y aplicaciones de Cloud Computing, ha facilitado, de una manera totalmente diferente, la coherencia de los recursos y las economías de escala a través de su modelo de negocio de pago por uso. Ya no se trata de un conjunto de dispositivos en una ubicación física que ejecutan un programa de software específico con todos los datos y los recursos presentes en un lugar físico, sino que es un sistema que se distribuye geográficamente, involucrando tanto a la aplicación como a los datos.

El desarrollo de arquitecturas y servicios distribuidos en la nube está lidiando con los mismos problemas de: escalabilidad, elasticidad respecto a la demanda, acceso a la red amplia, medición de utilización, aspectos de seguridad (tales como la autorización y autenticación) y muchos otros conceptos relacionados con los servicios multiusuario, con el fin de servir a un gran número de usuarios simultáneos en Internet. La solución puede ser una nube pública, privada o híbrida, dependiendo del tipo de industria u organización del que se trate.

Los objetivos de este tema son:

* Conocer los tipos de nube.
* Analizar los diferentes niveles de servicio.
* Comprender las ventajas de la utilización de las tecnologías de nube.

![](data:image/jpeg;base64...)

Figura 1. Consumo frente a recursos con TI tradicional. Fuente: SlidePlayer, s.f.

![](data:image/jpeg;base64...)

Figura 2. Consumo frente a recursos con utilización de nube. Fuente: SlidePlayer, s.f.

6.2. Tipos de nube

El hecho de que la información resida, de forma temporal o definitiva, en servidores de nube da como resultado que dichos servicios ofrezcan distintos formatos de privacidad que cada usuario puede elegir, según sus necesidades. De ahí que se planteen varios modelos de nubes como espacios de desarrollo de los servicios ofertados. Estos son:

* Nube pública.
* Nube privada.
* Nube híbrida.

Nubes públicas

**Los usuarios acceden a los servicios de manera compartida sin que exista un exhaustivo control sobre la ubicación de la información,** que reside en los servidores del proveedor. Es importante resaltar que el hecho de sean públicas no es un sinónimo de sean inseguras, pero la realidad es que suelen ser más vulnerables a los ataques.

Cuando hablamos de nube pública, queremos decir que toda la infraestructura de computación se encuentra en las instalaciones de una empresa de Cloud Computing que ofrece el servicio en la nube. La ubicación permanece, por lo tanto, separada del cliente y este no tiene control físico sobre la infraestructura. Por último, como las nubes públicas utilizan recursos compartidos, se destacan principalmente por su buen rendimiento.

Nubes privadas

**Nube privada significa usar una infraestructura en la nube (red) por cada cliente u organización.** Si bien no se comparte con otros, se encuentra remotamente localizada. Las empresas tienen la opción de elegir una nube privada en la propia sede, que es más cara, pero tiene la ventaja de que así se puede tener control físico sobre la infraestructura. Resulta evidente que el nivel de seguridad y control es más alto cuando se utiliza una red privada que una red pública. Sin embargo, la reducción de costes puede ser mínima si la empresa necesita invertir en una infraestructura en la nube *on premise.*

Nubes híbridas

**Combinan características de las dos anteriores,** de manera que parte del servicio se puede ofrecer de manera privada (por ejemplo, la infraestructura) y otra parte de manera compartida (por ejemplo, las herramientas de desarrollo).

![](data:image/png;base64...)

Figura 3. Ventajas del uso de la nube. Fuente: SlidePlayer, s.f.

6.3. Niveles de servicio

Cuando hablamos de servicios en la nube, es importante establecer que existen diferentes opciones, dependiendo del tipo de servicios que se ofrecen y la implicación que tiene el cliente en la gestión de esta. La clasificación más aceptada consiste en dividir los niveles de servicio en tres:

* Infraestructura como servicio (en siglas, IaaS).
* Plataforma como servicio (en siglas, PaaS).
* Software como servicio (en siglas, SaaS).

![](data:image/png;base64...)

Figura 4. Niveles de Servicio en la nube. Fuente: SlidePlayer, s.f.

Infraestructura como servicio (IaaS)

La idea básica es la de hacer **uso externo de servidores para espacio en disco,** base de datos, *roters,* *switches,* así como tiempo de cómputo para evitar tener un servidor local y toda la infraestructura necesaria para la conectividad y mantenimiento dentro de una organizaron. Con una IaaS, lo que se tiene es una solución en la que se paga solamente por el consumo de los recursos usados: espacio en disco utilizado, tiempo de CPU, espacio para base de datos, transferencia de datos, etc.

Plataforma como servicio (SaaS)

Se trata de un modelo en el que se proporciona un **servicio de plataforma con todo lo necesario para dar soporte al ciclo de diseño, desarrollo y puesta en marcha de aplicaciones y servicios web a través de esta.** El proveedor es el encargado de escalar los recursos, en caso de que la aplicación lo requiera, para que la plataforma tenga un rendimiento óptimo, de la seguridad de acceso, etc. Para desarrollar software se necesitan: bases de datos, herramientas de desarrollo y, en ocasiones, servidores y redes. Con PaaS, el cliente únicamente se enfoca en desarrollar, depurar y probar que las herramientas necesarias para el desarrollo de software son ofrecidas a través de Internet, lo que teóricamente permite aumentar la productividad de los equipos de desarrollo, gracias a que abstrae del hardware físico al cliente.

Software como servicio (SaaS)

Consiste en la **entrega de aplicaciones completas como un servicio** que permite la abstracción completa, no solo del hardware subyacente, sino incluso de la plataforma y habilita al usuario (cliente) dedicarse únicamente a su uso (consumo).

![](data:image/png;base64...)

Figura 5. Comparativa de los niveles de servicio en la nube. Fuente: adaptado de SlideShare, 2012.

6.4. Proveedores de nube pública

En la actualidad, existen múltiples proveedores de nube publica que intentan repartirse el mercado de los servicios en la nube, sin embargo, existe un claro líder tanto de mercado como por número de servicios ofrecidos, regiones donde se pueden contratar y capacidad total. Ese líder es Amazon Web Services, también conocido como AWS, a quien exploraremos más en detalle luego.

Existen otros proveedores, también con amplias capacidades, que siguen de cerca al líder, en este caso hablamos de Google con su nube Google Cloud y Microsoft con Azure.

![](data:image/png;base64...)

Figura 6. Cuadrante Mágico. Fuente: MetaCompliance, 2019.

6.5. Aplicaciones móviles y nube

Por lo general, en las empresas, las aplicaciones móviles no están aisladas, diríamos que sirven más bien como *front-end* a múltiples aplicaciones empresariales, ya en uso por la empresa. Estas aplicaciones *back-end* de empresa pueden variar desde sistemas de procesamiento de transacciones hasta portales de empleados o sistemas de adquisición de clientes. **El desarrollo móvil y la entrega son complejos y requieren de un conjunto de servicios interdependientes, a fin de que puedan ser entregados de forma coordinada, fiable y eficiente.**

Para el caso de las aplicaciones móviles empresariales, sus ciclos de entrega y el lanzamiento de nuevas funciones deberán estar coordinados con las aplicaciones y servicios de la empresa con los que estas aplicaciones móviles interactúan. Por lo tanto, la adopción de DevOps debe incluir a los equipos de aplicaciones móviles prioritariamente, que a su vez sean colaborativos con resto de los equipos de desarrollo de software empresarial.

DevOps y tiendas de aplicaciones

Un aspecto característico de las aplicaciones móviles es la necesidad de despliegue en las tiendas de aplicaciones. **La mayoría de las aplicaciones tiene que «comercializarse» través de un vendedor que gestione la tienda de aplicaciones a fin de llegar a los usuarios.** Apple presentó este formato de distribución con su App Store y bloqueó sus dispositivos contra la instalación directa de aplicaciones, tanto de los desarrolladores de aplicaciones como de los proveedores. Los fabricantes de dispositivos tales como Research In Motion y Microsoft, que permitían antaño la instalación directa de aplicaciones, ahora siguen el modelo de Apple. Esta situación da como resultado que los desarrolladores ya no puedan realizar cambios bajo demanda a una aplicación. Incluso para las correcciones de errores críticos, las nuevas versiones de la aplicación tienen que pasar por procesos de revisión y examen de la tienda de aplicaciones. La entrega continua se convierte en «enviar y esperar». El despliegue continuo de desarrollo y pruebas sigue estando disponible, siendo el entorno de prueba simulado el de los dispositivos en los que se implementará la aplicación o bancos de dispositivos físicos.

La Internet de las cosas *(Internet of Things)*

El siguiente gran paso para DevOps es su evolución en los sistemas de dispositivos embebidos. Cuando comenzó la era de la Internet, la mayoría de los datos compartidos eran generados por humanos. Hoy en día, innumerables dispositivos conectados a Internet (tales como sensores) generan muchos más datos que los seres humanos. **Esta red de dispositivos interconectados a través de Internet se conoce comúnmente con el nombre de Internet de las cosas.**

La **Internet de las cosas (IoT, por sus siglas en inglés)** es un término acuñado por Kevin Ashton, un pionero de la tecnología de origen británico, especialista en la **identificación por radiofrecuencia (en siglas, RFID),** quien concibió un sistema de sensores omnipresentes conectando el mundo físico a Internet. Si bien «las cosas», Internet y la conectividad son los tres componentes básicos de IoT, el valor está en cerrar la brecha entre el mundo físico y digital mediante el autorrefuerzo y la automejora de los sistemas.

En este escenario, DevOps es potencialmente aún más esencial, debido a la codependencia del hardware y el software embebido que se ejecuta en él. Los principios de DevOps aseguran que el software incorporado y entregado a los dispositivos es un software de alta calidad, con las especificaciones técnicas adecuadas. Operaciones, en este caso, se sustituye por hardware o ingenieros de sistemas que diseñan y construyen hardware a medida para los dispositivos. La colaboración entre los equipos de desarrollo y pruebas y los ingenieros de sistemas es crucial para asegurar que el hardware y el software se desarrollan y entregan de manera coordinada, a pesar de que tengan diferentes ciclos de entrega.

Un MVP es un Producto Mínimo Viable (*Minimum Viable Product*). La creación de un MVP es un primer paso muy recomendable para la creación de una nueva aplicación. Podrás ver en detalle estas cuestiones en el vídeo *Producto mínimo viable.*

![](data:image/png;base64...)

6.6. Referencias bibliográficas

MetaComplience. (2019). *2019 Gartner Magic Quadrant for Security Awareness Computer Based Training.* <https://go.metacompliance.com/gartnermagicquadrant>

A fondo

Introducción a la gestión de máquinas virtuales

Google Cloud Tech. (2019, abril 12). *Introduction to Virtual Machines (Cloud Next '19)* [Vídeo]. YouTube. <https://www.youtube.com/watch?v=3aNDcgoJ-_8>

Este vídeo te permitirá profundizar en la utilización de Google Compute Platform para la creación y gestión de máquinas virtuales a escala en GCP.

Test

1. ¿A qué tipo de nube nos referimos si la aplicación y los datos tienen que ser gestionados por el usuario, pero lo demás está gestionado por el proveedor de nube?

A. PaaS.

B. SaaS.

C. IaaS.

D. Híbrida.

1. ¿A qué tipo de nube nos referimos si la infraestructura es propiedad de un usuario, normalmente no está accesible desde Internet y ofrece más control?

A. Privada.

B. PaaS.

C. IaaS.

D. Híbrida.

1. ¿A qué tipo de nube nos referimos si todo el *stack*, incluida la aplicación y los datos, es gestionado por el proveedor de nube?

A. PaaS.

B. SaaS.

C. IaaS.

D. Pública.

1. La infraestructura como servicio:

A. Consiste en la entrega de aplicaciones completas como un servicio.

B. Se proporciona un servicio de plataforma con todo lo necesario para dar soporte al ciclo de planteamiento, desarrollo y puesta en marcha de aplicaciones y servicios web a través de esta.

C. Es hacer uso externo de servidores para espacio en disco, base de datos, ruteadores, *switches,* así como tiempo de cómputo, evitando de esta manera tener un servidor local y toda la infraestructura necesaria para la conectividad y mantenimiento dentro de una organizaron.

D. Ninguna de las definiciones corresponden.

1. No es un proveedor de Infraestructura de nube pública:

A. IBM.

B. AWS.

C. Netflix.

D. Google.

1. Selecciona la respuesta correcta en referencia a Microsoft Azure:

A. Azure ofrece exclusivamente servicios de almacenamiento.

B. Azure ofrece servicios de nube centrados exclusivamente en Windows.

C. Azure ofrece servicios de Cloud Computing basados tanto en Windows como en Linux, además de almacenamiento y múltiples productos en un modelo de pago por uso.

D. Todas las anteriores son falsas.

1. ¿A qué tipo de nube nos referimos si no es propiedad de los usuarios que comparten infraestructura y su uso principalmente desde Internet?

A. Pública.

B. PaaS.

C. IaaS.

D. Privada.

1. ¿Cómo afecta la nube al desarrollo e implantación de DevOps?

A. Provee entornos bajo demanda.

B. Aumenta el marketing.

C. Reduce la necesidad de DevOps.

D. No hay relación.

1. ¿Cómo es el consumo frente al aprovisionamiento de recursos cuando se utiliza la nube?

A. Aumenta de forma descontrolada.

B. Los recursos aprovisionados crecen en paralelo con la demanda.

C. No hay relación.

D. Desciende de forma progresiva.

1. ¿Qué tecnología facilita el aprovisionamiento y configuración de un entorno de producción?

A. La nube pública.

B. La nube privada.

C. La nube híbrida.

D. Cualquiera de las anteriores.
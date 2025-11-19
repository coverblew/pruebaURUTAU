Tema 7

Amazon Web Services

Cloud Computing, DevOps and DevOps Culture

Índice

[Esquema 3](#_Toc76652372)

[Ideas clave 4](#_Toc76652373)

[7.1. Introducción y objetivos 4](#_Toc76652374)

[7.2. ¿Qué es AWS? 4](#_Toc76652375)

[7.3. Control de costes en AWS 16](#_Toc76652376)

[7.4. Despliegues en AWS 20](#_Toc76652377)

[7.5. Automatización 26](#_Toc76652378)

[7.6. Seguridad 30](#_Toc76652379)

[7.7. Referencias bibliográficas 31](#_Toc76652380)

[A fondo 33](#_Toc76652381)

[Test 35](#_Toc76652382)

Esquema

![](data:image/jpeg;base64...)

Ideas clave

7.1. Introducción y objetivos

En este tema haremos una aproximación a los conceptos fundamentales de AWS y las capacidades esenciales que proporciona.

Los objetivos que se pretenden conseguir son:

* Conocer qué es AWS.
* Adquirir el conocimiento a alto nivel sobre qué podemos realizar con AWS.
* Descubrir cómo realizar un buen control de costes y de la capa gratuita de AWS.
* Establecer un plan para automatizar el ciclo de vida en AWS.
* Aprender a desplegar en AWS.
* Conocer cuáles son los controles de seguridad en AWS.

7.2. ¿Qué es AWS?

Amazon Web Services (en adelante, AWS) es una plataforma de servicios en la nube que provee un gran número de servicios de infraestructuras, tales como:

* Almacenamiento.
* Comunicaciones.
* Bases de datos (BBDD).
* Macrodatos (Big Data).
* Aprendizaje automático (*machine learning*).
* Servicios de movilidad.
* Soluciones empresariales pre-paquetizadas y certificadas.
* Securización.
* Gestión de identidades.

Dichas infraestructuras proporcionan a las empresas un crecimiento y control de gastos a medida y, sobre todo, aportan escalabilidad.

En la actualidad, AWS dispone de tres modelos de servicios compatibles entre ellos que proporcionan diferentes soluciones, según las necesidades de cada proyecto y empresa. Veamos, a continuación, cuáles son:

Infraestructura como servicio (en siglas, IaaS)

Este modelo está relacionado con la infraestructura de tecnología de la información (en siglas, TI) y proporciona una gran flexibilidad al cliente, ya que le permite decidir cuáles son los recursos que realmente necesita (procesador, memoria RAM, disco, seguridad, copia de seguridad, etc.) y pagar por ellos.

AWS ofrece las siguientes prestaciones a sus clientes:

* **Creación, mantenimiento y actualización de las infraestructuras** de los centros de datos de forma regular.
* **Securización** frente actores externos.
* **Creación de un punto de acceso** para los clientes puedan acceder a sus recursos asignados.
* **Provisión de herramientas de gestión** para la administración de infraestructura.
* **Provisión de un mapa de su arquitectura.**

Los clientes, por su parte, tienen las siguientes tareas a cargo:

* Decidir la arquitectura adecuada a sus necesidades.
* Instalar, mantener y actualizar el sistema operativo (en siglas, SO) y programas específicos.
* Administrar la configuración de comunicaciones y *firewalls.*
* Configurar las autorizaciones y métodos de autenticación.
* Cifrar de los datos y gestión de *backups.*

Dentro de los proveedores de servicios de infraestructura, actualmente AWS se encuentra en la primera posición en el cuadrante de Gartner, como se puede ver en la siguiente imagen:

![](data:image/png;base64...)

Figura 1. Cuadrante de Gartner. Fuente: Gartner. (2019, julio). Fuente: Amazon Web Services, s.f.

Plataforma como servicio (en siglas, PaaS)

Cuando hablamos de plataforma como servicio (en adelante, PaaS), hacemos referencia a **un servicio que se encuentra en la nube del proveedor, que proporciona al cliente un entorno de desarrollo junto con las herramientas necesarias para construir nuevas aplicaciones.** Cuando hablamos de PaaS nos referimos al nexo entre la infraestructura IaaS y el software como servicio (en siglas, SaaS). PaaS proporciona al cliente un conjunto de herramientas y entornos con los cuales diseñar, probar, automatizar y desplegar un producto concreto sin necesidad de preocuparse de los recursos de este.

Es importante resaltar que el modelo PaaS se encuentra muy ligado al modelo IaaS y, gracias a ello, no hay que preocuparse de la adquisición y gestión de la infraestructura, sino solo de la plataforma de desarrollo. Existen diferentes ámbitos en los cuales es posible utilizar PaaS, además de para el desarrollo de aplicaciones, como son:

* Creación de *Application Programming Interfaces* (en siglas, API).
* Análisis de un gran volumen de datos.
* Implantación de sistemas de gestión empresarial como pueden ser SAP, Oracle.
* Plataforma de comunicación.
* Base de datos.
* Dentro de los proyectos de innovación, como ejemplo para la implementación de soluciones de Internet de las cosas.

![](data:image/jpeg;base64...)

Figura 2. Ejemplo de PaaS. Fuente: de Valence, 2018.

Software como servicio (SaaS)

Proporciona un producto completo al cliente, el cual ejecuta y administra el proveedor. En este caso, el cliente solo debe preocuparse por sus necesidades de software. **Es una forma de disponer de diferentes tipos de software de forma centralizada y el usuario final puede acceder a este de forma online.** Como programas o softwares más destacados dentro de los servicios SaaS, podemos destacar SAP, CRM, gestores de proyectos o gestores de archivos.

![](data:image/png;base64...)

Figura 3. Ejemplo de SaaS. Fuente: Golding, 2017.

A su vez, existen tres modelos de implementación de IaaS, PaaS y SaaS:

![Diagrama  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 4. Modelos de implementación informática en la nube. Fuente: adaptado de Amazon Web Services, s. f.

![Diagrama, Texto  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 5. Modelos de implementación informática en la nube. Fuente: adaptado de Amazon Web Services, s. f.

![Diagrama  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 6. Modelos de implementación de informática en la nube. Fuente: adaptado de Amazon Web Services, s. f.

En la actualidad, AWS proporciona más de 175 servicios combinables entre ellos, que se agrupan de la siguiente manera:

![](data:image/png;base64...)

Figura 7. Grupo de Productos AWS. Fuente: adaptado de Amazon Web Services, s. f.

A continuación, pasamos a detallar algunos de los grupos dentro del abanico de servicios de AWS:

![](data:image/jpeg;base64...)Tabla 1. Integración de aplicaciones. Fuente: elaboración propia.

![](data:image/jpeg;base64...)

Tabla 2. Contenedores. Fuente: elaboración propia.

![](data:image/jpeg;base64...)Tabla 3. Informática. Fuente: elaboración propia.

![](data:image/jpeg;base64...)Tabla 4. Migraciones y Transferencias. Fuente: elaboración propia.

![](data:image/jpeg;base64...)Tabla 5. Almacenamiento. Fuente: elaboración propia.

Dichos servicios se encuentran disponibles a partir de centros de datos distribuidos alrededor del globo, divididos en 76 zonas disponibles de utilización y repartidos por veinticuatro zonas geográficas, con una zonal local para proporcionar latencias ínfimas, por lo que proporciona una **disponibilidad global,** como se puede ver a continuación:

![](data:image/png;base64...)

Figura 8. Infraestructura global AWS. Fuente: Amazon Web Services, s. f.

7.3. Control de costes en AWS

Es necesario que las empresas puedan realizar un control exhaustivo de los costes derivados del consumo de servicios, por lo que AWS proporciona **un sistema de pago por uso sin subscripciones.** Esto significa que en el momento en que dejemos de necesitar algún servicio, ya no deberemos pagar por él.

Dentro del catálogo de productos existen los siguientes servicios para el control de costes:

![](data:image/jpeg;base64...)

Tabla 6. Administración de Costes AWS. Fuente: elaboración propia.

Adicionalmente a estos servicios, antes de empezar a utilizar AWS es necesario tener un presupuesto del servicio o conjunto de servicios a utilizar. A este fin, **AWS proporciona dos calculadoras** para la realización de presupuestos y análisis del coste de la utilización de servicios individuales, paquetes o, incluso, de soluciones completas.

Calculadora de precios de AWS

Es posible realizar una estimación de costes de los productos y servicios que ofrece AWS adaptados a las necesidades de la empresa, o incluso de forma personal. La utilización de esta es totalmente gratuita y para usarla deberemos seguir los siguientes pasos:

1. Acceder a [AWS Pricing Calculator](https://calculator.aws/#/) y seleccionar el botón **crear estimación.**
2. Seleccionar el o los **servicios** en los que estemos interesados, la **configuración** que necesitamos e indicar en qué **región** lo queremos activado.

Una vez realizado el presupuesto, se podrá guardar o compartir con quien sea necesario y podremos tener vinculados tantos presupuestos como necesitemos o queramos crear, sin que estos sean vinculantes.

Calculadora de coste total de propiedad (TCO)

La calculadora de coste total de propiedad permite realizar una evaluación, o análisis de ahorro, en la utilización de productos y servicios de AWS. Realiza una comparación con entornos locales o híbridos de forma completa y realista. Para utilizar esta calculadora, se deben seguir los siguientes pasos:

![](data:image/png;base64...)

Figura 9. Calculadora de coste total de propiedad (TCO) de AWS. Fuente: elaboración propia.

Capa gratuita AWS

Dentro del ecosistema AWS, existe una capa gratuita que proporciona más de sesenta productos, que pueden probarse o utilizarse sin ningún coste. Existen tres tipos de ofertas dentro de la capa gratuita, dependiendo del tipo de producto que se quiera utilizar.

* **Gratis para siempre:** oferta disponible para clientes existentes o nuevos clientes. Pasados los doce meses, estas ofertas no vencerán. Gracias a esto, será posible empezar a familiarizarse con AWS.
* **Doce meses de uso gratuito:** consiste en una oferta disponible durante doce meses a partir de la fecha de subscripción y solo para nuevos usuarios. Dichas ofertas tienen un límite de cómputo y, en el caso de que se supere dicho computo, será necesario pagar las tarifas estipuladas para dicho servicio.
* **Pruebas:** es una oferta exclusiva para pruebas que comienza desde el primer uso de estas y, una vez que haya expirado el plazo de prueba, al igual que en la modalidad anterior, se empezará a tarificar según el uso del servicio.

Para poder ver todos los servicios disponibles en las modalidades anteriormente explicadas, puedes acceder a la capa gratuita de AWS a través de la siguiente dirección web: [https://aws.amazon.com/es/free/](https://aws.amazon.com/es/free/%29%5B6)

![](data:image/png;base64...)

Figura 10. Ejemplo de servicios capa gratuita. Fuente: Amazon Web Services, s.f.

7.4. Despliegues en AWS

Desde un punto de vista simplista, realizar un despliegue básico en Amazon implica la creación de una máquina virtual. Para la creación de dicha máquina virtual, son necesarios algunos de los conceptos que veremos a continuación.

AWS AMI

**Amazon Machine Image (en adelante, AMI)** es un ejemplo de esta «infraestructura como código». Este componente fundamental de la computación de AWS es una especie de plantilla digital que puede lanzar (aprovisionar) instancias de Amazon EC2, el entorno fundamental de AWS de cómputo en la nube. Desde un punto de vista práctico, podemos decir que en la mayoría de los casos el AMI es el sistema operativo.

Se puede elegir entre tres tipos de AMI:

* Publicada por AWS.
* De terceros.
* Personalizada.

**AWS publica las AMI** que contienen configuraciones comunes de software basado en sistemas operativos populares como Linux y Microsoft Windows. Las **AMI también pueden obtenerse a partir de terceros,** algunos de los cuales están disponibles en el

AWS Marketplace. Una organización también puede crear y publicar sus propias **AMI personalizadas.**

Las AMI específicas de una organización incluyen, generalmente: software corporativo (sistemas operativos reforzados), software antivirus y suites de software de oficina. Tienen la posibilidad de incluir software de aplicación que viene empaquetado junto con la AMI o puede contener *scripts* y software que permitan a la instancia de instalar el software de aplicación al momento del lanzamiento, llamada *booting.*

¿Cuáles son los pros y contras de cargar, de antemano, software de nivel de aplicación en una AMI? Como ventaja, hemos de indicar que pueden **ser lanzados con gran rapidez,** ya que no es necesario instalar ningún software adicional en el arranque. Como desventaja, hay que indicar que puede ser necesario **crear una nueva AMI cada vez que haya cambios** de software a nivel de aplicación.

AWS CodeDeploy

El despliegue continuo es otro concepto fundamental en una estrategia de DevOps. Su objetivo principal es permitir el despliegue automático del código de aplicación «listo para producción». Algunas veces, al despliegue continuo se lo llama entrega continua. La única diferencia es que el despliegue continuo, por lo general, se refiere a los despliegues de producción.

Mediante el uso de las prácticas y herramientas de entrega continua, el software se puede implementar rápidamente, de forma reiterativa y fiable. Si un despliegue falla, se puede hacer *roll-back* automáticamente a la versión anterior. Un buen ejemplo de este principio en AWS es el servicio de implementación de código AWS CodeDeploy. Sus características principales proporcionan la habilidad de **desplegar aplicaciones a través de Amazon EC2 con un tiempo de inactividad mínimo, centralizando el control e integrándose con la versión existente de software o proceso de entrega continua.**

![](data:image/png;base64...)

Figura 11. AWS CodeDeploy. Fuente: SupportPRO, s.f.

Veamos cómo funciona:

1. El contenido de la aplicación se empaqueta y se despliega en Amazon S3 junto con un archivo de Aplicación Específica (AppSpec) que define una serie de pasos de despliegue que AWS CodeDeploy necesita ejecutar. El paquete se llama «CodeDeploy revision».
2. Se crea una aplicación en AWS CodeDeploy y se definen las instancias en las que la aplicación debe ser desplegada (**DeploymentGroup**). La aplicación también define el *bucket* de Amazon S3, donde reside el paquete de despliegue.
3. Un agente de AWS CodeDeploy se implementa en cada instancia Amazon EC2 participante. Los agentes de AWS CodeDeploy determinan qué y cuándo aplicar una revisión del depósito de Amazon S3 especificado.
4. El agente AWS CodeDeploy obtiene el código de la aplicación empaquetada y lo despliega en la instancia.

AWS CodePipeline

AWS CodePipeline es un **servicio de automatización de entrega continua** que ayuda a suavizar los despliegues. Se puede diseñar el desarrollo del flujo de trabajo para: la comprobación del código, la construcción del código, el despliegue de la aplicación en los distintos escenarios, las pruebas y el pase a producción. Se pueden integrar herramientas de terceros en cualquier etapa del proceso, o bien, se puede utilizar AWS CodePipeline como una solución de extremo a extremo. Con esta herramienta, se pueden realizar rápidamente actualizaciones y *features* (características) de alta calidad y tiene varios beneficios que se alinean con el principio de DevOps de despliegue continuo:

* Entrega rápida.
* Mejora de la calidad.
* Flujo de trabajo configurable.
* Facilidad de integración.

![](data:image/png;base64...)

Figura 12. Implementación de DevSecOps con AWS CodePipeline. Fuente: Adabala, 2017.

AWS CodeCommit

AWS CodeCommit es un **servicio de gestión de control de fuente** que aloja los repositorios privados Git y que se caracteriza por ser seguro y escalable. Elimina la necesidad de operar con el sistema de control de código fuente propio o tener que preocuparse acerca de la expansión de la infraestructura. Además, se puede utilizar para almacenar cualquier cosa, desde código hasta números binarios, y es compatible con la funcionalidad estándar de Git, lo que permite trabajar sin problemas con las herramientas existentes, basadas en este último. Para trabajar en equipo, también se pueden utilizar las herramientas de código online de CodeCommit para navegar, editar y colaborar en proyectos. Entre sus beneficios, vale la pena destacar:

* Gestión completa.
* Almacenamiento flexible.
* Alta disponibilidad.
* Ciclos de vida de desarrollo más rápidos.
* Funcionamiento adecuado con las herramientas existentes.
* Seguridad.

AWS Elastic Beanstalk y AWS OpsWorks

Tanto AWS OpsWorks como AWS Elastic Beanstalk soportan la implementación continua de cambios en el código de aplicación y modificaciones en la infraestructura. En AWS Elastic Beanstalk, los despliegues de cambio de código se almacenan como «versiones de las aplicaciones» y los cambios en la infraestructura se despliegan como «configuraciones guardadas». Un ejemplo de una versión de aplicación sería una nueva aplicación Java que se carga como un archivo ZIP o WAR. Un ejemplo de una configuración guardada sería una configuración de AWS Elastic Beanstalk, que utiliza Elastic Load Balancing y Auto Scaling en lugar de una sola instancia.

**AWS Elastic Beanstalk** apoya la práctica DevOps llamada *rolling deployments*. Cuando se activa, la configuración de los despliegues trabaja mano a mano con Auto Scaling para asegurar que siempre haya un número definido de instancias disponibles cuando se realizan cambios de configuración. Esto aporta control cuando las instancias de Amazon EC2 se actualizan. Por ejemplo, si se está cambiando el tipo de instancia EC2, el usuario puede determinar si AWS Elastic Beanstalk debe actualizar todas las instancias al mismo tiempo o si se quieren dejar algunas instancias corriendo.

Despliegue Blue-Green

El despliegue Blue-Green es una práctica de despliegue de DevOps que utiliza los servicios de nombres de dominio (en siglas, DNS) para realizar el despliegue de aplicaciones. **La estrategia consiste en comenzar con un entorno existente (azul) mientras se prueba uno nuevo (verde).** Cuando el nuevo entorno ha pasado todas las pruebas necesarias y está listo para utilizarse, simplemente hay que redirigir el tráfico desde el antiguo entorno a la nueva vía DNS.

AWS ofrece todas las herramientas que se necesitan para implementar una estrategia de desarrollo Blue-Green. Se puede configurar un entorno ideal de nueva infraestructura mediante el uso de un servicio como AWS CloudFormation o AWS Elastic Beanstalk. Con las plantillas de CloudFormation AWS, se puede crear fácilmente un nuevo entorno, idéntico al entorno de producción existente.

Si se utiliza el servicio AWS DNS Amazon Route 53, se puede dirigir el tráfico a través de conjuntos de registros de recursos ponderados. Mediante el uso de estos conjuntos, se pueden definir varios servicios o equilibradores de carga (*load balancers*) con una resolución de DNS. La resolución del servicio DNS (conversión de un nombre de dominio a una dirección IP) es ponderada, lo que significa que se puede definir la cantidad de tráfico que se dirige al entorno de producción. De esta forma, se pueden hacer pruebas del entorno y, cuando se tiene la certeza de que el despliegue es bueno, aumentar la ponderación. Cuando el entorno de producción antiguo está recibiendo 0 % de tráfico, se puede guardar como copia de seguridad, o bien desmantelarse. A medida que la cantidad de tráfico en los nuevos entornos aumenta, se puede utilizar Auto Scaling para ampliar las instancias adicionales de Amazon EC2. Esta capacidad de crear y disponer de entornos idénticos fácilmente en la nube de AWS posibilita la aplicación de las prácticas de DevOps como el despliegue Blue-Green. También, se puede utilizar el despliegue Blue-Green para los servicios de *back-end* como el despliegue de bases de datos y conmutación por error.

![](data:image/png;base64...)

Figura 13. Implementación azul-verde en AWS. Fuente: Abdala, 2017.

Accede a la Figura 13, «Implementación azul-verde en AWS*»,* a través del aula virtual.

7.5. Automatización

Otra filosofía y práctica fundamental de DevOps es la automatización. **La automatización se centra en la instalación, configuración, implementación y soporte de la infraestructura y las aplicaciones que se ejecutan en ella.** Mediante el uso de la automatización, se pueden configurar entornos con mayor rapidez de una manera estandarizada y repetible.

La eliminación de los procesos manuales es la clave para una estrategia DevOps exitosa. Históricamente**, la configuración del servidor y la implementación de aplicaciones han sido procesos manuales, pero es sabido que la automatización es fundamental para obtener el máximo beneficio de la nube.** AWS se apoya, en gran medida, en la automatización para proporcionar las características básicas de elasticidad y escalabilidad. Los procesos manuales son propensos a errores, poco fiables e insuficientes para soportar un negocio ágil. Si bien las organizaciones pueden contar con recursos altamente calificados para proporcionar la configuración manual, en la mayoría de los casos se podría aprovechar mejor el tiempo, invirtiéndolo en otras actividades de valor que resulten más críticas dentro de la empresa y que estén dirigidas a los objetivos del negocio.

Los entornos operativos modernos, comúnmente, se basan en la automatización completa para eliminar la intervención manual, esto incluye: todo el software, la configuración del equipo, parches del sistema operativo, resolución de problemas o corrección de errores o *bugs.* Muchos niveles de prácticas de automatización se pueden utilizar juntos para proporcionar un proceso automatizado de alto nivel de extremo a extremo.

Como puedes imaginar, la automatización tiene muchos beneficios. Entre ellos encontramos:

* Posibilidad de generar cambios con rapidez.
* Mejora de la productividad.
* Configuraciones repetibles.
* Entornos reproducibles.
* Elasticidad.
* Escalabilidad.
* Pruebas automatizadas.

AWS Elastic Beanstalk

AWS Elastic Beanstalk es un ejemplo de automatización en AWS. Este **es un servicio que permite a los desarrolladores desplegar aplicaciones en pilas o stacks de tecnología de uso común.** Su (bien lograda) interfaz ayuda a los desarrolladores a desplegar aplicaciones con múltiples capas de forma rápida y sencilla.

AWS Elastic Beanstalk es compatible con la automatización y numerosas buenas prácticas de DevOps, incluyendo el despliegue automatizado de aplicaciones, la monitorización, la configuración de la infraestructura y la gestión de versiones. Los cambios en las aplicaciones y la infraestructura se pueden gestionar fácilmente, yendo hacia adelante o hacia atrás, según sea necesario.

Elastic Beanstalk es también un buen ejemplo de la automatización en la creación de entornos: solo hay que especificar los detalles del entorno y este se encarga de todo el trabajo de configuración y aprovisionamiento. Por ejemplo, aquí hay solo algunas de las opciones que se pueden especificar en el asistente de creación de la aplicación:

* Definir si quieres un servidor web Tier (que contiene un servidor web y un servidor aplicación) o un nivel Tier (que utiliza Amazon Simple Queue Service).
* Definir qué plataforma utilizar para la aplicación. Las opciones incluyen IIS, Node.js, PHP, Python, Ruby, Tomcat, Java, Go, .Net, Docker, por ejemplo.
* Definir si vas a lanzar una sola instancia o crearás un entorno auto escalable de carga balanceada.
* Definir qué URL asignarás automáticamente al entorno.
* Definir si el entorno incluirá una instancia Amazon Relational Database.
* Definir si crearás el entorno dentro de Amazon Virtual Private Cloud.
* Definir qué URL utilizarás para los controles de salud (automáticas) de la aplicación.
* Definir qué etiquetas (si las hay) utilizarás para identificar el entorno.

**AWS Elastic Beanstalk** también utiliza la automatización para desplegar aplicaciones. Dependiendo de la plataforma, todo lo que se necesita hacer para desplegar aplicaciones es cargar paquetes en forma de archivos WAR o ZIP directamente desde un ordenador o desde Amazon S3. A medida que se está creando el entorno, AWS Elastic Beanstalk registra automáticamente los eventos en la consola de gestión que proporciona retroalimentación sobre el progreso y el estado del lanzamiento. Una vez completado, se puede acceder a la aplicación mediante la URL definida.

AWS OpsWorks

AWS OpsWorks lleva los principios DevOps incluso aún más lejos que AWS Elastic Beanstalk, ya que proporciona **más niveles de automatización con funciones adicionales como la integración con el software de gestión de la configuración (Chef) y la administración del ciclo de vida de aplicaciones.** Permite, entonces, definir cuándo configurar los recursos, desplegarlos, replegarlos o terminarlos.

Para aumentar la flexibilidad, AWS OpsWorks permite definir su aplicación en pilas o *stacks* configurables, pero también se pueden seleccionar pilas de aplicaciones predefinidas. Estas pilas contienen todo el aprovisionamiento de recursos de AWS que requiere la aplicación, incluyendo servidores de aplicación, servidores web, bases de datos y los equilibradores de carga.

Los *stacks* de aplicaciones se organizan en capas o niveles arquitectónicos con el propósito de que las pilas se puedan mantener de forma independiente. Las capas o niveles podrían ser de web, de aplicación y de bases de datos. A su vez, AWS OpsWorks también simplifica la creación de grupos de Auto Scaling y equilibradores de carga, lo que ilustra, además, el principio DevOps de automatización. Al igual que AWS Elastic Beanstalk, es compatible con la generación de versiones de aplicaciones *(versioning),* el despliegue continuo y la gestión de la configuración de la infraestructura.

AWS OpsWorks también es compatible con las prácticas DevOps de supervisión y registro (cubierto en la siguiente sección). El soporte de la supervisión está proporcionado por Amazon CloudWatch. Todos los eventos del ciclo de vida se registran y, en un registro separado, los documentos de Chef, todas las «recetas» de Chef que se ejecutan, sin excepción.

![](data:image/png;base64...)

Figura 14. AWS OpsWorks. Fuente: Trager, 2017.

7.6. Seguridad

En un entorno DevOps, el foco en la seguridad es un aspecto de suma importancia. La infraestructura y los activos de la empresa deben ser protegidos y, cuando surjan problemas, estos deben ser resueltos de forma rápida y eficaz.

Gestión de Identidad y Acceso (IAM)

El servicio AWS IAM (gestión de identidad y acceso) es un componente de la infraestructura de seguridad de AWS. Con IAM, se puede administrar de forma centralizada a los usuarios y las credenciales de seguridad, tales como: contraseñas, claves de acceso y políticas de permisos que controlan a qué servicios de AWS y a qué recursos pueden acceder los usuarios. También se puede utilizar IAM para crear roles que se utilicen comúnmente dentro de una estrategia DevOps. Con un rol IAM puedes definir un conjunto de permisos para acceder a los recursos de un usuario o servicio según las necesidades.

Pero en lugar de endosar permisos a un usuario o a un grupo específico, se pueden asociar a una determinada función o rol. Los recursos pueden estar asociados con los roles y los servicios pueden ser, entonces, definidos mediante programación para un determinado papel o rol dentro de la organización. Los requisitos de seguridad y los

controles deben ser agregados durante el proceso de automatización y hay que tener especial cuidado cuando se trabaja con contraseñas y claves.

La colaboración es un elemento clave en DevOps, pero no solo entre desarrolladores y trabajadores del área de operaciones, sino que también hablamos de colaboración entre los propios desarrolladores. Hace ya un tiempo que estos cuentan con herramientas como los repositorios de código y el control de versiones para materializar este verdadero trabajo coordinado que llevan a cabo en las organizaciones que apuestan por la agilidad y la filosofía DevOps. En el vídeo *Repositorios y control de visiones* se tratarán varios de estos tópicos.

![](data:image/png;base64...)

7.7. Referencias bibliográficas

Abadala, R. (2017, marzo 23). *Implementing DevSecOps Using AWS CodePipeline.* Amazon Web Services. <https://aws.amazon.com/es/blogs/devops/implementing-devsecops-using-aws-codepipeline/>

Amazon Web Services. (s.f.). *Productos en la nube.* <https://aws.amazon.com/es/products/?pg=WIAWS-N&tile=learn_more>

Amazon Web Services. (s.f.). *Tipos de informática en la nube.* <https://aws.amazon.com/es/types-of-cloud-computing/>

Amazon Web Services. (s.f.). *Infraestructura global.* <https://aws.amazon.com/es/about-aws/global-infrastructure/>

Amazon Web Services. (s.f.). *2020 Magic Quadrant for Cloud Infraestructura & Platform Services.* <https://pages.awscloud.com/Gartner-Magic-Quadrant-for-Infrastructure-as-a-Service-Worldwide/?pg=WIAWS-mp>

Golding, T. (2018, marzo 21). Enabling New Saas Strategies with AWS PrivateLink. *AWS Partner Network (APN) Blog.* <https://aws.amazon.com/es/blogs/apn/enabling-new-saas-strategies-with-aws-privatelink/>

Martins, F. (2020, enero 17). Calculadora Cloud: Quanto a minha TI poderá custar na nuvem? *Inova Globalweb.* <https://inova.globalweb.com.br/post/quanto-a-minha-ti-podera-custar-na-nuvem>

Trager, D. (2017, junio 23). AWS OpsWorks: fallacies and pitfalls. *Flat Stack.* <https://medium.flatstack.com/aws-opsworks-fallacies-and-pitfalls-f97944bf3e81>

SupportPRO. (s.f.). *AWS CodeDeploy.* <https://www.supportpro.com/blog/aws-codedeploy/>

Valence, P. (2018, septiembre 10). Mainframe Modernization Platform-as-a-Service (ModPaaS) from Modern Systems. *AWS Partner Network (APN) Blog.* <https://aws.amazon.com/es/blogs/apn/mainframe-modernization-platform-as-a-service-with-modern-systems-modpaas/>

A fondo

Documentación oficial AWS

Amazon Web Services. (s.f.) *AWS Documentation.* <https://docs.aws.amazon.com/index.html?nc2=h_ql_doc_do>

AWS proporciona la documentación específica de todos sus productos y servicios junto con documentación de los SDK de los diferentes lenguajes de programación, recursos generales, diferentes tutoriales y proyectos.

Comparativa y crecimiento de AWS frente a sus competidores

McAfee. (2019, octubre 25). *Cloud Market in 2019 and Predictions for 2022.* <https://www.mcafee.com/blogs/enterprise/cloud-security/microsoft-azure-closes-iaas-adoption-gap-with-amazon-aws/>

En este enlace podemos ver la cuota de mercado de AWS frente a sus competidores y la predicción de crecimiento en los próximos años, donde vemos que AWS tiene una expectativa de crecimiento grande y gran cuota de mercado.

SAP on AWS

Amazon Web Services. (s.f.). *SAP on AWS.* <https://aws.amazon.com/es/sap/>

AWS proporciona la posibilidad de implementar todas las *suites* disponibles de SAP bajo su ecosistema. Dos grandes se unen para dar un valor añadido a las empresas que están pensando en migrar sus sistemas a la nube y todo ello certificado por el mayor fabricante de software empresarial a nivel mundial.

Desplegando y desarrollando aplicaciones modernas en la nube

Amazon Web Services LATAM. (2019, noviembre 21). *AWS Cloud Experience CA: Desplegando y Desarrollando Aplicaciones Modernas en la Nube.* SlideShare. <https://www.slideshare.net/AmazonWebServicesLATAM/aws-cloud-experience-ca-desplegando-y-desarrollando-aplicaciones-modernas-en-la-nube>

Sesión magistral del AWS Cloud Experience del 2019.

Test

1. ¿Cuáles son los modelos de servicios e implementación que proporciona AWS?

A. IaaS, VaaS, SaaS (nube y local).

B. Iaav, PaaS, SaaS (nube, híbrida y local).

C. IaaS, PaaS, MaaS (local e híbrida).

D. IaaS, PaaS, SaaS (local, híbrida y nube).

1. ¿Cuántos grupos de servicios dispone AWS en la actualidad?

A. 175.

B. 25.

C. 300.

D. 17.

1. Relaciona grupo y servicio de AWS

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| Amazon QM | 1 |  | A | Informática |
| AWS Lamdba | 2 |  | B | Integración Apps. |
| Familia de productos AWS Snow | 3 |  | C | Migración y Transferencia |
| Amazon S3 | 4 |  | D | Almacenamiento |

1. ¿En caso de superar el cómputo de la capa gratuita, es necesario pagar?

A. No, porque son gratuitos todos los servicios a utilizar.

B. Sí, porque es necesario pagar para crearte una cuenta de AWS.

C. Solo hay que pagar en el caso de que superes el cómputo en algunos de los servicios.

D. Todas son falsas.

1. Señala el beneficio o los beneficios de la utilización de AWS PipeLine:

A. Automatización de entregas.

B. Fácil integración.

C. Empobrece la calidad del producto.

D. Solo compatible con productos de terceros.

1. ¿En qué consiste el despliegue Blue-Green?

A. Despliegue de DevOps que utiliza los servicios de nombres de dominio (en siglas, DNS) para realizar el despliegue de aplicaciones.

B. Despliegue de soluciones empresariales para desplegar en AWS.

C. Es un código de colores que identifica el estado en el que se encuentra nuestra aplicación.

D. Despliegue de un servicio directamente en producción.

1. ¿AWS OpsWorks permite la creación y administración de servidores Chef?

A. Sí.

B. No.

C. No porque es compatible.

D. Sí, pero en la región de Estados Unidos únicamente.

1. ¿Qué tipos de aplicaciones son compatibles con AWS Elastic BeanStalk?

A..Net, PHP, Python, Ruby, Docker, Java, ABAP for Hana.

B. ABAP, Hana, Python, .Net, PHP.

C. Java.

D..Net, PHP, Python, Ruby, Docker, Java, Node.js, Go.

1. ¿El pago de AWS es mediante el método de subscripción, pagando un coste fijo todos los meses?

A. Sí, en AWS pagas una subscripción mensual.

B. No, pagas una subscripción mensual fija más el computo utilizado.

C. No, la modalidad de pago es un pago por uso.

D. AWS es totalmente gratuita y el coste es el del proveedor de Internet.

1. ¿Por qué es importante AWS IAM?

A. Porque nos muestra el cómputo que llevamos utilizado en el último mes.

B. Porque sin AWS no tenemos acceso a la red.

C. Porque con AWS IAM gestionamos usuarios, grupos, autorizaciones y accesos.

D. Ninguna de las anteriores.
Tema 5

Casos de uso en virtualización

Cloud Computing, DevOps and DevOps Culture

Índice

[Esquema 3](#_Toc76382268)

[Ideas clave 4](#_Toc76382269)

[5.1. Introducción y objetivos 4](#_Toc76382270)

[5.2. Casos de uso de virtualización 4](#_Toc76382271)

[5.3. Resultados de alto impacto 16](#_Toc76382272)

[5.4. Buenas prácticas en administración de TI 19](#_Toc76382273)

[5.5. Cómo encauzar tu proyecto de virtualización 22](#_Toc76382274)

[A fondo 29](#_Toc76382275)

[Test 30](#_Toc76382276)

Esquema

![](data:image/jpeg;base64...)

Ideas clave

5.1. Introducción y objetivos

Resulta importante mostrar ejemplos de aplicación de la virtualización para complementar los conocimientos técnicos y teóricos de su funcionamiento y ver las formas de aplicarla de manera exitosa.

Siguiendo con esta idea, los objetivos que pretendemos alcanzar con este tema son:

* Entender las áreas más comunes donde la virtualización es beneficiosa.
* Conocer ejemplos exitosos de virtualización.
* Analizar la importancia de la gobernanza de tecnología de información (en adelante, TI) en conjunción con la virtualización.

5.2. Casos de uso de virtualización

La virtualización es útil en varios escenarios, que pueden ser simples o extremadamente complejos. Lo que resulta importante es comprender cómo se desea utilizar la virtualización, ya que esto determinará qué solución es la más adecuada para cada circunstancia u organización. Para ello, vamos a repasar algunos de sus principales usos.

Consolidación de servidores

El primer caso de uso de la virtualización suele ser la consolidación de servidores. Esta se refiere a **tomar instancias separadas del servidor y migrarlas a máquinas virtuales que se ejecutan en un único servidor.** Pero además de ello, la consolidación de servidores también puede ser entendida como el acto de coger numerosos servidores separados y migrarlos a menos servidores, con múltiples máquinas virtuales ejecutadas en cada servidor.

Las empresas que implementan la consolidación de servidores experimentan una profunda transformación: pasan de ejecutar 150 servidores físicos a ejecutar 150 máquinas virtuales en solo quince servidores, lo que redunda en una enorme reducción de costes e inversión de hardware, energía y refrigeración, empleados, tiempo y, en muchos casos, costes de licencias de software. Por tanto, **podemos afirmar que la consolidación de servidores puede llegar a ofrecer un 60 % u 80 % de mejora de utilización de recursos.**

Entornos de desarrollo y pruebas

Vamos a imaginar que un ingeniero construye un software capaz de implementar una determinada funcionalidad. Antes de pasar a la siguiente fase, el software se ha de ejecutar y probar en una variedad de sistemas (por ejemplo, Windows y Linux), así como varias versiones de esos productos. Entonces, un departamento de calidad, o *quality assurance* (en siglas, QA), realiza todas las pruebas necesarias para garantizar que cumple con los requisitos aplicables de funcionalidad, escalabilidad, robustez, y detectar errores.

Gracias a la implementación de la virtualización, un desarrollador o *tester* puede replicar un entorno distribuido con varios sistemas en una sola pieza de hardware. Esto permite librarse de la necesidad de tener un montón de servidores aparcados, esperando que los *testers* o desarrolladores necesiten utilizarlo.

A su vez, la virtualización también es útil en entornos de prueba y desarrollo por otro motivo. Uno de los efectos secundarios del software de prueba es que las primeras versiones a menudo se bloquean y dañan no solo a la aplicación, sino también al funcionamiento del sistema subyacente, así como a otras aplicaciones en la pila de software y, para poder iniciar la recuperación, es necesario reinstalar todo el software. Resulta evidente que esto representa un verdadero impedimento para la productividad. Pues bien, a través de la virtualización esto puede evitarse ya que solo la aplicación de prueba, la máquina virtual y el software relacionado con esta se ven afectados.

Computación en la nube privada

En pocas palabras, la computación en la nube es un medio para proporcionar servicios de tecnología bajo demanda a través de Internet. **Una nube privada es un entorno donde estos servicios operan para una única organización.** Numerosas organizaciones de TI están explorando cómo construir sus propias nubes privadas para aumentar la agilidad y reducir sus costes. La virtualización es un componente clave de las nubes privadas porque permite un rápido aprovisionamiento y desaprovisionamiento de servicios bajo demanda.

Calidad de servicio

Las organizaciones de TI deben centrarse en la calidad de los servicios que brindan, es decir, **el buen mantenimiento de las aplicaciones y la infraestructura subyacente.** Cuando la virtualización se gestiona adecuadamente, puede ayudar a mejorar la calidad del servicio porque elimina la dependencia del hardware. Además, la virtualización de los sistemas permite responder con más rapidez a todo tipo de fallos (sean estos de hardware, de red), incluso si son causados por el software de virtualización. También, se puede implementar de forma preventiva para evitar fallos al mover cargas de trabajo de un sistema que presenta signos de problemas inminentes (memoria, disco, etc.).

Conmutación por error

El hipervisor monitoriza constantemente el estatus de cada máquina virtual, por lo que es relativamente sencillo configurarlo para iniciar una nueva instancia de una máquina virtual, en caso de que se observe que una que se estaba ejecutando anteriormente ya no está presente. El hipervisor, simplemente, tiene que iniciar una máquina virtual nueva basada en la imagen de la máquina virtual anterior. Este proceso puede durar apenas unos segundos y, obviamente, representa una importante mejora sobre la duración típica de restauraciones de sistemas no virtualizados.

Alta disponibilidad

La alta disponibilidad o *high availability* (en siglas, HA) extiende el concepto de conmutación por error **al incorporar un servidor de hardware adicional.** Es decir que, en el caso de que la máquina virtual fallase, esta no se iniciaría en la misma pieza de hardware, sino que se iniciaría en un servidor diferente, evitando así el problema de conmutación por error de virtualización por adición del hardware.

¿Cómo funciona la alta disponibilidad?

¿Cómo es posible que un hipervisor, en un servidor físico, inicie una máquina virtual en otro hipervisor? La respuesta es clara: no es posible. No puede. La alta disponibilidad se basa en un software de virtualización global que coordina los esfuerzos de múltiples hipervisores. Cuando una máquina virtual en un servidor de hardware falla, el software de coordinación inicia una nueva máquina virtual en un servidor de hardware separado.

En realidad, es un poco más complejo que eso. El software de coordinación de virtualización monitoriza constantemente todos los hipervisores y sus máquinas virtuales. Si el software de coordinación ve que el hipervisor en un servidor ya no responde, reinicia las máquinas virtuales del hardware que ha fallado en otro hardware. Por lo tanto, **la alta disponibilidad aborda el problema del fallo del hardware mediante el uso de un software de virtualización de mayor nivel para coordinar los hipervisores en dos o más máquinas, a través de la monitorización continua y el reinicio de máquinas virtuales en otras máquinas si es necesario.**

Como se puede apreciar, esto ciertamente aborda el problema de fallo del hardware y hace que la conmutación por error sea más robusta. Parte del estado de una máquina virtual es su dirección de red y sus recursos de almacenamiento. Si se mueve una máquina virtual a otra pieza de hardware, estos *bits* de su estado necesitan moverse también, ya que, en caso contrario, la nueva máquina virtual no podrá ubicar el almacenamiento ni conectarse a las redes. Por lo tanto, la alta disponibilidad requiere que el software de virtualización pueda migrar estas partes (estados) de la máquina virtual a otro servidor físico y configurar el hipervisor de ese servidor para usar el estado de la máquina virtual del hardware original que ha fallado. Algunos programas (software) de alta disponibilidad incluso tienen la capacidad de ver lo que sucede dentro de una máquina virtual y reiniciar la aplicación que se estaba ejecutando en otra máquina virtual distinta.

**La HA proporciona una capa adicional de protección contra la conmutación por error a través del software de virtualización.** Sin embargo, la HA no proporciona la capacidad para migrar el estado actual de la memoria de la máquina virtual a la segunda máquina. Dicho de otra manera, aunque se pueda ejecutar una máquina virtual en una segunda máquina, los usuarios que trabajan en la máquina virtual original perderán el estado de su trabajo. Dependiendo de qué tipo de aplicación se trate, esa pérdida podría ser inaceptable. Por ejemplo, si la solicitud está procesando transacciones multimillonarias en dólares estadounidenses, una pérdida mínima puede impactar significativamente a la organización.

Agrupamiento o *clustering*

**El agrupamiento está diseñado para garantizar que no se pierdan datos en caso de que haya un fallo de software o de hardware.** El *clustering* ha sido ofrecido, históricamente, por los proveedores de aplicaciones como complemento de otros productos, pero con algunos inconvenientes relacionados: gastos adicionales, soluciones redundantes e infraestructura compleja. El gasto extra, o adicional, se produce por la necesidad de contar con hardware adicional, con el sistema en espejo en espera (en modo *standby*), listo para asumir el control si fallase el sistema primario. Como verán, no hace falta ser un experto para reconocer que la compra de un segundo conjunto de hardware hace que el agrupamiento represente un gasto significativo. Sin embargo, si en el sistema se operan transacciones de millones de euros (o cualquier otra moneda), mantener un servidor redundante que esté listo para operar cuando haya un fallo, puede ser una inversión que valga la pena.

¿Cómo funciona el agrupamiento?

Esencialmente**, el software de coordinación de virtualización ejecuta dos máquinas virtuales en máquinas separadas.** Las máquinas virtuales son idénticas en cuanto al sistema operativo y la configuración de la aplicación, pero difieren, naturalmente, en los detalles de sus conexiones de red y hardware local. El supervisor de virtualización se comunica constantemente con las máquinas virtuales en el clúster para confirmar que están trabajando (esto generalmente se conoce como *heartbeat* o latido del corazón). Una máquina virtual (en siglas, VM) es el servidor primario y es el sistema con el que los usuarios interactúan. La segunda VM sirve como copia de seguridad, lista para actuar en caso de que el servidor primario se caiga.

El servidor primario envía constantemente cualquier cambio al servidor secundario para que su estado refleje el de la VM primaria en todo momento. Si la VM principal falla, el supervisor de virtualización detecta que no está disponible y cambia a los usuarios al servidor de respaldo. Los usuarios que se conecten después del cambio no notarán nada y no serán conscientes de que están conectados a una VM diferente. Por su parte, los usuarios que se han conectado a la VM original, que ya no está disponible, tampoco serán conscientes del cambio, porque el software de virtualización ha ido enviando el estado de estos usuarios a la máquina secundaria. A lo sumo, podrán notar un descenso en la capacidad de respuesta mientras se realizaba el cambio, pero generalmente es tan rápido que es difícil que lo detecten.

Ahora bien, como podemos ver, hay un recurso poco aprovechado en el clúster de virtualización: hay una VM que actúa como copia de seguridad y que se mantiene actualizada, pero que no realiza ningún trabajo. Aunque ejecutar una VM en un servidor virtualizado es ciertamente menos costoso que dedicar un servidor completo para actuar, como una copia de seguridad activa, esto genera costes.

Duplicación de datos *(data mirroring)*

Hasta aquí hemos abordado los mecanismos involucrados en mantener a las máquinas virtuales en funcionamiento, pero ¿qué hay de los datos? Después de todo, las aplicaciones dentro de las máquinas virtuales son inútiles sin datos, por lo que es claramente importante garantizar la disponibilidad de los datos como parte de una estrategia general de calidad de servicio.

Una forma de mantener los datos disponibles es a través de la duplicación. Como el nombre implica, esta duplicación o reflejo significa que los datos existentes en un sitio son reflejados en otro, y ambas contienen la misma información. La duplicación permite la consistencia en tiempo real entre dos fuentes de datos. Esto posibilita el cambio inmediato entre un sistema y otro, es decir, conectando el segundo sistema a la duplicación o el reflejo de los datos del sistema primario.

Réplica de datos

La replicación es otro servicio orientado a mejorar la calidad del servicio de datos. A diferencia de la duplicación *(data mirroring)* que se enfoca en cómo mantener copias de datos consistentes en tiempo real**, la replicación aborda la necesidad de mantener copias completas de los datos para que puedan ser utilizados en la reconstrucción del sistema.** Esto se logra enviando copias de datos a un almacenamiento centralizado, lo que permite a una organización tener la seguridad de que en caso de que necesite acceder a los datos críticos por algún motivo, estos están almacenados de forma segura y disponibles en caso de ser necesarios.

La eficiencia es vital para la replicación, es decir que, no debemos pensar que porque los datos se están moviendo a una ubicación de almacenamiento hay que olvidarse de que los datos deben fluir correctamente. Un software de replicación inteligente mantiene los cambios, minuto a minuto, fluyendo a la ubicación central, asegurando así que una organización de TI pueda localizar rápidamente los datos y usarlos para reconstruir el sistema en caso de fallos.

Flexibilidad operacional de TI

Las organizaciones de TI deben estar preparadas para responder ante los cambios y las condiciones de negocio. Es por ello por lo que no hay mejor palabra para definir esta cualidad que el adjetivo «ágil». Cuando pensamos en un atleta ágil, probablemente imaginamos a alguien que puede cambiar de rumbo rápidamente, detenerse o cambiar la dirección para adaptarse a lo que sucede en el entorno que le rodea.

Como es sabido, estos son los requisitos para las organizaciones de TI en la actualidad:

* Deben ser lo suficientemente flexibles como para aumentar o reducir los recursos informáticos que dedican al desarrollo de sus aplicaciones.
* Deben implementar infraestructura y procesos que reduzcan la cantidad de trabajo manual para cambiar los recursos informáticos que utilizan.

En resumen, **la organización de TI actual debe estar lista para moverse rápidamente en cualquier dirección a fin de responder a los cambios internos o externos del entorno.**

Balanceo de carga (*load balancing*)

El equilibrio o balanceo de carga protege a un sistema de la vulnerabilidad contra cualquier condición de error dada al implementar la denominada redundancia. Esta se logra a través de **la ejecución de una o más copias de una máquina virtual en servidores separados.** Cuando se ejecutan dos instancias de una máquina virtual y una de ellas se bloquea, la otra continúa funcionando. Si el hardware que da soporte a una de las máquinas virtuales falla, la otra máquina sigue funcionando. De esta manera, se evita que la aplicación sufra una interrupción.

El balanceo de carga también hace un mejor uso de los recursos de la máquina. Esto es así porque, en lugar de que la segunda máquina virtual esté inactiva y no realice ningún trabajo útil (aunque esté siendo actualizada por la máquina principal), la segunda VM lleva la mitad de la carga y esto hace que al menos la mitad de sus recursos se utilicen. El uso de recursos duplicados puede extenderse más allá de las máquinas virtuales en sí mismas. Las organizaciones que luchan por alcanzar altos niveles de disponibilidad a menudo implementan redes duplicadas con cada servidor físico con conexión cruzada con el resto de la red, lo que garantiza que las máquinas virtuales continuarán siendo capaces de comunicarse, incluso si parte de la red se cae.

La migración hacia un almacenamiento virtualizado puede ayudar con el balance de carga, la combinación de almacenamiento y virtualización en el servidor proporciona:

* Máxima flexibilidad.
* Mayor aprovechamiento.
* Administración más sencilla.

Es necesario el almacenamiento en la red si las máquinas virtuales se ejecutan en servidores diferentes. Las máquinas virtuales con carga balanceada también se pueden configurar para que funcionen como un agrupamiento o clúster y que compartan el estado entre ellas. De esa manera, si una máquina virtual falla, su trabajo puede ser retomado por la otra máquina virtual.

Agrupación de servidores *(server pooling)*

Con la agrupación de servidores, el software de virtualización gestiona un grupo *(pool)* de servidores virtualizados. **En lugar de instalar una VM en un servidor en particular, simplemente se apunta el software de virtualización a la imagen de la VM** y este software determina qué servidor físico es el más adecuado para ejecutar la VM. El software del *pool* de servidores también realiza un seguimiento de cada VM y servidor para determinar cómo se asignan los recursos. Si una VM necesita ser reubicada para utilizar mejor los recursos disponibles, el software de virtualización automáticamente migra la VM a un servidor más adecuado.

El *pool* se gestiona a través de una consola de administración y, si se advierte que este está alcanzando su tasa de utilización máxima, se puede agregar de forma transparente otro servidor adicional al grupo. A continuación, el software de virtualización reequilibra las cargas para que el uso de todos los recursos de los servidores sea lo más efectivo posible. Debido a que no se puede saber qué servidor físico ejecutará la máquina virtual, el almacenamiento debe estar conectado en red para que una VM en cualquier servidor pueda acceder a los datos.

Sin lugar a duda, **aquí está la semilla del futuro de la virtualización.** En un futuro próximo, los departamentos de TI dejarán a un lado la instalación manual sistemas operativos en servidores individuales, o incluso en la gestión de clústers de máquinas virtuales en servidores individuales, debido a que son prácticas ineficientes.

Gestión de recuperación ante desastres

La recuperación ante desastres engloba a productos y procesos que ayudan a las organizaciones de TI para que puedan responder ante situaciones catastróficas, mucho peores que aquellas que se desatan cuando una VM falla o aquellas en las que falla una pieza de hardware. **La recuperación ante desastres entra en juego cuando todo el centro de datos se pierde, ya sea de forma temporal o permanente.**

En estos casos, las organizaciones de TI necesitan luchar para mantener la infraestructura informática de toda la empresa en funcionamiento. Pensemos en el huracán Katrina: cuando se desató la catástrofe muchas empresas de TI perdieron toda la capacidad de procesamiento porque sus centros de datos quedaron completamente inundados. Como si eso fuese poco, también se perdió la conectividad a Internet debido a que los centros de telecomunicaciones también estaban inundados. En estos casos, la capacidad de reserva en el centro de datos no tiene ninguna relevancia. Ante siniestros de esta magnitud como tormentas, terremotos o desastres provocados por el hombre, **se necesita contar con la capacidad de recuperación ante desastres.**

Es un requisito indispensable contar con capacidad adicional en el centro de datos, facilidad para recuperar los sistemas operativos y las aplicaciones, y una ágil administración de la infraestructura migrada. Además, se necesitará contar con un plan de contingencia para el proceso de recuperación de desastres, de modo que, si este ocurriera, el personal de TI pueda ejecutar el plan documentado y ensayado.

La virtualización será útil para la recuperación de la aplicación y las tareas de gestión: la tolerancia a fallos, la alta disponibilidad, el agrupamiento o *clustering* y las capacidades de virtualización de balance de carga (o agrupación de servidores) se pueden aplicar en un escenario de recuperación ante desastres. Todo dependerá de cuánto se desee gestionar físicamente durante el proceso de recuperación ante desastres.

Debido a que las imágenes de la VM pueden capturarse en archivos y luego iniciarse a través del hipervisor, la virtualización es una tecnología ideal para escenarios de recuperación ante desastres. Como se puede imaginar, en un momento crítico, localizar servidores físicos, configurarlos, instalar y configurar aplicaciones, hacer una copia de seguridad y actualizar el sistema puede ser una verdadera pesadilla. Además, mantener una capacidad informática adicional en un centro de datos remoto, que refleje completamente la infraestructura informática primaria, es extremadamente caro.

A través de la virtualización, un conjunto mucho más pequeño de máquinas puede mantenerse disponible en un centro de datos remoto, con un software de virtualización preinstalado y listo para aceptar imágenes de una VM. En el caso de que se produzca un siniestro de enormes proporciones, las imágenes de la VM se pueden transferir desde el centro de datos de producción hacia el centro de datos de *backup.* Estas imágenes de la VM pueden iniciarse con el software de virtualización preinstalado y ponerse en marcha en solo unos minutos.

En caso de dudas, si existe un riesgo inminente de que algunas transacciones se perdieran sin que hubiese tiempo para migrar imágenes de una VM, se puede ejecutar el clúster o el balanceo de carga, a fin de que los dos centros de datos permanezcan actualizados. Esta infraestructura asegura el acceso al más valioso activo de toda organización: los datos, y, además, ayuda a las empresas a ser resilientes en caso de que se pierda el acceso a los datos en una de las ubicaciones.

Ejemplos concretos

![](data:image/jpeg;base64...)

Tabla 1. Ejemplos reales de virtualización. Fuente: elaboración propia.

5.3. Resultados de alto impacto

Los centros de datos tradicionales, aunque ofrecen buenas capacidades de procesamiento, tienen sus limitaciones, y está claro que no podrán satisfacer las necesidades de TI del mañana. Están formados por sistemas aislados, cada uno de los cuales proporciona funcionalidades específicas, pero que no pueden trabajar de forma cooperativa con otros sistemas. El modelo tradicional «una aplicación, un servidor», tan típico de muchos centros de datos: aplicaciones en servidores físicos incapaces de compartir datos, incapaces de aprovechar eficientemente el hardware y poco ágiles para responder rápidamente a las condiciones cambiantes (y a veces caprichosas) de negocio. **La virtualización proporciona beneficios reales en términos de rendimiento empresarial: mejor utilización del hardware e infraestructuras de TI más robustas y ahorro de costes de energía eléctrica.**

Infraestructura convergente

La virtualización está cambiando el paradigma de los negocios de TI y es por ello por lo que es necesario examinar todos los supuestos y prácticas preexistentes para alinearlos con la nueva realidad.

Implementar la virtualización a una determinada infraestructura, sin hacer un análisis previo, puede generar fricciones y opacar una visión objetiva sobre todos los beneficios que puede ofrecer la tecnología. Por el contrario, un enfoque más eficiente consiste en repensar cómo está montada la infraestructura y qué cambios se pueden aplicar en pos de la virtualización.

Estrategias de éxito

Análisis de la infraestructura

En lugar de enfocar a la virtualización como un esfuerzo fragmentario, es necesario tener **una visión integral de la infraestructura** y planificar con detenimiento cómo se podría aplicar la virtualización en todo el centro de datos. Es necesario hacerse estas preguntas: ¿qué servidores se pueden virtualizar?, ¿qué aplicaciones deben permanecer en sistemas independientes?, ¿qué tipo de redes y almacenamiento necesitas para dar soporte a un entorno altamente virtualizado, que permita un rápido movimiento entre las VM y las cargas de trabajo de las aplicaciones?

Uso y preferencia de tecnología diseñada y optimizada para la virtualización

Cuando llega el momento de reemplazar el hardware existente o agregar capacidad, asegúrate de que los nuevos productos sean compatibles con la virtualización. Actualmente, se están diseñando servidores, almacenamiento y sistemas *Blade* compatibles con la virtualización y es por ello por lo que incluyen memoria adicional, balance de carga automatizado, más conexiones de red, e incluso software de virtualización integrado. Asegúrate de que el nuevo equipo de infraestructura puede soportar los planes de virtualización que tienes en mente.

Crea un entorno de almacenamiento en red o compartido

Si bien el concepto de «una aplicación, un servidor» era suficiente para las organizaciones TI del pasado, en la actualidad **es un modelo que ha quedado desfasado.** Sabemos que el almacenamiento que no se puede compartir representa una gran desventaja, porque mantiene los sistemas aislados e incapaces de responder a las condiciones cambiantes de mercado. Se requiere una red de área de almacenamiento compartido, del inglés *Network Attached Storage*, (en siglas, SAN o NAS) para aprovechar las capacidades de virtualización del servidor como: la migración en tiempo real de las máquinas virtuales, la alta disponibilidad, la tolerancia a fallos y la recuperación ante desastres.

Virtualización de las conexiones de red

Las conexiones que vinculan los servidores a las redes de almacenamiento y a las **redes de área local (en siglas, LAN)** pueden representar una importante barrera. Cada cambio que requiera intervención manual ralentizará a la organización de TI y la alejará de la agilidad tan característica de DevOps. Las conexiones de red virtualizadas permiten que estos posibles puntos de fricción se gestionen de forma remota, eliminando así los cuellos de botella.

Gestiona los recursos virtuales y físicos con las mismas herramientas

Muchas organizaciones de TI instalan una solución de gestión de la virtualización junto a los recursos de gestión existentes y luego se preguntan por qué la carga de trabajo ha aumentado en vez de disminuir. El enfoque más recomendado es aquel que te permita gestionar los dispositivos físicos y virtuales desde la misma interfaz.

5.4. Buenas prácticas en administración de TI

**La clave para hacer coincidir los requisitos de negocio con las operaciones de TI consiste en una alineación adecuada y decisiones acertadas a la hora de elegir los recursos físicos y virtuales necesarios para brindar los servicios que permitirán alcanzar los objetivos comerciales.** Además, dichos recursos deben administrarse en tiempo real para garantizar que las aplicaciones y la infraestructura estén siempre listas para cumplir con las demandas del servicio.

![](data:image/png;base64...)

Figura 1. El Gobierno de TI se aplica también a la virtualización. Fuente: elaboración propia.

A continuación, veremos las áreas más importantes en las que debemos focalizarnos para que esta alineación sea eficiente y productiva:

* **Considera a la virtualización como un servicio de negocio**. Al tener esta perspectiva, estarás motivado bajo la premisa de que la virtualización forma parte de un esfuerzo conjunto de la organización para cumplir con los requisitos de negocio.
* **Monitoriza los servicios en las infraestructuras físicas y de virtualización.** Los complejos procesos empresariales actuales están controlados por múltiples aplicaciones, que pueden ubicarse en infraestructuras físicas o virtuales. La administración desde una perspectiva de negocio te permitirá realizar un seguimiento de las operaciones de TI en todo el espectro de recursos de TI y optimizarlos de manera integral. El uso de un enfoque unificado hacia la administración física y virtual evitará que haya grietas (y, por tanto, fallos y pérdidas de información) entre estos dos bloques.
* **Virtualiza los procesos de gestión de los servicios.** Las soluciones de gestión proporcionan procesos como la gestión de incidentes y fallos. También aportan soluciones consistentes para gestionar el cumplimiento de las licencias en entornos virtuales y físicos. Además, favorecen la alineación de todos los recursos y procesos para las iniciativas de optimización de servicios.
* **Integra la virtualización en la gestión de calidad.** Las áreas que se benefician en mayor medida de la virtualización son aquellas relacionadas con las pruebas y la calidad, ya que se pueden eliminar las intervenciones manuales. Como beneficio aparejado, veremos un aumento de la coherencia, porque se podrán utilizar recursos idénticos en todo el ciclo de vida de QA y se evitarán errores derivados de una configuración incorrecta o una instalación inconsistente.

Virtualización del cliente desde el escritorio hasta el centro de datos

La **virtualización del cliente** es la última frontera en la tecnología de virtualización y es sabido que brinda enormes beneficios a las organizaciones. Aunque la virtualización del servidor mejora las operaciones del centro de datos, la virtualización del cliente puede mejorar los resultados para cualquier otra parte de la organización, en otras palabras, para la gran mayoría de empleados.

Existen numerosos enfoques para implementar la virtualización del cliente y cada uno de ellos presenta beneficios. Sin embargo, es importante que las circunstancias sean las adecuadas para asegurar que se obtenga el máximo valor de su implementación.

Estas son algunas de las consideraciones más importantes que hay que analizar antes de proceder hacia la virtualización del cliente:

No pierdas de vista los requisitos de negocio

El ordenador tradicional proporciona un buen nivel de productividad a los trabajadores, pero tal vez no sea suficiente para cumplir con todos los objetivos de negocio. Por ejemplo, las necesidades de recuperación ante desastres pueden establecer que las aplicaciones y los datos se mantengan dentro de los centros datos donde se puedan ser migrados rápidamente, a través de la virtualización, hacia otros centros de datos.

Asegúrate de que la tecnología que elijas es adecuada para cada tipo de usuario

Dependiendo del tipo de empleado del que se trate, puedes elegir una variedad de virtualización del cliente u otra. Las soluciones informáticas basadas en el servidor proporcionan acceso remoto a la aplicación, a un escritorio en un entorno operativo compartido. Ciertamente, desde un punto de vista financiero, esto puede representar cierta rentabilidad, ya que aumenta la seguridad del cliente y mejora la protección de datos y la capacidad de administración para aquellos trabajadores que desempeñan sus funciones resolviendo tiques o tareas concretas.

Por su parte, la infraestructura de escritorio virtual, del inglés *Virtual Desktop Infrastructure,* (en siglas, VDI) proporciona escritorios completamente funcionales y personalizados, que se entregan a través de la red desde un servidor compartido. Cada escritorio virtual está aislado y seguro en el centro de datos, compartiendo recursos del centro de datos físico, para garantizar un uso óptimo de sus recursos a través de la virtualización. Esta opción resulta ideal para las aplicaciones básicas de oficina y permite que TI maximice la utilización, reduzca costes y aumente la fiabilidad.

Los Blade resultan óptimos para las aplicaciones especializadas que operan, por ejemplo, con gráficos pesados, ya que ofrecen un rendimiento muy fluido y sin interrupciones (generando una excelente experiencia de usuario), junto con un control centralizado y seguridad en el centro de datos.

Determina cuáles son tus necesidades de almacenamiento

La gran mayoría de las soluciones de virtualización del cliente requieren que se muevan datos fuera del dispositivo local hacia otra solución de almacenamiento centralizada. Asegúrate de que en tu planificación de virtualización de cliente incluyes requisitos y opciones de almacenamiento que puedan dar soporte de forma eficiente.

No olvides ser coherente en tus esfuerzos de virtualización de cliente

Cuando implementas varias tecnologías diferentes de virtualización del cliente, hay que asegurar que todas ellas funcionan bien juntas. Por ello, obtener soluciones de diferentes proveedores puede complicar aún más las cosas y perjudicar el esfuerzo global de virtualización, y, ciertamente, obstaculizará la premisa de mantenerse alineado con los requisitos de negocio. Dicho esto, es probable que la opción más coherente sea la de contar con un único proveedor que proporcione una cartera completa de soluciones y servicios de cliente.

5.5. Cómo encauzar tu proyecto de virtualización

A continuación, descubriremos cuáles son las premisas fundamentales que debes tener en mente si deseas emprender el viaje hacia la virtualización y quieres trabajar de forma metódica y ordenada.

Para comenzar, lo más importante que debes saber es que **la virtualización es un camino para emprender, no un producto.** Cualquier proyecto importante requiere una planificación cuidadosa y, por supuesto, una monitorización en cada una de sus etapas. Deberás pasar por la planificación, la implementación y tareas ligadas al área de operaciones, y luego dar seguimiento al proyecto y evaluar los hitos. La virtualización hace que el proceso de planificación de proyectos sea aún más importante porque, después de que las organizaciones de TI comienzan a ver los beneficios tangibles de la migración a entornos virtualizados, comienzan a cuestionarse en qué otras áreas podrían aplicar la virtualización.

A continuación, **es recomendable que realices una evaluación de los casos de uso.** En pocas palabras, cómo aplicarás, o cómo aplicarías en un futuro próximo la virtualización. Un caso de uso es sumamente útil para identificar las capacidades de virtualización que quizás no necesites hoy en día, pero que podrían ser relevantes en el futuro. Debido a que hay varias maneras diferentes de usar la tecnología de virtualización, debes pensar en cómo quieres o puedes aplicarla. La gama de productos que se pueden utilizar para la virtualización tiende a reducirse a medida que aumenta la complejidad de las aplicaciones. En estos casos, acudir a un taller o *workshop* organizado por un proveedor puede ayudarte a esclarecer qué producto es más conveniente para tu caso particular. Otra herramienta valiosa es realizar una prueba de concepto, del inglés *proof of concept*, (en siglas, POC) de virtualización.

El siguiente paso en este plan metódico es **analizar la estructura del equipo de operaciones de la organización.** Es tentador creer que la virtualización es un asunto puramente técnico, pero eso sería muy simplista. Lo que sí es un hecho contrastado es que los humanos somos animales políticos (o, al menos, sociales). Eso significa que las decisiones, incluso las tecnológicas, confrontan con los prejuicios emocionales de las personas que forman parte de la organización y afectan la aceptación de nuevas iniciativas (resistencia al cambio).

Muchos equipos de operaciones de TI están organizados de forma funcional. En otras palabras, un grupo administra servidores, otro grupo administra la red y otro administra los recursos de almacenamiento. Sin embargo, la virtualización integra todas estas funciones en una unidad, por lo que estos grupos autónomos necesitarán colaborar y cooperar. Por lo tanto, **es necesario examinar el «lado humano» de los equipos de operaciones de TI para garantizar que la virtualización se llevará a cabo de manera fluida.**

Para continuar avanzando en el viaje hacia la virtualización, es necesario que definas tu arquitectura. Esto es una forma elegante de decir que debes **recoger la información que has recabado sobre los casos de uso, así como de la estructura organizativa de operaciones y definir cuál será tu diseño de infraestructura de virtualización.** Este diseño es absolutamente crítico y es necesario que sea revisado por todas las partes interesadas e involucradas. Este proceso de revisión tiene dos propósitos fundamentales: por un lado, garantiza que se han recogido las necesidades de todas las partes y, por otro lado, tiende a generar conciencia y compromiso en los diferentes grupos involucrados en la virtualización.

Una vez que hayas definido tu arquitectura de virtualización, ya puedes **seleccionar el producto o los productos (software) que usarás en tu proyecto de virtualización.** Esta selección debería ser un ejercicio relativamente sencillo, ya que previamente has identificado qué funcionalidad debe estar presente en tu arquitectura de virtualización. En cuanto al servidor, los productos de VMware, Citrix y Microsoft son opciones más que consolidadas. A su vez, numerosos productos de virtualización de almacenamiento están en el mercado, y esta se está extendiendo a nuevas áreas como las redes. Es una cartera mucho más rica, pero con una gran cantidad soluciones, solo debes seleccionar cuidadosamente aquellos productos que cumplan con los requisitos de los casos de uso que has detectado.

Y como es de esperar, lo siguiente que debes tener en cuenta para tu proyecto es seleccionar el hardware de virtualización. **Un punto clave es que te asegures de que el hardware es compatible con la virtualización.** Muchas organizaciones intentan reutilizar hardware del que ya disponen y descubren que no es escalable ni es adecuado para los casos de uso que tienen en mente.

Además, cada vez que virtualizas servidores, también debes evaluar:

* La infraestructura de almacenamiento para que satisfaga las demandas del servidor.
* Las implementaciones de virtualización del cliente y que, a su vez, estén estrechamente integradas con la plataforma del software de virtualización.

Llegados a este punto, **es necesario que realices una prueba piloto para confirmar que todo funciona, como es debido, en producción.** Realiza una prueba de tu solución de virtualización en un entorno de prueba controlado para asegurarte de que todo funciona correctamente. Ya tienes tu software de virtualización, el hardware que te acompañará en este viaje hacia la virtualización y cualquier otro dispositivo necesario para que el centro de datos funcione adecuadamente. Este es el momento de confirmar que tienes todo lo que necesitas para seguir adelante con la migración hacia tu nueva arquitectura. Este paso tiene que ejecutarse con cautela y sin errores, porque si la infraestructura no está bien montada, los sistemas de producción no trabajarán correctamente. Así que, pon a punto las configuraciones y asegúrate de que se inicia correctamente.

Poner gobierno y política en el lugar correcto

La virtualización reduce, en gran medida, el esfuerzo para implementar nuevos sistemas. Eso puede causar problemas, ya que, los nuevos sistemas se crean con poca supervisión. Puedes evitar esta expansión descontrolada poniendo en práctica procesos y políticas. Esto se conoce como el término «gobierno» que, como es de esperar, implica estructura y reglas formales por las que se rigen el uso de los recursos de TI.

Gestiona tu infraestructura virtualizada

Asumamos que finalmente has implementado tu infraestructura de virtualización y conseguiste que sus servidores físicos sean migrados a ella. Quizás crees que has terminado, pero de ninguna manera. Necesitas administrar el nuevo entorno. Además, para obtener el máximo beneficio de tus nuevas capacidades de virtualización, necesitas integrarlos en tu proceso de gestión general, para que puedas administrar sistemas físicos y virtuales con las mismas herramientas, los mismos procesos y las mismas personas. Esto es particularmente importante porque las organizaciones están cambiando cómo implementan los sistemas hoy en día: puedes mantenerlos virtuales a lo largo de las fases de desarrollo y despliegue o puedes desarrollarlos virtualmente y desplegar físicamente. Por esta razón, se utiliza un proceso de gestión y un conjunto de productos que pueden fácilmente gestionar tanto lo físico como lo virtual es importante.

Diez errores de virtualización que debes evitar

* **No esperes la perfección.** El campo de virtualización está en un gran flujo porque así están sucediendo muchos cambios, a veces parece un hay nuevos productos o servicios disponibles todos los días. Algunas personas deciden abrazar un campo que cambia rápidamente porque esperan que ofrezca tremendo potencial. Otros se quedan atrás, con el pensamiento de que preferirían diferir la acción hasta que las cosas estén más estable.
* **No escatimes en el entrenamiento.** Una de las cosas más desconcertantes sobre las organizaciones de TI es que invertirán grandes sumas en nuevo hardware y software, pero escatiman en asegurar que sus empleados sepan cómo usar sus nuevos sistemas.
* **No te expongas a problemas legales: *compliance*.** Otra área potencial para considerar en un entorno virtualizado es el licenciamiento de software. Cuando sistemas físicos individuales se aprovisionan y presentan como sistemas múltiples, y el uso de sistemas virtuales es variable, los acuerdos de licencia históricos y los escenarios pueden cambiar. Además, con el auge de los dispositivos virtuales y la gran cantidad de nuevos sistemas posibles (debido a la virtualización), hace muy complicado, y más importante, el seguimiento de las licencias de software. Así que es necesario asegurarse de poner los procesos para garantizar que realiza un seguimiento de licencias y mantener el cumplimiento de todas sus responsabilidades.
* **No pienses que la virtualización es estática.** Las condiciones de su negocio no solo dictarán que evalúes continuamente qué tan bien tu infraestructura de virtualización cumple con las realidades comerciales actuales, pero la virtualización en sí está cambiando constantemente. Esto significa que tu solución de virtualización de vanguardia, implementada hace dieciocho meses, puede necesitar ser renovada a la luz de los nuevos desarrollos de virtualización.
* **No evites hacer el trabajo que consideras aburrido.** Es divertido instalar software y ver surgir cosas nuevas. No es tan divertido utilizar entrevistas de casos o revisiones técnicas. Pero ten en cuenta que esas tareas «aburridas» hacen posibles a las cosas divertidas. De hecho, a menos que completes estas tareas aburridas, probablemente no obtendrás el visto bueno para avanzar con el proyecto y divertirte haciendo las cosas interesantes.
* **Presta atención a los casos de negocio.** En estos tiempos de presupuestos ajustados para las organizaciones de TI, hoy no hay forma más segura de que tu proyecto sea derribado que la falta de casos negocios para él. Por otro lado, no hay manera 100 % segura de asegurar que tu proyecto obtenga apoyo ejecutivo y navegue a través del proceso de aprobación, más que demostrando impresionantes beneficios financieros generados al avanzar con el proyecto. Esto significa que te corresponde: evaluar la situación financiera, el impacto de pasar a la virtualización y presentar esa información como parte del proceso de aprobación del proyecto.
* **Presta atención a la organización.** Debido a que la virtualización afecta a tantos grupos, es importante que trabajes con cada uno de ellos y los convenzas de que la virtualización hará que su trabajo sea mejor y más fácil. Esto incluye no solo grupos técnicos, sino patrocinadores comerciales, así como la alta gerencia. Cuando cambias la infraestructura afecta a muchos grupos, así que asegúrate de incluirlos a todos en la planificación de tu proyecto. La clave es hacer que sus flujos y modelos de trabajo organizacionales explícitos.
* **Presta atención al hardware.** La virtualización es un software que habilita a otros recursos de software para aprovechar mejor el hardware subyacente. Pero no imagines que el hardware en sí no tiene ningún efecto en la virtualización. Lejos de eso, el tipo y la capacidad del hardware que utilizas para alojar su solución de virtualización puede afectar drásticamente la densidad de virtualización que logres, así como el rendimiento y los niveles de disponibilidad para tus máquinas virtuales o clientes. Así que, idealmente, tu hardware debe estar alineado a tus requisitos y expectativas.
* **Presta atención a la administración de servicios.** La mayoría de las plataformas de virtualización vienen con su propio conjunto de herramientas de administración. Aunque muchas de estas herramientas funcionan bien dentro de sus dominios propios, no son lo suficientemente maduros o robustos para administrar más allá de sus plataformas originales. También tienden a requerir capacitación adicional para ejecutar, mantener y producir gestión de información que reside fuera de los procedimientos de operaciones estándar aceptados. En lugar de adoptar un conjunto de herramientas y procedimientos para la virtualización, y otro para entornos físicos, buscar soluciones de gestión que administren tanto entornos físicos como virtuales en común facilitara el éxito.
* **Prepárate para un futuro aún más virtualizado.** La virtualización facilita la creación de nuevos sistemas, reduciendo el esfuerzo de días o semanas a meros minutos. Asimismo, el coste puede reducirse en un orden de magnitud. Dada esta facilidad de creación de sistemas, algunas organizaciones descubren que de repente tienen un exceso de sistemas: están expandiendo todo y, aunque el coste y el esfuerzo de crear un sistema virtual es bajo, si se hace en exceso, el problema de multiplicidad, volumen y falta de control será mucho mayor que con los sistemas físicos.

Existe una concepción errónea de que la nube es una solución económica y preferible a otras soluciones como la virtualización o la tecnología *serverless*. En la píldora *¿Cuál es el precio de la nube?* comentaremos los pros y contras de algunas de estas estrategias.

![](data:image/jpeg;base64...)

A fondo

*Caso éxito virtualización - MAPFRE*

Agilitix - Beyond Productivity. (2016, mayo 23). *Caso Éxito Virtualización - MAPFRE* [Vídeo]. YouTube. <https://www.youtube.com/watch?v=n-JeZ23NkM0>

En este vídeo podrás ver cómo funcionó la implementación de la virtualización dentro de MAPFRE para a dar paso hacia mejores prácticas de implementación y uso de esta tecnología integrada.

Test

1. Señala la opción que no se encuentra entre los casos de uso apropiados para virtualización:

A. Consolidación de servidores.

B. Entornos de desarrollo y pruebas.

C. Computación de nube privada.

D. Incrementar la seguridad de red.

1. Señala la opción que ayudará a encauzar la puesta en marcha de un proyecto de virtualización:

A. Establecer el gobierno y las políticas necesarias.

B. Consolidación de servidores siempre.

C. Contratar gente nueva.

D. Ninguna de las anteriores.

1. Señala la opción que no se encuentra entre los casos de uso apropiados para virtualización:

A. Calidad del servicio.

B. Alta disponibilidad.

C. Aumentar la capacidad de almacenamiento sin inversión adicional.

D. Recuperación de desastres.

1. Señala la opción que se corresponde con un error común en proyectos de virtualización:

A. Pensar que el hardware no importa y cualquier hardware es bueno para los proyectos de virtualización.

B. Organizar sesiones de entrenamiento para todo el equipo.

C. Contratar expertos.

D. Ninguna de las anteriores.

1. Señala la opción que mejor encaja con una estrategia de éxito para virtualización:

A. Aumentar la calidad del servicio.

B. Una nueva estrategia requiere gente nueva.

C. Establecer un sistema de almacenamiento virtual compartido.

D. Recuperación de desastres.

1. Señala la opción que se corresponde con un error común en proyectos de virtualización:

A. Organizar sesiones de entrenamiento que no incluyen a toda la empresa.

B. Incurrir en problemas legales y/o de *compliance.*

C. A y B son ciertas.

D. Ninguna de las anteriores.

1. Señala la opción que no se encuentra entre los casos de uso apropiados para virtualización:

A. Clusterización.

B. Entornos de desarrollo y pruebas.

C. Recuperación de desastres.

D. Incrementar capacidad computacional de la empresa.

1. Señala la opción que mejor encaja con una estrategia de éxito para virtualización:

A. Reducir el equipo de gestión.

B. Invertir en hardware, pero no en formación.

C. Realizar un análisis previo a iniciar el proyecto de virtualización.

D. Todas las anteriores.

1. Señala la opción que mejor encaja con «buena práctica de administración de TI»:

A. Realizar *backups* de los sistemas más críticos.

B. Invertir en software de virtualización.

C. Monitorizar las infraestructuras tanto virtuales como físicas.

D. Todas las anteriores.

1. Señala la opción que se corresponde con el significado de POC:

A. POC significa *proof of concept* o prueba de concepto.

B. *Push to Talk over Celular*.

C. *Power on connectivity* y permite acceder a funciones de red sin tener el hardware encendido.

D. Ninguna de las anteriores.
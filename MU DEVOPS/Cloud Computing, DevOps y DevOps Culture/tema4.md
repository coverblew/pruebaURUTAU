Tema 4

Tecnologías de virtualización

Cloud Computing, DevOps and DevOps Culture

Índice

[Esquema 3](#_Toc76127495)

[Ideas clave 4](#_Toc76127496)

[4.1. Introducción y objetivos 4](#_Toc76127497)

[4.2. Virtualización de servidores 4](#_Toc76127498)

[4.3. Tipos de hipervisores y productos 6](#_Toc76127499)

[4.4. Componentes y servicios susceptibles a ser virtualizados 11](#_Toc76127500)

[A fondo 18](#_Toc76127501)

[Test 19](#_Toc76127502)

Esquema

![](data:image/jpeg;base64...)

Ideas clave

4.1. Introducción y objetivos

La virtualización tiene varios usos comunes y, lo cierto, es que todos ellos giran en torno al concepto de que su tecnología representa una abstracción de los recursos físicos. De hecho, existen demasiados tipos de virtualización y, es por ello por lo que, resulta un tanto confuso tratar de determinar cuál es la mejor solución que se puede aplicar en cada organización. Los dos tipos más comunes de virtualización aplicados a los centros de datos son: la virtualización de servidores y la virtualización de almacenamiento. Dentro de cada uno de estos, existen, además, diferentes enfoques o «sabores», cada uno con sus beneficios y desventajas. A continuación, vamos a explorar estos «sabores» básicos de las tecnologías de virtualización para que puedas descubrir las particularidades de cada uno y tomes decisiones estratégicas en la organización donde desarrolles tu actividad profesional.

Los objetivos de este tema son:

* Conocer las diferentes tecnologías existentes referentes a la virtualización.
* Conocer las diferentes herramientas que existen.
* Conocer los diferentes elementos susceptibles de ser virtualizados.

4.2. Virtualización de servidores

Existen tres tipos principales de virtualización de servidores que son: virtualización del sistema operativo (tecnología que se conoce bajo el nombre de Contenedores), imitación o emulación del hardware y paravirtualización. En este tema desarrollaremos los dos últimos.

Imitación o emulación del hardware

En este caso, **el software de virtualización (denominado hipervisor) crea una máquina virtual que imita todo el entorno de hardware.** El sistema operativo, que está cargado en una máquina virtual, es un producto estándar no modificado. Cuando realiza llamadas para recursos del sistema, el software de emulación de hardware captura la llamada del sistema y la redirige para que pueda gestionar estructuras de datos proporcionadas por el hipervisor. Es el propio hipervisor el que realiza las llamadas al hardware físico real, subyacente a toda la aglomeración de software.

![](data:image/png;base64...)

Figura 1. Virtualización por emulación de hardware. Fuente: Hewlett Packard Enterprise, s.f.

La emulación o imitación de hardware también es conocida como virtualización de metal desnudo (del inglés *bare metal virtualization*), para simbolizar el hecho de que ningún software se encuentra entre hipervisor y el «metal» del servidor. Como hemos mencionado, el hipervisor intercepta las llamadas del sistema desde la máquina virtual huésped y coordina el acceso al hardware subyacente directamente.

Paravirtualización

La paravirtualización no intenta emular un entorno de hardware en software, sino que un hipervisor de paravirtualización coordina (o multiplexa) el acceso a los recursos de hardware subyacentes del servidor. La arquitectura de la paravirtualización se puede ver en la Figura 2, que representa a Xen.

![](data:image/png;base64...)

Figura 2. Estructura de la paravirtualización. Fuente: Hewlett Packard Enterprise, s.f.

**En la paravirtualización, el hipervisor reside en el hardware y, por lo tanto, esta se puede concebir como una arquitectura de virtualización de metal desnudo.** Uno o más sistemas operativos huésped (equivalente a máquinas virtuales en virtualización de emulación del hardware) se ejecutan sobre el hipervisor. Un huésped privilegiado se ejecuta como una máquina virtual huésped, pero tiene privilegios que le permiten acceder directamente a ciertos recursos en el hardware subyacente.

4.3. Tipos de hipervisores y productos

VMware, Citrix y Microsoft son los principales proveedores de virtualización de servidores x86 en entornos profesionales, más adelante veremos otras opciones susceptibles de ser usadas también en entornos personales y de prueba.

* **VMware:** es el proveedor de virtualización de servidores más extendido y afianzado en el mercado. La plataforma insignia de VMware, vSphere, utiliza la tecnología de emulación de hardware.
* **Citrix:** ofrece un producto de virtualización de servidor, llamado XenServer, basado en paravirtualización. El huésped privilegiado (llamado *control domain* en lenguaje Xen) y el hipervisor Xen trabajan en equipo para permitir que las máquinas virtuales huésped interactúen con el hardware subyacente.
* **Microsoft:** Hyper-V, el producto de virtualización del servidor de Microsoft, tiene una arquitectura muy similar a la de Xen. En lugar de usar el término *control domain* para referirse a las máquinas virtuales huésped, Hyper-V se refiere a ellas como particiones y a la contraparte del *control domain* de Xen se la denomina partición principal.

Una definición sencilla de hipervisor podría ser: la parte de la nube privada que gestiona las máquinas virtuales, es decir, es la parte (programa) que permite que múltiples sistemas operativos compartan el mismo hardware. Cada sistema operativo podría usar todo el hardware (procesador, memoria) si no hay otro sistema operativo encendido. Ese es el hardware máximo disponible para un sistema operativo en la nube. Sin embargo, **el hipervisor es lo que controla y asigna qué parte de los recursos de hardware debe obtener cada sistema operativo, para que cada uno obtenga lo que necesita y no se interrumpa entre sí.** Hay dos tipos de hipervisores:

* Hipervisor de tipo 1. Los hipervisores se ejecutan directamente en el hardware del sistema: un hipervisor integrado «básico».
* Hipervisor tipo 2. Los hipervisores se ejecutan en un sistema operativo *host* que proporciona servicios de virtualización, como soporte de dispositivos de E/S y administración de memoria.

![](data:image/png;base64...)

Figura 3. Diferencias entre los tipos de hipervisores. Fuente: Projekt Cloud Computing, s.f.

Hipervisores tipo 1

VMware ESX y ESXi

Estos hipervisores ofrecen funciones avanzadas y escalabilidad, pero requieren licencia, por lo que los costos son más altos. VMware ofrece algunos paquetes de menor costo y pueden hacer que la tecnología de hipervisor sea más asequible para infraestructuras pequeñas. VMware es el líder en los hipervisores tipo 1. Su producto vSphere ESXi está disponible en una edición gratuita y en cinco ediciones comerciales.

Microsoft Hyper-V

El hipervisor de Microsoft, Hyper-V, no ofrece muchas de las funciones avanzadas que ofrecen los productos de VMware. Sin embargo, con XenServer y vSphere, Hyper‑V es uno de los tres principales hipervisores tipo 1. Se lanzó por primera vez con Windows Server, pero ahora, Hyper-V se ha mejorado enormemente con Windows Server 2012 Hyper-V. Hyper-V está disponible tanto en una edición gratuita (sin GUI y sin derechos de virtualización) como en cuatro ediciones comerciales: Fundamentos (solo OEM), *Essentials,* *Standard* y *Datacenter* Hyper-V. Actualmente, las nuevas versiones de supervisores de Microsoft están íntimamente relacionadas a sus productos de *Cloud* *Platform* y se les conoce como *Azure Stack.*

Citrix XenServer

Comenzó como un proyecto de código abierto. La tecnología principal del hipervisor es gratuita, pero al igual que ESXi gratuito de VMware, casi no tiene características avanzadas. Xen es un hipervisor de tipo desnudo de tipo 1 y, así como Red Hat Enterprise Virtualization usa KVM, Citrix usa Xen en el XenServer comercial.

Hoy, los proyectos y la comunidad de código abierto de Xen están en [Xen.org.](https://xenproject.org/) Hoy, XenServer es una solución comercial de hipervisor tipo 1 de Citrix, que se ofrece en cuatro ediciones. Confusamente, Citrix también ha calificado sus otras soluciones propietarias como XenApp y XenDesktop con el nombre Xen.

Oracle VM

El hipervisor Oracle se basa en el código abierto Xen. Sin embargo, si necesita soporte de hipervisor y actualizaciones de productos, le costará. Oracle VM carece de muchas de las características avanzadas que se encuentran en otros hipervisores de virtualización de metal desnudo.

Hipervisores tipo 2

VMware Workstation/Fusion/Player

VMware Player es un hipervisor de virtualización gratuito. Está destinado a ejecutar solo una máquina virtual (en siglas, VM) y no permite crear máquinas virtuales. VMware Workstation es un hipervisor más robusto con algunas características avanzadas, como grabación y reproducción y compatibilidad con instantáneas de VM.

VMware Workstation tiene tres casos de uso principales:

* Para ejecutar múltiples sistemas operativos.
* Para ejecutar versiones diferentes de un sistema operativo en un escritorio.
* Para desarrolladores que necesitan entornos de *sandbox* e instantáneas, o para laboratorios y con fines de demostración.

Servidor VMware

VMware Server es un hipervisor de virtualización alojado gratuito que es muy similar a VMware Workstation. VMware ha detenido el desarrollo en el servidor desde 2009.

Microsoft Virtual PC

Esta es la última versión de Microsoft de esta tecnología de hipervisor, Windows Virtual PC y solo se ejecuta en Windows 7 y solo es compatible con los sistemas operativos Windows que se ejecutan en él.

Oracle VM VirtualBox

La tecnología de hipervisor VirtualBox proporciona un rendimiento y características razonables si desea virtualizar con un presupuesto limitado. A pesar de ser un producto alojado gratuito con una huella muy pequeña, VirtualBox comparte muchas características con VMware vSphere y Microsoft Hyper-V.

Red Hat Enterprise Virtualization

La máquina virtual basada en el kernel (en siglas, KVM) de Red Hat tiene cualidades tanto de un hipervisor de virtualización alojado como virtual. Puede convertir el núcleo de Linux en un hipervisor para que las máquinas virtuales tengan acceso directo al hardware físico.

KVM

Esta es una infraestructura de virtualización para el kernel de Linux. Admite la virtualización nativa en procesadores con extensiones de virtualización de hardware. El KVM de código abierto (o máquina virtual basada en el núcleo) es un hipervisor tipo 1 basado en Linux que se puede agregar a la mayoría de los sistemas operativos Linux (incluidos Ubuntu, Debian, SUSE y Red Hat Enterprise Linux) pero también Solaris y Windows.

4.4. Componentes y servicios susceptibles a ser virtualizados

Virtualización de almacenamiento

La cantidad de datos que las organizaciones están creando y almacenando ha alcanzado cifras récord. Este repentino crecimiento en los requisitos de almacenamiento ha hecho que la virtualización del almacenamiento sea cada vez más importante.

La virtualización del almacenamiento puede ser entendida como el proceso de abstracción lógica del almacenamiento físico. Los recursos de almacenamiento físico (como las unidades de disco) se agregan en agrupaciones de almacenamiento, desde donde el almacenamiento lógico se crea y se presenta al entorno de aplicación. Esta se puede implementar dentro del almacenamiento de matrices en sí misma (virtualización basada en matrices) o bien en el nivel de red, donde múltiples matrices de discos o almacenamiento en red de sistemas de diferentes proveedores, dispersos por la red, se pueden agrupar en un único dispositivo de almacenamiento monolítico. Esto permite que las matrices múltiples se administren de manera uniforme como si

si se tratase de un solo grupo.

La virtualización basada en matrices ofrece más flexibilidad, simplifica la gestión y mejora el rendimiento y la utilización de la capacidad en comparación con las matrices de discos tradicionales.

Hay dos tipos principales de sistemas de almacenamiento en red con virtualización de almacenamiento: los sistemas *Network Attached Storage* (en siglas, NAS) y *Storage Area Network* (en siglas, SAN). Estos sistemas de almacenamiento compartido (SAN y NAS) permiten aprovechar las capacidades avanzadas de virtualización del servidor como la migración de máquinas virtuales en vivo, la alta disponibilidad, la tolerancia a fallos y la recuperación ante siniestros.

Almacenamiento conectado a la red (NAS)

El almacenamiento conectado a la red, o NAS, es un **dispositivo de almacenamiento que se encuentra en la propia red y ofrece almacenamiento a los servidores en la red.** Permite que múltiples clientes, como usuarios de PC y servidores, compartan archivos a través de una red de área local (en siglas, LAN). NAS utiliza archivos basados en protocolos como *Network File System* (en siglas, NFS), S*erver Message Block* (en siglas, SMB) o *Common Internet File System* (en siglas, CIFS), donde el almacenamiento es remoto y las ordenadoras solicitan un archivo en lugar de un bloque de disco. El hecho de tener todos los archivos movidos a una única ubicación central hace que se simplifique la administración de estos. Es decir que, en lugar de tener que hacer un seguimiento de todos los archivos repartidos entre docenas, cientos, o incluso miles de máquinas, todos los datos se encuentran en un lugar, lo que permite realizar una mejor copia de seguridad, archivado, etc. Una de las ventajas más acusadas del NAS es que está basado en *Internet Protocol* (en siglas, IP) y es fácil de usar, desplegar y gestionar. Los usos más comunes incluyen archivos de rápido almacenamiento para *rich media,* documentos y archivos de *back-up* y correo electrónico.

Redes de área de almacenamiento (SAN)

Una red de área de almacenamiento, o SAN, es un **dispositivo de almacenamiento (como una matriz de discos o una biblioteca de cintas) accesible a los servidores para que los dispositivos puedan permanecer localmente conectados al sistema operativo.** La SAN, normalmente, tiene su propia red de dispositivos de almacenamiento a los que usualmente no se puede acceder a través de una red ordinaria de dispositivos. Una SAN sola no proporciona la abstracción del «archivo» como en el caso de NAS, sino que solo provee operaciones a nivel de bloque.

La mayoría de las SAN usan la conectividad del canal de fibra, del inglés *Fibre Channel Connectivity* (en siglas, FC), una tecnología de red especialmente diseñada para gestionar comunicaciones de almacenamiento, o Internet SCSI (en siglas, iSCSI), que es un estándar de red basado en IP para vincular dispositivos de almacenamiento.

Las empresas utilizan almacenamiento este tipo de almacenamiento para centralizar la gestión de los datos corporativos. Los usos comunes de una SAN incluyen el aprovisionamiento de datos de acceso transaccional que requieren acceso a nivel de bloque de alta velocidad a los discos duros de almacenamiento, tales como servidores de correo electrónico, bases de datos y servidores de archivos de acusado uso.

Virtualización de E/S

La virtualización de servidores involucra a máquinas que funcionan en un servidor físico, lo que hace posible la ejecución de múltiples máquinas virtuales en un único sistema físico. **La virtualización del almacenamiento permite que los datos se transfieran a un almacenamiento centralizado y compartido, lo que permite que se gestione de manera eficiente y rentable.** Sin embargo, obtener datos de la máquina requiere pasar por *endpoints* de red y almacenamiento en el servidor, lo que puede traer aparejado otro conjunto de problemas.

¿De qué sirve tener máquinas virtuales y almacenamiento (que se pueda virtualizar y migrar, según sea necesario) cuando los dispositivos físicos de *endpoint* de entrada y salida (en adelante, E/S) que residen en el servidor son no son ágiles? La administración manual de un recurso clave en un entorno virtualizado significa que la eficiencia está reñida con la capacidad que tenga esa organización de TI para administrar manualmente estos dispositivos de E/S.

Virtualización de red

Si todo lo demás está virtualizado, está claro que la red también debe volverse más ágil y debe ser susceptible de ser administrada como un recurso virtual, en lugar de requerir actividad manual para responder a las cargas de trabajo o a las condiciones cambiantes de negocio. Como es de esperar, **la virtualización también se ha trasladado a la red y, en lugar de realizar cambios en la red moviendo cables entre diferentes recursos físicos, la tecnología de virtualización se aplica a la red en sí misma.**

La virtualización de red permite que la red se configure sobre la marcha, sin necesidad de tocar ni un solo cable o dispositivo. Por tanto, los dispositivos de red con capacidad de virtualización se administran de forma remota y se pueden reconfigurar lógicamente.

Esta capacidad de realizar modificaciones en la red de forma remota (y lógica) completa la virtualización del centro de datos. Cada tipo de recurso, desde el servidor hasta el almacenamiento y todo lo demás, ya no está físicamente vinculado a piezas específicas de hardware. Por el contrario, cada tipo de recurso puede ser abordado lógicamente y reconfigurado sin necesidad de configurarlo físicamente.

Virtualización de clientes

La virtualización no resuelve todos los problemas de las organizaciones de TI. Actualmente, se utilizan una gran cantidad de dispositivos cliente en las organizaciones. En muchas empresas, casi todos los empleados tienen su propia PC (ya sea un dispositivo de escritorio o un ordenador portátil), además de teléfonos inteligentes y blocs de notas.

Mantener todos esos dispositivos actualizados con parches en el sistema operativo, actualizaciones de aplicaciones, antivirus y *spyware,* etc., es una tarea prácticamente interminable. Se hace aún más difícil por el hecho de que estas máquinas están localizadas con el usuario, en oficinas y hasta en lugares de trabajo temporal como Starbucks. Hacer un seguimiento de los dispositivos y garantizar que estén seguros ha impulsado el movimiento hacia la virtualización de clientes.

Virtualización de aplicaciones

**La virtualización de aplicaciones es una separación de la ejecución del programa y de la visualización de este.** En otras palabras, un programa como Microsoft Word se ejecuta en un servidor ubicado en el centro de datos, pero la salida gráfica se envía a un dispositivo cliente remoto. El usuario final ve la pantalla gráfica completa del programa y puede interactuar con él a través del teclado y el ratón.

Una variante de la virtualización de aplicaciones es aquella en la que la aplicación no se ejecuta en un servidor en el centro de datos, sino en el dispositivo del cliente. La diferencia con el modo tradicional de uso de la aplicación radica en la forma en la que se administra la aplicación: en lugar de instalarse permanentemente en el dispositivo del cliente, se envía (en modo *streaming* o transmisión) al dispositivo del cliente cada vez que se ejecuta. Este modo de «instalación en cada uso» puede parecer repetitivo, pero permite que una organización de TI controle mejor la aplicación, para garantizar que se mantenga actualizada con versiones, parches y todo lo demás.

Virtualización de escritorio

A diferencia de la virtualización de aplicaciones, donde una o más aplicaciones se muestran o se transmiten desde un servidor central, **en la virtualización de escritorio el ordenador del usuario se ejecuta en un servidor central, con la salida gráfica de la pantalla a un dispositivo cliente.** Este tipo de virtualización se conoce como VDI (sigla del inglés, *Virtual Desktop Infrastructure*) que significa infraestructura de escritorio virtual. La ventaja de este enfoque es que es más fácil mantener actualizados los sistemas del cliente con parches, etc. Esto se debe a que, en lugar de administrar sistemas individuales que se encuentran por aquí y por allá, los equipos de TI pueden administrarlos en una ubicación centralizada.

En los últimos años, la virtualización de escritorios ha evolucionado con creces. En lugar de tener que almacenar una imagen de escritorio para cada usuario, usa una sola imagen que se clona según sea necesario. Supongamos que para 4000 usuarios se necesitan 4000 imágenes de disco, por lo que podemos deducir que haría falta una gran capacidad de almacenamiento, a pesar de que gran parte de cada imagen es idéntica a la otra. Por tanto, deducimos que esta eficiente clonación reduce enormemente la necesidad de almacenamiento y hace que la virtualización de escritorio sea muy atractiva desde un punto de vista «económico».

Pues bien... podríamos preguntarnos qué sucede con nuestra aplicación favorita que ejecutamos a diario en nuestro ordenador. ¿Desaparecería con la virtualización de escritorio? La respuesta es no. **Los datos y configuraciones se pueden guardar por separado y se aplican a la imagen clonada, para garantizar que cada usuario tenga sus aplicaciones y datos listos para cuando abra su escritorio.**

La virtualización de escritorio, a menudo, utiliza un dispositivo cliente económico para la visualización e interacción con el usuario final. Estos «clientes ligeros», como se les suele llamar, pueden ser dispositivos baratos con poca potencia, desde un punto de vista informático, y sin almacenamiento en disco local. Esto puede reducir significativamente el coste por dispositivo de usuario final: el hardware es menos costoso, pero generalmente usan menos energía, ocupan menos espacio y requieren menos soporte.

*Streaming* de escritorio

Una variante de la virtualización de escritorio es el *check-in,* *check-out* (entrada y salida) cliente. De esta forma, el almacenamiento continuo del sistema cliente está centralizado, pero cuando el usuario final está listo para comenzar a trabajar, el sistema del cliente se transfiere al dispositivo cliente y se utiliza como un ordenador tradicional. **Cuando finaliza la sesión, el usuario apaga el sistema y la imagen del ordenador se escribe en el repositorio central y no queda nada en el hardware del usuario.**

Esta forma de entrada y salida de virtualización cliente está comenzando a explorarse, pero es muy prometedora para los entornos donde la disponibilidad de conectividad de red de alta velocidad es incierta. Por ejemplo, cuando alguien trabaja de forma remota desde casa, puede que no esté claro si su conexión es lo suficientemente sólida como para permitir la virtualización de aplicaciones o la virtualización de escritorio tradicional. En estos casos, una única descarga del escritorio a un dispositivo cliente puede ser una buena opción.

La virtualización ha dado paso a las tecnologías basadas en la nube, posteriormente a los contenedores y, en los últimos años, el concepto *serverless* se ha instaurado como una nueva forma de construir aplicaciones de forma más eficiente, económica y efectiva. Ingresa al vídeo *¿Qué es Serverless?* para desarrollar más este concepto.

![](data:image/png;base64...)

4.6. Referencias bibliográficas

Projekt Cloud Computing. (s.f.). *Two types of hypervisors.* [https://oze.pwr.edu.pl//kursy/introcloud/content/start/K-04-03.html](https://oze.pwr.edu.pl/kursy/introcloud/content/start/K-04-03.html)

Hewlett Packard Enterprise. (s.f.). *Introducción a la virtualización de HP.* <https://www.hpe.com/>

A fondo

***Instalar y Configurar ESXi 6.7, 6.5 y 6 (VMwahre vSphere)***

TKapacito TIC. (2018, septiembre 24). *Instalar y Configurar ESXi 6.7, 6.5 y 6 (VMware vSphere)* [Vídeo]. YouTube. <https://www.youtube.com/watch?v=WARIBT97Z0w>

Este vídeo ayuda a instalar una solución de virtualización de VMware, que puede utilizarse para profundizar en los conocimientos prácticos de virtualización.

Test

1. Selecciona la afirmación que mejor se corresponde con la definición de virtualización de almacenamiento.

A. Es el proceso de abstracción lógica del almacenamiento físico.

B. Son los ficheros de las máquinas virtuales.

C. A y B son correctas.

D. Ninguna es correcta.

1. Selecciona la afirmación que mejor se corresponde con definición de virtualización de escritorio.

A. Es la posibilidad de tener sistemas de virtualización en un PC de escritorio.

B. Es el proceso de convertir los PC de escritorio en máquinas virtuales.

C. A y B son correctas.

D. Ninguna es correcta.

1. Selecciona la afirmación que mejor se corresponde con virtualización del sistema operativo.

A. Este tipo de virtualización se corresponde a lo que hoy en día llamamos contenedores (*containers*).

B. Es la virtualización de máquinas virtuales.

C. A y B son correctas.

D. Ninguna es correcta.

1. Selecciona la afirmación que mejor se corresponde con la definición de «paravirtualización».

A. Se llama así a la virtualización implementada sobre una segunda capa de virtualización.

B. Se llama así a la virtualización anidada.

C. La paravirtualización no intenta emular un entorno de hardware en software.

D. Ninguna es correcta.

1. Selecciona la afirmación que mejor se corresponde con la virtualización de red.

A. Es el proceso de abstracción lógica de la capa de red.

B. Es el servicio que facilita la transferencia de máquinas virtuales por la red.

C. A y B son correctas.

D. Ninguna es correcta.

1. Selecciona la afirmación que mejor se corresponde con la virtualización de aplicaciones.

A. Son máquinas virtuales especializadas en la ejecución de aplicaciones.

B. Es una separación de la ejecución del programa y de la visualización de este.

C. A y B son correctas.

D. Ninguna es correcta.

1. Selecciona la afirmación que mejor se corresponde con la definición de hipervisor de tipo 1.

A. Son los hipervisores que funcionan sobre un sistema operativo.

B. Son el tipo de hipervisor más antiguo.

C. Ninguna es correcta.

D. Son los hipervisores que pueden ejecutarse directamente sobre el hardware sin la necesidad de un sistema operativo.

1. Selecciona la afirmación que mejor se corresponde con la descripción de VirtualBox.

A. Es un software de virtualización propiedad de Oracle.

B. Es un software de virtualización de aplicaciones.

C. Es un hipervisor de tipo 2.

D. A y C son verdaderas.

1. Selecciona la afirmación que mejor se corresponde con la definición de *streaming* de escritorio.

A. Es proceso de capturar la entrada y salida de un escritorio (virtual o físico).

B. Utilizar servicios de *streaming* desde el escritorio.

C. A y B son correctas.

D. Ninguna es correcta.

1. Selecciona la afirmación que mejor se corresponde con la descripción de KVM.

A. Es el *Keyboard Virtual Module* que permite el uso de teclados en máquinas virtuales.

B. Es el sistema de virtualización incorporado en la mayoría de los sistemas Linux.

C. Es un producto de virtualización de VMware.

D. Ninguna es correcta.
Tema 6

Administración de servidores Windows

Administración de Sistemas en la Cloud

Índice

[Esquema 3](#_Toc81218683)

[Ideas clave 4](#_Toc81218684)

[6.1. Introducción y objetivos 4](#_Toc81218685)

[6.2. Ediciones de Windows 4](#_Toc81218686)

[6.3. Acceso remoto 8](#_Toc81218687)

[6.4. Directorio Activo 14](#_Toc81218688)

[6.5. Creación de un dominio 20](#_Toc81218689)

[6.6. Referencias bibliográficas 27](#_Toc81218690)

[A fondo 30](#_Toc81218691)

[Test 31](#_Toc81218692)

Esquema

![Interfaz de usuario gráfica, Texto, Aplicación  Descripción generada automáticamente](data:image/jpeg;base64...)

Ideas clave

6.1. Introducción y objetivos

Este tema presentará algunos de los conceptos básicos de la administración de sistemas Windows: sistemas de archivos, usuarios, grupos, etc. Es probable que cualquier instalación de *software* requiera de modificaciones y tareas sobre estos objetos.

Los **objetivos** que se pretenden conseguir son:

* Conocer los fundamentos de los conceptos básicos de Windows que aparecen de manera recurrente en muchas tareas administrativas.
* Aprender a manipular los objetos del sistema operativo para automatizar tareas sobre los mismos.

A continuación, en el vídeo *Instalación de Windows Server*, se ofrece una guía paso a paso para instalar una máquina con Windows Server y para conectarse remotamente por RDP, Server Manager consola MMC y PowerShell.

![](data:image/jpeg;base64...)

6.2. Ediciones de Windows

El ecosistema Windows no es tan extenso como el de las distribuciones de Linux, pero también puede dar lugar a confusión. Este tema se centrará en **Windows Server,** la versión de sistema operativo dedicada a servidores. No se tratará, por tanto, ninguna edición de escritorio.

Dentro de la oferta de Windows Server, Microsoft publica versiones de actualización a menudo. De manera similar a otros sistemas operativos, estas versiones son soportadas durante unos pocos años. Es decir, Microsoft publicará parches de funcionalidad y seguridad durante el periodo de soporte, además de ofrecer asistencia técnica a sus clientes. Por ejemplo, el [ciclo de soporte](https://docs.microsoft.com/es-es/lifecycle/products/?alpha=windows%20server%202016) de Windows Server 2019 empezó el 15/10/2019 y terminará el 12/1/2027. Este tema se centrará en Windows Server 2019, la versión más reciente, salvo cuando se indique lo contrario.

Windows Server 2019 está disponible en dos **ediciones**, también conocidas como SKU: Standard y Datacenter. Las ediciones se [diferencian](https://docs.microsoft.com/en-gb/windows-server/get-started-19/editions-comparison-19) por su precio y las funcionalidades que soportan. La edición **Datacenter** está enfocada principalmente a entornos de virtualización y puede alojar un número ilimitado de máquinas virtuales (siempre que el servidor sea capaz de servir los requisitos de *hardware* virtual), mientras que la edición **Standard** solo puede ejecutar dos máquinas.

Además de algunas diferencias específicas de Hyper-V (el hipervisor de virtualización de Windows), Datacenter soporta *software defined networking* ([SDN](https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking), redes definidas por *software*), una funcionalidad esencial de cualquier entorno de nube privada o pública. Es habitual que Microsoft distribuya las ediciones en una misma imagen ISO, por lo que la elección de edición puede hacerse durante la instalación (ver Figura 1).

Ambas ediciones soportan, además, varios modos de ejecución:

* Escritorio o Server with Desktop Experience.
* Server Core.
* Nano Server.

El modo de escritorio es el más familiar, ya que convierte al servidor en un *host* similar a cualquier máquina Windows: tiene botón de inicio, ventanas y consolas de configuración. El modo Core, sin embargo, no tiene escritorio. Mantiene las funcionalidades para soportar aplicaciones tradicionales y permite la activación de cualquier rol, pero no tiene el entorno de escritorio tradicional. Está pensando para ser administrado remotamente a través de la línea de comandos, con PowerShell o con consolas MMC remotas.

Hay otras diferencias, como que Server Core no incluye las herramientas de accesibilidad, soporte de audio o Internet Explorer. La Tabla 1 lista algunas de las diferencias en cuanto a disponibilidad de aplicaciones entre ambos modos.

![Tabla  Descripción generada automáticamente](data:image/jpeg;base64...)

Tabla 1. [Diferencias](https://docs.microsoft.com/en-us/windows-server/administration/server-core/what-is-server-core) entre Server Core y Server with Desktop Experience. Fuente: elaboración propia.

Tanto el modo Core como el modo de escritorio se seleccionan durante la instalación del sistema (ver Figura 1). La consola del modo Core sí tiene, no obstante, ventanas. Por ejemplo, el administrador de tareas está disponible y tiene una interfaz gráfica, tal como muestra la Figura 2. Microsoft ha incluido un menú rápido en modo texto para la configuración inicial, sconfig.cmd. La sección A fondo incluye documentación en profundidad sobre otras herramientas de configuración de Server Core.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 1. Elección de edición y modo en Windows Server 2019. Fuente: elaboración propia.

![Interfaz de usuario gráfica, Aplicación  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 2. Interfaz del modo Server Core. Fuente: elaboración propia.

El tercer modo de ejecución mencionado anteriormente, **Nano Server,** no es un modo de instalación y, de hecho, no es posible instalarlo sobre *hardware* físico o virtual. Esta opción era posible con Windows Server [2016](Esta%20opci%C3%B3n%20era%20posible%20con%20Windows%20Server%202016%20%28https%3A/docs.microsoft.com/en-gb/windows-server/get-started/getting-started-with-nano-server%29%2C%20pero%20no%20lo%20es%20con%20Windows%20Server%202019%20%28https%3A/docs.microsoft.com/en-us/windows-server/get-started/nano-in-semi-annual-channel%29.), pero no lo es con Windows Server [2019](https://docs.microsoft.com/en-us/windows-server/get-started/nano-in-semi-annual-channel). Nano Server solo está disponible para ser ejecutado como un contenedor y, por tanto, Microsoft no ofrece un disco de instalación, sino una [imagen](https://hub.docker.com/_/microsoft-windows-nanoserver?tab=description) base de contenedor. Nano Server es aún más limitado que Server Core, pero, al ser más ligero, está más indicado para entornos de virtualización.

6.3. Acceso remoto

Uno de los primeros pasos para administrar un servidor Windows, al igual que un servidor Linux, es poder acceder al mismo remotamente. Los siguientes apartados explicarán algunas de las principales [herramientas de administración remota](https://docs.microsoft.com/en-us/windows-server/administration/server-core/server-core-manage#managing-with-microsoft-management-console):

* Escritorio remoto o RDP.
* PowerShell.
* Server Manager.
* Consola remota MMC.
* Remote Server Administration Tools o RSAT.
* Otros.

Escritorio remoto

Remote Desktop Protocol (RDP) es un protocolo propietario, desarrollado por Microsoft, que proporciona al usuario una interfaz gráfica para conectarse a otro ordenador a **través de una conexión de red.** El usuario necesita un cliente RDP mientras que el otro equipo debe tener habilitada la funcionalidad de acceso remoto. Esta se puede habilitar a través del panel de control (ver Figura 3) o con el comando sconfig.cmd en Server Core. RDP funciona sobre el puerto TCP 3389.

![Interfaz de usuario gráfica, Texto, Aplicación, Correo electrónico  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 3. Funcionalidad de acceso remoto en Windows Server. Fuente: elaboración propia.

Server Core soporta RDP, aunque no tenga escritorio como tal. Tal como se comentó en el apartado anterior, Server Core no es una consola de texto, sino que tiene un entorno de ventanas. Una vez habilitado, una conexión de RDP es idéntica a una conexión a la consola virtual de una máquina virtual o a una pantalla física (ver Figura 4). Nano Server, sin embargo, no soporta RDP.

![](data:image/png;base64...)

Figura 4. Conexión por RDP a un servidor Windows 2019 Server Core con el cliente RDP en MacOS. Fuente: elaboración propia.

PowerShell

La **consola nativa de Windows,** PowerShell, permite ejecutar comandos al iniciar sesiones de consola en *hosts* remotos. Está disponible tanto en el servidor con escritorio como en Server Core y puede habilitarse en Nano Server si se instala PowerShell Core. Este apartado se limitará a la configuración para la ejecución remota.

Es necesario habilitar la invocación remota en el *host* de destino con Enable-PSRemoting -Force. A partir de ese momento, el *host* aceptará llamadas de PowerShell de otros equipos del dominio. Por ejemplo, el siguiente comando devolverá el contenido de la unidad C:

Invoke-Command -ComputerName 192.168.1.130 -ScriptBlock { Get-ChildItem C:\ } -credential USERNAME

Se podría iniciar una sesión remota con Enter-PSSession y ejecutar los comandos de forma interactiva. Por ejemplo, la Figura 5 muestra un inicio de sesión remota entre dos equipos que forman parte del mismo dominio.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 5. Sesión remota con PowerShell. Fuente: elaboración propia.

Server Manager

La herramienta de Administración de Servidor, o Server Manager, ofrece una interfaz gráfica para **ejecutar tareas de configuración,** tanto en el equipo local como en equipos remotos. Ofrece acceso a consolas de administración de roles de Windows, como DNS o Directorio Activo, desde un único punto, instalación de roles, escritorio remoto, etc. La Figura 6 muestra una instancia de Server Manager con dos equipos y las opciones que ofrece para administración remota. Server Manager permite administrar tanto servidores con escritorio como Server Core y Nano Server.

![A screenshot of a social media post  Description automatically generated](data:image/png;base64...)

Figura 6. Server Manager con dos equipos. Fuente: elaboración propia.

Consola remota MMC

La consola tradicional de administración de Windows, MMC (Microsoft Management Console), es otra herramienta gráfica de configuración. Mientras que Server Manager es una herramienta centralizada, MMC ofrece múltiples *snapins* para cada funcionalidad y solo permite administrar un equipo con cada *snapin*. De hecho, parte de la funcionalidad de Server Manager es abrir la consola MMC con el *snapin* correcto en un equipo concreto, ahorrando tiempo al administrador. MMC soporta servidores con escritorio, Server Core y Nano Server.

La Figura 7 muestra dos consolas MMC, una con el *snapin* de DNS conectada al equipo local y otra con el *snapin* de administración de discos conectada a un equipo remoto.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 7. Consola MMC con los *snapins* de DNS y Disk Management. Fuente: elaboración propia.

*Remote server administration tools*

[RSAT](https://docs.microsoft.com/en-us/windows-server/remote/remote-server-administration-tools) no es más que una colección de herramientas de administración remotas, listas para ser instaladas en un equipo Windows cliente (por ejemplo, Windows 10) con un único paquete. Incluye Server Manager, la consola MMC con múltiples *snapins* y *commandlets* de PowerShell que solo las versiones de Windows Server incorporan por defecto.

Otros

Al igual que en Linux, la oferta de sistemas de administración remota es muy amplia. Por ejemplo, hay versiones de VNC y TeamViewer disponibles para Windows. Microsoft incluyó [OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_overview) en Windows Server 2019 y en Windows 10, lo que añade otra herramienta al arsenal.

6.4. Directorio Activo

Directorio Activo, o AD (Active Directory), es un servicio de directorio para redes de equipos Windows. Cualquier versión de Windows Server puede actuar como controlador de dominio, desde Windows Server 2000. AD se usa para **tareas de administración centralizada,** aparte de integrar otras funcionalidades, como servicios de certificados.

Un controlador de dominio es un servidor Windows que ejecuta el servicio Active Directory Domain Service. **Autentica y autoriza** todos los usuarios y equipos de un dominio y les aplica políticas de seguridad. Por ejemplo, cuando un usuario inicia sesión en un ordenador que es parte de un dominio Windows, un controlador de dominio, y no el equipo local, comprueba que la contraseña sea válida.

A nivel de protocolos, AD se sirve de múltiples tecnologías:

* DNS para localizar servicios (gracias a entradas SRV) y para identificar tanto dominios como los equipos miembros del dominio.
* LDAP es el servicio de directorio como tal. Sirve de base de datos para alojar información de las cuentas de máquinas y de usuario. Es extensible, por lo que sistemas como Exchange pueden alojar datos adicionales de cada usuario, como los datos de la cuenta de correo, sin necesidad de crear otro repositorio de datos.
* Kerberos es el sistema de autenticación y autorización entre equipos.

AD funciona esencialmente como una base de datos administrativa. Usa una estructura jerárquica formada por objetos, dominio, árboles y bosques (DNS Stuff, 2019).

Objetos

Los objetos son los **elementos básicos del dominio.** Representan los ordenadores cliente (por ejemplo, los equipos ofimáticos de escritorio, que actúan como clientes de AD), los servidores de aplicaciones (que, a efectos del directorio, son también clientes de AD), carpetas compartidas y cuentas de usuario. Cada objeto tiene un identificador único y un conjunto de atributos. Por ejemplo, la Figura 8 muestra algunos de los campos básico de una cuenta de usuario, aunque en el resto de las pestañas hay muchos más.

Los objetos se pueden organizar en objetos **contenedores,** como **carpetas** y **unidades organizativas,** o OU. Las carpetas son similares a las de un sistema de ficheros, pero las unidades organizativas permiten, además, aplicar políticas de seguridad a los objetos de la OU y delegar la administración a otros usuarios.

![Interfaz de usuario gráfica  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 8. Propiedades de usuario de AD. Fuente: elaboración propia.

Dominios

Un dominio es un área de la red con una única base de datos de autenticación. A efectos prácticos, sirve para establecer límites administrativos entre diferentes grupos de red. Cualquier objeto pertenece a un único dominio y los objetos de un mismo dominio pueden estar dispersos en diferentes ubicaciones físicas. Por ejemplo, una organización puede establecer un dominio para cada departamento, pero en una misma oficina pueden convivir usuarios y equipos de departamentos diferentes sin que eso rompa la estructura del dominio.

Cada dominio tendrá al menos un **controlador de dominio,** o DC, que actúa como autoridad de aquel; es decir, es responsable de los permisos de los objetos, la autenticación y las modificaciones de objetos. Es habitual que un dominio disponga de más de un DC. Esta disposición es posible porque los DC pueden trabajar de manera distribuida y es necesaria porque la caída del único DC de un dominio colapsaría todas las máquinas del dominio, ya que nadie podría iniciar sesión ni acceder a carpetas compartidas. Los controladores de dominio suelen alojar el servicio DNS, que también puede funcionar en modo distribuido.

Cada dominio tiene una estructura de **árbol de contenedores.** Estos contenedores pueden ser carpetas normales o unidades organizativas. La Figura 9 muestra el árbol de carpetas de un dominio y el contenido de una de las carpetas.

![Interfaz de usuario gráfica, Texto, Aplicación, Correo electrónico  Descripción generada automáticamente](data:image/jpeg;base64...)

Figura 9. Estructura de árbol del dominio demo.loc. Fuente: elaboración propia.

Los dominios se identifican con un nombre DNS. De hecho, la creación de un dominio requiere la presencia de un servicio DNS asociado, bien externo o integrado en el propio dominio. Al ser un nombre DNS, las cuentas de máquina reciben un **nombre de dominio completo** (o FQDN, *fully qualified domain name*) en el que se une el nombre del *host* con el nombre del dominio.

Un equipo con nombre member en el dominio demo.loc tendrá un registro DNS member.demo.loc. La integración de AD con DNS es tan fuerte que los dominios siguen una estructura de árbol, de manera que un dominio padre puede ser demo.loc y un dominio hijo podría ser, a su vez, child.demo.loc. Cada dominio formará un **límite administrativo,** pero habrá ciertas interacciones permitidas entre ellos. Los dominios AD puede tener el nombre de dominio de Internet de una empresa, ya que es un nombre DNS válido, pero no es estrictamente necesario.

Bosques

Las empresas con cientos o miles de usuarios pueden disponer de varios árboles de directorios. Los administradores podrán organizar los árboles en bosques. Los bosques son el límite administrativo y de seguridad más amplio en una estructura AD.

Una organización puede decidir tener no ya varios dominios, sino varios bosques. Esta situación es habitual, por ejemplo, cuando hay uniones y adquisiciones de organizaciones. En estos casos, es posible conectar los bosques con una **relación de confianza.** Estas relaciones extienden la accesibilidad de los recursos de los dominios, de manera que centraliza la administración a nivel lógico.

Sitios

Los sitios de AD sirven para administrar organizaciones que tienen sucursales en diferentes ubicaciones geográficas, pero que caen bajo el mismo dominio. Los sitios son agrupaciones físicas de subredes IP bien conectadas, que se utilizan para replicar de manera eficiente la información entre los controladores de dominio (DC). Permiten ejercer control sobre el tráfico de replicación y el proceso de autenticación. Cuando hay DC disponibles en un sitio dado, los servicios de los equipos miembro pueden dirigir a estos las consultas de inicio de sesión y las búsquedas en el directorio. Los sitios también sirven para desplegar directivas de grupo específicas a nivel geográfico (las OU aplican las directivas a nivel lógico o departamental).

Sincronización de AD

Los objetos de un dominio se mantienen en una base de datos replicada y distribuida. Cada controlador de dominio contiene una copia de todos los objetos del dominio y puede servir prácticamente para todas las operaciones de AD. Hay ciertos roles que solo pueden estar asignados a un único DC en cada dominio. Si el DC con uno de esos roles, denominado *operation master*, deja de esta disponible, las tareas de ese rol no se pueden ejecutar. Estas tareas no son tan habituales como un inicio de sesión o un cambio de contraseña, por lo que admiten cierto *downtime,* sin impactar negativamente en el funcionamiento del dominio.

Cualquier cambio en un objeto realizado en un controlador de dominio se transferirá automáticamente a las réplicas en los otros DC. Como la topología de dominios es independiente de la topología de red, es habitual que los DC de un dominio estén distribuidos geográficamente para proporcionar una mejor resiliencia.

Niveles funcionales

Todas las versiones de Windows Server usan un concepto llamado **nivel funcional de bosque y de dominio** (Panek, 2018). El nivel funcional se escoge en el momento de la creación y determina las funcionalidades disponibles. En una instalación de cero, es habitual escoger el nivel más alto, pero en el momento en que hay controladores de dominio de diversas versiones de Windows Server (una situación muy habitual, especialmente en situaciones de actualización a una versión reciente), la respuesta no es tan sencilla.

Windows Server 2019 no añade ningún [nivel funcional](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-functional-levels) nuevo, sino que mantiene los niveles de Windows Server 2016. Este nivel funcional añade funcionalidades, como el soporte de NTLM para usuarios restringidos a dispositivos específicos del dominio, pero tiene la limitación de que todos los controladores del dominio deben ser Windows Server 2016 o Windows Server 2019. Es habitual tener un dominio en un nivel funcional dado (Windows Server 2012, por ejemplo) con todos los DC en una versión dada (Windows Server 2012 R2, por ejemplo) y que, durante un proceso de actualización, se sustituyan los DC por otros nuevos con Windows Server 2019. Una vez todos los DC antiguos han sido sustituidos, el administrador puede elevar el nivel funcional y hacer uso de las nuevas funcionalidades.

6.5. Creación de un dominio

Un servidor Windows Server se convierte en controlador de dominio mediante la activación del rol **Active Directory Domain Services**. Este apartado ejemplifica cómo activar este rol en un equipo recién instalado y cómo crear el primer dominio en un bosque nuevo.

* El primer paso es configurar la tarjeta de red del servidor que se convertirá en controlador del dominio. La instalación de AD es muy dependiente del despliegue de DNS subyacente, por lo que el servidor suele tener una IP estática (ver Figura 10). No es un requisito del proceso de instalación, pero es muy habitual en instalaciones empresariales. El servidor DNS de la subred se configura de manera estática, también, pero es habitual, una vez creado el dominio, configurar la propia IP del equipo como servidor DNS, ya que el servicio DNS de AD se encargará de resolver nombres tanto del dominio de AD como de dominios externos.
* También conviene fijar el nombre de la máquina antes de promocionarla a controlador de dominio. En este ejemplo, el *hostname* será dc1.

![A screenshot of a social media post  Description automatically generated](data:image/png;base64...)

Figura 10. Tarjeta de red con IP estática. Fuente: elaboración propia.

* El siguiente paso consiste en añadir el rol de Active Directory Domain Services. Esto se puede llevar a cabo desde el Server Manager, en Add roles and features. Tras seleccionar el equipo local, hay que marcar el rol Active Directory Domain Services y aceptar la instalación de herramientas adicionales, como el la Figura 11. En el resto de los pasos de la instalación, se pueden aceptar los valores por defecto, ya que la configuración del dominio se lleva a cabo en un cuadro de diálogo diferente, tras la instalación.

![A screenshot of a social media post  Description automatically generated](data:image/png;base64...)

Figura 11. Selección de rol Active Directory Domain Services. Fuente: elaboración propia.

* Una vez terminada la instalación del rol, Server Manager muestra una opción para promocionar el servidor a controlador de dominio. En versiones anteriores, este proceso se arranca con el comando dcpromo, pero ya no está disponible en Windows Server 2019.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 12. Mensaje de promoción a controlador de dominio. Fuente: elaboración propia.

* La primera página del diálogo de promoción es dónde promocionar el DC: en un dominio existente, en un dominio nuevo en bosque existente o en un nuevo dominio en un nuevo bosque. En la primera opción, solo hay que seleccionar el dominio en el que ubicar el DC. En la segunda, hay que indicar el dominio padre, si el dominio pertenecerá a un árbol existente, o simplemente el nombre del bosque, si el nuevo dominio será la raíz de un árbol nuevo. En la última opción, la que se seguirá en este ejemplo, es necesario indicar el nombre del bosque y el nombre del dominio, que será el dominio raíz en el primer árbol (ver Figura 13).

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 13. Controlador de dominio en un nuevo bosque. Fuente: elaboración propia.

* A continuación, se seleccionan los niveles funcionales del dominio y del bosque. Este ejemplo despliega un dominio de cero, así que es seguro escoger el nivel más alto, pero, en un entorno con versiones antiguas de DC, habría que revisar las matrices de compatibilidad (ver Figura 14).
* El diálogo ofrece varios servicios disponibles para el controlador de dominio:
  + DNS. Es habitual, pero no estrictamente necesario, que un DC sea un servidor DNS. Con un servicio DNS integrado, la gestión de nombres se simplifica, ya que cualquier equipo unido al dominio será dado de alta en la zona DNS automáticamente.
  + Catálogo Global. El servicio de GC acelera las búsquedas de recursos en AD, gracias a que el equipo almacena toda la información del esquema y un subconjunto de los atributos de los objetos de todos los dominios del bosque (Panek, 2018). Cada dominio debe tener al menos uno, pero suele haber más.
  + Controlador de dominio de solo lectura (RODC). Estos DC suelen desplegarse en oficinas remotas con baja seguridad, donde es necesario desplegar un DC para acelerar los inicios de sesión, pero existe riesgo de que un ataque altere los datos del DC.

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 14. Niveles funcionales y servicios adicionales. Fuente: elaboración propia.

* Los siguientes pasos solicitan detalles sobre la configuración DNS (si el DC va a actuar como tal) y del dominio NetBIOS. Los nombres NetBIOS son herencia de las versiones más antiguas de Windows Server (concretamente, de Windows NT), que Microsoft sigue manteniendo por compatibilidad. También es posible cambiar las rutas por defecto de la ubicación de la base de datos de AD. En este caso, no es necesario cambiar estas opciones.
* El diálogo de instalación termina comprobando que todas las opciones son válidas. Si todo va bien, el proceso termina cerrando la sesión del usuario. Un controlador de dominio no tiene cuentas locales, ya que solo es posible iniciar sesión con cuentas de dominio (en un equipo miembro es posible iniciar sesión tanto con cuentas locales como con cuentas de dominio).

![A picture containing drawing  Description automatically generated](data:image/png;base64...)

Figura 15. Fin de la promoción del servidor a controlador de dominio. Fuente: elaboración propia.

Tras el reinicio, el equipo ya actuará como DC del nuevo domino. Los equipos de la red podrán hacerle peticiones siempre que puedan localizarlo por DNS. La Figura 16 muestra algunos de los registros SRV del nuevo dominio. Estos registros no son utilizados para resolver nombres de equipo, sino para localizar servicios. Por ejemplo, la entrada \_ldap de la imagen indica que el equipo dc1.demo.loc ofrece el servicio LDAP en el dominio demo.loc. Cuando se solicita, por ejemplo, la unión de un equipo cliente a un dominio, Windows consultará estos registros para localizar el controlador de dominio al que dirigir las peticiones.

![A screenshot of a social media post  Description automatically generated](data:image/png;base64...)

Figura 16. Registros SRV de un Directorio Activo. Fuente: elaboración propia.

Unión de equipos al dominio

Mientras que promocionar controladores de dominio es una tarea relativamente poco frecuente, la **unión de equipos al dominio** ocurre a menudo: cada nuevo servidor Windows y cada nuevo equipo de cliente debe ser unido al dominio para facilitar los inicios de sesión, el control de políticas de seguridad, etc.

En un equipo con Server Core, por ejemplo, se puede usar el menú sconfig.cmd para unir el equipo al dominio. Una primera comprobación debe ser que el sistema pueda resolver correctamente el nombre del dominio (ver Figura 17).

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 17. Resolución del nombre del dominio con ping. Fuente: elaboración propia.

Una vez comprobado, el menú de sconfig solicita el nombre del dominio y las credenciales de un administrador (ver Figura 18).

![A screenshot of a cell phone  Description automatically generated](data:image/png;base64...)

Figura 18. Unión de Server Core a un dominio. Fuente: elaboración propia.

Tras un reinicio, el equipo será un servidor «miembro» del dominio, con todo lo que ello conlleva. Entre otras cosas, se habrá creado una cuenta de máquina en el directorio con el nombre del equipo, como muestra la Figura 19.

![A screenshot of a social media post  Description automatically generated](data:image/png;base64...)

Figura 19. Detalles de cuenta de máquina. Fuente: elaboración propia.

6.6. Referencias bibliográficas

DNS Stuff. (2019, diciembre 16). *Active Directory Forest and Domain Guide 2020 + Best Tools.* <https://www.dnsstuff.com/active-directory-forest>

Docker Hub. (s. f.). *Nano Server*. <https://hub.docker.com/_/microsoft-windows-nanoserver?tab=description>

Lynn, S. (2013). *Windows Server 2012: Up and Running*. O'Reilly Media Inc.

Microsoft. (2018, febrero 20). *What is the Server Core installation option in Windows Server?* <https://docs.microsoft.com/en-us/windows-server/administration/server-core/what-is-server-core>

Microsoft. (2018, agosto 9). *SDN in Windows Server overview.* <https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking>

Microsoft. (2019, enero 7). *OpenSSH in Windows*. <https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_overview>

Microsoft. (2019, mayo 5). *Install Nano Server*. <https://docs.microsoft.com/en-us/windows-server/get-started/nano-in-semi-annual-channel>

Microsoft. (2019, mayo 21). *Changes to Nano Server in Windows Server Semi-Annual Channel*. <https://docs.microsoft.com/en-us/windows-server/get-started/nano-in-semi-annual-channel>

Microsoft. (2019, julio 23). *Manage a Server Core server*.

<https://docs.microsoft.com/en-us/windows-server/administration/server-core/server-core-manage#managing-with-microsoft-management-console>

Microsoft. (2020, agosto 25). *Forest and Domain Functional Levels*.

<https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-functional-levels>

Microsoft. (2020, septiembre 9). *Remote Server Administration Tools*.

<https://docs.microsoft.com/en-us/windows-server/remote/remote-server-administration-tools>

Microsoft. (2020, octubre 12). *Comparison of Standard and Datacenter editions of Windows Server 2019*. <https://docs.microsoft.com/en-gb/windows-server/get-started-19/editions-comparison-19>

Microsoft. (s. f.). *Buscar información sobre el ciclo de vida de los productos y servicios*. <https://docs.microsoft.com/es-es/lifecycle/products/?alpha=windows%20server%202016>

Panek, W. (2018). *MCSA Windows Server 2016 Complete Study Guide*. Sybex.

A fondo

Tareas básicas en Server Core

Microsoft. (s. f.). *Administer a Server Core server*.

<https://docs.microsoft.com/en-us/windows-server/administration/server-core/server-core-administer>

Una instalación de Server Core puede parecer difícil de mantener, incluso para administradores experimentados en Windows. Esta guía incluye pistas para una configuración inicial: fijar una dirección IP, cambiar el nombre del *host,* unir a un dominio, crear un usuario, activar la licencia, etc. La mayoría de estas tareas ya se podían realizar en la línea de comandos antes de que Server Core estuviera disponible, con Windows Server 2008.

Introducción al Directorio Activo

Manage Engine. (2011, julio 22). *What is Active Directory?* [Vídeo]. YouTube.

<https://www.youtube.com/watch?v=qkN4bvqWqvo>

Este vídeo explica algunos de los conceptos del Directorio Activo presentados en este tema. Los diagramas son muy claros y pueden ser útil para aclarar los conceptos clave, como dominios, bosques, OU, etc.

Test

1. ¿Cuál es el nivel más amplio de límite administrativo en el Directorio Activo?

A. Bosque.

B. Dominio.

C. Unidad Organizativa (OU).

D. Árbol de dominios.

1. ¿Qué diferencia hay entre una carpeta contenedora y una unidad organizativa?

A. Ninguna, las carpetas se mantienen por compatibilidad con versiones antiguas de AD.

B. Las unidades organizativas permiten delegar la administración de los objetos contenidos en esta, mientras que las carpetas no lo permiten.

C. Las políticas de seguridad se pueden aplicar a una OU, pero no a una carpeta.

D. B y C son correctas.

1. ¿Qué modo de instalación de Windows Server 2019 no se puede instalar en un servidor físico?

A. Nano Server.

B. Server Core.

C. Windows Server with Desktop Experience.

D. Ninguno de los anteriores.

1. ¿Con qué modos de instalación se puede usar RDP?

A. Server Core.

B. Windows Server with Desktop Experience.

C. A y B son correctas.

D. Nano Server.

1. ¿Cuál de las siguientes herramientas se puede usar para administrar una instalación de Server Core?

A. RDP.

B. Server Manager.

C. PowerShell.

D. Todas las anteriores.

1. ¿Qué protocolo se integra con el Directorio Activo para la resolución de nombres de equipos, dominios y servicios?

A. LDAP.

B. DNS.

C. Kerberos.

D. WINS.

1. ¿Qué mecanismo permite acceder a los recursos de un dominio desde un dominio de un bosque diferente?

A. Relación de confianza.

B. Árbol de dominios.

C. Kerberos.

D. Ninguna de las anteriores.

1. ¿Cuál es el nivel funcional de dominio más moderno soportado por Windows Server 2019?

A. Windows Server 2012 R2.

B. Windows Server 2019.

C. Windows Server 2016 R2.

D. Windows Server 2016.

1. ¿Qué es necesario instalar en un equipo Windows para unirlo a un dominio?

A. El rol de Active Directory Domain Services.

B. Las herramientas de administración de Active Directory Domain Services.

C. Nada, solo es necesario configurar la conexión al dominio, pero no hay que instalar nada.

D. El rol de Active Directory Federation Services.

1. ¿Cuántos controladores de dominio debería tener un dominio?

A. Dos o más.

B. Al menos uno.

C. Puede no tener y usar un catálogo global de otro dominio.

D. Tantos como oficinas.
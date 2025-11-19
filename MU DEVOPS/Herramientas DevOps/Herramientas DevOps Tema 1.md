Tema nº1

El Ciclo DevOps

Herramientas DevOps

Índice

[Esquema 3](#_Toc47194331)

[Ideas clave 4](#_Toc47194332)

[1.1. Introducción y objetivos 4](#_Toc47194333)

[1.2. Diseño y Arquitectura 6](#_Toc47194334)

[1.3. Implementación y despliegue 7](#_Toc47194335)

[1.4. Mantenimiento 19](#_Toc47194336)

[1.5. Mejora Continua 20](#_Toc47194337)

[1.6. Conclusiones 20](#_Toc47194338)

[1.7. Referencias bibliográficas 21](#_Toc47194339)

[A fondo 22](#_Toc47194340)

[Actividades 24](#_Toc47194341)

[Test 25](#_Toc47194342)

![](data:image/png;base64...)Esquema

Ideas clave

1.1. Introducción y objetivos

En esta asignatura analizaremos diferentes herramientas que soportan una implementación exitosa de la filosofía DevOps para diferentes tipos de aplicaciones y sistemas, con especial foco en los sistemas altamente escalables, con alta disponibilidad y despliegue continuo.

En este tema se pretenden conseguir los siguientes los objetivos:

* Analizar el ciclo DevOps y cada una de sus fases.
* Detectar las necesidades y problemáticas que pueden aparecer en cada una de las fases.
* Conocer las herramientas y procesos que puedan ayudarnos a solucionar los problemas emergentes.

![](data:image/png;base64...)

Figura 1 Ciclo DevOps[[1]](#footnote-1)

El ciclo DevOps puede ser definido de múltiples formas. En nuestro caso nos centraremos en las tareas de Diseño y Arquitectura, que se realizan frecuentemente durante la planificación (*Plan*) y creación (*Create*). Posteriormente, hablaremos de las herramientas que nos permiten realizar las tareas de empaquetamiento (*Package*), entrega (*Release*) y configuración (*Configure*) hablando de cómo hacer la Implementación y Despliegue de las decisiones que hayamos tomado en fases anteriores.

Al hablar de la monitorización *(Monitor)* veremos las diferentes tareas de mantenimiento y qué herramientas nos pueden ayudar a monitorizar el estado de nuestras aplicaciones y sistemas.

Las tareas de verificación y configuración se verán en mayor profundidad en otras asignaturas del máster y nosotros solo las mencionaremos por su relación con las herramientas que vamos a analizar.

Es importante destacar de que, aunque las fases se traten linealmente en esta asignatura, estas no se implementaran en cascada. Una de las enseñanzas más importantes de DevOps es la necesidad de iterar e ir realizando pasos incrementales lo más frecuentes posibles. Esto nos llevará a hablar en todas las fases de cómo las diferentes herramientas pueden soportar esta iteración.

Resulta imprescindible no perder de vista esa iteración y la contribución de las herramientas a cada una de las fases, y no solo a la principal fase para la que se implementan.

El objetivo final de esta asignatura es que el alumno conozca las principales herramientas disponibles para una gran variedad de problemas y cómo y cuando tiene sentido utilizarlas. Además, se estudiarán algunas herramientas ampliamente utilizadas en la industria y que son compatibles con casos de uso que permitirán aplicar directamente los conocimientos y competencias adquiridas.

1.2. Diseño y Arquitectura

En esta asignatura definiremos al Diseño y la Arquitectura como un aspecto que hace foco en elementos que van "más allá de los algoritmos y estructuras de datos de la computación; el diseño y especificación de la estructura global del sistema” según la definición de David Garlan y Mary Shaw.

Es decir, durante el diseño y la arquitectura hablaremos principalmente de la estructura global del sistema y de qué piezas podemos usar y reusar para componer un sistema completo. Podríamos pensar que el diseño y arquitectura son solo usados en metodologías de desarrollo en cascada tradicionales. Esto es un error común en nuevos equipos que están en un proceso de transición hacia metodologías ágiles y de DevOps. En metodologías en cascada era frecuente realizar diagramas de arquitectura en la fase de diseño; y el resultado de este diseño era un documento importante y formal que guiaba las siguientes fases con gran nivel de detalle.

En las metodologías ágiles, la medida del progreso es el código funcional y por tanto no se suelen realizar grandes documentos de diseño. Las tareas de diseño y arquitectura se suelen realizar informalmente, durante las fases de planificación y creación. En ocasiones se realizan durante las sesiones de *grooming* u otros rituales dependiendo de la forma de implementar la metodología sin considerarlas como una tarea diferenciada distinta al desarrollo.

Esta percepción “informal” de la arquitectura tiene ventajas, porque evita que la arquitectura se “osifique” y se vuelva inmutable. Es importante considerar que la arquitectura de una aplicación debería cambiar conforme la aplicación evoluciona, aunque frecuentemente lo haga a una velocidad menor que otras facetas.

Una de las ventajas de la filosofía DevOps es que aporta una perspectiva operativa en todas las fases del desarrollo de software. Es importante no solo que en la arquitectura se eviten duplicidades y se conserven los principios SOLID, por ejemplo, sino que además es importante considerar cuan “mantenible” o gestionable es la solución, cómo nos va a permitir gestionar los cambios en los ciclos, cuáles son las características de disponibilidad, cuál es el radio de influencia en el caso de un error (“blast radius”), etc.

En los siguientes temas hablaremos de las diferentes características de los componentes inherentes a ellos. También veremos diferentes formas de conectar estos componentes y comprender como se afectan entre ellos y como podemos analizar y reflexionar sobre ellos en general. Veremos desde patrones de despliegue de cómputo como la infraestructura como servicio o las funciones como servicio (IaaS y FaaS) hasta diferentes bases de datos, motores de búsqueda, colas de tareas y gestores de la configuración. Esto nos permitirá decidir en qué ocasiones escribir una funcionalidad o apoyarnos en un componente reusable; y si tenemos que escribir nuestra propia funcionalidad, sabremos cómo hay que desplegarla, monitorizarla y evolucionarla.

1.3. Implementación y despliegue

Definiremos a la Implementación y Despliegue como la fase en la que aplicamos una nueva versión de nuestra aplicación al entorno productivo. Es importante destacar que eso no es únicamente desplegar una nueva versión de código (aunque es una parte esencial y compleja en sí misma) sino desplegar un entorno nuevo, cambiar las piezas necesarias, desplegar componentes nuevos completos, configurar conexiones y eliminar las piezas que dejen de ser fundamentales.

Estudiaremos herramientas como Packer que nos servirán para crear nuevas imágenes para reducir el riesgo de configuración cuando utilicemos IaaS. Esto nos permitirá no solo desplegar cómodamente sino realizar entornos de desarrollo locales más similares a entornos productivos que minimicen los errores por diferencias entre entornos.

Luego hablaremos de cómo cambiar entornos completos de nube con las herramientas de Infraestructura como Código. Veremos cómo es posible utilizar herramientas específicas de la nube además de Terraform, una herramienta multinube que nos permitirá gestionar el ciclo de vida de nuestra configuración de arquitectura.

Existen varios conceptos que veremos en esta sección y que afectan a como analizamos los cambios de esta fase y son interesantes para evaluar su impacto en el ciclo DevOps.

Compilación y ejecución

La implementación y despliegue es una de las etapas clave del ciclo DevOps. Durante esta fase se realizan múltiples tareas y resulta útil clasificarlas en función de si impactan sobre entornos productivos o pueden realizarse en otros entornos.

Algunas de las tareas, como la creación de las imágenes, la compilación del software que lo requiera, la compresión de ficheros y otras similares, frecuentemente no dependen del entorno productivo en su totalidad y es posible realizarlas en un entorno diferente. Otras tareas, como el cambio de ficheros de configuración en una máquina virtual, añadir nuevos usuarios de sistema a una máquina existente o cambiar los puertos habilitados en un firewall son tareas que se realizan en los entornos productivos. Ambos tipos de tareas pertenecen al ciclo de implementación y despliegue, pero la forma de gestionarlas es distinta. De hecho, estas tareas no son una distinción perfecta y en ocasiones es posible mover tareas de una a otra de estas categorías. Por ejemplo, en el caso de piezas de arquitectura sin estado sobre las que hablaremos más adelante, es posible crear servidores virtuales completamente nuevos en lugar de cambiar las configuraciones de red de uno ya existente. Con esta acción lo que haremos será mover una tarea de configuración de la fase de ejecución hacia la tarea de creación de la imagen en la fase de compilación.

Infraestructura inmutable

La infraestructura inmutable es un paradigma que intenta considerar las piezas de infraestructura como inmutables y, por tanto, la forma de cambiarlas sería reemplazarlas por una nueva con la próxima versión.

Un ejemplo de infraestructura mutable es el de las máquinas virtuales o los servidores físicos. Estos equipos tienen un estado determinado y cuando queremos que sean distintos es necesario configurarlos; esta configuración variará de acuerdo con su estado de configuración inicial. Otros ejemplos podrían ser algunos elementos como los contenedores, que frecuentemente son tratados como inmutables. Otros ejemplos son elementos de red de la nube, que en muchas ocasiones, si queremos cambiar su configuración, es necesario crearlos de nuevo.

En el caso de los componentes inmutables, si necesitamos uno con un comportamiento o configuración distinta este habría de ser reemplazado.

Existen diferentes ejemplos y formas de considerar las piezas de infraestructura y también técnicas que permite hacer mejor o más fácil tratar las piezas como inmutables.

Una de las características en el uso de las nubes es que introdujo habilidades que hacían mucho más conveniente el uso de componentes si se podía. Mientras antes si necesitábamos cambiar una máquina virtual era mucho más efectivo hacerlo desde ella, puesto que crear una nueva consumía recursos del centro de cómputo que podría llegar a sobrepasar el máximo, en la nube la creación de una nueva máquina podía costar muy poco tiempo y dinero y una vez estuviera lista, eliminando la anterior se volvía al anterior nivel de uso y frecuentemente sin cortes de servicio.

Este proceso ha hecho que se haya intentado aplicar y rescatar las ventajas de estos componentes inmutables en componentes tradicionalmente inmutables. Por ejemplo, en lugar de ejecutar un sistema de gestión de la configuración como Ansible sobre el entorno productivo, se utilizaba para crear una imagen mediante Packer y se realizaba un despliegue nuevo para reemplazar el existente.

También sistemas donde el estado se puede desconectar, como discos separados de las máquinas virtuales, permiten realizar este tipo de técnicas incluso en componentes con estado.

Infraestructura como código

El proceso de virtualización de muchos de los componentes ha ido lentamente permitiendo expresar los diversos componentes de infraestructura de una forma cada vez más sintética y digital. El uso de máquinas virtuales en la nube en lugar de físicas permite tener un inventario automático de las máquinas disponibles. El uso de redes virtualizadas en lugar de redes físicas hace más fácil entender como esta todo conectado y que tipo de tráfico se permite. Muchas de estas cosas son perfectamente posibles en sistemas más antiguos pero la transición a la nube hizo este tipo de expresión mucho más sencilla.

Una vez que se empezó a poder expresar de forma digital los recursos, empezó una transformación para expresar no solo el estado actual sino el estado deseado y tener herramientas que crean o transformas elementos para llevarlos a nuestro estado deseado.

Este tipo de tecnologías permiten definir nuestra estructura como un código que es sencillo de revisar y analizar, y que diversos sistemas son capaces de transformar en recursos específicos. Este tipo de lenguajes expresan de forma declarativa los recursos que queremos, en lugar de hacerlo en forma imperativa explicando los pasos para obtenerlos.

Las diferentes nubes han ido implementando lenguajes propios que permiten expresar los recursos que soportan y han surgido algunos proyectos que ofrecen soporte de infraestructura como código sobre diferentes nubes. En esta asignatura veremos Terraform como un ejemplo de esta potente técnica.

Soluciones nativas a la infraestructura como código

Las diferentes nubes han ido implementando diferentes soluciones de infraestructura como código. Algunas de las más importantes son:

* **Cloud Formation en AWS**

La solución de Amazon se basa en documentos JSON que se despliegan en los que llamados *stacks*. A continuación, mostramos un ejemplo de un recurso de DynamoDB basado en los ejemplos de AWS.

{

"AWSTemplateFormatVersion" : "2010-09-09",

"Description" : "AWS CloudFormation Sample Template DynamoDB\_Table: This template demonstrates the creation of a DynamoDB table. \*\*WARNING\*\* This template creates an Amazon DynamoDB table. You will be billed for the AWS resources used if you create a stack from this template.",

"Parameters" : {

"HashKeyElementName" : {

"Description" : "HashType PrimaryKey Name",

"Type" : "String",

"AllowedPattern" : "[a-zA-Z0-9]\*",

"MinLength": "1",

"MaxLength": "2048",

"ConstraintDescription" : "must contain only alphanumberic characters"

},

"HashKeyElementType" : {

"Description" : "HashType PrimaryKey Type",

"Type" : "String",

"Default" : "S",

"AllowedPattern" : "[S|N]",

"MinLength": "1",

"MaxLength": "1",

"ConstraintDescription" : "must be either S or N"

},

"ReadCapacityUnits" : {

"Description" : "Provisioned read throughput",

"Type" : "Number",

"Default" : "5",

"MinValue": "5",

"MaxValue": "10000",

"ConstraintDescription" : "must be between 5 and 10000"

},

"WriteCapacityUnits" : {

"Description" : "Provisioned write throughput",

"Type" : "Number",

"Default" : "10",

"MinValue": "5",

"MaxValue": "10000",

"ConstraintDescription" : "must be between 5 and 10000"

}

},

"Resources" : {

"myDynamoDBTable" : {

"Type" : "AWS::DynamoDB::Table",

"Properties" : {

"AttributeDefinitions": [ {

"AttributeName" : {"Ref" : "HashKeyElementName"},

"AttributeType" : {"Ref" : "HashKeyElementType"}

} ],

"KeySchema": [

{ "AttributeName": {"Ref" : "HashKeyElementName"}, "KeyType": "HASH" }

],

"ProvisionedThroughput" : {

"ReadCapacityUnits" : {"Ref" : "ReadCapacityUnits"},

"WriteCapacityUnits" : {"Ref" : "WriteCapacityUnits"}

}

}

}

},

"Outputs" : {

"TableName" : {

"Value" : {"Ref" : "myDynamoDBTable"},

"Description" : "Table name of the newly created DynamoDB table"

}

}

}

Figura 2 Ejemplo de código de CloudFormation Origen AWS

Podemos ver que existen varias secciones diferenciadas, siendo Resources la sección principal donde se puede poner uno o varios recursos. Es posible parametrizar los recursos que creemos y almacenar ciertos valores, como sus identificadores y valores dinámicos mediante los Outputs.

También se puede actualizar la *template* (plantilla) de un *stack* (pila), lo cual modificará los recursos de esa pila o *stack*. En algunos casos, los recursos serán modificados y en otros actualizados.

* **Azure Resource Manager en Azure**

Azure Resource Manager permite desplegar recursos en un Resource Group de Azure. Podemos separar a las *templates* en otras *subtemplates* y los recursos se despliegan sobre un Resource Group.

Un ejemplo de *template* sería el siguiente:

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"adminUsername": {

"type": "string",

"metadata": {

"description": "User name for the Virtual Machine."

}

},

"adminPassword": {

"type": "securestring",

"metadata": {

"description": "Password for the Virtual Machine."

}

},

"dnsLabelPrefix": {

"type": "string",

"defaultValue": "[concat('vm-', uniqueString(resourceGroup().id))]",

"metadata": {

"description": "Unique DNS Name for the Public IP used to access the Virtual Machine."

}

},

"windowsOSVersion": {

"type": "string",

"defaultValue": "2019-Datacenter",

"allowedValues": [

"2012-Datacenter",

"2012-R2-Datacenter",

"2016-Datacenter",

"2019-Datacenter"

],

"metadata": {

"description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter."

}

},

"location": {

"type": "string",

"defaultValue": "[resourceGroup().location]",

"metadata": {

"description": "Location for all resources."

}

},

"vmSize": {

"type": "string",

"defaultValue": "Standard\_D2\_v3",

"metadata": {

"description": "Size of the VM"

}

}

},

"variables": {

"storageAccountName": "[concat(uniquestring(resourceGroup().id), 'sawinvm')]",

"imagePublisher": "MicrosoftWindowsServer",

"imageOffer": "WindowsServer",

"nicName": "myVMNic",

"addressPrefix": "10.0.0.0/16",

"subnetName": "Subnet",

"subnetPrefix": "10.0.0.0/24",

"storageAccountType": "Standard\_LRS",

"publicIPAddressName": "myPublicIP",

"publicIPAddressType": "Dynamic",

"vmName": "SimpleWindowsVM",

"virtualNetworkName": "MyVNET",

"subnetRef": "[resourceId('Microsoft.Network/virtualNetworks/subnets', variables('virtualNetworkName'), variables('subnetName'))]",

"networkSecurityGroupName": "[concat(variables('subnetName'), '-nsg')]"

},

"resources": [

{

"type": "Microsoft.Storage/storageAccounts",

"name": "[variables('storageAccountName')]",

"apiVersion": "2019-06-01",

"location": "[parameters('location')]",

"kind": "Storage",

"sku": {

"name": "[variables('storageAccountType')]"

}

},

{

"apiVersion": "2019-11-01",

"type": "Microsoft.Network/publicIPAddresses",

"name": "[variables('publicIPAddressName')]",

"location": "[parameters('location')]",

"properties": {

"publicIPAllocationMethod": "[variables('publicIPAddressType')]",

"dnsSettings": {

"domainNameLabel": "[parameters('dnsLabelPrefix')]"

}

}

},

{

"comments": "Simple Network Security Group for subnet [variables('subnetName')]",

"type": "Microsoft.Network/networkSecurityGroups",

"apiVersion": "2019-11-01",

"name": "[variables('networkSecurityGroupName')]",

"location": "[parameters('location')]",

"properties": {

"securityRules": [

{

"name": "default-allow-3389",

"properties": {

"priority": 1000,

"access": "Allow",

"direction": "Inbound",

"destinationPortRange": "3389",

"protocol": "Tcp",

"sourceAddressPrefix": "\*",

"sourcePortRange": "\*",

"destinationAddressPrefix": "\*"

}

}

]

}

},

{

"apiVersion": "2019-11-01",

"type": "Microsoft.Network/virtualNetworks",

"name": "[variables('virtualNetworkName')]",

"location": "[parameters('location')]",

"dependsOn": [

"[variables('networkSecurityGroupName')]"

],

"properties": {

"addressSpace": {

"addressPrefixes": [

"[variables('addressPrefix')]"

]

},

"subnets": [

{

"name": "[variables('subnetName')]",

"properties": {

"addressPrefix": "[variables('subnetPrefix')]",

"networkSecurityGroup": {

"id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroupName'))]"

}

}

}

]

}

},

{

"apiVersion": "2019-11-01",

"type": "Microsoft.Network/networkInterfaces",

"name": "[variables('nicName')]",

"location": "[parameters('location')]",

"dependsOn": [

"[variables('publicIPAddressName')]",

"[variables('virtualNetworkName')]"

],

"properties": {

"ipConfigurations": [

{

"name": "ipconfig1",

"properties": {

"privateIPAllocationMethod": "Dynamic",

"publicIPAddress": {

"id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIPAddressName'))]"

},

"subnet": {

"id": "[variables('subnetRef')]"

}

}

}

]

}

},

{

"apiVersion": "2019-12-01",

"type": "Microsoft.Compute/virtualMachines",

"name": "[variables('vmName')]",

"location": "[parameters('location')]",

"dependsOn": [

"[variables('storageAccountName')]",

"[variables('nicName')]"

],

"properties": {

"hardwareProfile": {

"vmSize": "[parameters('vmSize')]"

},

"osProfile": {

"computerName": "[variables('vmName')]",

"adminUsername": "[parameters('adminUsername')]",

"adminPassword": "[parameters('adminPassword')]"

},

"storageProfile": {

"imageReference": {

"publisher": "[variables('imagePublisher')]",

"offer": "[variables('imageOffer')]",

"sku": "[parameters('windowsOSVersion')]",

"version": "latest"

},

"osDisk": {

"createOption": "FromImage"

},

"dataDisks": [

{

"diskSizeGB": 1023,

"lun": 0,

"createOption": "Empty"

}

]

},

"networkProfile": {

"networkInterfaces": [

{

"id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"

}

]

},

"diagnosticsProfile": {

"bootDiagnostics": {

"enabled": true,

"storageUri": "[reference(variables('storageAccountName')).primaryEndpoints.blob]"

}

}

}

}

]

}

Figura 3 Ejemplo de Template de ARM oficial. Origen Azure

La sección *Resources* contiene los distintos recursos que se desplegarán. Es posible incluir diferentes parámetros mediante la sección de *parameters*. Los *template*s de Azure además soportan variables internas de ésta*,* que permiten que sean más mantenibles y que incluyan funciones adicionales para procesar las variables. Por último, es posible recoger en *outputs* los valores asociados a los recursos generales que nos sean útiles.

* Cloud Deployment Manager en Google Cloud

Los *templates* de Cloud Deployment Manager de GCP se expresan en YAML y pueden realizarse piezas reusables en Python y Jinja2 (un sistema de interpolación de plantillas del ecosistema de Python).

Un ejemplo obtenido de la documentación de GCP:

# Copyright 2016 Google Inc. All rights reserved.

#

# Licensed under the Apache License, Version 2.0 (the "License");

# you may not use this file except in compliance with the License.

# You may obtain a copy of the License at

#

# http://www.apache.org/licenses/LICENSE-2.0

#

# Unless required by applicable law or agreed to in writing, software

# distributed under the License is distributed on an "AS IS" BASIS,

# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.

# See the License for the specific language governing permissions and

# limitations under the License.

# Put all your resources under `resources:`. For each resource, you need:

# - The type of resource. In this example, the type is a Compute VM instance.

# - An internal name for the resource.

# - The properties for the resource. In this example, for VM instances, you add

# the machine type, a boot disk, network information, and so on.

#

# For a list of supported resources,

# see https://cloud.google.com/deployment-manager/docs/configuration/supported-resource-types.

resources:

- type: compute.v1.instance

name: quickstart-deployment-vm

properties:

# The properties of the resource depend on the type of resource. For a list

# of properties, see the API reference for the resource.

zone: us-central1-f

# Replace [MY\_PROJECT] with your project ID

machineType: https://www.googleapis.com/compute/v1/projects/[MY\_PROJECT]/zones/us-central1-f/machineTypes/f1-micro

disks:

- deviceName: boot

type: PERSISTENT

boot: true

autoDelete: true

initializeParams:

# See a full list of image families at https://cloud.google.com/compute/docs/images#os-compute-support

# The format of the sourceImage URL is: https://www.googleapis.com/compute/v1/projects/[IMAGE\_PROJECT]/global/images/family/[FAMILY\_NAME]

sourceImage: https://www.googleapis.com/compute/v1/projects/debian-cloud/global/images/family/debian-9

# Replace [MY\_PROJECT] with your project ID

networkInterfaces:

- network: https://www.googleapis.com/compute/v1/projects/[MY\_PROJECT]/global/networks/default

# Access Config required to give the instance a public IP address

accessConfigs:

- name: External NAT

type: ONE\_TO\_ONE\_NAT

Figura 4 Ejemplo de template para Deployment Manager. Origen: Documentación de GCP.

Los recursos se indican en la sección de *resources*. Es posible utilizar toda la potencia de Jinja2 para interpolar valores, tratar variables y generar *template*s dinámicos. Deployment Manager es capaz de crear, eliminar y actualizar recursos.

1.4. Mantenimiento

El mantenimiento de un sistema consiste en lograr que el sistema continúe funcionando y mantenga nuestro objetivo de nivel de servicio, SLO (del inglés *Service Level Objectives*) y nuestros acuerdos de servicio, SLA del inglés *Service Level Agreement*).

En una metodología en cascada, el mantenimiento es una fase final cuando se realizan los cambios necesarios en la aplicación, pero asumiendo que estos van a ser pequeños y la aplicación sigue funcionando como fue diseñada. Por el contrario, en la metodología DevOps consideramos que la aplicación debe ir cambiando y adaptándose de forma continua, y el mantenimiento consiste en mantener nuestro nivel de servicio durante toda la vida de la aplicación y tendrá un impacto en todas las fases.

Dependiendo de nuestro nivel de servicio, podría por ejemplo influenciar cómo realizamos la implementación y el despliegue de cambios, ya que no podemos cortar el servicio mientras estos procesos se ejecutan.

Dado que el mantenimiento es una tarea compartida entre los perfiles más orientados al desarrollo y los más orientados a las operaciones, es más importante que nunca tener una buena visibilidad sobre lo que está ocurriendo en nuestro entorno de forma que no nos distraiga de otras tareas importantes que estaremos realizando.

En el caso de problemas con la aplicación, también es esencial que podamos analizar qué es lo que pasa e informar para que se puedan hacer mejoras, se resuelvan dichos problemas, o se empleen mejores herramientas de mantenimiento. El mantenimiento no es realmente una fase del ciclo de vida, sino que es una tarea continua que deberemos optimizar para mejorar la forma en que el ciclo DevOps se lleva a cabo.

1.5. Mejora Continua

La mejora continua es otra de las tareas que se llevan a cabo durante todas las fases del ciclo de vida DevOps. Es frecuente que se haga hincapié en la mejora continua durante las fases de planificación, ya que ahí es cuando se analizan y deciden cuáles son los puntos de mejora que se van a llevar a cabo. Sin embargo, esto no implica que la mejora se realice solo en esa fase.

El ciclo de vida DevOps de una aplicación es continuo y ágil, por ello resulta crucial utilizar herramientas que nos permitan trabajar con velocidad en las iteraciones y que permitan que las tareas de desarrollo y operaciones se apoyen y se complementen para automatizar y mejorar continuamente este proceso.

La mejora continua requiere de un análisis de la situación real, y además de un análisis sobre qué cambios queremos realizar. La monitorización nos ayudará significativamente a conocer nuestros datos actuales a fin de predecir problemas y evitarlos en la siguiente iteración.

En esta asignatura veremos diferentes herramientas de monitorización, como Elastic Beats, y herramientas para el análisis y prospección de las mismas, como Kibana. Con estas herramientas obtendremos un mejor conocimiento de las capacidades de las herramientas similares en el ecosistema y aplicándolas, realizar un mejor análisis para mejorar en nuestro ciclo DevOps.

1.6. Conclusiones

En este tema hemos visto las diferentes fases del ciclo de vida DevOps. Es importante recordar que estas fases se van a realizar en una rápida sucesión y de forma repetida. Durante un proyecto, especialmente si es innovador, veremos que las fases son algo más lentas en la primera iteración, pero con la mejora continua se irá acelerando la velocidad de ésta, lo que dará como resultado el aumento de la calidad del proceso y la posibilidad de aplicar cambios.

1.7. Referencias bibliográficas

The DevOps Handbook: How to Create World-Class Agility, Reliability, and Security in Technology Organizations

ISBN-13: 978-1942788003

Team Topologies: Organizing Business and Technology Teams for Fast Flow

ISBN: 978-1942788812

Infrastructure as Code by Kief Morris (O'Reilly Publishing, June 2016)

ISBN: 9781491924358

A fondo

**DevOps Topologies**

Analisis de diferentes formas de repartir el trabajo entre diferentes grupos y roles considerando desarrolladores y operadores principalmente.

<https://web.devopstopologies.com/index.html>

Es interesante leer las diferentes clasificaciones y reflexionar el impacto que tendría sobre un ciclo DevOps. Por ejemplo, pensar quien es el responsable de mejorar la monitorización en cada uno de los tipos de topologías.

Buenas prácticas de Deployment Manager con GCP

Recopilación de mejores prácticas por Google para Deployment Manager <https://cloud.google.com/deployment-manager/docs/step-by-step-guide>

Esta recopilación nos ayudará a sacar el mayor partido a Deployment Manager y es muy recomendable si vamos a utilizar Google Cloud en general.

**Accelerate**

Accelerate: Building and scaling High Performing Technology Organizations. ISBN: 9781942788331

Interesante libro con muchos datos de investigación y buenos datos empíricos sobre que funciona y como en la producción de software.

**Team Topologies: Organizing Business and Technology Teams for Fast Flow**

Libro sobre diferentes formas de estructurar los equipos en organizaciones medianas o grandes. https://teamtopologies.com/book

Si habéis leído las topologías DevOps puede ser interesante reflexionar sobre topologías de equipos más en general y como acelerar el trabajo y tiempo de iteración.

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

1. ¿Cuáles de las siguientes fases pertenecen a la definición del ciclo DevOps?
   1. Análisis de viabilidad del proyecto
   2. Pentesting
   3. Monitorización \*(La monitorización es una de las partes y fases del ciclo DevOps)
   4. A y B son correctas
2. ¿Qué es el blast radius en un contexto DevOps?
   1. El radio de infección de un virus informático
   2. El radio de influencia en caso de error de un componente \* (En DevOps, el Blast Radius se define como el impacto de un problema en un componente)
   3. Todas las respuestas son correctas
   4. La distancia que es necesario dejar entre servidores
3. La infraestructura inmutable:
   1. Consiste en piezas de infraestructura que no pueden cambiar bajo cortes de suministro o acceso
   2. Consiste en piezas de infraestructura que no pueden cambiar por limitaciones propias de los componentes, como la región en muchos servicios de nube
   3. Consiste en piezas de infraestructura que no pueden cambiar o bien por limitación de la tecnología o por política propia \*(La infraestructura inmutable consiste en la técnica de evitar modificar los componentes y optar por reemplazarlos en la medida de lo posible para evitar diferencias entre los distintos nodos debido a su historia)
   4. Consiste en piezas de infraestructura que pueden cambiar y se modifican internamente, pero con ciertas facetas que se mantienen estables como un servidor cuyo tipo no cambia, pero sus paquetes si son actualizados y configurados
4. La infraestructura como código:
   1. Consiste en definir la infraestructura de forma encriptada
   2. Consiste en definir la infraestructura en forma de código frecuentemente declarativo \*(La infraestructura como código define la infraestructura usando códigos declarativos o principalmente declarativos)
   3. Consiste en usar imágenes codificadas de máquinas virtuales en lugar de configurarlas
   4. Consiste en definir la infraestructura en forma de código exclusivamente imperativo
5. CloudFormation es el sistema de infraestructura como código:
   1. De la nube pública de Google, GCP
   2. De la nube pública de Amazon, AWS \*(CloudFormation ha sido generado por Amazon)
   3. De la nube pública de Microsoft, Azure
   4. Soportando multiples nubes siendo generado por una compañia independiente
6. Resource Manager es el sistema de infraestructura como código:
   1. De la nube pública de Google, GCP
   2. De la nube pública de Amazon, AWS
   3. De la nube pública de Microsoft, Azure \*(Resource Manager ha sido generado por Microsoft para Azure)
   4. Soportando multiples nubes siendo generado por una compañia independiente
7. Deployment Manager es el sistema de infraestructura como código:
   1. De la nube pública de Google, GCP \*(Deployment Manager ha sido generado por Google para GCP)
   2. De la nube pública de Amazon, AWS
   3. De la nube pública de Microsoft, Azure
   4. Soportando multiples nubes siendo generado por una compañia independiente
8. Service Level Objectives:
   1. Consiste en el nivel de servicio que objetivamente se percibe del servicios
   2. Consiste en el nivel de servicio que se busca proveer a los clientes \*(Service Level Objectives son los objetivos que una organización se propone como el nivel que desea ofrecer o mantener)
   3. Consiste en el nivel de servicio que es necesario proveer por motivos contractuales con al menos uno de los clientes
   4. Todas las respuestas son incorrectas
9. Service Level Agreement:
   1. Consiste en el nivel de servicio que objetivamente se percibe del servicios
   2. Consiste en el nivel de servicio que se busca proveer a los clientes
   3. Consiste en el nivel de servicio que es necesario proveer por motivos contractuales con al menos uno de los clientes \*(Service Level Agreement es el nivel de servicio que se contrata y que debe mantenerse para evitar las penalizaciones contempladas en el contrato)
   4. Todas las respuestas son incorrectas
10. El mantenimiento en DevOps
    1. Es una fase realizada únicamente cuando se han finalizado las mejoras iterativas y no se esperan más cambios.
    2. Es una fase consistente en mantener el sistema operando y funcionando con respecto a nuestro Service Level Objetive, obteniendo datos para informar las mejorar que podríamos realizar \*(El mantenimiento en DevOps es una fase continuada y parcialmente iterativa ya que informa de datos para poder realizar la siguiente iteración de una forma correcta)
    3. No es una fase de DevOps ya que el mantenimiento corre a cargo de otro equipo
    4. A y B son correctas

1. Kharnagy / CC BY-SA (https://creativecommons.org/licenses/by-sa/4.0) [↑](#footnote-ref-1)
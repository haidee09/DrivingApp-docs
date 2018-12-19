## Configuraciones Generales de DrivingApp

DrivingApp utiliza servicios externos para consumir la información que muestra al usuario en la aplicación. El Orion ContextBroker de FIWARE es uno de estos servicios externos, este componente administra la información de contexto que produce la aplicación. Otros servicios que utiliza DrivingApp son los servicios web, estos tienen como función manipular las entidades de datos y las consultas de la aplicación móvil; además estos servicios web permiten a la aplicación móvil administrar la información de las notificaciones que recibe la aplicación.  
El proyecto DrivingApp contiene archivos de configuración para modificar las URLs de los servicios que utiliza la aplicación. Para modificar estos archivos siga los pasos siguientes:

#### 1.- Descargar el proyecto DrivingApp

Este [enlace](https://github.com/cenidetiot/DrivingApp.git) envía al repositorio del proyecto DrivingApp en Github. Si desea descargar el proyecto a través del software de control de versiones git, ejecute el siguiente comando en consola: 

```sh
git clone https://github.com/cenidetiot/DrivingApp.git.  
```

Además, Github también proporciona la opción de descargar un proyecto mediante un archivo comprimido .zip

#### 2.- Abrir el proyecto DrivingApp en Android Studio

Cuando haya descargado el proyecto DrivingApp, ábralo con el entorno de desarrollo Android Studio. Para más información acerca la descarga y configuración de Android Studio visite el siguiente [enlace](https://developer.android.com/studio/)

**NOTA**: El Android SDK número 23 está configurado como la versión mínima del proyecto DrivingApp.

#### 3.- Configurar  los servicios de la aplicación DrivingApp

Abra el proyecto DrivingApp en Android Studio y configure lo siguiente:

##### 3.1 Configurar la conexión con una instancia Orion ContextBroker

El archivo `config.properties` del proyecto DrivingApp está ubicado en la ruta: ngsi/src/main/assets/, y contiene las propiedades de configuración para la conexión con una instancia Orion ContetxBroker. Este archivo define las propiedades: `host`, `port` y `apiversion`, las cuales especifican lo siguiente:

- La propiedad `host` define la url ó IP de la instancia del Orion ContextBroker.
- La propiedad `port` especifica el puerto de la instancia Orion ContextBroker definida.
- La propiedad `apiversion` define la versión de la API con la que son definidas las solicitudes al Orion ContextBroker.

Un ejemplo de la configuración del archivo `config.properties` es la siguiente:

```java
http.host = http://130.206.113.226 // Change it for your Orion host 
http.port = 1026 // Change it form your Orion port
http.apiversion = v2 // Change if for your Orion api version
```

##### 3.2	Configurar DrivingAppService

DrivingApp utiliza DrivingAppService para manipular las entidades públicas del proyecto,basadas en modelos de datos FIWARE; además de las entidades privadas creadas para este proyecto. DrivingAppService proporciona una API RESTFul para la administración de estas entidades públicas y privadas que utiliza la aplicación móvil DrivingApp. Además, DrivingApp también utiliza el servicio DrivingAppService para realizar consultas de contexto y gestionar la información de las alertas. Puede consultar el código fuente de este servicio web en este [enlace](https://github.com/cenidetiot/smartsecurity-web-service)

Para configurar DrivingAppService en el proyecto DrivingApp debe modificar el archivo `ConfigServer.java`, con configurar la URL de DrivingAppService. Este archivo está en la ruta: cenidetsdk/src/main/java/mx/edu/cenidet/cenidetsdk/utilities/ del proyecto DrivingApp. 

Un ejemplo de la configuración de este archivo es el siguiente:

```java
http_host("https://smartsecurity-webservice.herokuapp.com")
```

##### 3.3 Configuración del proyecto Firebase Cloud Messaging (FCM) para la aplicación DrivingApp

Firebase Cloud Messaging (FCM) es una solución multiplataforma en la nube para envío de mensajes y notificaciones a dispositivos Android, iOS y aplicaciones web. Este servicio es proporcionado por Firebase y actualmente se puede utilizar sin costo alguno.
La aplicación DrivingApp utiliza los servicios de FCM para replicar las notificaciones de alertas a los dispositivos de los usuarios. Los algoritmos de la aplicación para el envío de alertas pueden utilizarse para replicar y recibir notificaciones de alertas, sin realizar modificaciones adicionales al código. Por otro lado, para implementar notificaciones de alertas personalizadas en DrivingApp ó en otra aplicación, realice las instrucciones que se presentan a continuación para configurar los servicios de FCM en la aplicación móvil:

1.- Acceda al sitio de Firebase en este [enlace](https://console.firebase.google.com/) y seleccione la opción de *Añadir Proyecto*.

![Bienvenida Firebase](img/fcm/1.png)

2.- Agregue un nombre de proyecto y seleccione el país o región. El nombre de proyecto puede ser DrivingApp o el nombre de la aplicación que esté desarrollando. Firebase agrega un número de serie al nombre del proyecto que lo identifica entre otros proyectos con nombre similar. Cuando haya completado esta información, de click en el botón **Crear Proyecto**.

![Nombre de proyecto Firebase](img/fcm/2.png)

3.- Firebase crea el proyecto y abre la vista de la consola con el menú de funciones. En esta vista debe seleccionar la opción *Añade Firebase a tu aplicación móvil de Android* para comenzar con la configuración de Firebase en su aplicación Android, como muestra la siguiente imagen.

![Consola Firebase](img/fcm/3.png)

4.-	Registre su aplicación agregando el nombre del paquete de la aplicación Android. Si desea configurar DrivingApp nuevamente, el nombre de paquete es `mx.edu.cenidet.drivingapp`; en cambio, si es una aplicación propia, agregue el nombre del paquete correspondiente. Cuando haya completado esta información, de click en el botón **Registrar Aplicación**.

![Registro de la aplicación Android](img/fcm/4.png)

5.- Descargue el archivo de configuración `google-services.json` y muévalo a la carpeta principal del proyecto para añadir Firebase a su aplicación móvil Android. En el proyecto DrivingApp, este archivo de configuración está en la carpeta principal, debe reemplazarlo si desea configurar el proyecto nuevamente. Posteriormente de click en el botón **Continuar**.

![Añadir Firebase a la aplicación Android](img/fcm/5.png)

![Archivo de configuración en proyecto DrivingApp](img/fcm/6.png)

6.- Modifique el archivo `build.gradle` del proyecto y el archivo `build.gradle` de la aplicación como se muestra en la imagen para utilizar el complemento de los servicios de Google para Gradle. Esta configuración ya se ha realizado en el proyecto DrivingApp, sin embargo, si está creando un nuevo proyecto a partir del código de DrivingApp debe modificar los archivos como se indica.

![Archivos de los servicios de Gradle](img/fcm/7.png)

7.- Finalmente, Firebase le muestra las estadísticas de los usuarios que utilizan la aplicación Android que ha configurado.

![Firebase Panel de Administración](img/fcm/8.png)
## Configuraciones Generales de DrivingApp

DrivingApp utiliza servicios externos para consumir la información que muestra al usuario en la aplicación. El Orion ContextBroker de FIWARE es uno de estos servicios externos, este componente administra la información de contexto que produce la aplicación. Otros servicios que utiliza DrivingApp son los servicios web, estos tienen como función manipular las entidades de datos y las consultas de la aplicación móvil; además estos servicios web permiten a la aplicación móvil administrar la información de las notificaciones que recibe la aplicación.  
El proyecto DrivingApp contiene archivos de configuración para modificar las URLs de los servicios que utiliza la aplicación. Para modificar estos archivos siga los pasos siguientes:

#### 1.- Descargar el proyecto DrivingApp

Este [enlace](https://github.com/cenidetiot/DrivingApp.git) envía al repositorio del proyecto DrvingApp en Github. Si desea descargar el proyecto a través del software de control de versiones git, ejecute el siguiente comando en consola: 

```sh
git clone https://github.com/cenidetiot/DrivingApp.git.  
```

Además, Github también proporciona la opción de descargar un proyecto mediante un archivo comprimido .zip

#### 2.- Abrir el proyecto DrivingApp en Android Studio

Cuando haya descargado el proyecto DrivingApp, ábralo con el entorno de desarrollo Android Studio. Para más información acerca la descarga y configuración de Android Studio visite el este [enlace](https://developer.android.com/studio/)

**NOTA**: El Android SDK número 23 está configurado como la versión mínima del proyecto DrivingApp.

#### 3.- Configurar  los servicios de la aplicación DrivingApp

Abra el proyecto DrivingApp y configure lo siguiente:

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

DrivingApp utiliza DrivingAppService para manipular las entidades públicas del proyecto,basadas en modelos de datos FIWARE; además de las entidades privadas creadas para este proyecto. DrivingAppService proporciona una API RESTFul para la administración de estas entidades públicas y privadas que utiliza la aplicación móvil DrivingApp. Además, DrivingApp también utiliza el servicio DrivingAppService para realizar consultas de contexto y gestionar la información de las alertas. Puede consultar el código fuente de este servicio web en este [link](https://github.com/cenidetiot/smartsecurity-web-service)

Para configurar DrivingAppService en el proyecto DrivingApp debe modificar el archivo `ConfigServer.java`, con configurar la URL de DrivingAppService. Este archivo está en la ruta: cenidetsdk/src/main/java/mx/edu/cenidet/cenidetsdk/utilities/ del proyecto DrivingApp. 

Un ejemplo de la configuración de este archivo es el siguiente:

```java
http_host("https://smartsecurity-webservice.herokuapp.com")
```
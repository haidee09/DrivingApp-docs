## General DrivingApp Configurations

DrivingApp uses external services to consume the information that shows the user in the application. The Orion ContextBroker of FIWARE is one of these external services, this component manages the context information produced by the application. Other services that DrivingApp uses are web services, these have the function of manipulating data entities and queries of the mobile application; In addition, these web services allow the mobile application to manage the information of the notifications received by the application.  
The DrivingApp project contains configuration files to modify the URLs of the services used by the application. To modify these files, follow the steps below.

#### 1.- Download the DrivingApp project

You can consult the DrivingApp project in this [repository] (https://github.com/cenidetiot/DrivingApp.git) of Github. If you want to download the project through the git version control software, run the following console command:

```sh
git clone https://github.com/cenidetiot/DrivingApp.git.  
```

In addition, Github also provides the option to download a project in a .zip file.

#### 2.- Open the DrivingApp project in Android Studio

Once you have downloaded the DrivingApp project, open it with the Android Studio development environment. For more information about downloading and configuring Android Studio visit the following [link](https://developer.android.com/studio/)

**NOTE**: The Android SDK number 23 is configured as the minimum version of the DrivingApp project.

#### 3.- Configure the services of the DrivingApp application

Open the DrivingApp project in Android Studio and configure the following:

##### 3.1 Configure the connection with an Orion ContextBroker instance

The `config.properties` file of the DrivingApp project is located in the path: ngsi/src/main/assets/, and contains the configuration properties for the connection to an Orion ContetxBroker instance. This file defines the properties: `host`,` port` and `apiversion`, which specify the following:

- The `host` property defines the url or IP of the Orion ContextBroker instance.
- The `port` property specifies the port of the Orion ContextBroker instance defined.
- The `apiversion` property defines the version of the Orion ContextBroker API.

A configuration example of the `config.properties` file is the following:

```java
http.host = http://130.206.113.226 // Change it for your Orion host 
http.port = 1026 // Change it form your Orion port
http.apiversion = v2 // Change if for your Orion api version
```

##### 3.2	Configure DrivingAppService

DrivingApp uses DrivingApp Service to manipulate the public entities (based on FIWARE data models) and the private entities created for the project. DrivingAppService provides a RESTFul API for the administration of these public and private entities using the DrivingApp mobile application. In addition, DrivingApp also uses the DrivingAppService service to perform context queries and manage alert information. You can check the source code of this web service on this [link](https://github.com/cenidetiot/smartsecurity-web-service)

To configure the DrivingApp Service URL in the DrivingApp project, you must modify the `ConfigServer.java` file. This file is on the route: cenidetsdk/src/main/java/mx/edu/cenidet/cenidetsdk/utilities/ from the DrivingApp project.

An example of the configuration of this file is the following:

```java
http_host("https://smartsecurity-webservice.herokuapp.com")
```

##### [3.3 Configuración del proyecto Firebase Cloud Messaging (FCM) para la aplicación DrivingApp](#configuracion-fcm)

Firebase Cloud Messaging (FCM) is a cross-platform solution in the cloud for sending messages and notifications to Android devices, iOS and web applications. This service is provided by Firebase and can currently be used at no cost.
The DrivingApp application uses FCM services to replicate alert notifications to users' devices. The algorithms of the application for sending alerts can be used to replicate and receive alert notifications, without making additional modifications to the code. On the other hand, to implement personalized alert notifications in DrivingApp or in another application, perform the instructions presented below to configure the FCM services in the mobile application.

1.- Access the Firebase site on this [link] (https://console.firebase.google.com/) and select the option of *Add Project* 

![Bienvenida Firebase](img/fcm/1.png)

2.- Add a project name and select the country or region. The project name can be DrivingApp or the name of the application you are developing. Firebase adds a serial number to the name of the project that identifies it among other projects with a similar name. When you have completed this information, click on the **Create Project** button.

![Nombre de proyecto Firebase](img/fcm/2.png)

3.- Firebase creates the project and opens the console view with the function menu. In this view, you must select the option *Add Firebase to your Android* mobile application to start configuring Firebase in your Android application, as the following image shows.

![Consola Firebase](img/fcm/3.png)

4.-	Register your application by adding the name of the Android application package. If you want to configure DrivingApp again, the package name is `mx.edu.cenidet.drivingapp`; on the other hand, if it is your own application, add the name of the corresponding package. When you have completed this information, click on the **Register Application** button.

![Registro de la aplicación Android](img/fcm/4.png)

5.- Download the `google-services.json` configuration file and move it to the main project folder to add Firebase to your Android mobile application. In the DrivingApp project, this configuration file is in the main folder, you must replace it if you want to configure the project again. Then click on the **Continue** button.

![Añadir Firebase a la aplicación Android](img/fcm/5.png)

![Archivo de configuración en proyecto DrivingApp](img/fcm/6.png)

6.- Modify the `build.gradle` file of the project and the` build.gradle` file of the application as shown in the image, to use the Google services plugin for Gradle. This configuration has already been made in the DrivingApp project, however, if you are creating a new project from the DrivingApp code you must modify the files as indicated.

![Archivos de los servicios de Gradle](img/fcm/7.png)

7.- Finally, Firebase shows you statistics of users who use the configured Android application.

![Firebase Panel de Administración](img/fcm/8.png)
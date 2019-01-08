## DrivingApp Web Services deployment

### DrivingApp Service

#### General Requirements

- **Git Version Control Software**, you can check the Git documentation in the following [link](https://git-scm.com/).
- **Execution environment Node.js**, you can check the installation documentation in the following [link](https://nodejs.org/en/download/).
- **Package manager npm or yarn**, you can check the npm documentation [here](https://docs.npmjs.com/) and the documentation of yarn [here](https://yarnpkg.com/en/docs).
- **MariaDB database manager system** version 10.4, visit the following [link](https://mariadb.org/download/) to install MariaDB.
- **FIWARE Orion ContextBroker** in a version higher than 1.15.1, you can check the official documentation in the following [link](https://fiware-orion.readthedocs.io/en/master/).
- **Orion ContextBroker de FIWARE** en una versión superior a la 1.15.1, puede consultar la documentación oficial en el siguiente [enlace](https://fiware-orion.readthedocs.io/en/master/). 
- **IDM - FIWARE KeyRock** in a version less than or equal to 6, or **Keystone from Openstack**. You can check the official repository of IDM - Keyrock in the following [link](https://github.com/ging/fiware-idm-deprecated) and the docs of Keystone - Openstack version 3 in this [link](https://docs.openstack.org/keystone/latest/).

#### Optional requirements

- Persistence of data by time series:  

*DrivingApp Service* provides the functionality to obtain the location data of a user in a specific area. To implement this functionality, it is necessary to deploy the *FIWARE QuantumLeap API* and configure *DrivingApp Service* to establish a connection with the SGBD *CrateDB*. You can get more information about the deployment and use of the *QuantumLeap API* in the following [link](https://quantumleap.readthedocs.io/en/latest/).

#### Installation

1.- Download the source code of the web service from its official repository on GitHub using the command:
```sh
$ git clone https://github.com/smartsdkCenidet/DrivingApp-service.git
```

2.- Install the npm modules required by the web services, using the following command within the project folder:
```sh
$ npm install
```

Optionally, you can use yarn to install these same modules quickly, using the command: 
```sh
$ yarn install 
```

#### Configuration

The configuration file for *DrivingApp Service* is `config.js`, this file is located inside the `config/` folder of the project. You must configure this file with the *URLs* of the services that interact with *DrivingApp Service*, as well as the user and password used in the project database. This is an example of the `config.js` file.

```json
exports.mysql = {
    host : 'URL', // MySQL Host
    db : 'databasename', //Database name
    user : 'databaseuser', // Database User
    password : '*******' // Database Password
  }
exports.context = "URL" // Orion URL
exports.keyrock = "URL" //KeyRock URL
exports.crate = "URL"; // CrateDB Host
```

Next, each of the parameters of the `config.js` file is described in detail: 

- **exports.mysql**: JSON object that contains the parameters for the connection to the *MariaDB* database. The connection is performed using the npm module *Sequelize*. The data used by *Sequelize* to establish the connection with the database are the following:
  * **host**: URL where MariaDB is located.
  * **db**: Name of the database.
  * **user**: User name that has the privileges to READ, EDIT, CREATE and DELETE data in the specified database.
  * **password**: Access password for the specified username.

The connection between *DrivingApp Service* and *MariaDB* is done by default through port 3306, if you want to modify the configuration of *Sequelize*  edit the file `DataModelsAPI/db/ sequelize.js`. For more information consult the *Sequelize* documentation on this [link] (http://docs.sequelizejs.com/).

- **exports.context**: The variable **context** must contain the URL of the Orion ContextBroker instance used. This URL must include the HTTP or HTTPS protocol so that *DrivingApp Service* can connect to the Orion ContextBroker, as well as the version of the NGSI API used. An URL example of an Orion ContextBroker instance is: [http://35.185.120.11:1026/v2](http://35.185.120.11:1026/v2)

The connection between DrivingApp Service and the Orion ContextBroker is established through the JavaScript NGSI library, you can check the official documentation of this library on this [link](https://ngsi-js-library.readthedocs.io/en/latest/).

- **exports.keyrock**: The variable **keyrock** refers to the URL of the authentication service used: this can be *IDM-Keyrock of FIWARE* or *Keystone of Openstack*. *DrivingApp Service* uses this authentication service to control the access of the users in the mobile application *DrivingApp*. You can check in this [link](https://developer.openstack.org/api-ref/identity/v3/index.html) the documentation of Identity API v3, implemented in the IDM-KeyRock and KeyStone.

*IDM - KeyRock* minor versions to 7 use port 5000 with a *Keystone version of Openstack*. In addition, the Keystone service of OpenStack uses port 35357 by default. You should consider these port numbers when configuring the selected service in *DrivingApp Service*, and thus avoid confusion between both services.

#### Optional Configurations

- **exports.crate**: The variable **crate** specifies the URL of the time series database *CrateDB*. By default *CrateDB* uses port 4200 to make the connection to the database.

*DrivingApp Service* uses the npm module called **node-crate** to make the connection with *CrateDB* and consult the data stored in the database. You can check the **node-crate** documentation in the following [link](https://www.npmjs.com/package/node-crate).

#### DrivingApp Service deployment 

The deployment of DrivingApp Service can be done in three ways: local, as a daemon and with a docker image. Below are described each of these options.

##### Local deployment

DrivingApp Service can be executed using npm or yarn as detailed below:

- To run the DrivingApp Service using npm, type the following command in the console, inside the service folder:
```sh
$ npm run start 
```
- To run DrivingApp Service using yarn, type the following command in the console, inside the service folder:
```sh
$ yarn start
```

##### Deployment as a demon 

DrivingApp Service can also be executed as a daemon, using the npm module called **forever** as described below:

1.- Install **forever** in the system globally, with the following comand.Thus the **forever** package can be used as a terminal command.
```sh
$ sudo npm install -g forever 
```

2.- Run the main file of the project inside the service folder, with the command: 
```sh
$ sudo forever start server.js
```

To stop *DrivingApp Service* use the following command to identify the id of the process that  **forever** assigned to the service.
```sh 
$ forever list 
```

Then use the following command (followed by the process id) to stop the process.
```sh
$ forever stop <id> 
```

##### Docker deployment

##### Requeriments

- **Docker**: For more information about Docker and its installation consult the following [link](https://docs.docker.com/cs-engine/1.12/).

The official Docker image of *DrivingApp Service* is **cenidetiot/drivingapp-service** and the official repository **cenidetiot** is in **DockerHub**, in this [link](https://hub.docker.com/r/cenidetiot/drivingapp-service/).

##### Environment variables

The environment variables of the docker image of DrivingApp Service are replaced with the data of the services and DBMS used by the DrivingApp Service.
The variables that start with **MYSQL _** refer to the mysql variable in the `config.js` file.

- **MYSQL_HOST**: URL where the DBMS MariaDB is installed.
- **MYSQL_DB**: Name of the database.
- **MYSQL_USER**: User name that has the privileges to READ, EDIT, CREATE and DELETE data in the specified database.
- **MYSQL_PASSWORD**: Password to access the specified username.
- **ORION**: Refers to the context variable of the `config.js` file.
- **KEYROCK**: Refers to the keyrock variable in the `config.js` file.
- **CRATEDB**: Refers to the crate variable in the `config.js` file.

##### Execution 

The Docker image of DrivingApp Service runs by default in the port 4005, the command to execute the image is:
```sh
$ docker run -p 4005:4005 --env="MYSQL_HOST=<MYSQL_HOST>" --env="MYSQL_DB=<MYSQL_DB_NAME>" \ --env="MYSQL_USER=<MYSQL_AUTORIZED_USER>" --env="MYSQL_PASSWORD=<MYSQL_PASSWORD>" \  --env="CRATEDB=<CRATEDB_HOST>" --env="ORION=<ORION_CONTEXT_BROKER_URL>"  \ cenidetiot/drivingapp-service
```

### Notifications Service

#### Requeriments

- **Software de Control de versiones Git**, puede consultar la documentación de Git en el siguiente [enlace](https://git-scm.com/)
- **Python** versión 2.7.X, para instalar Python en su sistema operativo consulte el siguiente [enlace](https://www.python.org/downloads/release/python-2715/)
- Manejador de paquetes pip para Python, para instalar este paquete consulta el siguiente [enlace]( https://pip.pypa.io/en/stable/installing/)
- Servicio web DrivingApp Service, consulta el repositorio oficial de este servicio en el siguiente [enlace](https://github.com/smartsdkCenidet/smartsecurity-web-service.)

#### Installation

1. Descargar el código de Notifications Service desde el repositorio oficial con el comando: 
```sh
$ git clone https://github.com/smartsdkCenidet/Notifications-service.git
```
2. Instalar los requerimientos del servicio con el comando: 
```sh
$ pip install -r requirements.txt
```

#### Configuration

El archivo de configuración de Notifications Service es config.py. Este archivo está en la carpeta raíz del proyecto y contiene los parámetros de configuración necesarios para que el proyecto funcione. El archivo config.py especifica los siguientes parámetros: 

> smart = "https://smartsecurity-webservice.herokuapp.com"  
fcm = "*******"  
username = 'daniel'  
password = "sm2"

- **smart**: El atributo smart contiene la URL de DrivingApp Service. El servicio Notifications Service utiliza DrvingApp Service para consumir los datos de zonas y dispositivos registrados. Recuerde que DrivingApp Service utiliza por defecto el puerto 4005.
- **fcm**: El atributo fcm contiene el código de la aplicación configurada en Firebase en esta [sección](../userManual/configurations#configuracion-fcm). Para  obtener el código de un proyecto Firebase siga los pasos siguientes.

1.- Dentro de la consola del proyecto en Firebase, seleccione el símbolo del engrane en la sección **Project Overview** y  en el menú emergente de click en **Configuración del Proyecto**.
![FCM key Server 1](./img/FCMkeyServer1.png)

2.- Ingrese a la sección de **Mensajería en la nube**.
![FCM key Server 2](./img/FCMkeyServer2.png)

3.- Copie la clave del servidor y agregue esta clave a la variable fcm del archivo config.py 
![FCM key Server 3](./img/FCMkeyServer3.png)

#### Optional Configuration

Atributos **username** y **password**: Estos atributos son utilizados para suscribir una aplicación web a las notificaciones del servicio Notifications Service. Para recibir las notificaciones de alertas en una aplicación web, configure estos parámetros por medio de web sockets.

#### Creating Alert Subscription in the Orion ContextBroker

El *Orion ContextBroker* utiliza suscripciones para notificar a aplicaciones o servicios de terceros cambios en las entidades de contexto. Notifications Service se suscribe al Orion ContextBroker para recibir notificaciones sobre cambios en las entidades de alerta, o la creación de nuevas entidades de alerta. Para conocer más acerca de la creación y administración de Suscripciones NGSIv2 en el Orion ContextBroker, consulte el siguiente [enlace](https://fiware-orion.readthedocs.io/en/master/user/walkthrough_apiv2/index.html#subscriptions) 
La suscripción de *Notifications Service* al Orion ContextBroker tiene como objetivo obtener los datos de las entidades de tipo **Alert** que sean actualizadas o creadas. *Notifications Service* recibe los datos de la entidad de alerta en formato `KeyValues`, para más información acerca de este formato consulte este [enlace]( http://fiware.github.io/specifications/ngsiv2/stable/), en la sección **Subscriptions** atributo **attrsFormat**

Ejemplo de la suscripción de Alerta para Notifications Service.

```json
{
    "description": "Alert subscription",
    "subject": {
     "entities": [
        {	
          "idPattern": ".*", 
 "type": "Alert" 
        }
      ],
      "condition": {
        "attrs": [
          "id",
          "type",
          "category",
          "subCategory",
          "location",
          "dateObserved",
          "description",
          "alertSource",
          "data",
          "severity"
        ]
      }
    },
    "notification": {
      "http": {
        "url": "http://10.0.0.7:8001/notify"
      },
      "attrs": [
        "id",
          "type",
          "category",
          "subCategory",
          "location",
          "dateObserved",
          "description",
          "alertSource",
          "data",
          "severity"
      ],
      "attrsFormat":"keyValues"
    },
    "expires": "2040-01-01T14:00:00.00Z",
    "throttling": 5
}
```

Entre los atributos destacables de esta subscripción se encuentran: 

- **entities**: Este atributo tiene como valor un array que especifica mediante los atributos id y type, las entidades que estarán suscritas a la aplicación o servicio. Se puede utilizar una suscripción para más de un tipo de entidad. En la suscripción de ejemplo se especifica que las entidades suscritas a Notifications Service son todas las entidades con **type: Alert**. Los atributos de las entidades de alerta deben cumplir con el modelo de datos **Alert** de FIWARE. Para conocer la especificación oficial de este modelo, consulta este [enlace](https://github.com/Fiware/dataModels/tree/master/specs/Alert)

Para suscribir Notifications Service a las alertas de la aplicación móvil DrivingApp, el atributo entities debe contener el atributo idPattern con la siguiente expresión regular: **"Alert:Device_Smartphone_.*"**.Así, el Orion ContextBroker enviará las Alertas que inicien con el texto **"Alert:Device_Smartphone_"** en el atributo **id**

- **notification**: Este atributo tiene como valor la URL a la que se enviarán los datos de las alertas que sean creadas o actualizadas. Notifications Service utiliza la ruta **/notify** para recibir las notificaciones de alertas enviadas por el Orion ContextBroker.

- **attrsFormat**: En la suscripción de alertas, este atributo debe tener el valor `keyValues`, para que Notifications Service pueda interpretar los datos de alerta enviados por el Orion ContextBroker.

#### Deployment

El despliegue de Notifications Service puede realizarse de dos maneras: local y con una imagen 
docker. A continuación se detallan cada una de estas opciones.

##### Local deployment

- Utilizando Python

Para ejecutar NotificationsService con Python utilice el siguiente comando que  ejecuta el archivo principal del proyecto:  
```sh
$ python run.py
```

- Utilizando Flask

Para ejecutar NotificationsService con Flask realice los pasos siguientes:

1.- Exporte como variable de entorno el nombre del archivo principal del proyecto,  con el comando: 
```sh
$ export FLASK_APP=run.py 
```
Puede consultar la documentación oficial de Flask en el siguiente [enlace](http://flask.pocoo.org/) 

2.- Ejecutar el servicio utilizando el siguiente comando: 
```sh
$ flask run
```

- Utilizando Gunicorn

Ejecuta el siguiente comando: 
```sh
$ gunicorn app:app 
```
Puede consultar la documentación oficial de gunicorn en el siguiente [enlace](https://gunicorn.org/#docs)

##### Docker deployment

##### Requeriments

- **Docker**: Para más información acerca de Docker y su instalación consulta el siguiente [enlace](https://docs.docker.com/cs-engine/1.12/).

La imagen oficial Notifications Service se llama **cenidetiot/notifications-service** y se encuentra el repositorio oficial **cenidetiot** en **DockerHub**, en el siguiente [enlace]( https://hub.docker.com/r/cenidetiot/notifications-service/)

##### Environment variables 

Las variables de entorno de la imagen Docker de NotificationsService  se reemplazan con los datos de la configuración del servicio. 

- **SMART_SERVICE**: Hace referencia a la variable smart del archivo `config.py`.
- **FCM_SERVER_TOKEN**: Hace referencia a la variable fcm del archivo `config.py`.
- **PASSWORD**: Hace referencia a la variable password del archivo `config.py`.
- **USER_NAME**: Hace referencia a la variable username del archivo `config.py`.

##### Execution

La imagen Docker de NotificationsService utiliza por defecto el puerto 3001, el comando  para ejecutar la imagen es el siguiente: 

```sh
$ docker run -ti --env="SMART_SERVICE=<DRIVINGAPP_SERVICE>" \ --env="FCM_SERVER_TOKEN=<FCM_SERVER_TOKEN>" --env="PASSWORD=<USER_PASSWORD>" \ --env="USER_NAME=<USER_NAME>" -p 3001:3001 cenidetiot/notifications-service
```

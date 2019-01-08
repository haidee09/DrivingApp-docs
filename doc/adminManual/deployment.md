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

- **Git Version Control Software**, you can check the Git documentation in the following [link](https://git-scm.com/).
- **Python** version 2.7.X, to install Python in your operating system see the following [link](https://www.python.org/downloads/release/python-2715/).
- **Pip package manager for Python**, to install this package visit the following [link](https://pip.pypa.io/en/stable/installing/).
- **DrivingApp Service - web service**, check the official repository of this service in the following [link](https://github.com/smartsdkCenidet/smartsecurity-web-service).

#### Installation

1. Download the Notifications Service code from the official repository with the command:
```sh
$ git clone https://github.com/smartsdkCenidet/Notifications-service.git
```
2. Install the service requirements with the command: 
```sh
$ pip install -r requirements.txt
```

#### Configuration

The Notifications Service configuration file is config.py. This file is in the root folder of the project and contains the configuration parameters necessary for the project to work. The config.py file specifies the following parameters:

> smart = "https://smartsecurity-webservice.herokuapp.com"  
fcm = "*******"  
username = 'daniel'  
password = "sm2"

- **smart**: The smart attribute contains the DrivingApp Service URL. Notifications Service uses DrvingApp Service to consume data from registered zones and devices. Remember that the DrivingApp Service uses port 4005 by default.
- **fcm**: The fcm attribute contains the application code configured in Firebase in this [section](../userManual/configurations#configuration-fcm). To obtain the code of a Firebase project, follow the steps below.

1.- In the project console on Firebase, select the gear symbol in the **Project Overview** section and in the pop-up menu click on **Project Configuration**.
![FCM key Server 1](./img/FCMkeyServer1.png)

2.- Enter to the **Cloud Messaging** section. 
![FCM key Server 2](./img/FCMkeyServer2.png)

3.- Copy the server key and add this key to the fcm variable in the config.py file.
![FCM key Server 3](./img/FCMkeyServer3.png)

#### Optional Configuration

Attributes **username** and **password** in config.py file: These attributes are used to subscribe a web application to the notifications of the service Notifications Service. To receive alert notifications in a web application, configure these parameters through web sockets.

#### Creating Alert Subscription in the Orion ContextBroker

The *Orion ContextBroker* uses subscriptions to notify third-party applications or services of changes in context entities. Notifications Service subscribes to the Orion ContextBroker to receive notifications about changes in alert entities, or the creation of new alert entities. To learn more about the creation and administration of NGSIv2 Subscriptions in the Orion ContextBroker, visit the following [link](https://fiware-orion.readthedocs.io/en/master/user/walkthrough_apiv2/index.html#subscriptions).

The subscription of *Notifications Service* to the Orion ContextBroker aims to obtain the data of the entities of type **Alert** that are updated or created. *Notifications Service* receives the data from the alert entity in `KeyValues` format, for more information about this format consult this [link](http://fiware.github.io/specifications/ngsiv2/stable/), in the section **Subscriptions** attribute **attrsFormat**.

Example of the Alert subscription for Notifications Service.

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

Among the attributes of this subscription are:

- **entities**: This attribute is an array that specifies through the id and type attributes, the entities that will be subscribed to the application or service. A subscription can be used for more than one type of entity. The example subscription specifies that the entities subscribed to the Notifications Service are all entities with **type: Alert**. The attributes of the alert entities must comply with the data model **Alert** of FIWARE. To know more about the official specification of this model, visit this [link](https://github.com/Fiware/dataModels/tree/master/specs/Alert).

To subscribe Notifications Service to the alerts of DrivingApp, the entities attribute must contain the idPattern attribute with the following regular expression: **"Alert: Device_Smartphone _.*"**. Thus, the Orion ContextBroker will send Alerts that begin with the text **"Alert: Device_Smartphone _"** in the attribute **id**.

- **notification**: This attribute contains the URL of the service to which will be sent the data of the alerts created or updated. Notifications Service uses the **/notify** path to receive notifications of alerts sent by the Orion ContextBroker.

- **attrsFormat**: In the subscription of alerts, this attribute must have the value `keyValues`, so that Notifications Service can interpret the alert data sent by the Orion ContextBroker.

#### Deployment

The deployment of Notifications Service can be done in two ways: local and with an docker image. Below are described each of these options.

##### Local deployment

- Using Python

To run Notifications Service with Python, use the following command that executes the main file of the project:
```sh
$ python run.py
```

- Using Flask

To run NotificationsService with Flask, perform the following steps. You can check the official Flask documentation in the following [link](http://flask.pocoo.org/)

1.- Export the name of the project's main file as an environment variable, with the command:
```sh
$ export FLASK_APP=run.py 
```

2.- Execute the service using the following command:
```sh
$ flask run
```

- Using Gunicorn

Execute the following command.You can check the official documentation of gunicorn in the following [link](https://gunicorn.org/#docs).
```sh
$ gunicorn app:app 
```

##### Docker deployment

##### Requeriments

- **Docker**: For more information about Docker and its installation consult the following [link](https://docs.docker.com/cs-engine/1.12/).

The docker image official of Notifications Service image is **cenidetiot/notifications-service** and the official repository **cenidetiot** is in **DockerHub**, in this [link](https://hub.docker.com/r/cenidetiot/notifications-service/).

##### Environment variables 

The environment variables in the Docker image of NotificationsService are replaced with the data of the service configuration.

- **SMART_SERVICE**: Refers to the smart variable in the `config.py` file.
- **FCM_SERVER_TOKEN**: Refers to the fcm variable in the `config.py` file.
- **PASSWORD**: Refers to the password variable in the `config.py` file.
- **USER_NAME**: Refers to the username variable in the `config.py` file.

##### Execution

The Docker image of NotificationsService uses port 3001 by default, the command to execute the image is:
```sh
$ docker run -ti --env="SMART_SERVICE=<DRIVINGAPP_SERVICE>" \ --env="FCM_SERVER_TOKEN=<FCM_SERVER_TOKEN>" --env="PASSWORD=<USER_PASSWORD>" \ --env="USER_NAME=<USER_NAME>" -p 3001:3001 cenidetiot/notifications-service
```

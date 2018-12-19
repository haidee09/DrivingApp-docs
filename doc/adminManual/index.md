## Servicios Web

Los servicios web que utiliza la aplicación DrivingApp son: *DrivingApp Service* y *Notifications Service*, los cuales se describen a continuación.

### DrivingApp Service

*DrivingApp Service* es un servicio web que manipula los modelos de datos públicos y privados de la aplicación móvil y los servicios de consulta. Este servicio es una implementación de API REST creada con el entorno NodeJS, y permite administrar la información proporcionada por tres fuentes de datos: el Orion ContextBroker de FIWARE, que se utiliza para administrar la información de contexto; el SGBD MariaDB, que se utiliza para almacenar la información de modelos de datos; y por último CrateDB que es utilizado por la API QuantumLeap de FIWARE para almacenar información de series de tiempo. El repositorio de *DrivingApp Service* lo puedes consultar en este [enlace]( https://github.com/smartsdkCenidet/DrivingApp-service).

*DrivingApp Service* está compuesto por 1 ruta raíz y 3 APIs con rutas específicas. Estas rutas definen lo siguiente.

##### Ruta raíz 

- **/**: Este es la ruta principal del servicio web DrivingApp Service. La solicitud a esta ruta raíz comprueba que el despliegue del servicio se ha realizado de manera exitosa. El servicio web responde a esta solicitud con el siguiente mensaje JSON:
```json
{ message: 'Welcome to Smart Security Web Service' }
```

##### APIs

- **/api**: Esta es la API RESTFul que administra las entidades de datos públicas y privadas que utiliza la aplicación DrivingApp. La API REST administra las operaciones CRUD de las entidades de datos: zone, parking, road, road segment deviceTokens y user; y esta información se almacena en la base de datos smartsecurity a través el gestor MariaDB. *DrivingApp Service* responde a esta solicitud con el siguiente  mensaje JSON:
```json
{ message: 'Welcome to DataModels API REST' }
```

- **/service**: Este API administra los servicios de consultas especiales para los modelos de datos Alerta y Device, implementando los servicios del Orion ContextBroker de FIWARE. El servicio web responde a esta solicitud con el siguiente mensaje JSON:
```json
{ message: 'Welcome to Special Services API' }
```

- **/crate**: Este API administra la ruta para consultar la localización de los dispositivos de usuarios en una fecha y hora específicos, utilizando los datos almacenados en CrateDB por medio de la API QuantumLeap de FIWARE. La respuesta a esta solicitud es el siguiente mensaje JSON:
```json
{ message: 'Welcome to CrateDB-QuantumLeap API' }
```

En este [enlace](https://drivingappservice.docs.apiary.io/) puedes consultar la especificación de los modelos de datos utilizados en *DrivingApp Service*.

### Notifications Service

*Notifications Service* es un servicio web que manipula la información de las entidades de Alerta, obtenidas por medio de la notificación de una suscripción creada en el Orion ContextBroker. Cuando este servicio recibe una entidad alerta enviada por el Orion, la replica a los dispositivos móviles que utilizan DrivingApp, utilizando los servicios de Firebase Cloud Messaging. El repositorio de Notifications Service lo puedes encontrar en este [enlace](https://github.com/smartsdkCenidet/Notifications-service) 

Notifications Service está compuesto por dos rutas descritas a continuación.

##### Ruta raíz

- **/**: Esta es la ruta por defecto de Notifications Service. La solicitud a esta ruta comprueba que el despliegue del servicio se ha realizado de manera exitosa. El servicio web responde a esta solicitud con el siguiente mensaje.

> **SmartSecurity Notifications is running....**
© Cenidet 2018

##### Ruta de notificación

- **/notify**: Esta ruta es utilizada para generar las notificaciones de alerta que se envían a los dispositivos móviles. El servicio lleva a cabo las siguientes funciones en esta ruta:

1.	Recibe la entidad de  alerta.
2.	Obtiene la localización de la alerta
3.	Obtiene las zonas registradas en DrivingApp Service
4.	Determina la zona en la que sucedió la alerta
5.	Obtiene de DrivingApp Service los dispositivos en la zona de la alerta 
6.	Obtiene de DrivingApp Service los dispositivos cercanos a la alerta
7.	Verifica que los dispositivos cercanos y los que están en la zona no se repitan
8.	Crea la lista de dispositivos finales
9.	Obtiene de DrivingApp Service  los tokens de los dispositivos  finales
10.	Envía la notificación a cada uno de los dispositivos 

La ruta **/notify** recibe los datos de las entidades de alerta enviadas por  el Orion ContextBroker a través de una petición POST. El servicio recibe la alerta y extrae la información relevante para enviar la notificación de la alerta a los dispositivos que tienen la aplicación DrivingApp instalada. La entidad de alerta que recibe el servicio debe ser un objeto JSON con el siguiente formato: 

```json
{
	“data” : [
		{
            “id”: "Alert:Device_Smartphone_f2751c243d2b4295_1540484159603",
            “type”: "Alert",
            “alertSource”: "Device_Smartphone_f2751c243d2b4295",
            “category”: "security",
            “dateCreated”: "2018-10-25T16:15:59.00Z",
            “dateObserved”: "2018-10-23T16:15:59.999Z",
            “description”: "Alert generated by Simulator",
            “location”: "19.599157972898347,-99.22552046196473",
            “severity”: "high",
            “subCategory”: "speeding",
            “validFrom”: "2018-10-23T16:15:59.999Z",
            “validTo”: "2018-10-23T16:15:59.999Z",  
        }
    ]
} 
```

*Notifications Service* utiliza los servicios de consulta de DrivingApp Service para obtener los datos de las entidades de zonas y realizar el cálculo para determinar la zona en la que se emitió una alerta. Además de obtener los dispositivos que se encuentran en la zona que ocurrió la alerta y los dispositivos que se encuentran a menos de 100 metros de la alerta.



## Pruebas Unitarias de Ejecución de Servicios

Para revisar la ejecución correcta del sistema de DrivingApp siga las instrucciones de cada servicio.

### Orion ContextBroker

Para revisar la ejecución del Orion ContextBroker utilice el siguiente comando en consola:

```sh
$ curl -X GET http://0.0.0.0:1026/version -H 'Accept: application/json'
```

La respuesta del Orion debe retornar **status: 200 OK**

### API QuantumLeap

Para revisar la ejecución de la API de QuantumLeap utilice el siguiente comando en consola:
```sh
$ curl -X GET http://0.0.0.0:8668/v2/version -H 'Accept: application/json'
```

La respuesta de la API QuantumLeap debe retornar **status: 200 OK**

### DrivingApp Service

Verifica la ejecución de cada una de las rutas API de DrivingApp Service, utilizando los siguientes comandos en consola:

- Para revisar la ruta  /api utilice el siguiente comando:

```sh
$ curl -X GET http://0.0.0.0:4005/api -H 'Accept: application/json'
```

La ruta /api debe retornar como respuesta el siguiente mensaje:
```json
{ message: 'Welcome to DataModels API REST' }
```

- Para revisar la ruta /service utilice el siguiente comando:

```sh
$ curl -X GET http://0.0.0.0:4005/service -H 'Accept: application/json'
```

La ruta /service debe retornar como respuesta el siguiente mensaje:
```json
{ message: 'Welcome to Special Services API' }
```

- Para revisar la ruta /create utilice el siguiente comando:

```sh
$ curl -X GET http://0.0.0.0:4005/crate -H 'Accept: application/json'
```

La ruta /crate debe retornar como respuesta el siguien mensaje:
```json
{ message: 'Welcome to CrateDB-QuantumLeap API' }
```

### Notifications Service

- Para revisar la ejecución de Notifications Service utilice el siguiente comando en consola: 

```sh
$ curl -X GET http://0.0.0.0:3001/
```

Notifications Service debe retornar como respuesta el mensaje siguiente en el navegador:
    
> SmartSecurity Notifications is running....  
> © Cenidet 2018

***NOTA***: Observe que la respuesta de Notifications Service retorna la cabecera `Content-Type`: `text/html`, a diferencia de las APIs de DrivingApp Service que retornan como respuesta la cabecera `Content-Type`: `application/json`.

### IDM- KEYROCK /KEYSTONE

- Para revisar la ejecución del IDM-KeyRock o KeyStone utilice el siguiente comando en consola:

```sh
$ curl -X GET http://0.0.0.0:5000/ -H 'Accept: application/json' -H 'X-Auth-token: ADMIN'
```

El IDM- KeyRock o KeyStone debe retornar como respuesta:

```json
{
    "version": {
        "status": "stable",
        "updated": "2013-03-06T00:00:00Z",
        "media-types": [
        {
            "base": "application/json",
            "type": "application/vnd.openstack.identity-v3+json"
        },
  	    {
            "base": "application/xml",
            "type": "application/vnd.openstack.identity-v3+xml"
        }
        ],
        "id": "v3.0",
        "links": [
  		{
            "href": "http://localhost:5000/v3/",
            "rel": "self"
        }
        ],
    }
}
```

## Creación de Suscripciones 

Es necesario crear algunas suscripciones en el Orion ContextBroker, para que el sistema de DrivingApp funcione correctamente. Con estas suscripciones los componentes Orion ContextBroker, QuantumLeap y Notifications Service pueden comunicarse entre sí. Las suscripciones que deben crearse en el Orion ContextBroker se encuentran en la carpeta Subscriptions del proyecto DrivingApp-docker. Para registrar estas suscripciones en el Orion ContextBroker utilice los siguientes comandos:

1.- Para crear la suscripción de la entidad Device a QuantumLeap utilice el siguiente comando en consola:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/subscriptions -d @Subscriptions/DeviceToQL.json --header "Content-Type: application/json"
```

2.- Para crear la suscripción de la entidad Alert a QuantumLeap utilice el siguiente comando en consola:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/subscriptions -d @Subscriptions/AlertToQL.json --header "Content-Type: application/json"
```

3.- Para crear la suscripción de la entidad Device a Notifications Service utilice el siguiente comando en consola:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/subscriptions -d @Subscriptions/AlertToNotifications.json --header "Content-Type: application/json"
```

***NOTA***: La creación de estas suscripciones son requeridas para que el sistema funcione correctamente, de lo contrario algunas funciones no estarán disponibles en la aplicación DrivingApp.

## [Creación de entidades para la Integración de Servicios](#creacion-de-entidades-para-la-integracion-de-servicios)

La creación de las siguientes entidades le permiten verificar que los servicios se comunican correctamente entre ellos, creelas el orden que se indica:

1.- Crear una entidad de prueba tipo Device en el Orion ContextBroker utilizando el siguiente comando:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/entities -d @"Orion Entities/Device.json" --header "Content-Type: application/json"
```

2.- Crear una entidad de prueba tipo DeviceToken en DrivingApp Service utilizando el siguiente comando:

```sh
$ curl -iX POST http://0.0.0.0:4005/api/device/token -d @"Private Entities/DeviceToken.json" --header "Content-Type: application/json"  
```

3.- Crear una entidad de prueba tipo Zone en DrivingApp Service utilizando el siguiente comando:

```sh
$ curl -iX POST http://0.0.0.0:4005/api/zone  -d @"Private Entities/Zone.json" --header "Content-Type: application/json"
```

4.- Crear una entidad de prueba tipo User en DrivingApp Service utilizando el siguiente comando:

```sh
$ curl -iX POST http://0.0.0.0:4005/api/user  -d @"Private Entities/User.json" --header "Content-Type: application/json"
```

5.- Crear una entidad de prueba tipo Alert en el Orion Context Broker utilizando el siguiente comando:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/entities -d @"Orion Entities/Alert.json" --header "Content-Type: application/json"
```

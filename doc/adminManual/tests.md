## Tests services execution 

To review the correct execution of the DrivingApp system, execute the following commands per service:

### Orion ContextBroker

To review the execution of the Orion ContextBroker use the following console command:

```sh
$ curl -X GET http://0.0.0.0:1026/version -H 'Accept: application/json'
```

The Orion ContextBroker must return **status: 200 OK**

### API QuantumLeap

To review the execution of the QuantumLeap API use the following console command:
```sh
$ curl -X GET http://0.0.0.0:8668/v2/version -H 'Accept: application/json'
```
The QuantumLeap API must return **status: 200 OK**

### DrivingApp Service

Verify the execution of every endpoint of DrivingApp Service API, using the following console commands:

- To check the endpoint /api use the following command: 

```sh
$ curl -X GET http://0.0.0.0:4005/api -H 'Accept: application/json'
```

The endpoint /api must return the following message: 

```json
{ message: 'Welcome to DataModels API REST' }
```

- To check the endpoint /service use the following command:

```sh
$ curl -X GET http://0.0.0.0:4005/service -H 'Accept: application/json'
```

The endpoint /service must return the following message: 

```json
{ message: 'Welcome to Special Services API' }
```

- To check the endpoint /create use the following command: 

```sh
$ curl -X GET http://0.0.0.0:4005/crate -H 'Accept: application/json'
```

The endpoint /crate must return the following message: 

```json
{ message: 'Welcome to CrateDB-QuantumLeap API' }
```

### Notifications Service

- To review the running of Notifications Service use the following console command:

```sh
$ curl -X GET http://0.0.0.0:3001/
```

Notifications Service must return the following message in the browser as a response:
    
> SmartSecurity Notifications is running....  
> © Cenidet 2018

***NOTA***: Note that the response of Notifications Service returns the header `Content-Type` : `text/html`, unlike the APIs of DrivingApp Service that return the header `Content-Type`: `application/json`

### IDM- KEYROCK /KEYSTONE

- To review the running of IDM-KeyRock or KeyStone, use the following console command: 
```sh
$ curl -X GET http://0.0.0.0:5000/ -H 'Accept: application/json' -H 'X-Auth-token: ADMIN'
```

The response of IDM- KeyRock o KeyStone must be the following json:

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

## Subscriptions Creation  

It is necessary to create some subscriptions in the Orion ContextBroke, so that the DrivingApp system works correctly. With these subscriptions the Orion ContextBroker, QuantumLeap and Notifications Service components can communicate with each other. The subscriptions that must be created in the Orion ContextBroker are in the Subscriptions folder of the DrivingApp-docker project. To register these subscriptions in the Orion ContextBroker use the following commands:

1.- To create the subscription of the Device entity to QuantumLeap, use the following console command:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/subscriptions -d @Subscriptions/DeviceToQL.json --header "Content-Type: application/json"
```

2.- To create the subscription of the Alert entity to QuantumLeap, use the following console command: 

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/subscriptions -d @Subscriptions/AlertToQL.json --header "Content-Type: application/json"
```

3.- To create the subscription of the Device entity to Notifications Service use the following console command:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/subscriptions -d @Subscriptions/AlertToNotifications.json --header "Content-Type: application/json"
```

***NOTA***: The creation of these subscriptions is necessary for the system to work properly, otherwise some functions will not be available in the DrivingApp application. 

## [Services integration creating entities](#services-integration-creating-entities)

The creation of the following entities allow you to verify the services communicate correctly among them, it is necessary to create the following test entities in the order indicated:

1.- Create a Device entity in the Orion ContextBroker using the following command: 

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/entities -d @"Orion Entities/Device.json" --header "Content-Type: application/json"
```

2.- Create a DeviceToken entity in DrivingApp Service using the following command: 

```sh
$ curl -iX POST http://0.0.0.0:4005/api/device/token -d @"Private Entities/DeviceToken.json" --header "Content-Type: application/json"  
```

3.- Create a Zone entity in DrivingApp Service using the following command:

```sh
$ curl -iX POST http://0.0.0.0:4005/api/zone  -d @"Private Entities/Zone.json" --header "Content-Type: application/json"
```

4.- Create a User entity in DrivingApp Service using the following command:

```sh
$ curl -iX POST http://0.0.0.0:4005/api/user  -d @"Private Entities/User.json" --header "Content-Type: application/json"
```

5.- Create an Alert entity in the Orion Context Broker using the following command:

```sh
$ curl -iX POST http://0.0.0.0:1026/v2/entities -d @"Orion Entities/Alert.json" --header "Content-Type: application/json"
```

## DrivingApp System Administration

This Guide provides information about how to administer the DrivingApp application system. The following describes the administration applications that can be used with DrivingApp, in addition to the administration of the application databases.

### ViVA

ViVA is a Video Surveillance application that aims to support the security guard to prevent situations of risk and consequently improve the quality of life of the people who live in the monitored area. The ViVA application focuses on detecting and analyzing risk situations, such as: theft, access control, people detection, fights, crowd analysis, etc., through the combination of video cameras and sensors, both indoors and outdoors scenarios. For example, parking lots and buildings. You can check the documentation of ViVA at the following [link](https://video-surveillance-application.readthedocs.io/en/latest/).

ViVA includes modules for data management of zones, parking lots and streets; these modules are necessary for the DrivingApp application to work properly. In addition, ViVA has a module to consult the location of the users of DrivingApp that are, or who were within any of the registered zones. You can access the ViVA web application in [this](https://viva-smartsdk.duckdns.org/) link.

### DrivingApp Administration Application

In order to offer a lightweight tool that includes area management modules and user location consultation, a simple administration application for DrivingApp was developed using the Web2py framework. This administration application contains the modules that ViVA includes to manipulate the information of zones, parking lots and streets, as well as to consult the location of the users of DrivingApp. The source code of this application is on this [repository](https://github.com/smartsdkCenidet/SimpleAdmin).

#### Requeriments

- **Git version control system**, you can check the official documentation of Git in the following [link](https://git-scm.com/).
- **Python 2.7.X**, you can check how to install Python on your operating system in the following [link](https://www.python.org/downloads/release/python-2715/).

#### Installation and running

1.- Download the web2py project with the following git command: 
```sh
$ git clone --recursive https://github.com/web2py/web2py.git
```
2.-	Download the SimpleAdmin project inside the /applications folder of the web2py project.

Use the following command to move to the applications folder:
```sh
$ cd applications
```

Run the following command to download the SimpleAdmin project inside the applications folder:
```sh
$ git clone https://github.com/smartsdkCenidet/SimpleAdmin.git
```

3.-	Finally, run the file web2py.py, this file is in the main folder of the web2py project .

Remember to change the folder with the command:
```sh
$ cd ..
```

Then, use the following command to run the web2py application: 
```sh
$ python web2py.py
```

This command displays a window where it is necessary to configure a password for the server, as shown in the following image:

![Web2py admin](./img/web2pyAdmin.png)

After typing the password, click on the Start Server button and the server will start running. Now you can access the SimpleAdmin application at the following address:[http://127.0.0.1:8000/appmapasWeb2py/default/index](http://127.0.0.1:8000/appmapasWeb2py/default/index).

#### Configuration

The configuration of the application must be updated by changing the address of the DrivingApp Service. This configuration is updated by modifying the smartService variable in the default.py file located in the controllers folder of the application. Example:

> smartService = T('http://0.0.0.0:4005')

#### Manual of the administration app of DrivingApp

The following manual describes the functions of each view of the SimpleAdmin application, for the administration of the DrivingApp system.

#### Map Tools in SimpleAdmin App 

The tools of the maps in the administration application are the following:

- **Map in full screen**: this functionality allows you to see the map to the size of the screen. Activate this option by pressing the box button on the map tools. To exit full screen you can use the Esc key on your keyboard or the same box button of the map tools.
- **Satellite View**: this functionality allows you to see the map in satellite view. You can activate this option by selecting the SateliteMap option in the upper right part of the map.
- **Streets View**: this functionality allows you to see the map with streets view. You can activate this option by selecting the StreetsMap option at the upper right part of the map. This option is selected by default on the map.
- **Zoom**: the + and - tools allow you to zoom in or zoom out the map area as needed.
- **Drawing tools**: Among the drawing tools are, the tool to delimit a new area, polygon; the tool to delimit street segments, polyline; and the tool to eliminate the marked area, the trash can. The edit tool is disabled in this version of the system.

#### Zones administration in the system

The administration of zones in the system consists of two views: the list of zones and the registration of new zones.

#### List of zones

The view of list of zones presents the relevant information of each zone registered in the application, such as: name, address and description. In addition, each zone record contains a button to remove that record from the list; this record is eliminated logically in the system. In the upper right part of the list, the view shows the **Add new zone** button, which is used to go to the Zone Registration view and create new zones in the system. The following image shows an example of this view.

![Lista de Zonas](./img/zonesList.png)

#### Zones Registration

The zone registration view shows a form for the creation of new zones, in this form you must register the data of the zone as: the name, the address and a description of the zone. It is important that the address of the area is a real address. When you type the address of the area in the text field, press the **Search Address on Map** button to search the address of the area on the map. This search is done using a Google Maps API, centering the map center on the direction of the area. Finally, you must define the area of the zone on the map with the  polygon tool. When you have registered the zone data and marked its delimitation on the map, press the **Save** button to register the new zone in the system.
The following image shows an example of this view.

![Registro de Zonas](./img/zonesForm.png)

#### Parking lots administration in the systema

The administration of parkings in the system consist of two views: the list of parking lots and the registration of new parking lots.

#### Parking lots List 

The view of list of Parking lots presents the relevant information of each parking lot registered in the system as: the name, its description and the name of the parking area. In addition, each parking record contains a button to remove that record from the list; this record is eliminated logically in the system. In the upper right part of the list, the view shows the **Add new parking** button, which redirects to the Parking Registration view to create new parking lots in the system. The following image shows this view.

![Lista de Estacionamientos](./img/parkingsList.png)

#### Parking lot registration

The Parking lots registration view shows a form for the creation of new parking, in this form you must register the parking information such as: the area to which the parking belongs, its category, the name and a description of the parking lot. Finally, you must define the parking area on the map with the polygon tool. Once you have registered the parking information and marked its delimitation on the map, press the **Save** button to register the new parking in the system. The following image shows this view.

![Registro de estacionamiento](./img/parkingsForm.png)

#### Roads and Roads Segments administration in the system

The administration of roads and roads segments in the system consist of three views: the list of roads, the list of roads segments, and the roads and roads segments registration.

#### Roads List

The Roads list view presents the relevant information of each road registered in the system as: the name, its description, and the area responsible for the road. In addition, each road record contains a button to remove that record from the list; this record is eliminated logically in the system. In the upper right part of the roads list, the view shows two buttons: **See roadSegments** and **Add new Road and Segments**. The **See roadSegments** button redirects to the view Road segments list and the **Add new Road and Segments** button redirects the view to create new road and road segments.

![Listado de Calles](./img/roadsList.png)

#### Roads Segments List

The Roads segments list view shows the data of each road segment registered in the system as: the name of the road segment, the name of the road, the direction of the road, the allowed speed and the width of the road in meters. In addition, each road segment record contains a button to remove that record from the list; this record is removed logically from the system. At the top of the list, is shown **Add new Road and Segments** button, which redirects the view to create roads and road segments.

![Listado de Segmentos de Calles](./img/roadSegmentsList.png)

#### Road and Roads Segments registration

The road registration  and the road segment view shows a form for creating new street segments. To register a segment of road, you must select and enter the following data in the view.

1. Select if the road segment belongs to a parking lot or an zone. 
    - If the road segment belongs to a road of an area, select the zone and consequently the name of the road. 
    - If the road segment belongs to a road of a parking lot, select: the zone of the parking, the name of the parking lot and the name of the road. 

2. Enter the name of the road segment, its minimum and maximum speed, the direction of the segment and the width of the segment in meters. 

3. Delimit the segment with the polyline tool. 

4. Press the Save button to record the data of the road segment and its delimitation. 

La following image shows the view of roads segments registration.

![Registro de Road Segments](./img/roadSegmentsForm.png)

If the main road of the segment is not registered in the system, you can create a new road by pressing the **Add** button, this shows a form to register a new road and link the road segment to this road. When registering the road data press the **Save Road** button to store the information in the system and continue with the road segment registration. The following image shows the road registration view.

![Registro de Road](./img/roadsForm.png)

#### Búsqueda de usuarios en zonas

La aplicación de administración incluye un módulo de búsqueda de usuarios. Este módulo tiene la función buscar si un usuario está o estuvo en una zona registrada en una fecha y hora determinadas, además de buscar todos los usuarios que se están dentro de una zona. Estos tres tipos de búsquedas se describen a continuación:

#### 1. Búsqueda de usuario que estuvo en una zona 

La búsqueda de usuario que estuvo en una zona muestra un formulario para ingresar los datos de búsqueda, estos datos son: la zona de búsqueda, el número de teléfono del usuario y,  la fecha y hora de búsqueda. Cuando haya ingresado estos datos presione el botón Consult  para realizar la búsqueda. Si el sistema encuentra el registro del usuario en la zona, fecha y hora indicadas, este muestra la última ubicación del usuario en el mapa.   La imagen siguiente muestra la vista de esta búsqueda.

![Búsqueda de usuario 1](./img/userSearching1.png)

#### 2. Búsqueda de usuario que está en una zona

La búsqueda de usuario que está una zona muestra un formulario para ingresar los datos de la búsqueda, estos datos son: seleccionar la zona de búsqueda e ingresar el número de teléfono del usuario. Cuando haya ingresado esto estos datos presione le botón Consult para realizar la búsqueda. Si el sistema encuentra al usuario en la zona, este muestra en el mapa su ubicación actual. La imagen siguiente muestra la vista de esta búsqueda.

![Búsqueda de usuario 2](./img/userSearching2.png)

#### 3. Búsqueda de usuarios en una zona

La búsqueda de usuarios en una zona muestra un formulario para seleccionar la zona de búsqueda de los usuarios. Cuando haya seleccionado la zona de búsqueda presione el botón Consult. Si el sistema encuentra usuarios dentro de la zona, este muestra en el mapa la ubicación actual de los usuarios. La vista siguiente muestra la imagen de esta búsqueda.

![Búsqueda de Usuario 3](./img/userSearching3.png)

#### Panel de Alertas

El panel de alertas presenta dos tipos de búsquedas de alertas: el historial de alertas y las alertas actuales. Para mostrar la ubicación de las alertas en el mapa seleccione en el formulario la zona y el tipo visualización de alertas.  La opción History Alerts muestra en el mapa la ubicación de las últimas 10 alertas y la opción Current Alerts muestra la ubicación de las alertas del día. Cuando haya seleccionado las opciones en el formulario presione el botón Consult. Si el sistema encuentra alertas con los parámetros seleccionados, este muestra la ubicación de las alertas en el mapa.

![Panel de Alertas](./img/alertsPanel.png)

### Administración de bases de datos 

Los datos de DrivingApp están administrados por tres Sistemas gestores de bases de datos: MariaDB, Mongo DB y CrateDB. La siguiente imagen muestra un diagrama relacional de las entidades. 

Las entidades almacenadas en  MariaDB se muestran en el diagrama en color amarillo, la base de datos administra las entidades en MariaDB se llama smartsdksecurity. Las entidades almacenadas en MongoDB se muestran en el diagrama color verde, la base de datos de estas entidades es administrada por el Orion ContextBroker para almacenar la información de contexto de cada entidad. Las entidades  almacenadas en CrateDB  registran los datos históricos de las entidades administradas por el Orion ContextBroker, estas entidades se muestran en el diagrama en color rojo.

![Modelo Relacional de Base de datos](./img/relationalModelDB.png)

Tablas de la base de datos smartsecurity en MYSQL

- zone: La tabla zone está basada en el modelo de datos [Building]( https://github.com/Fiware/dataModels/tree/master/specs/Building/Building) de FIWARE. 
- offStreetParking: La tabla offStreetParking está basada en el modelo de datos [OffStreetParking](https://github.com/Fiware/dataModels/tree/master/specs/Parking/OffStreetParking) de FIWARE. 
- road: La tabla road está basada en el modelo de datos [Road]( https://github.com/Fiware/dataModels/tree/master/specs/Transportation/Road) de FIWARE. 
se utiliza en la aplicación SmartSecurity para definir las calles de estacionamiento de una organización. También este modelo de datos se utiliza para definir las calles que están dentro del espacio geográfico de la organización utilizando el atributo responsible.
- roadSegment: La tabla roadSegment está basada en el modelo de datos de [RoadSegment]( https://github.com/Fiware/dataModels/tree/master/specs/Transportation/RoadSegment) de FIWARE, este  se utiliza en la aplicación Smart Security para describir las características de los segmentos en los que se puede dividir una calle; además, este modelo proporciona atributos para detallar las propiedades de las líneas o carriles que contiene el segmento de la calle.
- mobileUser: La tabla mobileUser está basada en el modelo de datos User diseñado para el escenario de seguridad inteligente. Este modelo cumple con los atributos básicos utilizados para el servicio de autenticación de FIWARE, el  Identity Manager – Keyrock.
- deviceToken: La tabla deviceToken está basada en el modelo de datos DeviceToken diseñado para completar la información de los dispositivos, representada en el modelo de datos Device de FIWARE. El modelo DeviceToken incluye atributos para el funcionamiento del envío y administración de notificaciones push en aplicación móvil.  

Entidades de contexto del Orion ContextBroker almacenadas en MongoDB  

- Device: Las entidades Device están basadas en el modelo de datos [Device]( https://github.com/Fiware/dataModels/blob/master/specs/Device/Device/) de FIWARE, utilizando los atributos requeridos y algunos opcionales.
- Alert: Las entidades Alert están basadas en el modelo de datos [Alert]( https://github.com/Fiware/dataModels/blob/master/specs/Alert/) de FIWARE.

Tablas de la base de datos de series de tiempo en CrateDB  

- etDevice: La tabla etDevice está basada en el modelo de datos [Device]( https://github.com/Fiware/dataModels/blob/master/specs/Device/Device/) de FIWARE. La API de QuantumLeap convierte las entidades de modelo Device del Orion en registros relacionales, para almacenarlos en la base de datos CrateDB. Para más información consulte esta [sección]( https://smartsdk.github.io/ngsi-timeseries-api/user/#data-insertion) en la documentación oficial de QuantumLeap. 
- etAlert: La tabla etAlert está basada en el modelo de datos [Alert](https://github.com/Fiware/dataModels/blob/master/specs/Alert/) de FIWARE. La API de QuantumLeap convierte las entidades de modelo Alert del Orion en registros relacionales, para almacenarlos en la base de datos CrateDB. Para más información consulte esta [sección](https://smartsdk.github.io/ngsi-timeseries-api/user/#data-insertion) en la documentación oficial de QuantuamLeap.







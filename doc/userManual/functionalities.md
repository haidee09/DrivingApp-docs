## DrivingApp functionalities

### Identification of the user's location

DrivingApp identifies the user's location when it is within the area of a delimited area. This zone must be registered by the administrator or security guard of the system, through the ViVA interface.
When the user logs into DrivingApp, the application's Home view shows the user's area, name and address. In addition, the zone map view shows the delimitation of the zone, its parking lots and the current location of the device within the zone. The following images show an example of these views.

![Ubicacion del Usuario - Vista de Inicio](img/drivingapp/ubicacionUsuarioInicio.png)

### Manual generation of alerts

DrivingApp allows users to generate manual traffic alerts, security and car accidents. These alerts can be of 3 types: traffic jam, car accident and unknown emergency. Each of these alerts can be sent with a level of severity according to the severity of the event observed by the user. The severity levels of each alert can be: informational, low, medium, high or critical. The alerts of unknown emergency events are always sent with the level of critical severity, because the type of event ocurred is unknown.

To generate a manual traffic alert, follow the steps below:

1. Press the floating alert button (red color) on the application's Home screen, and select the type of alert to be generated pressing the floating button of traffic jam or car accident.
2. Select the  severity level of the alert pressing the button with the corresponding color icon and write a description that identifies the alert event. Afterwards, click on the Send Alert button.
3. The application will inform you of the successful sending of the alert through a message.

![Crear Alerta de Tráfico](img/drivingapp/crearAlertaTrafico.png)

To generate an unknown emergency alert, follow the steps below:

1. Press the floating alert button (red color) in the application's Start screen and select the option: unknown emergency.
2. Confirm the sending of the alert by pressing the option YES.
3. The application will inform you of the successful sending of the alert through a message.

![Crear Alerta de Emergencia Desconocida](img/drivingapp/crearAlertaEmergencia.png)

### Notifications of alerts and their visualization on the map

The alerts that users issue through DrivingApp, are replicated in the form of notifications to the mobile devices of other users. These alert notifications show the category and subcategory of the alert event. The user can open the alert notifications to visualize the location of each alert on the map. The following images show an example of the notification of an alert:

1. An alert notification arrives at the mobile device and is located in the notification bar. This notification shows the category and subcategory of the alert event.
2. The user presses the notification and the application shows the location of the alert on the map.

![Notificación de Alerta](img/drivingapp/notificacionAlerta.png)

### List of alerts and their display on the map

The alerts sent by the users are grouped in the DrivingApp alerts list, each alert in the list shows the subcategory and description of the alert. To view the location of a listing alert, follow the steps listed below:

1. Press and hold the alert you want to locate on the map.
2. Press the option see on the map to observe the location of the alert on the map.
3. The application shows the location of the alert on the map, using a marker that shows the subcategory and description of the event.

![Visualización de Alertas](img/drivingapp/visualizacionAlertas.png)

### Driving view for vehicle driving.

For driving users, DrivingApp is useful for automatically detecting incorrect driving events within a defined area. The events that DrivingApp can identify are: driving at unauthorized speed, driving in the opposite direction and sudden stops of a vehicle. The user driving a vehicle within a defined area can activate the driving mode in the application. The following image shows the Home view of DrivingApp, pointing to the button to activate the vehicle driving mode.

![Botón Vista de Manejo](img/drivingapp/botonVistaManejo.png)

La vista de manejo muestra la velocidad del vehículo en km/hr, y el límite máximo y mínimo de velocidad permitida en la calle de la zona. Además, esta vista muestra mensajes al usuario como:

- Estás manejando de forma correcta.
- Te estás deteniendo.
- Estás detenido.
- Estás acelerando.

El usuario que conduce un automóvil, puede identificar de manera automática a través de la vista de manejo un evento de infracción. Los botones de la vista de manejo se iluminan de acuerdo al ascenso o descenso de velocidad del vehículo. La siguiente imagen muestra los botones de cada evento en la vista de manejo de DrivingApp.

![Botones de la Vista de Manejo](img/drivingapp/botonesEventosAutomaticos.png)

Las alertas en la conducción de un vehículo se representan mediante los siguientes colores:

1.- Botón de evento de velocidad: 

- Color Naranja: indica que la velocidad del vehículo está por debajo del límite mínimo permitido.
- Color Rojo: indica que el vehículo ha excedido el límite de velocidad máximo permitido.
- Color Verde: indica que está conduciendo dentro del rango de límite de velocidad permitida. 

2.- Botón de evento de paradas:

- Color azul: indica que el vehículo se encuentra acelerando.
- Color Naranja: significa que el vehículo disminuye su velocidad.
- Color Rojo: indica que el vehículo se ha detenido.
- Color verde: significa que está conduciendo de forma correcta.

3.- Botón de evento de contrasentido:

- Color verde: indica que el usuario está conduciendo el vehículo en el sentido correcto de la calle.
- Color rojo: indica que el usuario está conduciendo el vehículo en el sentido incorrecto de la calle.

Las siguientes imágenes muestran ejemplos de la vista de manejo, donde se detectan diferentes eventos mediante la iluminación de cada uno de los botones.

![Vistas de Manejo](img/drivingapp/vistasManejo1.png)

![Vistas de Manejo ](img/drivingapp/vistasManejo2.png)
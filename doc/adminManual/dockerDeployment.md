## DrivingApp deployment with Docker Compose

Docker Compose is a tool for creating and running multi-container Docker applications. The DrivingApp system can be deployed through this tool. The following table shows the structure of DrivingApp system using Docker containers.

|Imagen Docker|Versión|Nombre del contenedor|Puertos|Depende de|
|---------|-----------|----------|----------|-----------|
|fiware/orion|1.15.1|orion|1026|mongo|
|mongo|3.2|mongo|27017|
|smartsdk/quantumleap|latest|quantumleap|8668|orion, mongo, crate|
|crate|3.0.5|crate|4200, 4300|
|grafana/grafana|latest|grafana|3000|crate
|redis|latest|redis|6379|
|mariadb|latest|mariadb|3306|
|cenidetiot/drivingapp-service|latest|drivingappservice|4005|mariadb, crate, orion, idm|
|cenidetiot/notifications-service|latest|notifications|3001|smartservice|
|ging/fiware-idm|latest|idm|5000|

### Requeriments

- **Git version control software**, you can check the Git documentation on this [link](https://git-scm.com/).
- **Docker**, you can check the installation of Docker in the following [link](https://docs.docker.com/cs-engine/1.12/).
- **Docker Compose**, you can check the installation of docker-compose in the following [link](https://docs.docker.com/compose/install/).

### Running

1.- Download the files from the official repository of DrivingApp-docker:

    $ git clone https://github.com/smartsdkCenidet/DrivingApp-docker.git


2.- Run the file docker-compose.yml using the command:

    $ docker-compose up -d 


**docker-compose** automatically downloads and executes docker images and containers for each image, this process may take a few minutes. The following image shows this process in console:

![docker-compose up -d](./img/dockerDeploy1.png)


3.- Verify that all containers are running with the command:

    $ docker ps 

![docker ps](./img/dockerDeploy2.png)


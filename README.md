#### Prueba 1:
 - Dentro de la carpeta diagram se encuentra el README con el digrama realizado y la explicacion de la arquitectura elegida.

#### Prueba 2:
 - Local deploy:
   El despliegue local está realizado con docker swarm, dentro de la carpeta swarm se encuentra el docker-compose.yml a usar.
   En un host con docker swarm ejecutar "docker stack deploy -c docker-compose.yml moni" para desplegar el stack moni.
   No posee ningun load balancer, estan los servicios expuestos exeptuando la DB.

 - Cloud deploy: 
   Para este despliegue se utilizo GitHub como repositorio, CircleCI para la intrgracion continua y GCP como cloud provider.
   Al igual que con el deploy local, los servicios no poseen un ingress y están expuestos mediante NodePort.
   El pipeline definido para el CI contiene 3 stages;
     * Test del front
     * Build de la imagen, tag y Push a la registry de GCP.
     * Deploy en Kubernetes. El despliegue se realiza siempre con las imagenes tagueadas como latest.

  No existe dominio asociado, la IP la instancia de GCP es 34.69.13.103.
  Para el backend el NodePort es 31000: http://34.69.13.103:31000/
  para el frontend el NodePort es el 32000: http://34.69.13.103:32000/

 * Los dockerfiles elaborados se encuentran dentro de las carpetas frontDeploy y backDeploy. 
 * En el backend se hardcodearon las variables para la db en el archivo settings, introducido al momento de generar la imagen.
 * Tanto en el despliegue local con swarm, como en el despliegue en la nube la DB no cuenta con su volumen asociado para persistir los datos. 

[![N|Solid](https://moni.com.ar/static/img/moni-logo-primary.svg)](https://moni.com.ar/)

#### Prueba 1 - Diagrama de Red

Produzca un diagrama de red (puede utilizar lucidchart) de una aplicación web en GCP o AWS y escriba una descripción de texto de 1/2 a 1 página de sus elecciones y arquitectura.

El diseño debe soportar:
-   Cargas variables
-   Contar con HA (alta disponibilidad)
-   Frontend en Js
-   La aplicación consume 2 microservicios externos
-   Una base de datos relacional y una no relacional

El diagrama debe hacer un mejor uso de las soluciones distribuidas.

#### Prueba 2 - Despliegue de una aplicación Django y React.js

Elaborar el deployment dockerizado de una aplicación en django (backend) con frontend en React.js contenida en el repositorio.

Se deben entregar los Dockerfiles pertinentes para elaborar el despliegue y justificar la forma en la que elabora el deployment (supervisor, scripts, docker-compose, kubernetes, etc)

Subir todo lo elaborado a un repositorio (github, gitlab, bitbucket, etc). En el repositorio se debe incluir el código de la aplicación y un archivo README.md con instrucciones detalladas para compilar y desplegar la aplicación, tanto en una PC local como en la nube (AWS o GCP).

##### Requisitos y deseables:

La solución al ejercicio debe mostrarnos que usted puede:

-   Automatizar la parte del proceso de despliegue.
-   usar conceptos de CI para aprovisionar el software necesario para que los entregables se ejecuten
-   use cualquier herramienta de CI de su elección para implementar el entregable
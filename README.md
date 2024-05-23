# Laboratorio de integración con docker

Actividades:

## 1. Revisar configuración de pipeline de CI/CD simulado:
   Build Stage:

    Code Commit: Developers commit code to a version control system, triggering the CI pipeline.
    Docker Image Creation: Dockerfiles define the environment and dependencies, and Docker builds an image which encapsulates the application and its runtime.
    Test Stage:
    
    Automated Testing: Docker images are used to spin up containers where automated tests are conducted, ensuring that the application behaves as expected in an environment identical to production.
    Deployment Stage:
    
    Container Registry: Successfully tested Docker images are tagged and pushed to a Docker registry.
    Orchestration and Deployment: Tools like Kubernetes or Docker Swarm manage the deployment of these images into containers across different environments, handling scaling and load balancing.

    
## 2. Analisis de mejoras y incidentes potenciales:

        * Beneficios: 
            Algunos de los beneficios de utilizar docker dentro de los pipelines de integración y entrega continuos son:
        
            - Portable y consistente: Al utilizar docker como herramienta para desarrollo nos permite tener la misma instalación para cualquiera de los ambientes donde se despliegue al establecer las versiones de librerias y herramientas a usar incluyendo staging y produccion por lo que brinda seguridad de que no se rompera por un tema de incompatibilidades e incluso nos permite compartir el codigo con compañeros para resolver algun bug en conjunto
            - Aislamiento: Al mantener las herramientas y librerias dentro de un contenedor nos permite tener aislada esa configuracion en caso de que se requiera probar algun otro proyecto con otras versiones de librerias    
            - Escalable: Si se requiere, se puede aumentar la capacidad y cantidad de los contenedores, tales como la memoria o el procesador, claro, esta dependera del equipo sobre donde se corre
          
      * Incidentes potenciales:
            Para mitigar posibles incidentes se sugiere:
             -  Utilizar imagenes confiables y verificadas, es decir que no tengan vulnerabilidades detectadas en la medida de lo posible
             -  Correr los contenedores con los permisos minimos con el fin de evitar que puediera escalar alguna vulnerabildiad
             -  Contar con versiones actualizadas de las imagenes de docker y estar al pendiente de si se encuentran nuevas vulnerabilidades (zero day)

   ## 3. Reporte de analisis:

       * Resumen de integracion de docker en las fases de ci/cd:
        
           En un pipeline de ci/cd las etapas se llevarian como sigue:
            - Build Stage: En esta fase se crearia el archivo dockerfile con la configuración necesaria para levantar  el container sobre el que correria la aplicación, incluyendo el runtime y las instalacion de las librerias y herramientas necesarias para ejecutar el proyecto, en caso de requerirse tambien se podria generar el docker-compose.yml con la configuracion de cada contenedor y los permisos de puertos, carpetas y dependencias necesarias para la comunicacion entre ellos. 
            - Test Stage: En esta etapa se generaran la configuracion necesaria para ejecutar las pruebas sobre el codigo, esto puede incluir, pruebas unitarias (junit), pruebas sast y dast, de seguridad de codigo (codeql, snyk, stackhawk) y de calidad de codigo (sonarqube, linting)
            - Deployment Stage: Durante la fase de despliegue los pipelines se encargaran de generar por ejemplo en caso de usar kubernete, dar de baja los pods anteriores y generar unos nuevos segun la estrategia de liberación y asi aplicar el despliegue de una nueva version
        
       * Analisis de los beneficios y retos potenciales identificados durante la revision:

          - Adicional a los beneficios comentados en el punto 2 pudiera agregar como beneficio adicional que el uso de docker dentro de nuestro ciclo ci/cd: disminuyen el tiempo de liberacion de entregables al automatizar el flujo de las pruebas, el analisis de codigo estatico y dinamico, la revision de vulnerabilidades, asi como el formateo del codigo y las metricas de cobertura 
          - Un reto que presenta inicialmente es la implementacion de una configuracion efectiva que no ralentize el despliegue, debido a que ciertos componentes pueden crear que el build de la imagen sea pesada o tardada de generar cada que se requiera 

          
     * Sugerencias sobre soluciones teoricas o mejores practicas para afrontar los retos
          - Configurar un dockerfile por multicapa para disminuir los tiempos de generacion de imagenes
          - Elegir por las opciones mas ligeras de imagenes en caso de que se requiera funcionalidades basicas para disminuir los tamaños de contenedores    
          - Revisar de manera constante por vulnerabilidades reportadas en las imagenes utilizadas y aplicar las actualizaciones pertinentes


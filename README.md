# Flask CRUD - Docker y Dokploy (Despliegue Continuo)

![Materia: Ingeniería en Sistemas](https://img.shields.io/badge/Materia-Ingeniería%20en%20Sistemas-blue?style=flat-square)
![Profesor: Ing. Jose Javier Moya Moya](https://img.shields.io/badge/Profesor-Ing.%20Jose%20Javier%20Moya%20Moya-green?style=flat-square)
![Despliegue: Dokploy](https://img.shields.io/badge/Despliegue-Dokploy-orange?style=flat-square)
![Plataforma: Docker](https://img.shields.io/badge/Plataforma-Docker-blue?style=flat-square&logo=docker)

Este proyecto es una aplicación CRUD desarrollada en Flask y MySQL, diseñada para la implementación de Despliegue Continuo (CD) utilizando Docker y la plataforma de orquestación Dokploy.

## Reconocimiento Especial
Proyecto desarrollado bajo la guía del Ing. Jose Javier Moya Moya. Gracias a su metodología, se logró transitar de un desarrollo local a un entorno de despliegue automatizado profesional. Un grande, el Profe Moya.

## Tecnologías Utilizadas

* Backend: Python 3.10 + Flask
* Base de Datos: MySQL 5.7
* Contenedores: Docker & Docker Compose
* Orquestación y CD: Dokploy en MV Ubuntu Server
* Repositorio: GitHub

## Arquitectura de Microservicios

El despliegue se gestiona a través de un archivo docker-compose.yml que levanta y vincula dos servicios fundamentales:

1. flask_app: El núcleo de la aplicación Python/Flask (Puerto 8081).
2. flask_db: Base de datos MySQL con persistencia de datos mediante volúmenes.

## Configuración de Alta Disponibilidad

Para cumplir con los estándares de producción, se implementó la política de reinicio automático:
* restart: always: Esta instrucción garantiza que, en caso de un fallo del contenedor o un reinicio de la Máquina Virtual (MV), los servicios de Flask y MySQL se levanten automáticamente sin intervención humana.

## Flujo de Despliegue Continuo (CD)

El sistema está configurado para que el código se actualice de forma automática:
1. Desarrollo: Cambios realizados en Windows.
2. Versionamiento: git push hacia este repositorio en GitHub.
3. Despliegue: Dokploy detecta el cambio en el repositorio, realiza el pull del nuevo código y reconstruye los contenedores en la MV de forma transparente.

## Comandos de Mantenimiento (En la MV)

## Vista

<img width="1919" height="854" alt="image" src="https://github.com/user-attachments/assets/84ed1dd1-12d4-40f9-aa02-5ab6009bbf51" />


Para recrear la tabla de la base de datos manualmente dentro del contenedor:

```bash
sudo docker exec -it flask_db mysql -u user -ppassword flaskcrud -e "CREATE TABLE IF NOT EXISTS contacts (id INT AUTO_INCREMENT PRIMARY KEY, fullname VARCHAR(255), phone VARCHAR(255), email VARCHAR(255));"

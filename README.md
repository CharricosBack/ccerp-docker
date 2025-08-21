# CCERP Docker

## Introducción
**CCERP (Charritos Cloud Enterprise Resource Planning)** es una plataforma interna de **Industrias Charritos** desarrollada para la gestión y procesamiento de información específica de la empresa.  
Su objetivo es cubrir necesidades que no pueden ser atendidas por soluciones comerciales estándar, como el control de gastos y el cambaceo (venta en ruta).

---

## Entorno de ejecución

### Sistema operativo
CCERP se ejecuta sobre **Ubuntu**, aprovechando su carácter open source y eliminando costos de licencias.  
- **Producción:** Ubuntu 18.x  
- **Pruebas:** Ubuntu 22.x  

### Servidor web
- **Producción:** Apache2  
- **Pruebas:** Nginx  

### Frontend
- **Framework:** Angular 13  
- **Entornos:** Producción y pruebas  
- **Estado:** Sin planes de migración en el corto plazo  

### Backend
- **Framework:** Laravel 8.x  
- **Lenguaje:** PHP 7.4  
- **Entornos:** Producción y pruebas  
- **Estado:** En planes de migración a nuevas versiones de PHP & Framework  

### Base de datos
- **Motor:** MySQL  
- **Producción:** 5.7.42  
- **Pruebas:** 8.x  


### Servicios de mensajería y tiempo real
- **Redis**: utilizado para el envío de notificaciones al frontend  
- **Servidor WebSocket**: implementado en Node.js con **Socket.io**, disponible en producción y pruebas  

---

## Uso de Docker
Con el fin de garantizar despliegues consistentes y modulares, así como facilitar la portabilidad entre entornos, se implementó la virtualización mediante **Docker**.

## Comparación de entornos

| Componente              | Producción                         | Pruebas                              |
|--------------------------|------------------------------------|---------------------------------------|
| **Sistema operativo**    | Ubuntu 18.x                        | Ubuntu 22.x                           |
| **Servidor web**         | Apache2                            | Nginx                                 |
| **Frontend**             | Angular 13 (fuera de Docker)       | Angular 13 (dockerizado)              |
| **Backend**              | Laravel 8.x / PHP 7.4 (Docker)     | Laravel 8.x / PHP 7.4 (Docker)        |
| **Base de datos**        | MySQL 5.7.42 (fuera de Docker)     | MySQL 8.x (dockerizado)               |
| **Redis**                | Docker                             | Docker                                |
| **Servidor WebSocket**   | Node.js + Socket.io (Docker)       | Node.js + Socket.io (Docker)          |
| **Nivel de Dockerización** | Parcial (backend, Redis, WebSocket) | Completo (DB, backend, frontend, Redis, WebSocket) |



### Estado actual
- **Entorno de pruebas:** todo el stack se encuentra dockerizado (Base de datos, backend, frontend, Redis y servidor WebSocket).  
- **Entorno de producción:** la implementación con Docker es parcial (backend, Redis y servidor WebSocket).  

---

## Objetivo del repositorio
Este repositorio tiene como propósito:  
1. Documentar y centralizar las configuraciones utilizadas en el entorno de **pruebas**.  
2. Establecer una base de referencia para completar la implementación en el entorno de **producción**.  
3. Facilitar la estandarización y despliegue de la plataforma mediante **contenedores Docker**.  

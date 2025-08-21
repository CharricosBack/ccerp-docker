# Frontend

## Descripción
El frontend de la aplicación se despliega utilizando la carpeta generada por **Angular** en el proceso de build (`dist/`).  
Este enfoque permite realizar un despliegue rápido y sencillo dentro de un contenedor Docker con **Nginx** como servidor web.

---

## Estructura de directorios
Después de ejecutar el build de Angular, se generará una estructura similar a la siguiente:

```
dist/
└── {nombre_proyecto}/
    ├── index.html
    ├── favicon.ico
    ├── assets/
    └── main.js
```

Debes tomar el contenido de {nombre_proyecto} y cargarlo al directorio de este repo:
```
ccerp-docker/
    └── frontend/
        ├── dist/
        │   ├── index.html
        │   ├── favicon.ico
        │   ├── assets/
        │   └── main.js
        ├── Dockerfile
        ├── nginx.conf
        └── docker-compose.yml
```

## Flujo de despliegue

```mermaid
flowchart LR
    A[Angular CLI: ng build] --> B[Carpeta dist/{nombre_proyecto}]
    B --> C[Copiar archivos a frontend/dist/]
    C --> D[Docker Build con Nginx]
    D --> E[Contenedor Frontend en ejecución]
    E --> F[Navegador del cliente]
```
## Despliegue
```
docker-compose up -d --build
```

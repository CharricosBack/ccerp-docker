# Dockerfile para el frontend Angular
FROM nginx:stable-alpine

# Elimina configuración por defecto de Nginx
RUN rm -rf /usr/share/nginx/html/*

# Copia los archivos compilados de Angular (dist/) a la carpeta de Nginx
COPY dist/ /usr/share/nginx/html

# Copia un archivo de configuración personalizado para Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

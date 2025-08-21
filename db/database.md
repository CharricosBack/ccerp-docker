# Base de datos

## Implementación
Para inicializar la base de datos en el contenedor es necesario contar con un archivo de respaldo llamado **backup.sql**.  
Este archivo será utilizado durante el despliegue para cargar la estructura y los datos iniciales.

### Beneficios
- Respaldo integrado al proceso de despliegue mediante Docker.  
- Estandarización de la base de datos entre distintos entornos.  
- Posibilidad de restauración rápida ante fallos o migraciones.  

---

## Nota técnica: diferencias entre MySQL 5.7 y 8.x

Actualmente existe una diferencia de versiones de MySQL entre los entornos:

- **Producción:** MySQL 5.7.42  
- **Pruebas:** MySQL 8.x  

### Riesgos y consideraciones de compatibilidad
1. **Cambios en autenticación**  
   - MySQL 8 utiliza por defecto `caching_sha2_password`, mientras que MySQL 5.7 usa `mysql_native_password`.  
   - Esto puede requerir ajustes en usuarios y clientes de conexión.

2. **Sintaxis SQL más estricta**  
   - MySQL 8 valida con mayor rigor consultas que en 5.7 eran aceptadas.  
   - Ejemplos: reglas de `GROUP BY`, alias en subconsultas o funciones obsoletas.

3. **Collations y codificación**  
   - MySQL 8 adopta `utf8mb4_0900_ai_ci` como collation por defecto.  
   - MySQL 5.7 utiliza `utf8mb4_general_ci`.  
   - Esto puede provocar diferencias en ordenamiento y comparaciones de cadenas.

4. **Funciones y características nuevas**  
   - MySQL 8 introduce índices invisibles, roles y mejoras en seguridad.  
   - Estas no son compatibles con MySQL 5.7.

5. **Optimizador de consultas**  
   - Cambios en el motor de optimización pueden alterar los planes de ejecución y el rendimiento.  

---

## Recomendaciones
- Homologar las versiones de MySQL entre **producción** y **pruebas** para evitar inconsistencias.  
- Validar la compatibilidad de las consultas más utilizadas antes de migrar a MySQL 8.x.  
- Documentar queries críticas y su comportamiento en ambos entornos.  
- Realizar pruebas de regresión antes de aplicar cambios en producción.  

---

## (Opcional) Procedimiento de restauración
Para restaurar la base de datos desde el respaldo, ejecutar el siguiente comando:

```bash
docker exec -i <nombre_contenedor_mysql> mysql -u<usuario> -p<password> basedatos < backup.sql
```

Donde:
- `<nombre_contenedor_mysql>`: Nombre del contenedor de MySQL.  
- `<usuario>`: Usuario con permisos para restaurar la base de datos.  
- `<password>`: Contraseña del usuario.  
- `basedatos`: Nombre de la base de datos destino.  

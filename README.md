# multy-tenancy


## Ejercicio:

Diseñe e implemente en DynamoDB una tabla Multi-tenancy de su preferencia e inserte 6 registros (2 por cada tenant_id).


## Antes que todo
Se tiene que crear una Maquina Virtual para la BD en MongoDB, y lo ideal es ponerle como puerto 21017. Lo mismo que la clase:

"CS2032 - Cloud Computing (Ciclo 2025-1) -
Balanceo de Carga y Alta disponibilidad
Semana 6 - Taller 4: Balanceador de Carga"

Primero poner la MV y sus respectivas configuraciones hechas en clase, una vez esto:

## Pasos para usar el microservicio:

2. Cómo se abordará
Se creará la tabla Multi-Tenant **t_universidad** en DynamoDB, aplicando el Patrón 1 (Single, Shared Database Schema)



### 1. Primero clonar el repositorio:
```c
git clone https://github.com/nonpr00/review-microservice.git

// luego:
cd review-microservice
```
 
### 2. Luego construir la imagen:
```
{
  "tenant_id": "CIENCIA_DE_LA_COMPUTACION",
  "course_id": "CURS001",
  "curso_datos": {
    "nombre": "Cloud Computing",
    "descripcion": "Introducción a la computación en la nube con práctica en AWS y sus fundamentos.",
    "ciclo": 4,
    "creditos": 4,
    "tipo": "Obligatorio",
    "docentes": ["Gerardo Colchado", "Oscar Mejia"],
    "modalidad": "Presencial",
    "horario": {
      "dias": ["Lunes", "Jueves", "Sabado"],
      "hora_inicial": "7:00",
      "hora_final": "9:00"
    }
  }
}
```
## Formato de la tabla:
En este caso cada elemento de la tabla tiene un elemento JSON el cual sus elementos mas relevantes son estos:
* **tenant_id:** clave de partición (Partition Key), esta identificará a las carreras de la universidad. Son 3: Ciencia de la Computación, Ingeniería Mecatrónica y Bioingeniería.
* **course_id:** clave de ordenamiento (Sort Key), permite identificar cada curso de forma única. 

Los otros atributos son adicionales que muestran información del curso seleccionado.

## Crear elemento:

Ingresamos a "Crear Elemento" y una vez presionado el enlace llenamos los respectivos datos del elemento a insertar:


### 4. Modificar el .env (variables de entorno):
```c
nano .env
```
Las variables tienen que ser:
```c
PORT=4000

MONGO_URI=mongodb://(ip_privada_mv_base_de_datos):27017/reviewsdb
## Ejemplo:
## MONGO_URI=mongodb://172.31.30.32:27017/reviewsdb

API_IP=ip_publica_de_la_mv_donde_estamos_ejecutando 
(MV Desarrollo en mi caso, ustedes puede ser otra)

## Ejemplo:
## API_IP=52.87.74.110

FRONTEND_URL = "http://localhost:5173" (esto para un futuro, no es necesario ahorita)
```
Recordar que 27017 es el puerto de la BD MongoDB desplegada en la MV Base de Datos.

### 3. Despues ejecutar la imagen en un contenedor
```c
docker run -d --rm --name api-review_c -p 4000:4000 api-review
```

### 4. Verificar el log con:
```c
docker logs api-review_c
```
Tiene que salir algo como:
```c
> reviews-microservice@1.0.0 start
> node index.js

52.87.74.110 (o la IP publica que esta en nuestra MV ejecutandose)
MongoDB connected
Review service running on port 4000
```

Si sale eso, entonces verificar en

(ip_publica_de_la_mv_donde_estamos_ejecutando):4000/docs

Ejm:

52.87.74.110:4000/docs

Si sale la docu Swagger y se pueden hacer consultas GET, POST, etc entonces todo esta OK.

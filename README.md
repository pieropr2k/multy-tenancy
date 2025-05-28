# multy-tenancy


## Ejercicio:

Diseñe e implemente en DynamoDB una tabla Multi-tenancy de su preferencia e inserte 6 registros (2 por cada tenant_id).

## 1. ¿Qué se hará?
Se creará la tabla Multi-Tenant **t_universidad** en DynamoDB, aplicando el Patrón 1 (Single, Shared Database Schema)
 
## 2. Luego construir la imagen:
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

### 3. Formato de los datos insertados:

En este caso cada elemento de la tabla tiene un elemento JSON el cual sus elementos mas relevantes son estos:
* **tenant_id:** clave de partición (Partition Key), esta identificará a las carreras de la universidad. Son 3: Ciencia de la Computación, Ingeniería Mecatrónica y Bioingeniería.
* **course_id:** clave de ordenamiento (Sort Key), permite identificar cada curso de forma única. 

Los otros atributos son adicionales que muestran información del curso seleccionado.

## 4. Crear elemento:

Ingresamos a "Crear Elemento" y una vez presionado el enlace llenamos los respectivos datos del elemento a insertar:

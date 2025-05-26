# Trabajo Práctico N°5
![image](https://github.com/user-attachments/assets/f2e54dc0-6027-4cd7-817a-a42e47570113)

## _Autores:_ 
* Pedro Fernandes Delgado
* Sebastian campos Rodriguez

## **PARTE 1:** Bases de Datos

### 1. ¿Qué tipo de base de datos es? 

Este tipo de base de datos es una base de datos relacional. Las bases de datos
relacionales se utilizan para almacenar y gestionar datos estructurados y están
organizadas en tablas que pueden estar relacionadas entre sí mediante primary keys y foreign keys.

### 2. Armar el diagrama entidad-relación de la base de datos dada. 
<img src="imágenes/helisulbaranBD02.png" alt="ejemplo_modelo-ER" style="width:500px;"/>

### 3. Armar el Modelo relacional de la base de datos dada.
![modelo_relacional](imágenes/modelo_relacional.png)

### 4. Considera que la base de datos está normalizada. En caso que no lo esté, ¿cómo podría hacerlo?

La normalización es un método utilizado para organizar una base de datos siguiendo ciertos principios que ayudan a reducir la redundancia de datos y mejorar su integridad. En el caso de la base de datos analizada, cada tabla cuenta con una primary key única, y todas las columnas no clave mantienen una relación directa con dicha clave. Además, no se identifican dependencias transitivas. Por lo tanto, se concluye que la base de datos ya cumple con los criterios de normalización y no sería necesario aplicar ajustes adicionales.

## **PARTE 2:** Bases de Datos

### 1. Cuando se realizan consultas sobre la tabla paciente agrupando por ciudad los tiempos de respuesta son demasiado largos. Proponer mediante una query SQL una solución a este problema.

```
query 1
```
(imagen del resultado de la query)

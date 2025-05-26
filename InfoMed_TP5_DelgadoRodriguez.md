# Trabajo Práctico N°5
![image](https://github.com/user-attachments/assets/f2e54dc0-6027-4cd7-817a-a42e47570113)

## _Autores:_ 
* Pedro Fernandes Delgado
* Sebastian Campos Rodriguez

## **PARTE 1:** Bases de Datos

### 1. ¿Qué tipo de base de datos es? Clasificarla según estructura y función.

Este tipo de base de datos es una base de datos relacional. Las bases de datos
relacionales se utilizan para almacenar y gestionar datos estructurados y están
organizadas en tablas que pueden estar relacionadas entre sí mediante primary keys y foreign keys.

### 2.  Armar el diagrama entidad-relación de la base de datos dada.
<img src="imágenes/helisulbaranBD02.png" alt="ejemplo_modelo-ER" style="width:500px;"/>

### 3. Armar el modelo lógico entidad-relación de la base de datos dada.
![modelo_relacional](imágenes/modelo_relacional.png)

### 4. Considera que la base de datos está normalizada. En caso que no lo esté, ¿cómo podría hacerlo?

La normalización es un método utilizado para organizar una base de datos siguiendo ciertos principios que ayudan a reducir la redundancia de datos y mejorar su integridad. En el caso de la base de datos analizada, cada tabla cuenta con una primary key única, y todas las columnas no clave mantienen una relación directa con dicha clave. Además, no se identifican dependencias transitivas. Por lo tanto, se concluye que la base de datos ya cumple con los criterios de normalización y no sería necesario aplicar ajustes adicionales.

## **PARTE 2:** Bases de Datos

### 1. Cuando se realizan consultas sobre la tabla paciente agrupando por ciudad los tiempos de respuesta son demasiado largos. Proponer mediante una query SQL una solución a este problema.

```
query 1
```
(imagen del resultado de la query)

### 2. Se tiene la fecha de nacimiento de los pacientes. Se desea calcular la edad de los pacientes y almacenarla de forma dinámica en el sistema ya que es un valor típicamente consultado, junto con otra información relevante del paciente.

```
query 2
```
(imagen del resultado de la query)

### 3. La paciente, “Luciana Gómez”, ha cambiado de dirección. Antes vivía en “Avenida Las Heras 121” en “Buenos Aires”, pero ahora vive en “Calle Corrientes 500” en “Buenos Aires”. Actualizar la dirección de este paciente en la base de datos.

```
query 3
```
(imagen del resultado de la query)

### 4. Seleccionar el nombre y la matrícula de cada médico cuya especialidad sea identificada por el id 4.

```
query 4
```
(imagen del resultado de la query)

### 5. Puede pasar que haya inconsistencias en la forma en la que están escritos los nombres de las ciudades, ¿cómo se corrige esto? Agregar la query correspondiente.

```
query 5
```
(imagen del resultado de la query)

### 6. Obtener el nombre y la dirección de los pacientes que viven en Buenos Aires.


```
query 6
```
(imagen del resultado de la query)

### 7. Cantidad de pacientes que viven en cada ciudad.
 

```
query 7
```
(imagen del resultado de la query)

### 8. Cantidad de pacientes por sexo que viven en cada ciudad.


```
query 8
```
(imagen del resultado de la query)

### 9. Obtener la cantidad de recetas emitidas por cada médico.

```
query 9
```
(imagen del resultado de la query)

### 10. Obtener todas las consultas médicas realizadas por el médico con ID igual a 3 durante el mes de agosto de 2024.

```
query 10
```
(imagen del resultado de la query)

### 11. Obtener el nombre de los pacientes junto con la fecha y el diagnóstico de todas las consultas médicas realizadas en agosto del 2024.

```
query 11
```
(imagen del resultado de la query)

### 12. Obtener el nombre de los medicamentos prescritos más de una vez por el médico con ID igual a 2.

```
query 12
```
(imagen del resultado de la query)

### 13. Obtener el nombre de los pacientes junto con la cantidad total de recetas que han recibido.

```
query 13
```
(imagen del resultado de la query)

### 14. Obtener el nombre del medicamento más recetado junto con la cantidad de recetas emitidas para ese medicamento.

```
query 14
```
(imagen del resultado de la query)

### 15. Obtener el nombre del médico junto con el nombre del paciente y el número total de consultas realizadas por cada médico para cada paciente, ordenado por médico y paciente.

```
query 15
```
(imagen del resultado de la query)

### 16. Obtener el nombre del médico junto con el nombre del paciente y el número total de consultas realizadas por cada médico para cada paciente, ordenado por médico y paciente.

```
query 16
```
(imagen del resultado de la query)

### 17. Obtener el nombre del medicamento junto con el total de recetas prescritas para ese medicamento, el nombre del médico que lo recetó y el nombre del paciente al que se le recetó, ordenado por total de recetas en orden descendente.

```
query 17
```
(imagen del resultado de la query)

### 18. Obtener el nombre del médico junto con el total de pacientes a los que ha atendido, ordenado por el total de pacientes en orden descendente.

```
query 18
```
(imagen del resultado de la query)

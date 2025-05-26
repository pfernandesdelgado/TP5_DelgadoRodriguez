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
<img src="imágenes/diagrama entidad-relación.jpeg" alt="diagrama entidad-relación" style="width:750px;"/>

### 3. Armar el modelo lógico entidad-relación de la base de datos dada.
![modelo_relacional](imágenes/modelo_relacional.jpeg)

### 4. Considera que la base de datos está normalizada. En caso que no lo esté, ¿cómo podría hacerlo?

La normalización es un método utilizado para organizar una base de datos siguiendo ciertos principios que ayudan a reducir la redundancia de datos y mejorar su integridad. En el caso de la base de datos analizada, cada tabla cuenta con una primary key única, y todas las columnas no clave mantienen una relación directa con dicha clave. Además, no se identifican dependencias transitivas. Por lo tanto, se concluye que la base de datos ya cumple con los criterios de normalización y no sería necesario aplicar ajustes adicionales.

## **PARTE 2:** Bases de Datos

### 1. Cuando se realizan consultas sobre la tabla paciente agrupando por ciudad los tiempos de respuesta son demasiado largos. Proponer mediante una query SQL una solución a este problema.

```
CREATE INDEX idx_pacientes_ciudad ON Pacientes(ciudad);

SELECT 
    CASE 
        WHEN LOWER(TRIM(ciudad)) IN ('buenos aires', 'bs aires', 'buenos aiers', 'buenos   aires') THEN 'Buenos Aires'
        WHEN LOWER(TRIM(ciudad)) IN ('cordoba', 'córdoba', 'córodba') THEN 'Córdoba'
        WHEN LOWER(TRIM(ciudad)) IN ('Mendoza', 'Mendzoa') THEN 'Mendoza'
        ELSE ciudad
    END AS ciudad_normalizada,
    COUNT(*) AS total_pacientes
FROM Pacientes
GROUP BY ciudad_normalizada;
```
(imagen del resultado de la query)

### 2. Se tiene la fecha de nacimiento de los pacientes. Se desea calcular la edad de los pacientes y almacenarla de forma dinámica en el sistema ya que es un valor típicamente consultado, junto con otra información relevante del paciente.

```
SELECT nombre, fecha_nacimiento,
       (strftime('%Y', 'now') - strftime('%Y', fecha_nacimiento)) 
       - (strftime('%m-%d', 'now') < strftime('%m-%d', fecha_nacimiento)) AS edad
FROM Pacientes;
```
![image](https://github.com/user-attachments/assets/830a3831-d522-4198-81fa-24c40461e064)

### 3. La paciente, “Luciana Gómez”, ha cambiado de dirección. Antes vivía en “Avenida Las Heras 121” en “Buenos Aires”, pero ahora vive en “Calle Corrientes 500” en “Buenos Aires”. Actualizar la dirección de este paciente en la base de datos.

```
UPDATE Pacientes
SET calle = 'Calle Corrientes', numero = '500'
WHERE nombre = 'Luciana Gómez' AND ciudad = 'Bs Aires' AND calle = 'Avenida Las Heras';
```
![image](https://github.com/user-attachments/assets/5e38f240-283a-42c2-87c1-94abcc2f20b9)

### 4. Seleccionar el nombre y la matrícula de cada médico cuya especialidad sea identificada por el id 4.

```
SELECT nombre, matricula
FROM Medicos
WHERE especialidad_id = 4;
```
![image](https://github.com/user-attachments/assets/4c4afc12-d377-40a8-bf72-822272ba5b73)

### 5. Puede pasar que haya inconsistencias en la forma en la que están escritos los nombres de las ciudades, ¿cómo se corrige esto? Agregar la query correspondiente.

```
UPDATE Pacientes SET ciudad = 'Buenos Aires' WHERE TRIM(LOWER(ciudad)) IN ('buenos aires', 'buenos   aires', 'bs aires', '  buenos aires', 'buenos aires ');
UPDATE Pacientes SET ciudad = 'Córdoba' WHERE TRIM(LOWER(ciudad)) IN ('cordoba', 'córdoba', 'córodba');
UPDATE Pacientes SET ciudad = 'Mendoza' WHERE TRIM(LOWER(ciudad)) IN ('mendoza', 'mendzoa');
```
![image](https://github.com/user-attachments/assets/98038830-d0fa-4b22-acc2-871d4186239c)

### 6. Obtener el nombre y la dirección de los pacientes que viven en Buenos Aires.

```
SELECT nombre, CONCAT(numero, ' ', calle) AS direccion
FROM Pacientes
WHERE TRIM(LOWER(ciudad)) = 'buenos aires';
```
![image](https://github.com/user-attachments/assets/9aa29234-6e6b-4c8c-b1bc-cc5d1ff5c0ad)

### 7. Cantidad de pacientes que viven en cada ciudad.
 
```
SELECT ciudad, COUNT(*) AS cantidad_pacientes
FROM Pacientes
GROUP BY ciudad;
```
![image](https://github.com/user-attachments/assets/b8ea7f65-e04f-47df-b36c-028e6fbc5ef4)

### 8. Cantidad de pacientes por sexo que viven en cada ciudad.

```
SELECT p.ciudad, s.descripcion AS sexo, COUNT(*) AS cantidad_pacientes
FROM Pacientes p
JOIN SexoBiologico s ON p.id_sexo = s.id_sexo
GROUP BY p.ciudad, s.descripcion;
```
![image](https://github.com/user-attachments/assets/0312125d-b980-46b0-bbb8-b5fc82a7101a)

### 9. Obtener la cantidad de recetas emitidas por cada médico.

```
SELECT m.nombre AS nombre_medico, 
COUNT(r.id_receta) AS cantidad_recetas
FROM Recetas r
JOIN Medicos m ON r.id_medico = m.id_medico
GROUP BY r.id_medico;
```
![image](https://github.com/user-attachments/assets/b10bf14e-fc09-4d48-94b0-1a93afb963eb)

### 10. Obtener todas las consultas médicas realizadas por el médico con ID igual a 3 durante el mes de agosto de 2024.

```
SELECT  c.id_consulta,  p.nombre AS nombre_paciente, c.fecha, c.diagnostico, c.tratamiento
FROM  Consultas c
JOIN Pacientes p ON c.id_paciente = p.id_paciente WHERE c.id_medico = 3 AND c.fecha BETWEEN '2024-08-01' AND '2024-08-31';
```
![image](https://github.com/user-attachments/assets/0d3b2037-7fcb-4146-867d-5bbd4e9f6be9)

### 11. Obtener el nombre de los pacientes junto con la fecha y el diagnóstico de todas las consultas médicas realizadas en agosto del 2024.

```
SELECT  p.nombre AS nombre_paciente, c.fecha, c.diagnostico
FROM Consultas c JOIN Pacientes p ON c.id_paciente = p.id_paciente WHERE  c.fecha BETWEEN '2024-08-01' AND '2024-08-31';
```
![image](https://github.com/user-attachments/assets/e22ef519-5251-45b6-b13e-53c69d20c249)

### 12. Obtener el nombre de los medicamentos prescritos más de una vez por el médico con ID igual a 2.

```
SELECT m.nombre AS nombre_medicamento,
COUNT(r.id_receta) AS cantidad_prescripciones
FROM Recetas r JOIN Medicamentos m ON r.id_medicamento = m.id_medicamento WHERE r.id_medico = 2
GROUP BY m.nombre
HAVING 
    COUNT(r.id_receta) > 1;
```
![image](https://github.com/user-attachments/assets/0baa9865-3ef2-4fde-a7e7-3fc1cd54259f)

### 13. Obtener el nombre de los pacientes junto con la cantidad total de recetas que han recibido.

```
SELECT p.nombre AS nombre_paciente, COUNT(r.id_receta) AS cantidad_recetas
FROM Pacientes p
LEFT JOIN Recetas r ON p.id_paciente = r.id_paciente
GROUP BY p.id_paciente;
```
![image](https://github.com/user-attachments/assets/bd57c49c-5c61-48f3-b8bc-afaf551db8c1)

### 14. Obtener el nombre del medicamento más recetado junto con la cantidad de recetas emitidas para ese medicamento.

```
SELECT m.nombre AS nombre_medicamento, COUNT(r.id_receta) AS cantidad_recetas
FROM Medicamentos m JOIN Recetas r ON m.id_medicamento = r.id_medicamento
GROUP BY m.id_medicamento
ORDER BY cantidad_recetas DESC
LIMIT 1;
```
![image](https://github.com/user-attachments/assets/a3ab6d20-5dc9-4a15-a1bd-cc34185aeefb)

### 15. Obtener el nombre del médico junto con el nombre del paciente y el número total de consultas realizadas por cada médico para cada paciente, ordenado por médico y paciente.

```
SELECT p.nombre AS NombrePaciente, 
       c.fecha AS FechaUltimaConsulta, 
       c.diagnostico AS Diagnostico
FROM Pacientes p
LEFT JOIN Consultas c ON p.id_paciente = c.id_paciente
WHERE c.fecha = (SELECT MAX(fecha) 
                 FROM Consultas 
                 WHERE id_paciente = p.id_paciente);
```
![image](https://github.com/user-attachments/assets/174250e7-520e-4483-9a26-1323f8575519)

### 16. Obtener el nombre del médico junto con el nombre del paciente y el número total de consultas realizadas por cada médico para cada paciente, ordenado por médico y paciente.

```
SELECT 
    m.nombre AS NombreMedico, p.nombre AS NombrePaciente, 
 COUNT(c.id_consulta) AS TotalConsultas

FROM 
    Medicos m
JOIN 
    Consultas c ON m.id_medico = c.id_medico
JOIN 
    Pacientes p ON c.id_paciente = p.id_paciente
GROUP BY 
    m.id_medico, p.id_paciente
ORDER BY 
    m.nombre, p.nombre;
```
![image](https://github.com/user-attachments/assets/b96671e6-d34f-4855-bd63-49388cebd17f)

### 17. Obtener el nombre del medicamento junto con el total de recetas prescritas para ese medicamento, el nombre del médico que lo recetó y el nombre del paciente al que se le recetó, ordenado por total de recetas en orden descendente.

```
SELECT me.nombre AS NombreMedicamento, COUNT(r.id_receta) AS TotalRecetas,m.nombre AS NombreMedico,p.nombre AS NombrePaciente
FROM Medicamentos me
JOIN  Recetas r ON me.id_medicamento = r.id_medicamento
JOIN Medicos m ON r.id_medico = m.id_medico
JOIN Pacientes p ON r.id_paciente = p.id_paciente
GROUP BY me.id_medicamento, m.id_medico, p.id_paciente
ORDER BY TotalRecetas DESC;
```
![image](https://github.com/user-attachments/assets/58e6d291-7ef8-49da-bc21-d43cd18711d3)

### 18. Obtener el nombre del médico junto con el total de pacientes a los que ha atendido, ordenado por el total de pacientes en orden descendente.

```
SELECT 
    m.nombre AS NombreMedico,
    COUNT(DISTINCT r.id_paciente) AS TotalPacientes
FROM 
    Medicos m
JOIN 
    Recetas r ON m.id_medico = r.id_medico
GROUP BY 
    m.id_medico
ORDER BY 
    TotalPacientes DESC;
```
![image](https://github.com/user-attachments/assets/497a5537-6859-40fe-8c05-ce1b5c534e13)


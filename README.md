# Proyecto Parte 1

Eduard Andres Rodriguez Holguin - Campuslands

### Modelo relacional

![drawSQL-sena-export-2023-12-06](https://github.com/EduardRodriguez20/Filtro_MySQL/assets/137240216/cd3860bf-db07-41d9-83ba-71cd0aee5737)

### Modelo entidad - relacion

![filtro](https://github.com/EduardRodriguez20/Filtro_MySQL/assets/137240216/82483311-5f78-4629-af36-75d348867266)

### Creacion y poblacion de las tablas

A continuacion se especifica la creacion de tablas y la poblacion de ellas mismas teniendo en cuenta mi criterio.

#### Creacion

```sql
   CREATE DATABASE sena;
   USE sena;

   CREATE TABLE carrera (
      id INT PRIMARY KEY NOT NULL,
      nombre VARCHAR(64) NOT NULL
   );
   CREATE TABLE ruta (
      id INT PRIMARY KEY NOT NULL,
      id_carrera INT NOT NULL,
      nombre VARCHAR(64) NOT NULL,
      FOREIGN KEY (id_carrera) REFERENCES carrera (id)  
   );
   CREATE TABLE aprendiz (
      id INT PRIMARY KEY NOT NULL,
      nombres VARCHAR(32) NOT NULL,
      apellidos VARCHAR(32) NOT NULL,
      edad INT NOT NULL
   );
   CREATE TABLE especialidad (
      id INT PRIMARY KEY NOT NULL,
      nombre VARCHAR(32) NOT NULL
   );
   CREATE TABLE instructor (
      id INT PRIMARY KEY NOT NULL,
      nombres VARCHAR(32) NOT NULL,
      apellidos VARCHAR(32) NOT NULL,
      id_especialidad INT NOT NULL,
      FOREIGN KEY (id_especialidad) REFERENCES especialidad (id)  
   );
   CREATE TABLE curso (
      id INT PRIMARY KEY NOT NULL,
      nombre VARCHAR(64) NOT NULL,
      id_instructor INT,
      FOREIGN KEY (id_instructor) REFERENCES instructor (id)
   );
   CREATE TABLE cursos_en_ruta (
      id INT PRIMARY KEY NOT NULL,
      id_ruta INT NOT NULL,
      id_curso INT NOT NULL,
      duracion_semanas INT NOT NULL,
      FOREIGN KEY (id_ruta) REFERENCES ruta (id),
      FOREIGN KEY (id_curso) REFERENCES curso (id)
   );
   CREATE TABLE matricula (
      id INT PRIMARY KEY NOT NULL,
      id_ruta INT NOT NULL,
      id_aprendiz INT NOT NULL,
      estado ENUM('Activo', 'Cancelado', 'Terminado'),
      FOREIGN KEY (id_ruta) REFERENCES ruta (id),
      FOREIGN KEY (id_aprendiz) REFERENCES aprendiz (id)
   );

   CREATE TABLE cursos_en_matricula (
    id INT PRIMARY KEY NOT NULL,
    id_matricula INT NOT NULL,
    id_curso_ruta INT NOT NULL,
    FOREIGN KEY (id_matricula) REFERENCES matricula (id),
    FOREIGN KEY (id_curso_ruta) REFERENCES cursos_en_ruta (id)
   );
```

#### Poblacion

```sql
   INSERT INTO carrera (id, nombre) VALUES
   (1, 'Desarrollo de Software'),
   (2, 'Electrónica'),
   (3, 'Mecánica Automotriz'),
   (4, 'Seguridad y Salud Ocupacional'),
   (5, 'Soldadura');

   INSERT INTO ruta (id, nombre, id_carrera) VALUES
   (1, 'Sistemas de Información Empresariales', 1),
   (2, 'Videojuegos', 1),
   (3, 'Machine Learning', 1),
   (4, 'Microcontroladores', 2),
   (5, 'Robótica', 2),
   (6, 'Dispositivos Bio-médicos', 2),
   (7, 'Motores Híbridos', 3),
   (8, 'Vehículos de Uso Agrícola', 3),
   (9, 'Sistemas de Gestión en Seguridad Ocupacional', 4),
   (10, 'Soldadura Autógena Industrial', 5),
   (11, 'Soldadura Eléctrica Industrial', 5),
   (12, 'Soldadura Submarina', 5);

   INSERT INTO aprendiz (id, nombres, apellidos, edad) VALUES
   (1, 'Carlos Saúl', 'Gómez', 18),
   (2, 'Leyla María', 'Delgado Vargas', 20),
   (3, 'Juan José', 'Cardona', 23),
   (4, 'Sergio Augusto', 'Contreras Navas', 19),
   (5, 'Ana María', 'Velázquez Parra', 24),
   (6, 'Gustavo', 'Noriega Alzate', 24),
   (7, 'Pedro Nell', 'Gómez Díaz', 21),
   (8, 'Jairo Augusto', 'Castro Camargo', 26),
   (9, 'Henry', 'Soler Vega', 25),
   (10, 'Antonio', 'Cañate Cortés', 28),
   (11, 'Daniel', 'Simancas Junior', 27);
   
   INSERT INTO especialidad (id, nombre) VALUES
   (1, 'Sistemas'),
   (2, 'Electrónica'),
   (3, 'Inglés'),
   (4, 'Salud Ocupacional'),
   (5, 'Soldadura'),
   (6, 'Mecánica');

   INSERT INTO instructor (id, nombres, apellidos, id_especialidad) VALUES
   (1, 'Ricardo Vicente', 'Jaimes', 1),
   (2, 'Marinela', 'Narvaez', 4),
   (3, 'Agustín', 'Parra Granados', 5),
   (4, 'Nelson Raúl', 'Buitrago', 6),
   (5, 'Roy Hernando', 'Llamas', 3),
   (6, 'Maria Jimena', 'Monsalve', 2),
   (7, 'Juan Carlos', 'Cobos', 2),
   (8, 'Pedro Nell', 'Santamaría', 1),
   (9, 'Andrea', 'González', 1),
   (10, 'Marisela', 'Sevilla', 4);

   INSERT INTO curso (id, nombre, id_instructor) VALUES
   (1, 'Matemáticas Básicas', 4),
   (2, 'Álgebra Computacional', 1),
   (3, 'Programación Básica', 3),
   (4, 'Inglés', 5),
   (5, 'Electrónica Básica', 7),
   (6, 'Motor de Cuatro Tiempos', NULL),
   (7, 'Enfermedades Laborales', NULL),
   (8, 'Higiene Postural en el Trabajo', NULL),
   (9, 'Ergonomía', NULL),
   (10, 'Legislación Laboral en Colombia', NULL),
   (11, 'Materiales de Soldadura', 3),
   (12, 'Métodos de Soldadura', NULL),
   (13, 'Fusión de Metales', 3),
   (14, 'Buceo 1', NULL),
   (15, 'Buceo 2', NULL),
   (16, 'Riesgo Eléctrico', NULL),
   (17, 'Bases de Datos Relacionales', 2),
   (18, 'Bases de Datos NO Relacionales', 2),
   (19, 'Electrónica Digital', 6),
   (20, 'Microprocesadores', 7);

   INSERT INTO cursos_en_ruta (id, id_ruta, id_curso, duracion_semanas) VALUES
   (1, 1, 1, 6),
   (2, 1, 2, 8),
   (3, 1, 3, 10),
   (4, 1, 4, 10),
   (5, 1, 17, 10),
   (6, 1, 18, 10),
   (7, 2, 1, 4),
   (8, 2, 2, 6),
   (9, 2, 3, 8),
   (10, 2, 4, 12),
   (11, 3, 3, 8),
   (12, 3, 4, 10),
   (13, 3, 17, 8),
   (14, 4, 5, 8),
   (15, 4, 19, 8),
   (16, 4, 20, 6),
   (17, 5, 5, 6),
   (18, 5, 19, 6),
   (19, 5, 20, 8),
   (20, 11, 11, 6),
   (21, 11, 13, 6),
   (22, 10, 11, 8),
   (23, 10, 14, 8);

   INSERT INTO matricula (id, id_ruta, id_aprendiz, estado) VALUES
   (1, 1, 1, 'Activo'),
   (2, 1, 2, 'Activo'),
   (3, 2, 3, 'Cancelado'),
   (4, 2, 4, 'Activo'),
   (5, 3, 5, 'Activo'),
   (6, 4, 6, 'Terminado'),
   (7, 4, 7, 'Terminado'),
   (8, 5, 8, 'Terminado'),
   (9, 5, 9, 'Cancelado'),
   (10, 11, 10, 'Terminado'),
   (11, 10, 11, 'Terminado');

   INSERT INTO cursos_en_matricula (id, id_matricula, id_curso_ruta) VALUES
   (1, 1, 5),
   (2, 1, 2),
   (3, 1, 3),
   (4, 1, 6),
   (5, 2, 1),
   (6, 2, 2),
   (7, 2, 3),
   (8, 2, 4),
   (9, 3, 7),
   (10, 3, 8),
   (11, 3, 9),
   (12, 4, 10),
   (13, 4, 7),
   (14, 4, 8),
   (15, 5, 11),
   (16, 5, 12),
   (17, 5, 13),
   (18, 6, 14),
   (19, 6, 15),
   (20, 6, 16),
   (21, 7, 14),
   (22, 7, 15),
   (23, 7, 16),
   (24, 8, 14),
   (25, 8, 15),
   (26, 9, 14),
   (27, 9, 15),
   (28, 9, 16),
   (29, 10, 20),
   (30, 10, 21),
   (31, 11, 22),
   (32, 11, 23);

```

### Consultas

1. Agregue un campo Estado_Matrícula a la tabla Matrícula que indique si el estudiante se encuentra “En Ejecución”, “Terminado” o “Cancelado”

   Se crea la tabla matricula con la especificacion requerida.

   ```sql
      CREATE TABLE matricula (
      id INT PRIMARY KEY NOT NULL,
      id_ruta INT NOT NULL,
      id_aprendiz INT NOT NULL,
      estado ENUM('Activo', 'Cancelado', 'Terminado'),
      FOREIGN KEY (id_ruta) REFERENCES ruta (id),
      FOREIGN KEY (id_aprendiz) REFERENCES aprendiz (id)
      );
   ```

   Validacion de la tabla:
   
   ```bash
   +-------------+----------------------------------------+------+-----+---------+-------+
   | Field       | Type                                   | Null | Key | Default | Extra |
   +-------------+----------------------------------------+------+-----+---------+-------+
   | id          | int                                    | NO   | PRI | NULL    |       |
   | id_ruta     | int                                    | NO   | MUL | NULL    |       |
   | id_aprendiz | int                                    | NO   | MUL | NULL    |       |
   | estado      | enum('Activo','Cancelado','Terminado') | YES  |     | NULL    |       |
   +-------------+----------------------------------------+------+-----+---------+-------+
   ```
   
2. Agregue a el campo edad a la tabla de Aprendices.

   Se cumple con el requerimiento desde la creacion de la tabla

   ```sql
      CREATE TABLE aprendiz (
      id INT PRIMARY KEY NOT NULL,
      nombres VARCHAR(32) NOT NULL,
      apellidos VARCHAR(32) NOT NULL,
      edad INT NOT NULL
      );
   ```

   Validacion de la tabla:
   
   ```bash
   +----------+-------------+------+-----+---------+-------+
   | Field    | Type        | Null | Key | Default | Extra |
   +----------+-------------+------+-----+---------+-------+
   | id       | int         | NO   | PRI | NULL    |       |
   | nombres  | varchar(32) | NO   |     | NULL    |       |
   | apellidos| varchar(32) | NO   |     | NULL    |       |
   | edad     | int         | NO   |     | NULL    |       |
   +----------+-------------+------+-----+---------+-------+
   ```

3. Si suponemos que los cursos tienen una duración diferente dependiendo de la ruta que lo contenga ¿qué modificación haría a la estructura de datos ya planteada?

   Creamos una tabla en la que se pueda establecer la relacion de muchos a muchos entre rutas y cursos, por lo tanto si un curso tiene diferente duracion teniendo en cuenta la ruta, en esta tabla se establece la duracion en semanas de la siguiente manera:

   ```sql
      CREATE TABLE cursos_en_ruta (
      id INT PRIMARY KEY NOT NULL,
      id_ruta INT NOT NULL,
      id_curso INT NOT NULL,
      duracion_semanas INT NOT NULL,
      FOREIGN KEY (id_ruta) REFERENCES ruta (id),
      FOREIGN KEY (id_curso) REFERENCES curso (id)
      );
   ```

   Validacion de la tabla:
   
   ```bash
   +------------------+------+------+-----+---------+-------+
   | Field            | Type | Null | Key | Default | Extra |
   +------------------+------+------+-----+---------+-------+
   | id               | int  | NO   | PRI | NULL    |       |
   | id_ruta          | int  | NO   | MUL | NULL    |       |
   | id_curso         | int  | NO   | MUL | NULL    |       |
   | duracion_semanas | int  | NO   |     | NULL    |       |
   +------------------+------+------+-----+---------+-------+
   ```

4. Seleccionar los nombres y edades de aprendices que están cursando la carrera de electrónica.

   ```sql
      SELECT CONCAT(aprendiz.nombres, " ", aprendiz.apellidos) AS nombre, aprendiz.edad AS edad FROM matricula
      INNER JOIN aprendiz ON id_aprendiz = aprendiz.id
      INNER JOIN ruta ON id_ruta = ruta.id
      INNER JOIN carrera ON ruta.id_carrera = carrera.id
      WHERE carrera.id = 2;
   ```

   Resultado:

   ```bash
   +------------------------------+------+
   | nombre                       | edad |
   +------------------------------+------+
   | Gustavo Noriega Alzate       |   24 |
   | Pedro Nell Gómez Díaz        |   21 |
   | Jairo Augusto Castro Camargo |   26 |
   | Henry Soler Vega             |   25 |
   +------------------------------+------+
   ```

5. Seleccionar Nombres de Aprendices junto al nombre de la ruta de aprendizaje que cancelaron.

   ```sql
      SELECT CONCAT(aprendiz.nombres, " ", aprendiz.apellidos) AS Aprendiz, ruta.nombre AS Ruta_Cancelada FROM matricula
      INNER JOIN aprendiz ON id_aprendiz = aprendiz.id
      INNER JOIN ruta ON id_ruta = ruta.id
      WHERE estado = "Cancelado";
   ```

   Resultado:
   
   ```bash
   +-------------------+----------------+
   | Aprendiz          | Ruta_Cancelada |
   +-------------------+----------------+
   | Juan José Cardona | Videojuegos    |
   | Henry Soler Vega  | Robótica       |
   +-------------------+----------------+
   ```

6. Seleccionar Nombre de los cursos que no tienen un instructor asignado.

   ```sql
      SELECT nombre FROM curso WHERE id_instructor IS NULL;
   ```

   Resultado:
   
   ```bash
   +---------------------------------+
   | nombre                          |
   +---------------------------------+
   | Motor de Cuatro Tiempos         |
   | Enfermedades Laborales          |
   | Higiene Postural en el Trabajo  |
   | Ergonomía                       |
   | Legislación Laboral en Colombia |
   | Métodos de Soldadura            |
   | Buceo 1                         |
   | Buceo 2                         |
   | Riesgo Eléctrico                |
   +---------------------------------+
   ```

7. Seleccionar Nombres de los instructores que dictan cursos en la ruta de aprendizaje “Sistemas de Información Empresariales”.

   ```sql
      SELECT CONCAT(instructor.nombres, " ", instructor.apellidos) AS Instructor, curso.nombre AS Curso FROM instructor
      INNER JOIN curso ON instructor.id = curso.id_instructor
      INNER JOIN cursos_en_ruta ON curso.id = cursos_en_ruta.id_curso
      INNER JOIN ruta ON cursos_en_ruta.id_ruta = ruta.id
      WHERE ruta.id = 1;
   ```

   Resultado:
   
   ```bash
   +------------------------+--------------------------------+
   | Instructor             | Curso                          |
   +------------------------+--------------------------------+
   | Nelson Raúl Buitrago   | Matemáticas Básicas            |
   | Ricardo Vicente Jaimes | Álgebra Computacional          |
   | Agustín Parra Granados | Programación Básica            |
   | Roy Hernando Llamas    | Inglés                         |
   | Marinela Narvaez       | Bases de Datos Relacionales    |
   | Marinela Narvaez       | Bases de Datos NO Relacionales |
   +------------------------+--------------------------------+
   ```

8. Genere un listado de todos los aprendices que terminaron una Carrera mostrando el nombre del profesional, el nombre de la carrera y el énfasis de la carrera (Nombre de la Ruta de aprendizaje)

   ```sql
      SELECT CONCAT(aprendiz.nombres, " ", aprendiz.apellidos) AS Profesional, 
      carrera.nombre AS Carrera,
      ruta.nombre AS Enfasis
      FROM matricula
      INNER JOIN aprendiz ON id_aprendiz = aprendiz.id
      INNER JOIN ruta ON id_ruta = ruta.id
      INNER JOIN carrera ON ruta.id_carrera = carrera.id
      WHERE matricula.estado = "Terminado";
   ```

   Resultado:
   
   ```bash
   +------------------------------+-------------+--------------------------------+
   | Profesional                  | Carrera     | Enfasis                        |
   +------------------------------+-------------+--------------------------------+
   | Gustavo Noriega Alzate       | Electrónica | Microcontroladores             |
   | Pedro Nell Gómez Díaz        | Electrónica | Microcontroladores             |
   | Jairo Augusto Castro Camargo | Electrónica | Robótica                       |
   | Antonio Cañate Cortés        | Soldadura   | Soldadura Eléctrica Industrial |
   | Daniel Simancas Junior       | Soldadura   | Soldadura Autógena Industrial  |
   +------------------------------+-------------+--------------------------------+
   ```

9. Genere un listado de los aprendices matriculados en el curso “Bases de Datos Relacionales”.

   Para esta consulta creamos una tabla que se llame cursos_en_matricula puesto que no se sabe que cursos ha escogido el estudiante en su matricula respecto a la ruta que ha escogido y asi poder dar solucion a la consulta

   ```sql
      CREATE TABLE cursos_en_matricula (
         id INT PRIMARY KEY NOT NULL,
         id_matricula INT NOT NULL,
         id_curso_ruta INT NOT NULL,
         FOREIGN KEY (id_matricula) REFERENCES matricula (id),
         FOREIGN KEY (id_curso_ruta) REFERENCES cursos_en_ruta (id)
      );
   ```

   Teniendo la tabla, poblamos teniendo en cuenta los datos del "INFORME GENERAL DE MATRICULAS" que se encuentra en el documento de la prueba.

   ```sql
      INSERT INTO cursos_en_matricula (id, id_matricula, id_curso_ruta) VALUES
      (1, 1, 5),
      (2, 1, 2),
      (3, 1, 3),
      (4, 1, 6),
      (5, 2, 1),
      (6, 2, 2),
      (7, 2, 3),
      (8, 2, 4),
      (9, 3, 7),
      (10, 3, 8),
      (11, 3, 9),
      (12, 4, 10),
      (13, 4, 7),
      (14, 4, 8),
      (15, 5, 11),
      (16, 5, 12),
      (17, 5, 13),
      (18, 6, 14),
      (19, 6, 15),
      (20, 6, 16),
      (21, 7, 14),
      (22, 7, 15),
      (23, 7, 16),
      (24, 8, 14),
      (25, 8, 15),
      (26, 9, 14),
      (27, 9, 15),
      (28, 9, 16),
      (29, 10, 20),
      (30, 10, 21),
      (31, 11, 22),
      (32, 11, 23);
   ```

   Por ultimo se hace la consulta requerida.

   ```sql
      SELECT CONCAT(aprendiz.nombres, " ", aprendiz.apellidos) AS Aprendiz, curso.nombre AS Curso FROM matricula
      INNER JOIN aprendiz ON id_aprendiz = aprendiz.id
      INNER JOIN cursos_en_matricula ON matricula.id = cursos_en_matricula.id_matricula
      INNER JOIN cursos_en_ruta ON cursos_en_matricula.id_curso_ruta = cursos_en_ruta.id
      INNER JOIN curso ON cursos_en_ruta.id_curso = curso.id
      WHERE curso.id = 17;
   ```

   Resultado:
   
   ```bash
   +---------------------------+-----------------------------+
   | Aprendiz                  | Curso                       |
   +---------------------------+-----------------------------+
   | Carlos Saúl Gómez         | Bases de Datos Relacionales |
   | Ana María Velázquez Parra | Bases de Datos Relacionales |
   +---------------------------+-----------------------------+
   ```

10.  Nombres de Instructores que no tienen curso asignado.
   
   ```sql
      SELECT CONCAT(instructor.nombres, " ", instructor.apellidos) FROM instructor 
      LEFT JOIN curso ON instructor.id = curso.id_instructor
      WHERE curso.id_instructor IS NULL;
   ```

   Resultado:
   
   ```bash
   +-----------------------+
   | nombre                |
   +-----------------------+
   | Pedro Nell Santamaría |
   | Andrea González       |
   | Marisela Sevilla      |
   +-----------------------+
   ```

### Preguntas de selección multiple

1. ¿Cuál es la definición correcta de un indice en MySQL?
- a) Una restricción que asegura que los valores en una columna sean únicos.
- b) Una estructura de datos que permite la rápida búsqueda de filas en una tabla.
- c) Un conjunto de datos almacenados para mejorar la seguridad de la base de datos.
- d) Un tipo de dato especializado para almacenar valores de fecha y hora.

Respuesta B

2. ¿Cuál de las siguientes afirmaciones sobre los indices en MySQL es verdadera?
- a) Los indices no afectan el rendimiento de las consultas.
- b) Los indices solo se utilizan para claves primarias.
- c) Los indices aceleran la velocidad de búsqueda de filas en una tabla.
- d) Los indices solo se pueden crear en columnas numéricas.

Respuesta C

3. ¿Cuál es el comando de SQL para crear un indice en una tabla en MySQL? 
- a) CREATE INDEX
- b) ADD INDEX
- c) SET INDEX
- d) MAKE INDEX

Respuesta A

4. ¿Qué comando de SQL se utiliza para eliminar un indice en MySQL?
- a) DROP INDEX
- b) REMOVE INDEX
- c) DELETE INDEX
- d) ERASE INDEX

Respuesta A

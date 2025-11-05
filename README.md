# trabajo-grupo-NicolasBello-y-FrankynVillalba
Nicolas Bello y Frankyn Villalba

# 📊 Proyecto de Bases de Datos Relacionales: PostgreSQL y MySQL

## 🎯 Objetivo del proyecto

Este proyecto tiene como finalidad aplicar de forma integral los conocimientos adquiridos en el curso, desarrollando el proceso completo de diseño e implementación de dos bases de datos relacionales: una en **PostgreSQL** y otra en **MySQL**, abordando temáticas distintas para cada motor.

---

## 🧠 Conceptos técnicos aplicados

### 🔹 Diseño conceptual y lógico
- **Modelo Entidad-Relación (E-R)**: Identificación de entidades, atributos, relaciones, cardinalidades y reglas de negocio.
- **Normalización**: Aplicación de buenas prácticas para evitar redundancia y asegurar integridad.
- **Cardinalidades**: Definición de relaciones uno-a-muchos y muchos-a-uno según el contexto.

### 🔹 Construcción física
- **Sentencias DDL**: Uso de `CREATE`, `ALTER`, `DROP` para definir tablas, claves primarias, foráneas, restricciones e índices.
- **Vistas**: Creación de vistas para facilitar consultas específicas.
- **Integridad referencial**: Implementación de claves foráneas y restricciones `NOT NULL`, `UNIQUE`, `CHECK`.

### 🔹 Carga de datos
- **Sentencias DML**: Uso de `INSERT` para poblar las tablas con datos de ejemplo que validan la estructura y relaciones.
- **Pruebas de integridad**: Validación de coherencia entre entidades relacionadas.

---

## 🧩 Codigos usados 

# crear contenedor

1. 

CREATE TABLE estacion (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100),
  ubicacion VARCHAR(100)
);

CREATE TABLE sensor (
  id SERIAL PRIMARY KEY,
  tipo VARCHAR(50),
  id_estacion INT REFERENCES estacion(id)
);

CREATE TABLE lectura (
  id SERIAL PRIMARY KEY,
  valor NUMERIC,
  fecha TIMESTAMP,
  id_sensor INT REFERENCES sensor(id)
);

CREATE TABLE tecnico (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100)
);

ALTER TABLE estacion ADD COLUMN id_tecnico INT REFERENCES tecnico(id);

2. 

CREATE TABLE libro (
  id INT AUTO_INCREMENT PRIMARY KEY,
  titulo VARCHAR(100),
  autor VARCHAR(100)
);

CREATE TABLE usuario (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100),
  correo VARCHAR(100)
);

CREATE TABLE prestamo (
  id INT AUTO_INCREMENT PRIMARY KEY,
  fecha_prestamo DATE,
  fecha_devolucion DATE,
  id_libro INT,
  id_usuario INT,
  FOREIGN KEY (id_libro) REFERENCES libro(id),
  FOREIGN KEY (id_usuario) REFERENCES usuario(id)
);

# crear bases postgres

INSERT INTO tecnico (nombre) VALUES ('Carlos Ruiz');
INSERT INTO estacion (nombre, ubicacion, id_tecnico) VALUES ('Estación Norte', 'Bogotá', 1);
INSERT INTO sensor (tipo, id_estacion) VALUES ('Temperatura', 1);
INSERT INTO lectura (valor, fecha, id_sensor) VALUES (22.5, NOW(), 1);

# crear bases sql

INSERT INTO libro (titulo, autor) VALUES ('El Principito', 'Antoine de Saint-Exupéry');
INSERT INTO usuario (nombre, correo) VALUES ('Laura Gómez', 'laura@example.com');
INSERT INTO prestamo (fecha_prestamo, fecha_devolucion, id_libro, id_usuario)
VALUES ('2025-11-01', '2025-11-15', 1, 1);

---

## 🧩 Decisiones de diseño

### 🐘 PostgreSQL – Sistema de Monitoreo Ambiental

- **Contexto**: Gestión de sensores IoT en estaciones meteorológicas.
- **Entidades clave**: `Estacion`, `Sensor`, `Lectura`, `Tecnico`.
- **Relaciones**:
  - Una estación tiene múltiples sensores.
  - Cada sensor genera múltiples lecturas.
  - Un técnico puede administrar varias estaciones.
- **Motivo de elección**: PostgreSQL permite trabajar con tipos de datos avanzados como `TIMESTAMP`, ideal para lecturas temporales.

### 🐬 MySQL – Biblioteca Escolar

- **Contexto**: Registro de préstamos de libros a estudiantes.
- **Entidades clave**: `Libro`, `Usuario`, `Prestamo`.
- **Relaciones**:
  - Un usuario puede realizar múltiples préstamos.
  - Cada préstamo está asociado a un único libro.
- **Motivo de elección**: MySQL es eficiente para operaciones transaccionales simples y consultas rápidas.

---

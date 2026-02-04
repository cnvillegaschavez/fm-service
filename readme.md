# DOCUMENTO DE ESPECIFICACIONES NO TÉCNICAS - SISTEMA FM

## 1. Objetivo

Registrar los acuerdos, configuraciones y parámetros definidos para la implementación del sistema FM, incluyendo características de equipos, codificación, parámetros técnicos, mantenimiento y reportes e integración con QR. Asegurando claridad, alcance para todos los participantes y equipos involucrados.

## 2. Ingreso al sistema

a. El ingreso deberá realizarse mediante un usuario y contraseña.

b. El usuario deberá logarse mediante un correo electrónico

c. La contraseña deberá generarla el usuario

d. Le debe llegar un token a su correo valido por 5 minutos para la creación de la contraseña

e. Debe tener un log de auditoria (con reporte)

f. Debe llegar un correo de notificación cuando se cree la contraseña o se restablezca, deberá llegar A un correo (parametrizable) del administrador

g. Debe de considerarse el restablecimiento de la contraseña, manejado también por un toquen

h. Cuando un usuario es externo (Cliente o Proveedor), su registro debe ser aprobada por el rol de gerente FM

## 3. Módulo de usuarios

a. El sistema tendrá un rol super administrador el cual ingresará los perfiles. Lo usuarios externos (proveedores y clientes) su registro en el sistema deberá pasar por aprobación del gerente de FM.

b. Los roles con los que cuenta el sistema son los siguientes:
   - Gerente general
   - Gerente de FM
   - Facility manager
   - Supervisor FM
   - Planner MTTO
   - Service desk FM
   - Técnicos
   - Proveedor
   - Cliente

### Permisos con los que cuentan los roles

| Roles/Módulos - Opciones | Clientes | Proveedores | Usuarios externos (Clientes, Proveedores) |
|--------------------------|----------|-------------|-------------------------------------------|
| Superadministrador | Registrar, editar y eliminar | | |
| Gerente general | | | |
| Gerente de FM | | | Aprueba registro de usuarios |
| Facility manager | | | |
| Supervisor FM | | | |
| Planner MTTO | | | |
| Service desk FM | | | |
| Técnicos | | | |
| Proveedor | | | |
| Cliente | | | |

c. El super administrador ingresa la data del usuario todos los campos son obligatorios:
   - Tipo de documento de identidad: DNI/CE
   - Número de Documento de identidad
   - Nombres del colaborador
   - Apellidos del colaborador
   - Correo corporativo
   - Celular

## 4. Módulo de Gestión de Clientes

Sistema que permite al Superadministrador registrar y administrar clientes con código autogenerado (RUC-CECO). Incluye datos básicos (RUC, razón social, domicilio fiscal, CECO), clasificación (público/privado, interno/externo, nacional/extranjero), y permite registrar múltiples representantes, usuarios y sucursales por cliente. Cuenta con listas desplegables con búsqueda, validación de RUC único, y capacidad de crear clientes sin salir de la ventana actual. Todas las acciones quedan registradas en auditoría.

### 4.1. Datos Generales del Cliente

#### 4.1.1. Código de Cliente
- Autogenerado por el sistema
- Formato: RUC-CECO
- Ejemplo: 20123456789-001
- Campo de solo lectura

#### 4.1.2. Nombre Completo / Razón Social
- Campo obligatorio
- Máximo 200 caracteres
- Campo de texto libre

#### 4.1.3. RUC (Registro Único de Contribuyentes)
- Campo obligatorio
- 11 dígitos numéricos
- Debe ser único en el sistema
- Validación automática de formato

#### 4.1.4. Domicilio Fiscal
- Campo obligatorio
- Dirección completa del domicilio fiscal del cliente

#### 4.1.5. Tipo de Cliente
- Campo con lista desplegable
- Opciones:
  - Público
  - Privado

#### 4.1.6. CECO (Centro de Costos)
- Campo obligatorio
- Código alfanumérico
- Utilizado para generar el Código de Cliente

#### 4.1.7. Clasificación: Interno o Externo
- Campo con lista desplegable
- Opciones: Interno, Externo

#### 4.1.8. Nacional / Extranjero
- Campo con lista desplegable
- Opciones: Nacional, Extranjero

#### 4.1.9. País
- Campo con lista desplegable
- Catálogo completo de países
- Campo obligatorio

### 4.2. Información de Contacto

#### 4.2.1. Email
- Campo obligatorio
- Validación de formato de correo electrónico
- Correo electrónico corporativo del cliente

#### 4.2.2. Teléfono
- Campo obligatorio
- Formato numérico
- Número de contacto principal del cliente

#### 4.2.3. WhatsApp
- Campo opcional
- Formato numérico
- Número de WhatsApp para contacto

### 4.3. Representante(s) del Cliente

El sistema debe permitir registrar uno o más representantes del cliente. Cada representante debe contar con los siguientes datos:

#### Campos del Representante:

- **Nombre Completo** (obligatorio)
  - Campo de texto libre
  - Nombre completo del representante

- **Correo Electrónico** (obligatorio)
  - Validación de formato de correo electrónico
  - Debe cumplir con estructura estándar de email

- **Celular** (obligatorio)
  - Formato numérico
  - Campo para número de contacto del representante

- **Cargo** (obligatorio)
  - Campo de texto libre
  - Cargo o posición del representante en la organización

#### Funcionalidades:

- Agregar representante
- Editar representante
- Eliminar representante

### 4.4. Usuarios del Cliente

El sistema debe permitir registrar uno o más usuarios del cliente. Cada usuario debe contar con los siguientes datos:

#### Campos del Usuario:

- **Nombre Completo** (obligatorio)
  - Campo de texto libre
  - Nombre completo del usuario

- **Correo Electrónico** (obligatorio)
  - Validación de formato de correo electrónico
  - Debe cumplir con estructura estándar de email

- **Celular** (obligatorio)
  - Formato numérico
  - Campo para número de contacto del usuario

- **Cargo** (obligatorio)
  - Campo de texto libre
  - Cargo o posición del usuario en la organización

#### Proceso de Aprobación:

- Estos usuarios serán aprobados por el rol de **Gerente de FM**

### 4.5. Sucursales del Cliente

El sistema debe permitir registrar una o más sucursales del cliente. Cada sucursal debe contar con:

#### Campos de la Sucursal:

- **Dirección** (obligatorio)
  - Dirección completa de la sucursal
  - Campo de texto libre

- **Sucursal Principal**
  - Opción para marcar una sucursal como principal
  - Solo una sucursal puede ser marcada como principal

### 4.6. Lógica de Generación del Código de Cliente

El sistema debe generar automáticamente el Código de Cliente mediante la concatenación de dos campos:

#### Fórmula:
```
Código de Cliente = RUC + "-" + CECO
```

#### Ejemplo:
- RUC ingresado: `20123456789`
- CECO ingresado: `001`
- Código generado: `20123456789-001`

#### Reglas:
- El código se genera automáticamente al guardar el registro del cliente
- El campo es de solo lectura, el usuario no puede editarlo
- El código debe ser único en el sistema
- El sistema debe validar que no exista duplicidad antes de guardar

### 4.7. Validaciones del Módulo de Clientes

- **RUC**: Debe ser único en el sistema (no se permite duplicados)
- **Formato de RUC**: 11 dígitos numéricos
- **Correo Electrónico**: Validación de formato válido (ejemplo@dominio.com)
- **Campos Obligatorios**: El sistema no debe permitir guardar si faltan campos obligatorios
- **CECO**: Campo obligatorio para poder generar el Código de Cliente

### 4.8. Funcionalidades de Búsqueda

El módulo debe contar con las siguientes opciones de búsqueda:

- Búsqueda por RUC (lista desplegable con autocompletado)
- Búsqueda por Razón Social 
- Búsqueda por Código de Cliente
- Búsqueda por Tipo de Cliente (Público/Privado)
- Búsqueda por ubicación
- Filtros combinados

## 5. Modulo de gestion integral de inmuebles

El módulo de gestión de inmuebles permite registrar y administrar las sedes o inmuebles asociados a los clientes. Cada inmueble puede estar vinculado a un cliente específico.

### 5.1. Campos del Formulario de Inmueble/Sede

#### 5.1.1. Información General

**Código de Inmueble o Sede**

- Autogenerado por el sistema
- Formato sugerido: INM-0001, INM-0002, etc.
- Campo de solo lectura
- Único en el sistema

**Nombre del Inmueble o Sede**

- Campo con lista desplegable para búsqueda
- Debe permitir crear o agregar nuevos inmuebles sin salir de la ventana actual
- Funcionalidad de autocompletado
- Al detectar que el inmueble no existe, debe mostrar opción: "¿Desea agregar un nuevo inmueble?"

#### 5.1.2. Ubicación del Inmueble

**Dirección del Inmueble o Sede**

- Campo obligatorio
- Dirección completa del inmueble

**Ubicación**

- Campo con lista desplegable
- Opciones:
  - Lima
  - Provincias

**Zona Geográfica**

- Campo con lista desplegable
- Opciones:
  - Zona Norte
  - Zona Sur
  - Zona Centro
  - Zona Oriente

**Departamento**

- Campo con lista desplegable
- Catálogo de departamentos del Perú
- Debe contar con funcionalidad de búsqueda para facilitar la selección

**Provincia**

- Campo con lista desplegable
- Catálogo de provincias del Perú
- Se debe filtrar según el departamento seleccionado
- Debe contar con funcionalidad de búsqueda

**País**

- Campo con lista desplegable
- Valor por defecto: Perú
- El sistema debe colocar automáticamente "Perú" como país predeterminado
- Campo editable si el inmueble se encuentra en otro país

#### 5.1.3. Fotos del Inmueble

**Fotos del Inmueble o Sede**

- El sistema debe permitir cargar hasta 3 fotos del inmueble
- Formatos permitidos: PNG, JPG
- Tamaño máximo recomendado: 5MB por archivo
- Debe mostrar vista previa de las imágenes cargadas
- Opción para eliminar fotos individuales

### 5.2. Filtros de Búsqueda

El módulo debe contar con filtros de búsqueda avanzados mediante listas desplegables:

- Búsqueda por Código de Inmueble
- Búsqueda por Nombre de Inmueble
- Búsqueda por Ubicación (Lima/Provincias)
- Búsqueda por Zona Geográfica
- Búsqueda por Departamento
- Búsqueda por Provincia
- Búsqueda por Cliente asociado
- Filtros combinados

### 5.3. Validaciones del Módulo de Inmuebles

- **Código de Inmueble**: Único en el sistema, generado automáticamente
- **Fotos**: Máximo 3 archivos, solo formatos PNG y JPG
- **Tamaño de archivos**: No exceder 5MB por imagen
- **Campos obligatorios**: Nombre, Dirección, Ubicación, Departamento, Provincia
- **País por defecto**: El sistema debe asignar "Perú" automáticamente
- **Relación con Departamento-Provincia**: La lista de provincias debe filtrarse según el departamento seleccionado

### 5.4. Relación entre Clientes e Inmuebles

#### 5.4.1. Modelo Relacional

- Un cliente puede tener múltiples inmuebles (relación 1 a muchos)
- Cada inmueble debe estar asociado a un cliente específico
- El sistema debe permitir visualizar todos los inmuebles asociados a un cliente
- Debe existir un campo o filtro para buscar inmuebles por cliente

#### 5.4.2. Visualización de Inmuebles por Cliente

En la ficha del cliente, debe existir una sección que muestre:

- Lista de inmuebles asociados al cliente
- Código y nombre de cada inmueble
- Dirección y ubicación
- Opciones para agregar, editar o eliminar inmueble

#### 5.4.3. Funcionalidad Especial: Crear Inmueble Sin Salir de Ventana

Cuando el usuario está registrando información del cliente y necesita agregar un nuevo inmueble que no existe en el sistema, debe poder hacerlo sin salir de la ventana actual.

**Flujo:**

1. El usuario comienza a escribir en el campo "Nombre del Inmueble o Sede"
2. Si el sistema no encuentra coincidencias, debe mostrar la opción: **[+ Crear Nuevo Inmueble]**
3. Al hacer clic, se abre un formulario modal o emergente con los campos necesarios
4. El usuario completa los datos del nuevo inmueble
5. Al guardar, el nuevo inmueble queda disponible y seleccionado automáticamente
6. El usuario puede continuar con el registro sin interrupciones

## 6. Gestión de Proveedores

Sistema que permite al Superadministrador registrar y administrar proveedores con código autogenerado (RUC). Incluye datos básicos (RUC, razón social, domicilio fiscal), clasificación (público/privado, nacional/extranjero), información de contacto, zona de cobertura y disponibilidad de servicios de emergencia. Permite registrar múltiples representantes por proveedor. Cuenta con listas desplegables con búsqueda, validación de RUC único, y capacidad de crear proveedores sin salir de la ventana actual. El sistema detecta proveedores cercanos al programar servicios, priorizando por zona de cobertura. Todas las acciones quedan registradas en auditoría.

### 6.1. Datos Generales del Proveedor

#### 6.1.1. Código de Proveedor
- Autogenerado por el sistema
- Formato: RUC
- Ejemplo: 20123456789
- Campo de solo lectura
- Único en el sistema

#### 6.1.2. Nombre Completo / Razón Social
- Campo obligatorio
- Máximo 200 caracteres
- Campo de texto libre
- Cuenta con lista desplegable para facilitar búsqueda
- Funcionalidad de autocompletado

#### 6.1.3. RUC (Registro Único de Contribuyentes)
- Campo obligatorio
- 11 dígitos numéricos
- Debe ser único en el sistema
- Validación automática de formato
- Campo con lista desplegable para búsqueda

#### 6.1.4. Domicilio Fiscal
- Campo obligatorio
- Dirección completa del domicilio fiscal del proveedor

#### 6.1.5. Tipo de Proveedor
- Campo con lista desplegable
- Opciones:
  - Público
  - Privado

#### 6.1.6. Nacional / Extranjero
- Campo con lista desplegable
- Opciones: Nacional, Extranjero

#### 6.1.7. País
- Campo con lista desplegable
- Catálogo completo de países
- Campo obligatorio

### 6.2. Información de Ubicación y Contacto

#### 6.2.1. Dirección del Proveedor
- Campo obligatorio
- Dirección completa de oficinas o sede principal

#### 6.2.2. Ubicación
- Campo con lista desplegable
- Opciones:
  - Lima
  - Provincias

#### 6.2.3. Departamento
- Campo con lista desplegable
- Catálogo de departamentos del Perú
- Ubicación de las oficinas del proveedor
- Debe contar con funcionalidad de búsqueda

#### 6.2.4. Email
- Campo obligatorio
- Validación de formato de correo electrónico
- Correo electrónico corporativo del proveedor

#### 6.2.5. Teléfono
- Campo obligatorio
- Formato numérico
- Número de contacto principal del proveedor

#### 6.2.6. WhatsApp
- Campo opcional
- Formato numérico
- Número de WhatsApp para contacto

### 6.3. Representante(s) del Proveedor

El sistema debe permitir registrar uno o más representantes del proveedor. Cada representante debe contar con los siguientes datos:

#### Campos del Representante:

- **Nombre Completo** (obligatorio)
  - Campo de texto libre
  - Nombre completo del representante

- **Correo Electrónico** (obligatorio)
  - Validación de formato de correo electrónico
  - Debe cumplir con estructura estándar de email

- **Celular** (obligatorio)
  - Formato numérico
  - Campo para número de contacto del representante

- **Cargo** (obligatorio)
  - Campo de texto libre
  - Cargo o posición del representante en la organización

#### Funcionalidades:

- Agregar representante
- Editar representante
- Eliminar representante

### 6.4. Zona de Cobertura

El sistema permite registrar una o más zonas de cobertura del proveedor:

#### 6.4.1. Departamento
- Campo con lista desplegable
- Catálogo de departamentos del Perú
- Permite seleccionar múltiples departamentos donde el proveedor brinda servicios

#### 6.4.2. Provincia
- Campo con lista desplegable
- Catálogo de provincias del Perú
- Se debe filtrar según el departamento seleccionado
- Permite seleccionar múltiples provincias de cobertura

#### 6.4.3. Distrito
- Campo con lista desplegable
- Catálogo de distritos del Perú
- Se debe filtrar según la provincia seleccionada
- Permite seleccionar múltiples distritos de cobertura

### 6.5. Servicios de Emergencia

#### 6.5.1. Atienden servicios de emergencia 24 x 7
- Campo tipo checkbox
- Opciones: Sí / No
- Esta información es utilizada por el sistema para priorizar proveedores en servicios de emergencia

### 6.6. Funcionalidades de Búsqueda

El módulo debe contar con las siguientes opciones de búsqueda:

- Búsqueda por RUC
- Búsqueda por Razón Social
- Búsqueda por Código de Proveedor
- Búsqueda por Tipo de Proveedor (Público/Privado)
- Búsqueda por Ubicación (Lima/Provincias)
- Búsqueda por Departamento
- Búsqueda por Zona de Cobertura
- Búsqueda por disponibilidad 24x7
- Filtros combinados

### 6.7. Validaciones del Módulo de Proveedores

- **RUC**: Debe ser único en el sistema (no se permite duplicados)
- **Formato de RUC**: 11 dígitos numéricos
- **Correo Electrónico**: Validación de formato válido (ejemplo@dominio.com)
- **Campos Obligatorios**: El sistema no debe permitir guardar si faltan campos obligatorios
- **Código de Proveedor**: Único en el sistema, generado automáticamente

## 7. Gestión de Equipos

Sistema que permite gestionar una base de datos completa de equipos con código autogenerado basado en categoría y subcategoría. Incluye información técnica (marca, modelo, serie), ubicación geográfica, integración con códigos QR, información financiera (precio con cálculo automático de IGV), y capacidad de almacenar fotografías. Cuenta con filtros de búsqueda avanzados por todas las variables del equipo.

### 7.1. Datos Generales del Equipo

#### 7.1.1. Código de Equipo
- Autogenerado por el sistema
- Formato: [Abreviatura Categoría] + [Número Subcategoría] + [Secuencial]
- Ejemplo: HV001 (HVAC + Ventiladores + 001)
- Campo de solo lectura
- Único en el sistema

#### 7.1.2. Descripción del Equipo
- Campo obligatorio
- Detalle completo del equipo
- Campo de texto libre

#### 7.1.3. Tipo de Equipo
- Campo con lista desplegable
- Opciones:
  - Equipos Mayores
  - Equipos Menores

#### 7.1.4. Marca del Equipo
- Campo obligatorio
- Campo de texto libre o lista desplegable

#### 7.1.5. Modelo del Equipo
- Campo obligatorio
- Campo alfanumérico
- Modelo específico del equipo

#### 7.1.6. Número de Serie
- Campo alfanumérico
- Identificador único del fabricante

### 7.2. Categorización del Equipo

#### 7.2.1. Categoría
El sistema cuenta con las siguientes categorías predefinidas:

| Categoría | Abreviatura |
|-----------|-------------|
| HVAC | HV |
| Sistema Eléctrico | SE |
| SACI | SA |
| Equipos de Sastrería | ES |
| Audio y Video | AV |

#### 7.2.2. Subcategoría
El sistema cuenta con subcategorías numeradas:

| Subcategoría | Código (3 dígitos) |
|--------------|-------------------|
| Ventiladores | 001 |
| Tablero | 002 |
| Panel de alarmas | 003 |
| Vaporizador | 004 |
| Proyector | 005 |
| Detectores | 006 |
| Máquina de coser | 007 |

#### 7.2.3. Equipo Asociado
- Campo opcional
- Permite vincular el equipo con otro equipo relacionado
- Lista desplegable con búsqueda

### 7.3. Ubicación del Equipo

#### 7.3.1. Ubicación
- Campo con lista desplegable
- Opciones:
  - Lima
  - Provincias

#### 7.3.2. Ubicación por Sede
- Campo con lista desplegable
- Muestra las sedes registradas en el sistema
- Vinculado con el módulo de Inmuebles

#### 7.3.3. Departamento
- Campo con lista desplegable
- Catálogo de departamentos del Perú
- Debe contar con funcionalidad de búsqueda

#### 7.3.4. Provincia
- Campo con lista desplegable
- Catálogo de provincias del Perú
- Se debe filtrar según el departamento seleccionado
- Debe contar con funcionalidad de búsqueda

#### 7.3.5. País
- Campo con lista desplegable
- Valor por defecto: Perú
- Campo editable si el equipo se encuentra en otro país

### 7.4. Información Administrativa

#### 7.4.1. Centro de Costo (CECO)
- Campo obligatorio
- Código alfanumérico
- Asociado al cliente o área responsable

#### 7.4.2. Código QR
- Campo para ingresar código QR del equipo
- Permite vincular el equipo con sistema de identificación por QR
- Campo alfanumérico

### 7.5. Información Financiera

#### 7.5.1. Precio del Equipo
- Campo obligatorio
- Formato numérico decimal
- Precio base del equipo (sin IGV)

#### 7.5.2. IGV
- Calculado automáticamente por el sistema
- Fórmula: Precio del Equipo × 18%
- Campo de solo lectura

#### 7.5.3. Precio Total (Incluido IGV)
- Calculado automáticamente por el sistema
- Fórmula: Precio del Equipo + IGV
- Campo de solo lectura

### 7.6. Fotografías del Equipo

#### 7.6.1. Fotos del Equipo
- El sistema debe permitir cargar hasta 3 fotos del equipo
- Formatos permitidos: PNG, JPG
- Tamaño máximo recomendado: 5MB por archivo
- Debe mostrar vista previa de las imágenes cargadas
- Opción para eliminar fotos individuales

### 7.7. Lógica de Generación del Código de Equipo

El sistema debe generar automáticamente el Código de Equipo mediante la siguiente estructura:

#### Fórmula:
```
Código de Equipo = [Abreviatura Categoría] + [Código Subcategoría] + [Número Secuencial]
```

#### Ejemplo:
- Categoría seleccionada: HVAC (Abreviatura: HV)
- Subcategoría seleccionada: Ventiladores (Código: 001)
- Número secuencial: Próximo disponible en el sistema
- Código generado: **HV001**

#### Reglas:
- El código se genera automáticamente al guardar el registro del equipo
- El campo es de solo lectura
- El código debe ser único en el sistema
- El número secuencial se incrementa automáticamente por cada nuevo equipo de la misma categoría y subcategoría

### 7.8. Funcionalidades de Búsqueda

El módulo debe contar con filtros de búsqueda por todas las variables:

- Búsqueda por Código de Equipo
- Búsqueda por Descripción
- Búsqueda por Tipo de Equipo (Mayores/Menores)
- Búsqueda por Marca
- Búsqueda por Modelo
- Búsqueda por Número de Serie
- Búsqueda por Categoría
- Búsqueda por Subcategoría
- Búsqueda por Ubicación (Lima/Provincias)
- Búsqueda por Sede
- Búsqueda por Departamento
- Búsqueda por Provincia
- Búsqueda por Centro de Costo
- Búsqueda por Código QR
- Búsqueda por rango de precio
- Filtros combinados

### 7.9. Validaciones del Módulo de Equipos

- **Código de Equipo**: Único en el sistema, generado automáticamente
- **Fotos**: Máximo 3 archivos, solo formatos PNG y JPG
- **Tamaño de archivos**: No exceder 5MB por imagen
- **Campos obligatorios**: Código, Descripción, Tipo, Marca, Modelo, Ubicación, Centro de Costo, Precio
- **Precio**: Debe ser un valor numérico positivo
- **IGV**: Cálculo automático, no editable manualmente
- **Código QR**: Debe ser único en el sistema
- **Relación Departamento-Provincia**: La lista de provincias debe filtrarse según el departamento seleccionado

## 8. Gestión de Herramientas

Sistema que permite gestionar una base de datos completa de herramientas, instrumentos y suministros con código autogenerado. Incluye información técnica (marca, serie), asignación a técnicos o almacenes, ubicación geográfica, integración con códigos QR, información financiera (precio con cálculo automático de IGV), y capacidad de almacenar fotografías. Cuenta con filtros de búsqueda avanzados por todas las variables.

### 8.1. Clasificación de Herramientas

El sistema cuenta con tres tipos principales:

| Código | Tipo | Ejemplo |
|--------|------|---------|
| H | Herramienta | Set de Alicates, Wincha, Martillo |
| I | Instrumento | Pinza Amperimétrica, Pirómetro, Taladro |
| S | Suministros | Cinta aislante, Cintillos, Tarugos |

### 8.2. Datos Generales de Herramientas

**Código de Herramienta**
- Autogenerado por el sistema
- Formato: [Tipo] + [Número Secuencial]
- Ejemplos: H01, I02, S03
- Campo de solo lectura
- Único en el sistema

**Descripción**
- Campo obligatorio
- Detalle completo de la herramienta o suministro
- Campo de texto libre

**Tipo de Herramienta**
- Campo con lista desplegable
- Opciones: Herramienta, Instrumento, Suministros
- Determina el prefijo del código

**Marca**
- Campo obligatorio
- Marca del fabricante
- Ejemplos: Stanley, Bosch, 3M, Fluker

**Número de Serie**
- Campo alfanumérico
- Identificador único del fabricante (cuando aplique)

**Unidad de Medida**
- Campo con lista desplegable
- Opciones: Und (Unidad), Pqt (Paquete), Set, etc.

**Cantidad**
- Campo numérico
- Cantidad de unidades disponibles

### 8.3. Asignación

**Asignado a**
- Campo con lista desplegable
- Opciones:
  - Técnico (nombre del técnico)
  - Almacén (ubicación del almacén)
- Permite rastrear la ubicación actual de la herramienta

**Ubicación**
- Cliente asociado
- Sede asociada
- Ubicación específica dentro de la sede

### 8.4. Información Administrativa

**Fecha de Compra**
- Campo con selector de fecha (lista desplegable)
- Formato: DD/MM/AAAA
- Campo obligatorio

**Centro de Costo (CECO)**
- Campo obligatorio
- Código alfanumérico
- Las herramientas deben estar asignadas a un centro de costo

**Código QR**
- Campo alfanumérico
- Permite vincular la herramienta con sistema de identificación por QR
- Debe ser único en el sistema

### 8.5. Ubicación Geográfica

**Departamento**
- Campo con lista desplegable
- Catálogo de departamentos del Perú

**Distrito**
- Campo con lista desplegable
- Catálogo de distritos del Perú
- Se filtra según departamento seleccionado

**País**
- Campo con lista desplegable
- Valor por defecto: Perú

### 8.6. Información Financiera

**Precio sin IGV**
- Campo obligatorio
- Formato numérico decimal
- Precio unitario de la herramienta

**IGV**
- Calculado automáticamente por el sistema
- Fórmula: Precio sin IGV × 18%
- Campo de solo lectura

**Precio con IGV**
- Calculado automáticamente por el sistema
- Fórmula: Precio sin IGV + IGV
- Campo de solo lectura

### 8.7. Fotografías

**Fotos de Herramienta**
- El sistema debe permitir cargar hasta 3 fotos
- Formatos permitidos: PNG, JPG, PDF
- Tamaño máximo recomendado: 5MB por archivo
- Debe mostrar vista previa de las imágenes cargadas
- Opción para eliminar fotos individuales

### 8.8. Catálogo de Herramientas Predefinidas

El sistema incluye un catálogo inicial de herramientas comunes:

| Código | Tipo | Descripción | Marca | Asignación | Unidad | Cantidad |
|--------|------|-------------|-------|------------|--------|----------|
| H01 | Herramienta | Set de Alicates dieléctricos | Stanley | Técnico | Und | 1 |
| H02 | Herramienta | Set de alicates dieléctricos Universal, punta, corte | Stanley | Técnico | Und | 1 |
| H03 | Herramienta | Wincha métrica | Stanley | Técnico | Und | 1 |
| H04 | Herramienta | Martillo mango de goma | Stanley | Técnico | Und | 1 |
| H05 | Herramienta | Llave francesa de 8" | Stanley | Técnico | Und | 1 |
| H06 | Herramienta | Llave stilson de 10" | Stanley | Técnico | Und | 1 |
| H07 | Herramienta | Set de brocas para madera | Stanley | Técnico | Und | 1 |
| H08 | Herramienta | Set de brocas para fierro | Stanley | Técnico | Und | 1 |
| H09 | Herramienta | Set de brocas para concreto | Stanley | Técnico | Und | 1 |
| H10 | Herramienta | Nivel profesional | Stanley | Técnico | Und | 1 |
| H11 | Herramienta | Cúter retráctil con seguro | Stanley | Técnico | Und | 1 |
| I01 | Instrumento | Pinza amperimétrica de 1000 Vac | Fluker | Técnico | Und | 1 |
| I02 | Instrumento | Pirómetro digital láser | Kusites | Técnico | Und | 1 |
| I03 | Instrumento | Taladro eléctrico | Bosch | Técnico | Und | 1 |
| I04 | Instrumento | Taladro atornillador con batería | Bosch | Técnico | Und | 1 |
| S01 | Suministros | Cinta aislante | 3M | Técnico | Und | 1 |
| S02 | Suministros | Paquete de cintillos | Nacional | Técnico | Pqt | 1 |
| S03 | Suministros | Tarugos de PVC | Nacional | Técnico | Pqt | 1 |

### 8.9. Funcionalidades de Búsqueda

Filtros de búsqueda por todas las variables:

- Búsqueda por Código de Herramienta
- Búsqueda por Descripción
- Búsqueda por Tipo (Herramienta/Instrumento/Suministros)
- Búsqueda por Marca
- Búsqueda por Número de Serie
- Búsqueda por Asignado a (Técnico/Almacén)
- Búsqueda por Cliente
- Búsqueda por Sede
- Búsqueda por Departamento
- Búsqueda por Distrito
- Búsqueda por Centro de Costo
- Búsqueda por Código QR
- Búsqueda por fecha de compra
- Búsqueda por rango de precio
- Filtros combinados

### 8.10. Validaciones

- **Código de Herramienta**: Único en el sistema, generado automáticamente
- **Fotos**: Máximo 3 archivos, formatos PNG, JPG, PDF permitidos
- **Tamaño de archivos**: No exceder 5MB por imagen
- **Campos obligatorios**: Código, Descripción, Tipo, Marca, Asignado a, Fecha de Compra, Centro de Costo, Precio
- **Precio**: Debe ser un valor numérico positivo
- **IGV**: Cálculo automático, no editable manualmente
- **Código QR**: Debe ser único en el sistema
- **Cantidad**: Debe ser un valor numérico positivo mayor a cero

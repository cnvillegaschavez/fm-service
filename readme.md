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

### 3.1. Gestión de Contraseñas de Usuarios

**Importante**: Los datos y contraseñas de usuarios deben actualizarse cada 3 meses.

**Proceso de Actualización de Contraseña**:
1. **Alerta Automática**: Sistema genera alerta automática 7 días antes del vencimiento de la contraseña
2. **Notificación al Usuario**: Usuario recibe notificación por correo electrónico para actualizar contraseña
3. **Bloqueo por Vencimiento**: Si el usuario no actualiza la contraseña en el plazo establecido, el sistema bloquea automáticamente el acceso
4. **Solicitud de Restablecimiento**: Usuario bloqueado debe solicitar restablecimiento de contraseña al Service Desk FM
5. **Restablecimiento Manual**: Service Desk FM puede restablecer manualmente la contraseña del usuario

**Validaciones**:
- La nueva contraseña debe ser diferente a las últimas 3 contraseñas utilizadas
- Debe contener al menos 8 caracteres
- Debe incluir mayúsculas, minúsculas, números y caracteres especiales
- El sistema registra en auditoría todos los cambios de contraseña

**Auditoría**:
- Fecha y hora de cambio de contraseña
- Usuario que realizó el cambio
- Tipo de cambio (manual, automático, restablecimiento)
- Estado anterior y nuevo estado

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

### 4.9. Funcionalidad de Registro de Cliente Nuevo

El sistema debe permitir el registro completo de información de clientes nuevos con las siguientes funcionalidades:

#### 4.9.1. Acceso al Módulo de Registro

El sistema debe proporcionar:
- Botón "Crear Cliente" o "Nuevo Cliente" visible en el módulo de Gestión de Clientes
- Acceso al formulario de registro de cliente
- Interfaz intuitiva para el ingreso de datos

#### 4.9.2. Validación de Duplicados

El sistema debe incluir:
- Barra de búsqueda por RUC antes de crear un nuevo registro
- Búsqueda automática en la base de datos al ingresar el RUC
- Mensaje de alerta si el RUC ya existe en el sistema
- Opción de visualizar el registro existente si se encuentra duplicado

#### 4.9.3. Formulario de Registro de Cliente

El sistema debe contar con un formulario completo que incluya los siguientes campos:

**Información Básica**:
- RUC (campo obligatorio, validación de formato)
- Razón Social (campo obligatorio)
- Domicilio Fiscal (campo obligatorio)
- CECO (campo obligatorio)
- Código de Cliente (generación automática: RUC-CECO)

**Clasificación**:
- Tipo de Cliente (Público/Privado) - campo obligatorio
- Clasificación (Interno/Externo) - campo obligatorio
- Origen (Nacional/Extranjero) - campo obligatorio
- País (campo obligatorio)

**Datos de Contacto**:
- Email (campo obligatorio, validación de formato)
- Teléfono (campo obligatorio)
- WhatsApp (opcional)

**Información Adicional**:
- Representantes (gestión de representantes legales)
- Usuarios (gestión de usuarios asociados al cliente)
- Sucursales (gestión de sucursales del cliente)

#### 4.9.4. Validaciones del Sistema

El sistema debe validar:
- Campos obligatorios completos antes de permitir guardar
- Formato correcto del RUC
- Formato válido de email
- Unicidad del RUC en la base de datos
- Formato del código de cliente generado automáticamente

#### 4.9.5. Generación Automática de Código de Cliente

El sistema debe:
- Generar automáticamente el Código de Cliente con el formato: RUC-CECO
- Mostrar el código generado en el formulario
- Permitir visualización del código antes de guardar el registro

#### 4.9.6. Actualización de Datos de Cliente Existente

Si el cliente ya existe en el sistema, el sistema debe permitir:
- Visualizar los datos actuales del cliente
- Editar campos modificables
- Comparar datos actuales con datos nuevos
- Guardar cambios realizados
- Registrar auditoría de las modificaciones

#### 4.9.7. Auditoría y Trazabilidad

El sistema debe registrar automáticamente:
- Usuario que creó el registro
- Fecha y hora de creación
- Usuario que realizó modificaciones
- Fecha y hora de cada actualización
- Historial de cambios en campos críticos
- Log completo de auditoría

#### 4.9.8. Funcionalidad de Envío de Correo de Bienvenida

El sistema debe incluir:
- Opción para enviar correo de bienvenida al cliente registrado
- Plantilla de correo predefinida con:
  - Asunto: "Bienvenido a Ruwaytech"
  - Mensaje de bienvenida personalizado
  - Código de cliente generado
  - Instrucciones de acceso al portal (si aplica)
  - Información de contacto de FM
- Envío automático al email registrado del cliente
- Confirmación de envío exitoso

#### 4.9.9. Consideraciones Especiales para Clientes Externos

**Nota Importante**: Para clientes externos nuevos, existe un proceso de validación de historial crediticio que se realiza **fuera del sistema** antes de proceder con el registro en el sistema. Este proceso involucra:
- Validación con CVC (Central de Verificación Crediticia)
- Aprobación previa antes del ingreso al sistema
- Una vez aprobado, se procede con el registro normal en el sistema

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

**Propósito**: Gestionar equipos instalados en sedes/inmuebles que requieren mantenimiento preventivo y correctivo.

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

**Propósito**: Gestionar herramientas de trabajo asignadas a técnicos o almacenadas en inventario.

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

## 9. Gestión de Contratos

**Propósito**: Gestionar el ciclo completo de contratos con clientes, desde la solicitud inicial hasta la firma electrónica y envío al cliente, incluyendo revisiones, observaciones y aprobaciones.

Sistema que permite gestionar el flujo de contratos de manera colaborativa entre FM, Cliente, Legal y Gerente General. Incluye carga de documentos, gestión de versiones, registro de observaciones, notificaciones automáticas, firma electrónica y auditoría completa. El sistema maneja dualidad de moneda (S/. y $), tipo de cambio automático desde SUNAT, gestión de IGV y cálculo de FEE.

**IMPORTANTE - Arquitectura de Dos Frentes:**

El módulo de Gestión de Contratos está diseñado con **dos interfaces separadas e independientes**:

1. **Módulo FM (Interno)** - Sección 9.1 a 9.10
   - Interface administrativa completa para usuarios internos
   - Roles: Superadministrador, Gerente General, Gerente de FM, Facility Manager, etc.
   - Gestión completa del ciclo de contratos
   - Configuración de FEE, IGV, documentos, estados
   - Auditoría y reportes avanzados

2. **Portal de Clientes (Externo)** - Sección 9.11
   - Interface exclusiva y simplificada para clientes
   - Acceso mediante credenciales propias
   - Vista limitada solo a información del cliente
   - Funcionalidades específicas: consulta, descarga, carga de contrapropuestas, firma
   - Dashboard personalizado por cliente

Ambos frentes comparten la misma base de datos pero tienen interfaces, permisos y funcionalidades diferenciadas según el tipo de usuario.

### 9.1. Estados del Contrato

El sistema debe manejar los siguientes estados del contrato:

| Estado | Descripción |
|--------|-------------|
| Recibido | Contrato inicial cargado al sistema (primer estado) |
| En Revisión | FM está revisando el contrato |
| Con Observaciones | FM registró observaciones al contrato |
| Observaciones Enviadas | Sistema notificó observaciones al cliente |
| Contrapropuesta Recibida | Cliente envió contrapropuesta (cargada al sistema) |
| En Revisión Legal | Contrato enviado a Legal para revisión |
| Legal con Observaciones | Legal envió observaciones y correcciones |
| Propuesta Enviada | FM envió 2da propuesta al cliente |
| Aceptado | Cliente aceptó la propuesta |
| En Firma | Habilitado para firma electrónica |
| Firmado | Contrato firmado por todas las partes |
| Finalizado | Contrato enviado al cliente y archivado |

### 9.2. Datos Generales del Contrato

#### 9.2.1. Código de Contrato
- Autogenerado por el sistema
- Formato: CTR-AAAA-NNNN (Ejemplo: CTR-2026-0001)
- Campo de solo lectura
- Único en el sistema

#### 9.2.2. Cliente
- Campo con lista desplegable
- Vinculado al módulo de Gestión de Clientes
- Campo obligatorio

#### 9.2.3. Tipo de Cliente
- Se obtiene automáticamente del cliente seleccionado
- Opciones: Interno / Externo
- Determina el cálculo del FEE

#### 9.2.4. Fecha de Solicitud
- Campo con selector de fecha
- Fecha en que FM solicita el contrato
- Se registra automáticamente al crear la solicitud

#### 9.2.5. Fecha de Vigencia
- Fecha de inicio de vigencia del contrato
- Campo obligatorio

#### 9.2.6. Fecha de Vencimiento
- Fecha de fin de vigencia del contrato
- Campo obligatorio

#### 9.2.7. Moneda
- Campo con lista desplegable
- Opciones: Soles (S/.) / Dólares ($)
- Campo obligatorio

### 9.3. Gestión de Documentos del Contrato

#### 9.3.1. Carga de Contrato Inicial
- El Gerente de FM debe cargar el contrato recibido del cliente
- Formatos permitidos: PDF, DOCX
- Tamaño máximo: 10MB
- El sistema debe registrar:
  - Fecha y hora de carga
  - Usuario que cargó el documento
  - Versión del documento (se inicia en v1.0)

#### 9.3.2. Versionado de Documentos
- El sistema debe mantener historial completo de versiones
- Cada nueva carga incrementa la versión
- Formato de versión: v1.0, v1.1, v2.0, etc.
- Se debe permitir descargar versiones anteriores
- No se pueden eliminar versiones anteriores

#### 9.3.3. Carga de Contrapropuestas
- Cuando el cliente envía contrapropuesta (por correo), FM debe cargarla al sistema
- El sistema genera nueva versión automáticamente
- Se notifica a los usuarios correspondientes

#### 9.3.4. Documentos de Legal
- Cuando Legal envía observaciones (por correo), FM debe cargarlas al sistema
- Formatos permitidos: PDF, DOCX
- Se vincula con el contrato principal

### 9.4. Gestión de Observaciones

#### 9.4.1. Registro de Observaciones por FM
- FM puede registrar observaciones al contrato
- Campos:
  - Descripción de la observación (obligatorio)
  - Tipo: Modificación / Aclaración / Rechazo
  - Prioridad: Alta / Media / Baja
  - Fecha de registro (automático)

#### 9.4.2. Envío de Observaciones
- FM envía observaciones al cliente desde el sistema
- El sistema genera notificación automática al cliente
- Se envía correo electrónico al cliente con las observaciones
- Estado del contrato cambia a "Observaciones Enviadas"

#### 9.4.3. Observaciones de Legal
- Legal envía observaciones por correo (proceso manual)
- FM debe registrar las observaciones de Legal en el sistema
- Se vinculan con el contrato

### 9.5. Sistema de Notificaciones

#### 9.5.1. Notificaciones Automáticas por Email

El sistema debe enviar notificaciones automáticas por correo electrónico en los siguientes casos:

| Evento | Destinatario | Contenido |
|--------|--------------|-----------|
| Contrato cargado al sistema | FM | Notificación de contrato disponible |
| Observaciones registradas | Gerente de FM | Notificación de observaciones pendientes |
| Observaciones enviadas al cliente | Cliente | Email con observaciones detalladas |
| Contrapropuesta cargada | FM | Notificación de nueva versión disponible |
| Contrato enviado a Legal | Legal | Notificación de contrato para revisión |
| Propuesta aceptada | Gerente de FM | Notificación de aceptación del cliente |
| Habilitado para firma | FM | Notificación para gestionar firmas |
| Contrato firmado | Gerente General | Notificación de contrato firmado |

#### 9.5.2. Notificaciones Internas del Sistema

- El sistema debe mostrar notificaciones internas para los usuarios
- Panel de notificaciones visible en el dashboard
- Contador de notificaciones pendientes
- Historial de notificaciones

### 9.6. Gestión de Firma Electrónica

#### 9.6.1. Habilitación de Firma
- Cuando el cliente acepta la propuesta (proceso manual), FM actualiza el estado en el sistema
- El sistema habilita automáticamente la opción de firma electrónica
- Se notifica a FM para gestionar las firmas

#### 9.6.2. Proceso de Firmas
- FM gestiona el proceso de firmas electrónicas
- El sistema debe registrar:
  - Firmantes requeridos (nombre, cargo, email)
  - Fecha y hora de cada firma
  - IP y ubicación de cada firma
  - Certificado digital de firma

#### 9.6.3. Validación de Firmas
- Todas las firmas requeridas deben completarse
- El sistema valida la autenticidad de cada firma
- Una vez firmado por todas las partes, el estado cambia a "Firmado"

#### 9.6.4. Notificación de Contrato Firmado
- El sistema notifica automáticamente al Gerente General
- Se genera versión final del contrato con todas las firmas
- El documento queda bloqueado para edición

### 9.7. Gestión de Moneda

- El sistema maneja dualidad de moneda (S/. y $)
- Todos los costos y ventas pueden registrarse en cualquiera de las dos monedas
- El sistema convierte automáticamente usando el tipo de cambio configurado en el módulo de **Datos Maestros** (Módulo 10)
- El tipo de cambio usado queda registrado en el contrato
- En reportes se muestra ambas monedas

### 9.8. Aplicación de IGV

- El sistema calcula automáticamente el IGV en cotizaciones
- Fórmula: Monto Base × IGV%
- Total con IGV = Monto Base + IGV
- El porcentaje de IGV se obtiene del módulo de **Datos Maestros** (Módulo 10)

### 9.9. Gestión y Cálculo del FEE

#### 9.9.1. Configuración del FEE
- Campo editable solo por **FM** y **Gerente de FM**
- Se edita durante el proceso de cotización formal
- Valor expresado en porcentaje (Ejemplo: 15%, 20%)
- El FEE queda registrado en el contrato

#### 9.9.2. Cálculo del FEE según Tipo de Cliente

**Para Cliente Externo:**
```
Precio de Venta = Costo del Servicio / (1 - FEE)
```

**Ejemplo Cliente Externo:**
- Costo del Servicio: S/. 1,000
- FEE: 20% (0.20)
- Precio de Venta = 1,000 / (1 - 0.20) = 1,000 / 0.80 = S/. 1,250

**Para Cliente Interno:**
```
Precio de Venta = Costo del Servicio × (1 + FEE)
```

**Ejemplo Cliente Interno:**
- Costo del Servicio: S/. 1,000
- FEE: 15% (0.15)
- Precio de Venta = 1,000 × (1 + 0.15) = 1,000 × 1.15 = S/. 1,150

#### 9.9.3. Visualización del FEE
- El sistema debe mostrar claramente:
  - Costo del Servicio
  - FEE aplicado (%)
  - Cálculo del FEE (monto en moneda)
  - Precio de Venta Final
  - IGV
  - Total con IGV

### 9.10. Funcionalidad del Proceso de Gestión de Contratos

El sistema debe permitir la gestión integral del ciclo de vida de los contratos con las siguientes funcionalidades:

#### 9.10.1. Registro Inicial de Contrato

El sistema debe proporcionar:
- **Dos modalidades de ingreso**:
  - **Modalidad A**: Registro manual por Gerente de FM cuando el cliente envía el contrato por correo
  - **Modalidad B**: Carga directa por el cliente desde el Portal de Clientes
- **Formulario de registro** con campos:
  - Generación automática del código de contrato
  - Fecha de solicitud
  - Fechas de vigencia y vencimiento
  - Selección de moneda (S/. o $)
  - Carga del documento inicial (PDF)
  - Datos generales del contrato
- **Estado inicial**: "Recibido"
- **Notificación automática** a FM y Gerente de FM

#### 9.10.2. Funcionalidad de Revisión y Observaciones

El sistema debe incluir:
- Sección para registro de observaciones al contrato
- Campo de texto para detallar cada observación
- Opción de marcar observaciones como críticas o menores
- Cambio automático de estado a "En Revisión" → "Con Observaciones"
- Historial de observaciones registradas
- Indicador de fecha y usuario que registró cada observación

#### 9.10.3. Envío Automático de Observaciones

El sistema debe permitir:
- Botón "Enviar Observaciones al Cliente"
- Generación automática de email con las observaciones registradas
- Notificación al cliente por correo electrónico
- Actualización automática del estado a "Observaciones Enviadas"
- Registro de fecha y hora de envío
- Confirmación de envío exitoso

#### 9.10.4. Gestión de Contrapropuestas

El sistema debe proporcionar:
- **Recepción de contrapropuestas** por dos vías:
  - Carga manual por FM cuando el cliente envía por correo
  - Carga directa por el cliente desde el Portal de Clientes
- **Versionamiento de documentos**:
  - Almacenamiento de cada versión del contrato
  - Numeración automática de versiones (v1, v2, v3, etc.)
  - Historial de versiones con fecha de carga
- **Notificación automática** a FM cuando se recibe contrapropuesta
- **Actualización de estado** a "Contrapropuesta Recibida"

#### 9.10.5. Gestión de Revisión Legal

El sistema debe incluir:
- Actualización de estado a "En Revisión Legal"
- Notificación automática al área Legal
- Sección para registrar observaciones de Legal
- Campo de texto para detallar correcciones solicitadas
- Cambio de estado a "Legal con Observaciones"
- Historial de observaciones legales

#### 9.10.6. Gestión de Propuestas

El sistema debe permitir:
- Carga de nueva versión del contrato (2da propuesta)
- Actualización automática del número de versión
- Envío automático de notificación al cliente
- Cambio de estado a "Propuesta Enviada"
- Registro de fecha de envío
- Opción de agregar comentarios a la propuesta enviada

#### 9.10.7. Funcionalidad de Aceptación

El sistema debe proporcionar:
- Opción para marcar el contrato como "Aceptado"
- Actualización automática del estado a "Aceptado"
- Notificación automática a Gerente de FM
- Registro de fecha de aceptación
- Confirmación visual de la aceptación

#### 9.10.8. Habilitación de Firma Electrónica

El sistema debe incluir:
- Activación automática de la opción de firma electrónica cuando el contrato es aceptado
- Cambio automático de estado a "En Firma"
- Notificación automática a FM
- Interfaz de gestión de firmas
- Indicador de firmas pendientes y completadas

#### 9.10.9. Gestión de Firmas Electrónicas

El sistema debe permitir:
- Registro de cada firma con validadores del sistema
- Identificación de firmantes requeridos
- Seguimiento del estado de cada firma (Pendiente/Completada)
- Validación de identidad del firmante
- Almacenamiento seguro de las firmas digitales
- Certificación de fecha y hora de cada firma
- Generación de hash de verificación

#### 9.10.10. Validación de Contrato Firmado

El sistema debe proporcionar:
- Validación automática de que todas las firmas estén completadas
- Actualización automática del estado a "Firmado"
- Notificación automática a Gerente General
- Generación del contrato final con todas las firmas
- Registro de fecha de finalización del proceso de firmas
- Sello de tiempo del documento firmado

#### 9.10.11. Archivado y Finalización

El sistema debe incluir:
- Opción de envío del contrato firmado al cliente
- Archivado automático del contrato en estado "Finalizado"
- Actualización del estado a "Finalizado"
- Almacenamiento seguro del documento final
- Generación de reporte de cierre del contrato
- Registro completo del historial del proceso

#### 9.10.12. Notificaciones Automáticas del Sistema

El sistema debe enviar notificaciones automáticas en los siguientes eventos:
- Registro de nuevo contrato → Notifica a FM y Gerente de FM
- Observaciones enviadas → Notifica al Cliente
- Contrapropuesta recibida → Notifica a FM
- Envío a Legal → Notifica a Legal
- Propuesta enviada → Notifica al Cliente
- Contrato aceptado → Notifica a Gerente de FM
- Firma electrónica habilitada → Notifica a FM
- Contrato firmado → Notifica a Gerente General

#### 9.10.13. Trazabilidad y Auditoría

El sistema debe registrar:
- Usuario que realizó cada acción
- Fecha y hora de cada cambio de estado
- Historial completo de versiones del documento
- Registro de todas las observaciones
- Log de notificaciones enviadas
- Historial de firmas electrónicas
- Auditoría completa del ciclo de vida del contrato

**Nota Importante**: La solicitud inicial de contrato al cliente se realiza **fuera del sistema** mediante correo electrónico o comunicación directa. El sistema entra en funcionamiento a partir del registro inicial del contrato (cuando el cliente o FM carga el primer documento).

### 9.11. Portal de Clientes - Bandeja de Contratos

**Propósito**: Proporcionar un portal web exclusivo para clientes con interfaz dedicada donde puedan visualizar, consultar y descargar sus contratos, así como responder a observaciones y gestionar el proceso de contrapropuestas de manera autónoma.

**NOTA IMPORTANTE:** Esta es una interfaz completamente separada del módulo administrativo de FM. El portal de clientes debe tener:
- URL dedicada (Ejemplo: clientes.sistemaFM.com o portal.sistemaFM.com)
- Diseño y branding diferenciado
- Login independiente con credenciales de cliente
- Seguridad reforzada para acceso externo
- Responsive design para acceso desde móviles y tablets

#### 9.11.1. Acceso al Portal de Clientes

**Autenticación:**
- El cliente accede mediante URL exclusiva del portal
- Login con correo electrónico y contraseña
- Validación con token (5 minutos de vigencia) al crear/restablecer contraseña
- Opción "Recordar sesión" por 30 días
- Autenticación de dos factores (opcional, configurable por Gerente FM)

**Permisos:**
- El rol **Cliente** tiene acceso a su propia bandeja de contratos
- Cada cliente solo puede ver los contratos asociados a su empresa
- Los usuarios del cliente pueden ver todos los contratos de su organización

**Acceso:**
- Menú principal: "Mis Contratos" o "Bandeja de Contratos"
- Dashboard con resumen de contratos activos, pendientes y finalizados

#### 9.11.2. Vista Principal de la Bandeja

La bandeja debe mostrar una lista de contratos con la siguiente información:

**Columnas Visibles:**
- Código de Contrato
- Fecha de Solicitud
- Estado del Contrato (con indicador visual de color)
- Fecha de Vigencia
- Fecha de Vencimiento
- Moneda (S/. o $)
- Versión del Documento
- Acciones Disponibles

**Indicadores Visuales por Estado:**
- **Solicitado**: Azul (información)
- **Con Observaciones / Observaciones Enviadas**: Amarillo (atención requerida)
- **Propuesta Enviada**: Naranja (acción requerida)
- **Aceptado / En Firma**: Verde claro (en proceso)
- **Firmado / Finalizado**: Verde (completado)

#### 9.11.3. Funcionalidades Disponibles para el Cliente

**Inicio de Contrato - Carga de Documento Inicial:**
- El cliente puede iniciar el registro de un nuevo contrato desde su portal
- Después de recibir la solicitud de FM por correo (proceso manual), el cliente accede al portal
- Botón "Nuevo Contrato" o "Cargar Contrato"
- El sistema solicita:
  - Cliente (autocompletado según el usuario logueado)
  - Fecha de Vigencia (obligatorio)
  - Fecha de Vencimiento (obligatorio)
  - Moneda (S/. o $) (obligatorio)
  - Documento de contrato inicial (PDF, DOCX, máximo 10MB)
  - Comentarios o notas adicionales (opcional)
- Al cargar el contrato inicial, el sistema:
  - Genera automáticamente el código de contrato (CTR-AAAA-NNNN)
  - Notifica automáticamente a FM y Gerente de FM
  - Crea el registro con estado "Recibido"
  - Genera versión inicial del documento (v1.0)
  - Registra fecha, hora y usuario que cargó el documento

**Visualización de Contratos:****
- Ver detalles completos del contrato
- Descargar versión actual del documento (PDF/DOCX)
- Descargar versiones anteriores del documento
- Ver historial de cambios y versiones

**Gestión de Observaciones:**
- Ver observaciones enviadas por FM
- Ver observaciones de Legal (cuando aplique)
- Botón "Descargar Observaciones" para exportar en PDF

**Carga de Contrapropuestas:**
- Cuando el estado es "Observaciones Enviadas", el cliente puede:
  - Cargar documento de contrapropuesta
  - Formatos permitidos: PDF, DOCX
  - Tamaño máximo: 10MB
  - Agregar comentarios o notas
- Al cargar contrapropuesta, el sistema:
  - Notifica automáticamente a FM
  - Cambia el estado a "Contrapropuesta Recibida"
  - Genera nueva versión del documento

**Aceptación de Propuestas:**
- Cuando el estado es "Propuesta Enviada", el cliente puede:
  - Botón "Aceptar Propuesta"
  - Botón "Enviar Observaciones Adicionales"
- Al aceptar propuesta:
  - El cliente debe confirmar la aceptación
  - El sistema cambia el estado a "Aceptado"
  - Se notifica automáticamente a FM y Gerente General

**Firma Electrónica:**
- Cuando el estado es "En Firma", el cliente puede:
  - Acceder al módulo de firma electrónica
  - Ver representantes habilitados para firmar
  - Firmar electrónicamente el contrato
- El sistema valida:
  - Identidad del firmante
  - Certificado digital
  - Registro de IP y ubicación

**Descarga de Contrato Firmado:**
- Cuando el estado es "Firmado" o "Finalizado":
  - Descargar contrato con todas las firmas electrónicas
  - Exportar certificado de firmas
  - Versión final con sello de "FIRMADO"

#### 9.11.4. Notificaciones para Clientes

El cliente recibe notificaciones automáticas por email y en el sistema en los siguientes casos:

| Evento | Contenido de la Notificación |
|--------|------------------------------|
| Contrato cargado por el cliente | "Su contrato [código] ha sido recibido y está en revisión" |
| Observaciones enviadas por FM | "Tiene observaciones pendientes en contrato [código]" |
| Propuesta enviada por FM | "Nueva propuesta disponible para contrato [código]" |
| Contrato habilitado para firma | "Contrato [código] listo para firma electrónica" |
| Contrato firmado completamente | "Contrato [código] ha sido firmado por todas las partes" |
| Contrato finalizado | "Contrato [código] ha sido enviado y archivado" |

#### 9.11.5. Panel de Resumen (Dashboard del Cliente)

**Indicadores Principales:**
- Total de contratos activos
- Contratos pendientes de acción del cliente
- Contratos en proceso de firma
- Contratos firmados este año
- Próximos vencimientos (contratos que vencen en los próximos 30 días)

**Gráficos Visuales:**
- Estados de contratos (gráfico de barras o circular)
- Línea de tiempo de contratos por mes
- Alertas de contratos por vencer

#### 9.11.6. Filtros de Búsqueda para Clientes

- Búsqueda por Código de Contrato
- Búsqueda por Estado
- Búsqueda por Fecha de Solicitud (rango)
- Búsqueda por Fecha de Vigencia (rango)
- Búsqueda por Fecha de Vencimiento (rango)
- Búsqueda por Moneda (S/. / $)
- Búsqueda por Versión del documento
- Filtro: "Requieren mi acción" (contratos con observaciones o pendientes de aceptación)
- Filtro: "Próximos a vencer" (en los próximos 30/60/90 días)
- Filtros combinados

#### 9.11.7. Validaciones en la Bandeja del Cliente

- El cliente solo puede ver contratos de su propia empresa
- Solo puede cargar contrapropuestas cuando el estado lo permite
- Solo puede aceptar propuestas cuando el estado es "Propuesta Enviada"
- La carga de documentos está limitada a formatos permitidos (PDF, DOCX)
- Tamaño máximo de archivo: 10MB
- Solo representantes autorizados pueden firmar electrónicamente

#### 9.11.8. Historial y Trazabilidad para el Cliente

El cliente puede ver:
- Historial completo del contrato
- Todas las versiones del documento
- Fecha y hora de cada acción
- Usuario que realizó cada acción (tanto del lado del cliente como de FM)
- Observaciones históricas
- Registro de notificaciones enviadas

#### 9.11.9. Exportación de Información

El cliente puede exportar:
- Lista de contratos a Excel/PDF
- Documento del contrato (cualquier versión)
- Observaciones en PDF
- Certificado de firmas electrónicas
- Reporte de contratos por período

#### 9.11.10. Características Técnicas del Portal de Clientes

**Infraestructura Separada:**
- URL independiente para el portal (subdominio o dominio propio)
- Hosting separado del sistema administrativo
- Base de datos compartida con permisos de solo lectura/escritura limitados
- API REST para comunicación con el sistema principal
- Certificado SSL/HTTPS obligatorio para seguridad

**Diseño de Interface:**
- Diseño responsive (compatible con móviles, tablets y desktop)
- Branding personalizable según configuración de FM
- Interface simplificada y amigable para usuarios no técnicos
- Menú reducido con solo las opciones relevantes para clientes
- Dashboard visual con gráficos y métricas claras
 

### 9.12. Funcionalidades de Búsqueda y Filtros (Módulo FM - Vista Interna)

El módulo debe contar con filtros de búsqueda para roles internos (FM, Gerente FM, etc.):

- Búsqueda por Código de Contrato
- Búsqueda por Cliente
- Búsqueda por Estado
- Búsqueda por Fecha de Solicitud (rango)
- Búsqueda por Fecha de Vigencia (rango)
- Búsqueda por Moneda (S/. / $)
- Búsqueda por Usuario que cargó el documento
- Búsqueda por Versión del documento
- Filtros combinados

### 9.13. Auditoría y Trazabilidad

El sistema debe registrar en auditoría:

- Todas las cargas de documentos (quién, cuándo, qué versión)
- Todos los cambios de estado del contrato
- Registro de observaciones (autor, fecha, tipo)
- Envío de notificaciones (destinatario, fecha, contenido)
- Firmas electrónicas (firmante, fecha, hora, IP, ubicación)
- Cambios en el FEE (usuario, valor anterior, valor nuevo, fecha)
- Cambios en el IGV (usuario, valor anterior, valor nuevo, fecha)
- Consultas de tipo de cambio (fecha, valor obtenido de SUNAT)
- Acciones del cliente en la bandeja (visualización, descarga, aceptación, carga de documentos)
- Acceso a la bandeja de contratos (cliente, fecha, hora, IP)

### 9.14. Validaciones del Módulo de Contratos

- **Código de Contrato**: Único en el sistema, generado automáticamente
- **Documentos**: Solo formatos PDF y DOCX permitidos
- **Tamaño de archivos**: No exceder 10MB
- **Campos obligatorios**: Cliente, Fecha de Vigencia, Fecha de Vencimiento, Moneda
- **FEE**: Debe ser un valor numérico entre 0% y 100%
- **IGV**: Solo editable por Gerente de FM (configurado en Datos Maestros)
- **Estados**: Solo pueden cambiar siguiendo el flujo establecido
- **Firmas**: Todas las firmas requeridas deben estar completas antes de marcar como "Firmado"
- **Tipo de Cambio**: Debe actualizarse diariamente desde SUNAT (configurado en Datos Maestros)

## 10. Datos Maestros del Sistema

**Propósito**: Centralizar la configuración de parámetros maestros del sistema que son utilizados de manera transversal en todos los módulos. Este módulo permite mantener la información base actualizada y garantiza la consistencia de datos en todo el sistema.

### 10.1. Tipo de Cambio (SUNAT)

Gestionar el tipo de cambio oficial del dólar estadounidense (USD) respecto al sol peruano (PEN), obtenido automáticamente desde SUNAT para ser utilizado en todas las transacciones del sistema.

#### 10.1.1. Actualización Automática del Tipo de Cambio

**Proceso Automático:**
- El sistema debe extraer el tipo de cambio desde la API de SUNAT diariamente
- Valor del Dólar ($) por cada unidad de Sol (S/.)
- Proceso automático ejecutado a las 00:00 hrs (medianoche)
- En caso de error en la consulta, el sistema debe:
  - Reintentar la consulta cada hora hasta obtener respuesta
  - Notificar al Superadministrador si no se obtiene respuesta en 24 horas
  - Utilizar el último tipo de cambio registrado hasta obtener actualización

**Campos del Registro:**
- **Fecha**: Fecha del tipo de cambio (automático)
- **Tipo de Cambio Compra**: Valor de compra del dólar (automático desde SUNAT)
- **Tipo de Cambio Venta**: Valor de venta del dólar (automático desde SUNAT)
- **Fuente**: SUNAT (automático)
- **Fecha y Hora de Actualización**: Timestamp de la última actualización (automático)
- **Estado**: Activo / Inactivo

#### 10.1.2. Consulta Manual del Tipo de Cambio

**Permisos:**
- Solo el **Superadministrador** puede ejecutar consulta manual

**Funcionalidad:**
- Botón "Consultar SUNAT" disponible en la pantalla de configuración
- Al presionar, el sistema consulta inmediatamente el tipo de cambio actual
- El sistema actualiza la tabla con el nuevo valor
- Se registra en auditoría la consulta manual (usuario, fecha, hora)

#### 10.1.3. Historial de Tipos de Cambio

**Registro Histórico:**
- El sistema debe mantener historial completo de todos los tipos de cambio
- No se pueden eliminar registros históricos
- Se debe poder consultar el tipo de cambio de cualquier fecha pasada
- Útil para auditorías y recálculos

**Campos de Búsqueda:**
- Búsqueda por fecha (rango)
- Búsqueda por mes/año
- Exportación del historial a Excel

#### 10.1.4. Aplicación del Tipo de Cambio en el Sistema

**Uso Transversal:**
- El tipo de cambio se utiliza en todos los módulos que manejan valores monetarios:
  - Gestión de Equipos (precio con IGV)
  - Gestión de Herramientas (precio con IGV)
  - Gestión de Contratos (costos, FEE, totales)
  - Cotizaciones
  - Órdenes de Servicio
  - Reportes financieros

**Reglas de Aplicación:**
- Para conversiones de Soles a Dólares: se usa el **Tipo de Cambio Venta**
- Para conversiones de Dólares a Soles: se usa el **Tipo de Cambio Compra**
- El tipo de cambio usado en una transacción queda registrado en el documento
- Los documentos mantienen el tipo de cambio del día de su creación

#### 10.1.5. Validaciones y Alertas

**Validaciones:**
- El tipo de cambio debe ser un valor numérico positivo mayor a cero
- Compra debe ser menor o igual a Venta
- El sistema debe validar variaciones extremas (ej: más de 10% de diferencia con el día anterior)

**Alertas:**
- Si el tipo de cambio varía más del 5% respecto al día anterior, notificar a:
  - Gerente de FM
  - Gerente General
- Si no se actualiza por más de 48 horas, notificar a Superadministrador

### 10.2. Gestión de IGV (Impuesto General a las Ventas)

**Propósito**: Centralizar la configuración del porcentaje de IGV aplicable a todas las transacciones del sistema, permitiendo su actualización cuando existan cambios en la legislación tributaria.

#### 10.2.1. Configuración del IGV

**Parámetros:**
- **Porcentaje de IGV**: Campo numérico decimal
- **Valor por Defecto**: 18% (0.18)
- **Fecha de Vigencia**: Fecha desde la cual aplica el porcentaje
- **Estado**: Activo / Inactivo
- **Observaciones**: Campo de texto libre para justificar cambios

**Permisos de Edición:**
- Solo editable por el rol **Gerente de FM**
- El Superadministrador puede ver pero no editar (para mantener trazabilidad)

#### 10.2.2. Proceso de Modificación del IGV

**Flujo de Cambio:**
1. El **Gerente de FM** accede al módulo de Datos Maestros
2. Selecciona la opción "Modificar IGV"
3. El sistema muestra el valor actual y solicita:
   - Nuevo porcentaje de IGV
   - Fecha de vigencia del cambio
   - Observaciones (obligatorio)

**Importante:**
- El cambio de IGV NO afecta documentos ya creados
- Los documentos nuevos utilizarán el IGV vigente a su fecha de creación
- Se mantiene historial completo de cambios de IGV


#### 10.2.4. Aplicación del IGV en el Sistema

**Uso Transversal:**
- El IGV se aplica automáticamente en:
  - Gestión de Equipos (cálculo de precio con IGV)
  - Gestión de Herramientas (cálculo de precio con IGV)
  - Gestión de Contratos (cotizaciones, totales)
  - Órdenes de Servicio
  - Facturación
  - Reportes financieros

**Fórmulas de Cálculo:**
- **IGV = Monto Base × Porcentaje IGV**
- **Total con IGV = Monto Base + IGV**
- **Monto Base desde Total = Total con IGV / (1 + Porcentaje IGV)**

**Reglas de Aplicación:**
- El IGV se calcula automáticamente en todos los campos de precio
- El usuario ve tanto el precio sin IGV como el precio con IGV
- El IGV usado en una transacción queda registrado en el documento
- Los documentos mantienen el IGV vigente al momento de su creación

### 10.3. Catálogo de Países

**Propósito**: Mantener un catálogo estandarizado de países para su uso en formularios de clientes, proveedores, ubicaciones y otros módulos del sistema.

#### 10.3.1. Gestión del Catálogo de Países

**Campos del Registro:**
- **Código ISO (2 dígitos)**: Código estándar internacional (Ejemplo: PE, US, CL)
- **Código ISO (3 dígitos)**: Código estándar internacional (Ejemplo: PER, USA, CHL)
- **Nombre del País**: Nombre oficial completo (Ejemplo: Perú, Estados Unidos, Chile)
- **Nombre Común**: Nombre de uso común (opcional)
- **Código Telefónico**: Código de llamada internacional (Ejemplo: +51, +1, +56)
- **Continente**: Lista desplegable (América, Europa, Asia, África, Oceanía)
- **Estado**: Activo / Inactivo

**Permisos:**
- Solo el **Superadministrador** puede agregar, editar o eliminar países
- Los demás usuarios solo pueden consultar

**Funcionalidades:**
- Búsqueda por nombre o código ISO
- Filtrado por continente
- Exportación de catálogo completo a Excel
- Importación masiva desde archivo Excel/CSV
- Ordenamiento alfabético por nombre de país

**Validaciones:**
- El código ISO debe ser único en el sistema
- No se pueden eliminar países que estén en uso en otros módulos
- Al inactivar un país, el sistema valida que no tenga registros activos asociados

**Uso en el Sistema:**
- Módulo de Clientes (campo País)
- Módulo de Proveedores (campo País)
- Módulo de Equipos (País de fabricación)
- Módulo de Inmuebles (Ubicación internacional)
- Reportes geográficos

### 10.4. Catálogo de Ubicaciones Geográficas (Perú)

**Propósito**: Mantener el catálogo oficial completo de ubicaciones geográficas de Perú con estructura jerárquica Departamento > Provincia > Distrito, sincronizado con UBIGEO-INEI.

#### 10.4.1. Estructura Jerárquica de Ubicaciones

**Nivel 1: Departamento**
- Código UBIGEO (2 dígitos)
- Nombre del Departamento
- Región Natural (Costa, Sierra, Selva)
- Capital departamental
- Estado (Activo/Inactivo)

**Nivel 2: Provincia**
- Código UBIGEO (4 dígitos)
- Nombre de la Provincia
- Departamento al que pertenece (relación jerárquica)
- Capital provincial
- Estado (Activo/Inactivo)

**Nivel 3: Distrito**
- Código UBIGEO (6 dígitos)
- Nombre del Distrito
- Provincia a la que pertenece (relación jerárquica)
- Capital distrital
- Zona (Urbana/Rural)
- Estado (Activo/Inactivo)

#### 10.4.2. Gestión del Catálogo de Ubicaciones

**Permisos:**
- Solo el **Superadministrador** puede modificar el catálogo
- Gerente de FM puede visualizar y exportar
- Los demás usuarios solo utilizan los catálogos en listas desplegables

**Funcionalidades:**

1. **Búsqueda y Filtrado**:
   - Búsqueda por código UBIGEO
   - Búsqueda por nombre (departamento, provincia, distrito)
   - Filtrado por departamento
   - Filtrado por provincia
   - Filtrado por región natural

2. **Gestión de Registros**:
   - Agregar nuevos departamentos/provincias/distritos
   - Editar información existente
   - Activar/Inactivar registros (no se pueden eliminar)
   - Sincronización con UBIGEO-INEI (actualización anual)

3. **Importación y Exportación**:
   - Importación masiva desde archivo Excel/CSV con formato UBIGEO
   - Exportación del catálogo completo a Excel
   - Descarga de plantilla de importación

#### 10.4.3. Sincronización con UBIGEO-INEI

**Proceso de Actualización:**
- El sistema debe permitir la carga del catálogo UBIGEO actualizado desde INEI
- Frecuencia: Anual (o cuando INEI publique actualizaciones)
- El Superadministrador descarga el archivo oficial de INEI
- El sistema valida el formato del archivo antes de importar
- Se mantiene historial de versiones del catálogo UBIGEO

**Validaciones en la Importación:**
- Verificar que los códigos UBIGEO sean válidos (formato de 2, 4 y 6 dígitos)
- Validar la estructura jerárquica (provincia debe pertenecer a un departamento existente)
- Detectar duplicados por código UBIGEO
- Alertar sobre registros nuevos o modificados

#### 10.4.4. Uso en el Sistema

**Módulos que Utilizan Ubicaciones Geográficas:**
- Módulo de Clientes (Domicilio fiscal)
- Módulo de Proveedores (Dirección, Zona de cobertura)
- Módulo de Inmuebles/Sedes (Ubicación completa)
- Módulo de Equipos (Ubicación del equipo)
- Módulo de Herramientas (Ubicación)
- Módulo de Solicitud de Atención (Ubicación de la incidencia)

**Funcionamiento en Formularios:**
- Lista desplegable 1: Departamento (nivel 1)
- Lista desplegable 2: Provincia (se filtra según departamento seleccionado)
- Lista desplegable 3: Distrito (se filtra según provincia seleccionada)
- Selección en cascada: al seleccionar departamento, se cargan las provincias correspondientes

#### 10.4.5. Validaciones

- No se pueden eliminar ubicaciones que tengan registros asociados en el sistema
- Al inactivar una ubicación, el sistema valida dependencias
- Los códigos UBIGEO deben ser únicos en el sistema
- La estructura jerárquica debe ser consistente (distrito → provincia → departamento)

### 10.5. Catálogo de Tipos de Documento de Identidad

**Propósito**: Estandarizar los tipos de documentos de identidad utilizados en el registro de usuarios, clientes y proveedores.

#### 10.5.1. Tipos de Documento

**Catálogo Estándar:**

| Código | Tipo de Documento | Longitud | Validación |
|--------|-------------------|----------|------------|
| DNI | Documento Nacional de Identidad | 8 dígitos | Solo números |
| CE | Carné de Extranjería | 9 dígitos | Alfanumérico |
| RUC | Registro Único de Contribuyentes | 11 dígitos | Solo números |
| Pasaporte | Pasaporte | 12 caracteres | Alfanumérico |

**Permisos:**
- Solo el **Superadministrador** puede modificar el catálogo
- Otros roles solo consultan

**Funcionalidades:**
- Agregar nuevos tipos de documento
- Editar validaciones y longitudes
- Activar/Inactivar tipos de documento
- No se pueden eliminar tipos en uso

### 10.6. Catálogo de Monedas

**Propósito**: Gestionar las monedas utilizadas en el sistema para transacciones financieras.

#### 10.6.1. Monedas Configuradas

**Catálogo Estándar:**

| Código | Moneda | Símbolo | País | Estado |
|--------|--------|---------|------|--------|
| PEN | Sol Peruano | S/. | Perú | Activo |
| USD | Dólar Estadounidense | $ | Estados Unidos | Activo |
| EUR | Euro | € | Unión Europea | Inactivo (configurable) |

**Campos del Registro:**
- **Código ISO (3 dígitos)**: Código estándar (PEN, USD, EUR)
- **Nombre de la Moneda**: Nombre completo
- **Símbolo**: Representación visual (S/., $, €)
- **País Principal**: País de origen
- **Decimales**: Cantidad de decimales permitidos (2 por defecto)
- **Estado**: Activo / Inactivo

**Permisos:**
- Solo el **Gerente de FM** puede activar/inactivar monedas
- Solo el **Superadministrador** puede agregar nuevas monedas

**Validaciones:**
- Solo se pueden usar monedas activas en transacciones nuevas
- No se pueden inactivar monedas con transacciones activas
- Debe haber al menos una moneda activa en el sistema

### 10.7. Catálogo de Categorías y Tipos de Equipos

**Propósito**: Estandarizar la clasificación de equipos en el sistema para facilitar su gestión, búsqueda y reportes.

#### 10.7.1. Estructura de Categorías de Equipos

**Nivel 1: Categoría Principal**
- Equipos Principales (equipos críticos para la operación)
- Equipos Auxiliares (equipos de soporte)
- Componentes (partes y piezas)

**Nivel 2: Subcategoría**
- Eléctricos
- Mecánicos
- Electrónicos
- Hidráulicos
- Climatización
- Seguridad
- Comunicaciones
- Otros

**Permisos:**
- **Superadministrador**: CRUD completo
- **Gerente de FM**: Agregar y editar
- Otros roles: Solo consulta

**Funcionalidades:**
- Crear nuevas categorías y subcategorías
- Editar nombres y descripciones
- Activar/Inactivar categorías
- Definir iconos o colores para cada categoría (visual)
- Exportar catálogo completo

### 10.8. Catálogo de Marcas de Equipos

**Propósito**: Mantener un listado estandarizado de marcas de equipos para facilitar el registro y búsqueda.

#### 10.8.1. Gestión de Marcas

**Campos del Registro:**
- **Nombre de la Marca**: Texto (Ejemplo: LG, Samsung, Carrier, Trane)
- **País de Origen**: Relación con catálogo de países
- **Categoría Principal**: Tipo de equipos que fabrica
- **Sitio Web**: URL (opcional)
- **Estado**: Activo / Inactivo

**Permisos:**
- **Superadministrador y Gerente de FM**: Pueden agregar marcas
- Otros roles: Solo consulta

**Funcionalidades:**
- Búsqueda por nombre de marca
- Filtrado por país de origen
- Filtrado por categoría principal
- Ordenamiento alfabético
- Autocompletado en formularios

**Validaciones:**
- Nombre de marca debe ser único
- No se pueden eliminar marcas con equipos registrados

### 10.9. Catálogo de Unidades de Medida

**Propósito**: Estandarizar las unidades de medida utilizadas en inventarios, cotizaciones y órdenes de servicio.

#### 10.9.1. Unidades de Medida Estándar

**Catálogo:**

| Código | Unidad | Tipo | Descripción |
|--------|--------|------|-------------|
| UND | Unidad | Cantidad | Unidad individual |
| M | Metro | Longitud | Metro lineal |
| M2 | Metro Cuadrado | Área | Superficie |
| M3 | Metro Cúbico | Volumen | Volumen |
| KG | Kilogramo | Peso | Masa |
| LT | Litro | Volumen | Capacidad líquida |
| HR | Hora | Tiempo | Hora de trabajo/servicio |
| GLN | Galón | Volumen | Capacidad líquida |
| PZA | Pieza | Cantidad | Pieza individual |
| SET | Set | Conjunto | Conjunto de piezas |
| PAR | Par | Cantidad | Par de unidades |

**Campos del Registro:**
- **Código**: Abreviatura estándar
- **Nombre**: Nombre completo de la unidad
- **Tipo**: Cantidad, Longitud, Área, Volumen, Peso, Tiempo
- **Descripción**: Explicación del uso
- **Estado**: Activo / Inactivo

**Permisos:**
- **Superadministrador**: CRUD completo
- Otros roles: Solo consulta

### 10.10. Catálogo de Tipos de Mantenimiento

**Propósito**: Clasificar los tipos de mantenimiento para solicitudes, órdenes de trabajo y reportes.

#### 10.10.1. Tipos de Mantenimiento

**Catálogo Estándar:**

| Código | Tipo de Mantenimiento | Descripción | Frecuencia Típica |
|--------|----------------------|-------------|-------------------|
| PREV | Preventivo | Mantenimiento programado | Mensual, Trimestral, Semestral, Anual |
| CORR | Correctivo | Reparación de fallas | Según necesidad |
| PRED | Predictivo | Basado en monitoreo de condiciones | Según análisis |
| EMER | Emergencia | Atención urgente 24/7 | Inmediato |
| MEJORA | Mejora | Optimización de sistemas | Según proyecto |

**Campos del Registro:**
- **Código**: Abreviatura única
- **Nombre del Tipo**: Nombre descriptivo
- **Descripción**: Definición del tipo de mantenimiento
- **Nivel de Prioridad por Defecto**: Alta, Media, Baja
- **Color de Identificación**: Para visualización en calendarios
- **Estado**: Activo / Inactivo

**Permisos:**
- **Gerente de FM**: Puede agregar y editar
- **Superadministrador**: CRUD completo
- Otros roles: Solo consulta

### 10.11. Catálogo de Criticidad de Equipos

**Propósito**: Clasificar equipos según su criticidad para priorizar el mantenimiento y atención.

#### 10.11.1. Niveles de Criticidad

**Catálogo Estándar:**

| Nivel | Criticidad | Descripción | Tiempo de Respuesta |
|-------|------------|-------------|---------------------|
| 1 | Crítico | Equipo esencial para operación | Inmediato (< 2 horas) |
| 2 | Alto | Equipo importante para operación | Urgente (< 24 horas) |
| 3 | Medio | Equipo necesario sin impacto crítico | Normal (< 72 horas) |
| 4 | Bajo | Equipo de respaldo o baja utilización | Programado (< 7 días) |

**Campos del Registro:**
- **Nivel**: Valor numérico (1-4)
- **Nombre**: Crítico, Alto, Medio, Bajo
- **Descripción**: Definición del nivel
- **Tiempo de Respuesta Máximo**: Horas o días
- **Color de Alerta**: Para indicadores visuales
- **Estado**: Activo / Inactivo

**Uso en el Sistema:**
- Asignación de criticidad a equipos en el módulo de Equipos
- Priorización automática de solicitudes de mantenimiento
- Alertas y notificaciones según nivel de criticidad
- Reportes de equipos críticos

### 10.12. Catálogo de Estados de Equipos

**Propósito**: Estandarizar los estados de los equipos para su gestión y control.

#### 10.12.1. Estados de Equipos

**Catálogo Estándar:**

| Código | Estado | Descripción | Color |
|--------|--------|-------------|-------|
| OPE | Operativo | Equipo funcionando normalmente | Verde |
| MTO | En Mantenimiento | Equipo en mantenimiento programado | Amarillo |
| REP | En Reparación | Equipo en reparación | Naranja |
| INOP | Inoperativo | Equipo fuera de servicio | Rojo |
| BAJA | Dado de Baja | Equipo retirado del inventario | Gris |
| RESER | Reserva | Equipo de respaldo | Azul |

**Permisos:**
- **Superadministrador**: CRUD completo
- **Gerente de FM**: Agregar y editar
- Otros roles: Solo consulta

### 10.13. Días Festivos y No Laborables

**Propósito**: Configurar días festivos y no laborables para cálculo de plazos, programación de mantenimientos y generación de reportes.

#### 10.13.1. Gestión de Días Festivos

**Campos del Registro:**
- **Fecha**: Día específico (dd/mm/yyyy)
- **Nombre del Festivo**: Descripción (Ejemplo: Año Nuevo, Fiestas Patrias)
- **Tipo**: Nacional, Regional, Local
- **Departamento**: Si aplica solo a una región específica
- **Año**: Año de aplicación
- **Estado**: Activo / Inactivo

**Permisos:**
- **Superadministrador**: CRUD completo
- **Gerente de FM**: Agregar y editar
- Otros roles: Solo consulta

**Funcionalidades:**
- Carga masiva de días festivos anuales
- Calendario visual con festivos marcados
- Exportación de listado de festivos por año
- Plantilla de importación Excel

**Uso en el Sistema:**
- Exclusión de festivos en cálculo de plazos de atención
- Programación automática de mantenimientos preventivos
- Alertas de servicios programados en días festivos
- Reportes de disponibilidad de personal

#### 10.13.2. Días Laborables por Defecto

**Configuración:**
- Definir días laborables de la semana (Lunes a Viernes por defecto)
- Opción de incluir Sábados como día laboral
- Horario laboral estándar (Ejemplo: 8:00 AM - 6:00 PM)

### 10.14. Horarios de Operación

**Propósito**: Configurar horarios estándar de operación del sistema FM para cálculo de tiempos de respuesta y disponibilidad de servicios.

#### 10.14.1. Configuración de Horarios

**Tipos de Horario:**
- **Horario Normal**: Lunes a Viernes (8:00 AM - 6:00 PM)
- **Horario Extendido**: Lunes a Sábado (7:00 AM - 7:00 PM)
- **24x7**: Atención continua (emergencias)

**Campos de Configuración:**
- **Nombre del Horario**: Descripción
- **Días de la Semana**: Selección múltiple (L, M, Mi, J, V, S, D)
- **Hora de Inicio**: HH:MM
- **Hora de Fin**: HH:MM
- **Tipo de Servicio**: Normal, Emergencia, Mantenimiento
- **Estado**: Activo / Inactivo

**Permisos:**
- **Gerente de FM**: Editar horarios
- **Superadministrador**: CRUD completo

**Uso en el Sistema:**
- Cálculo de SLA (Service Level Agreement)
- Programación de servicios
- Notificaciones fuera de horario
- Cálculo de horas hombre

### 10.15. Plantillas de Documentos

**Propósito**: Centralizar las plantillas de documentos utilizados en el sistema para garantizar estandarización y calidad.

#### 10.15.1. Tipos de Plantillas

**Catálogo de Plantillas:**

| Código | Plantilla | Formato | Uso |
|--------|-----------|---------|-----|
| COTIZ | Cotización Formal | PDF/Word | Cotizaciones a clientes |
| OC | Orden de Compra | PDF/Excel | Órdenes a proveedores |
| OS | Orden de Servicio | PDF | Órdenes de trabajo |
| CERT | Certificado de Servicio | PDF | Conformidad de servicio |
| CONTRATO | Contrato de Servicio | Word/PDF | Contratos con clientes |
| INFORME | Informe Técnico | Word | Reportes técnicos |
| LNT | Formato Obras Menores | Excel | Cotizaciones LNT |

**Gestión de Plantillas:**
- Carga de archivos de plantilla (.docx, .xlsx, .pdf)
- Versionamiento de plantillas
- Campos dinámicos configurables
- Previsualización de plantilla
- Descarga de plantilla activa

**Campos del Registro:**
- **Código de Plantilla**: Identificador único
- **Nombre**: Descripción de la plantilla
- **Tipo de Documento**: Cotización, Contrato, Orden, Certificado
- **Archivo**: Archivo de plantilla (.docx, .xlsx)
- **Versión**: Número de versión (v1.0, v1.1, etc.)
- **Fecha de Creación**: Fecha de carga
- **Usuario que Creó**: Usuario responsable
- **Estado**: Activa / Inactiva

**Permisos:**
- **Gerente de FM**: Cargar y editar plantillas
- **Superadministrador**: CRUD completo
- Otros roles: Solo uso de plantillas activas

### 10.16. Configuración de Correos Electrónicos

**Propósito**: Centralizar las configuraciones de correo electrónico para notificaciones automáticas del sistema.

#### 10.16.1. Correos de Notificación

**Configuraciones:**

| Tipo de Correo | Destinatario | Uso |
|----------------|--------------|-----|
| Correo de Soporte | soportefm@panoramabpo.com | Atención a usuarios |
| Correo de Notificaciones | notificaciones@sistemaFM.com | Envío automático de alertas |
| Correo de Administrador | admin@sistemaFM.com | Notificaciones críticas del sistema |
| Correo de Gerencia | gerenciafm@panoramabpo.com | Reportes ejecutivos |

**Campos de Configuración:**
- **Tipo de Correo**: Soporte, Notificaciones, Administrador, Gerencia
- **Dirección de Email**: Correo electrónico válido
- **Nombre del Remitente**: Nombre que aparece en el correo
- **Firma de Email**: Texto de firma automática
- **Estado**: Activo / Inactivo

**Permisos:**
- **Superadministrador**: CRUD completo
- Otros roles: Solo visualización

**Validaciones:**
- Formato de correo electrónico válido
- No se pueden inactivar correos esenciales del sistema
- Validación de servidor SMTP configurado

### 10.17. Parámetros Generales del Sistema

**Propósito**: Configurar parámetros transversales del sistema que afectan su comportamiento general.

#### 10.17.1. Configuraciones Generales

**Parámetros Configurables:**

| Parámetro | Descripción | Valor por Defecto | Editable por |
|-----------|-------------|-------------------|--------------|
| Nombre de la Empresa | Nombre de la organización | Panorama BPO | Superadministrador |
| Logo de la Empresa | Archivo de imagen del logo | - | Gerente de FM |
| Tiempo de Sesión | Minutos antes de cerrar sesión inactiva | 30 minutos | Superadministrador |
| Formato de Fecha | Formato de visualización de fechas | dd/mm/yyyy | Superadministrador |
| Idioma del Sistema | Idioma de la interfaz | Español | Superadministrador |
| Zona Horaria | Zona horaria del sistema | America/Lima (UTC-5) | Superadministrador |
| Tamaño Máximo de Archivo | MB permitidos para carga de archivos | 10 MB | Superadministrador |
| Días para Cambio de Contraseña | Frecuencia de actualización de contraseña | 90 días | Superadministrador |
| Intentos de Login | Intentos fallidos antes de bloqueo | 3 | Superadministrador |
| Longitud Mínima de Contraseña | Caracteres mínimos para contraseña | 8 | Superadministrador |

**Permisos:**
- **Superadministrador**: Editar todos los parámetros
- **Gerente de FM**: Editar logo y nombre de empresa
- Otros roles: Solo visualización

### 10.18. Auditoría del Módulo de Datos Maestros

**Registro de Auditoría:**

El sistema debe registrar todas las modificaciones realizadas en los datos maestros:

- Fecha y hora de modificación
- Usuario que realizó el cambio
- Tipo de catálogo modificado (País, Ubicación, Moneda, etc.)
- Registro específico modificado
- Valor anterior y valor nuevo
- Acción realizada (Crear, Editar, Activar, Inactivar)
- IP del usuario
- Observaciones (si aplica)

**Reportes de Auditoría:**
- Reporte de cambios por período
- Reporte de cambios por usuario
- Reporte de cambios por tipo de catálogo
- Exportación a Excel

### 10.19. Validaciones Generales del Módulo

- Solo usuarios autorizados pueden modificar datos maestros
- No se pueden eliminar registros que estén en uso en otros módulos
- Al inactivar un registro, el sistema valida dependencias
- Los códigos únicos (ISO, UBIGEO, etc.) no pueden duplicarse
- Los campos obligatorios deben completarse antes de guardar
- Las importaciones masivas deben validarse antes de ejecutarse
- Los cambios en datos maestros deben tener trazabilidad completa

### 10.20. Reglas de Negocio del Módulo

- **RN-10.1**: Los datos maestros son la única fuente de verdad para catálogos en el sistema
- **RN-10.2**: Los cambios en datos maestros no afectan registros históricos ya creados
- **RN-10.3**: El sistema debe sincronizar automáticamente con fuentes oficiales (SUNAT, INEI) cuando aplique
- **RN-10.4**: Debe existir al menos un registro activo en cada catálogo esencial (monedas, países, ubicaciones)
- **RN-10.5**: Los usuarios solo pueden utilizar registros activos en formularios y transacciones
- **RN-10.6**: Las plantillas de documentos deben versionarse para mantener trazabilidad
- **RN-10.7**: El catálogo UBIGEO debe actualizarse al menos una vez al año según publicaciones de INEI
- **RN-10.8**: Los días festivos deben cargarse al inicio de cada año fiscal
- **RN-10.9**: Los parámetros del sistema solo pueden ser modificados por usuarios con permisos específicos
- **RN-10.10**: Todos los cambios en datos maestros deben quedar registrados en auditoría

---

## 11. Solicitud de Atención de Incidencia

**Propósito**: Gestionar el registro y seguimiento de solicitudes de atención para mantenimiento de instalaciones, reparaciones, emergencias y suministros, permitiendo a los usuarios reportar incidencias con descripción detallada, imágenes y categorización automática según criticidad.

Sistema que permite a los usuarios (clientes internos/externos) crear solicitudes de atención de incidencias de manera estructurada mediante categorías jerárquicas de mantenimiento, incluyendo carga de imágenes, descripción del problema, y asignación automática a equipos de FM según nivel de urgencia. El sistema genera tickets de servicio y notifica al personal correspondiente.

**Frecuencia de Actualización**: Los datos y contraseñas de usuarios deben actualizarse cada 3 meses.

### 11.1. Tipos de Solicitud

El sistema maneja dos tipos principales de solicitudes:

| Tipo de Solicitud | Descripción |
|-------------------|-------------|
| **Mantenimiento** | Instalaciones, reparaciones, emergencias |
| **Suministros** | Útiles, materiales, consumibles |

**Campo**: Lista desplegable obligatoria

### 11.2. Estructura de Categorización Jerárquica


**A NIVEL DE INTERFAZ VISUAL**: El usuario interactúa ÚNICAMENTE con **2 listas desplegables**:

✅ **CATEGORIA** (Nivel 1) - Campo visible y seleccionable
✅ **UNIDAD DE MTTO** (Nivel 2) - Campo visible y seleccionable

❌ **SUB UNIDAD DE MTTO** (Nivel 3) - NO visible para el usuario

**Catálogo Completo de Información**:
El catálogo maestro de 3 niveles (ver sección 11.2.1) se mantiene completo para propósitos de administración, reportes y referencia técnica, pero **el usuario final solo ve y selecciona 2 niveles**.

**Funcionamiento Visual de la Interfaz**:
1. El usuario ve y selecciona la **CATEGORIA** desde una lista desplegable (ej: ÁREAS VERDES, CERRAJERÍA, HVAC)
2. El sistema filtra automáticamente y muestra solo las **UNIDADES DE MTTO** correspondientes a la categoría seleccionada
3. El usuario ve y selecciona la **UNIDAD DE MTTO** desde la segunda lista desplegable (ej: JARDINERÍA, CARPINTERÍA ALUMINIO)
4. La solicitud queda registrada con estos 2 niveles de categorización
5. El **tercer nivel (SUB UNIDAD DE MTTO)** existe en el catálogo pero NO aparece en ninguna pantalla del usuario

**Nota para el Equipo de Desarrollo**: Implementar solo 2 componentes de selección (dropdowns) en cascada. El nivel 3 del catálogo es solo para consulta del administrador.

#### 11.2.1. Catálogo Completo de Categorías de Mantenimiento

**1. ÁREAS VERDES**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| ÁREAS VERDES | JARDINERÍA | JARDINERA |
| | | MACETEROS |
| | | PLANTAS ORNAMENTALES |
| | | GRASS Y OTROS |
| | | PLANTAS ESPECIALES |
| | MACETEROS | GRASS Y OTROS |

**2. CERRAJERÍA**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| CERRAJERÍA | CARPINTERÍA ALUMINIO | MAMPARAS - GUÍAS |
| | | PUERTAS - CIERRA PUERTAS |
| | | VENTANAS - GUÍAS |
| | CARPINTERÍA DE MADERA | DIVISIONES - MAMPARAS |
| | | PUERTAS - BISAGRAS |
| | | PUERTAS - CHAPAS Y/O CERRADURAS |
| | | PUERTAS - CIERRA PUERTAS |
| | | PUERTAS - ESTRUCTURAS |
| | | PUERTAS - FRENOS DE PISO |
| | | PUERTAS - MANIJAS Y/O TIRADORES |
| | | VENTANAS - SELLADO |
| | CARPINTERÍA METÁLICA | BUZONES - TAPAS DE FIERRO |
| | | PASAMANOS - PINTURA |
| | | PORTONES/PUERTAS - BISAGRAS |
| | | PUERTAS - BRAZOS HIDRÁULICOS |
| | | PUERTAS - CERROJOS |
| | | PUERTAS - CHAPAS Y/O CERRADURAS |
| | | PUERTAS - CIERRA PUERTAS HIDRÁULICOS |
| | | PUERTAS - DUPLICADO DE LLAVES |
| | | PUERTAS - ESTRUCTURAS |
| | | PUERTAS - MANIJAS Y/O TIRADORES |
| | | PUERTAS - TOPES |
| | | PUERTAS ENROLLABLES - ESTRUCTURA |
| | | PUERTAS ENROLLABLES - SISTEMA DE APERTURA ELÉCTRICO |
| | | PUERTAS ENROLLABLES - SISTEMA DE APERTURA MANUAL |
| | | VENTANAS - ESTRUCTURAS |
| | | VENTANAS - GUÍAS |
| | | VENTANAS - MANIJAS Y/O TIRADORES |

**3. DACI (Detección Alarma Contra Incendios)**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| DACI | EQUIPOS DE DETECCIÓN DE INCENDIOS | DETECCIÓN DE INCENDIOS - DETECTORES DE ANIEGO |
| | | DETECTORES DE HUMO |
| | | ESTACIÓN MANUAL |
| | | FOTOBEEN |
| | | PANELES CONTRA INCENDIO |
| | | ROCIADORES |
| | EQUIPOS DE ELEVACIÓN | ASCENSORES - BOTONERAS |
| | | CABINA - PISOS |
| | | ILUMINACIÓN - LUMINARIAS |
| | | MOTOR - REPARACIÓN |
| | | PISO DE CABINA - NIVELACIÓN |
| | | PROGRAMACIÓN - TARJETAS |
| | | PUERTAS - RIELES |
| | | SISTEMA DE EXTRACCIÓN - EXTRACTOR DE AIRE |
| | | SISTEMA ELÉCTRICO - TARJETA |
| | | TABLERO - LLAVES, ITMs |

**4. EQUIPOS DE RESPALDO**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| EQUIPOS DE RESPALDO | GENERADORES | GRUPOS ELECTRÓGENOS - GE FIJOS |
| | | GRUPOS ELECTRÓGENOS - GE PORTÁTILES |
| | SISTEMAS REDUNDANTES | SUBESTACIÓN - CELDAS |
| | UPS | UPS - BATERÍAS |
| | | UPS - TARJETAS |

**5. EQUIPOS ELECTROMECÁNICOS**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| EQUIPOS ELECTROMECÁNICOS | SISTEMA DE BOMBEO | EQUIPOS DE BOMBEO - BOMBAS SUMERGIBLES |
| | | EQUIPOS DE BOMBEO - ELECTROBOMBAS |
| | | EQUIPOS DE BOMBEO - MOTOBOMBAS |
| | | SISTEMA DE CONTROL - SENSORES, COMPONENTES DEL SISTEMA |
| | SISTEMAS DE IMPULSIÓN | SISTEMA DE PRESIÓN CONSTANTE |
| | | TANQUE HIDRONEUMÁTICO |

**6. EQUIPOS MENORES**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| EQUIPOS MENORES | EQUIPOS DE SASTRERÍA | EQUIPOS DE COSTURA - BASTERAS |
| | | EQUIPOS DE COSTURA - MÁQUINAS DE COSER |
| | | EQUIPOS DE PLANCHADO DE PRENDAS - PLANCHAS |
| | | EQUIPOS DE PLANCHADO DE PRENDAS - VAPORIZADORES |
| | SEGURIDAD DE INSTALACIONES | EQUIPOS DE SEGURIDAD - ANTENAS DE SEGURIDAD |
| | | SENSORES DE PRENDAS - PIOCHAS Y PINES |

**7. HVAC (Heating, Ventilation, and Air Conditioning)**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| HVAC | AIRE ACONDICIONADO | CHILLERS - CONDENSADORES |
| | | DUCTOS Y TUBERÍAS |
| | | FAN COIL - FILTROS |
| | | SPLIT - INTERCAMBIADOR |
| | | TERMOSTATOS - DIGITALES/ANALÓGICOS |
| | EQUIPOS DE EXTRACCIÓN DE AIRE | EXTRACTORES DE AIRE - CAMPANA EXTRACTORA |
| | | EXTRACTORES DE AIRE - CONDUCTOS O DUCTOS |
| | | EXTRACTORES DE AIRE - FILTRO PURIFICADOR |
| | | EXTRACTORES DE AIRE - VENTILADOR |
| | EQUIPOS DE PRECISIÓN | CONDENSADOR - COMPRESOR |
| | EQUIPOS DE VENTILACIÓN | VENTILADORES - VENTILADORES DE PARED |
| | | VENTILADORES - VENTILADORES DE TECHO |

**8. INFRAESTRUCTURA**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| INFRAESTRUCTURA | INFRAESTRUCTURA | ALFOMBRAS |
| | | PISO TÉCNICO |
| | | ESTRUCTURAS - COLUMNAS Y VIGAS |
| | | ESTRUCTURAS - MUROS Y TABIQUES |
| | | FACHADAS - ALUCOBOND |
| | | FACHADAS - LIMPIEZA FACHADA |
| | | FACHADAS - VIDRIOS TEMPLADOS |
| | | FALSO CIELO RASO - ACCESORIOS |
| | | FALSO CIELO RASO - BALDOSAS |
| | | IMPERMEABILIZACIÓN DE TECHOS - IMPERMEABILIZANTES/EPÓXICOS |
| | | MUROS - ENLUCIDO DE MUROS |
| | | PINTURA - PINTURA LÁTEX |
| | | PISOS - CERÁMICO/PORCELANATO |
| | | TECHOS/COBERTURAS - DRENAJES |
| | | TECHOS/COBERTURAS - ESTRUCTURAS |
| | | TECHOS/COBERTURAS - TEJAS |
| | | TECHOS/COBERTURAS - TR4 |

**9. MOBILIARIO**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| MOBILIARIO | MOBILIARIO | CERRAJERÍA - LLAVES |
| | | ESCRITORIOS - DE MADERA |
| | | ESCRITORIOS - DE MELAMINA |
| | | ESCRITORIOS - METÁLICOS |
| | | MUEBLES - SILLONES Y AFINES |
| | | ORGANIZADORES - LOCKERS |
| | | SILLAS - OTRAS SILLAS |
| | | SILLAS - SILLAS DE OFICINA |

**10. SACI (Sistema Automático Contra Incendios)**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| SACI | EQUIPOS DE EXTINCIÓN | EXTINTORES - MANGUERA |
| | | EXTINTORES - MANÓMETRO |
| | | EXTINTORES - PALANCA DE PULVERIZADO |
| | | EXTINTORES - PRECINTO DE SEGURIDAD |
| | | EXTINTORES - TANQUE O CILINDRO |
| | | EXTINTORES - TUBO DE SIFÓN |
| | | ROCIADORES |
| | SISTEMAS DE EXTINCIÓN | PUERTAS - PUERTAS CORTAFUEGO |

**11. SANEAMIENTO AMBIENTAL**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| SANEAMIENTO AMBIENTAL | FUMIGACIÓN/DESRATIZACIÓN/AFINES | DESINSECTACIÓN |
| | | DESRATIZACIÓN |
| | | FUMIGACIÓN |

**12. SISTEMA ELÉCTRICO**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| SISTEMA ELÉCTRICO | CERCO ELÉCTRICO | SISTEMA DE SEGURIDAD PERIMETRAL - ENERGIZADOR |
| | | SISTEMA DE SEGURIDAD PERIMETRAL - LÍNEAS Y POSTES |
| | | SISTEMA DE SEGURIDAD PERIMETRAL - PANEL DE CONTROL |
| | EQUIPOS DE ILUMINACIÓN | EQUIPOS DE EMERGENCIA - LUCES DE EMERGENCIA |
| | | LUMINARIAS Y/O AFINES - EQUIPOS HIGH BAY |
| | | LUMINARIAS Y/O AFINES - LUMINARIAS LED |
| | | LUMINARIAS Y/O AFINES - LUMINARIAS TIPO CAÑÓN |
| | INSTALACIONES ELÉCTRICAS | CONDUCTORES - CABLE INDOPRENE |
| | | ESTABILIZADOR - BOBINADO |
| | | INTERRUPTORES - INTERRUPTOR SIMPLE |
| | | POZOS A TIERRA - POZOS A TIERRA HORIZONTALES |
| | | POZOS A TIERRA - POZOS A TIERRA VERTICALES |
| | | POZOS A TIERRA - TIPO MALLA |
| | | TABLEROS ELÉCTRICOS - LLAVES DIFERENCIALES |
| | | TABLEROS ELÉCTRICOS - LLAVES TERMOMAGNÉ TICAS |
| | | TABLEROS ELÉCTRICOS - PLANOS UNILINARES |
| | | TOMACORRIENTES - TOMACORRIENTE DOBLE |
| | LETREROS | LETREROS ILUMINADOS - LETREROS LUMINOSOS |
| | | LETREROS NO ILUMINADOS - GIGANTOGRAFÍAS |
| | | LETREROS NO ILUMINADOS |
| | SUBESTACIÓN | TRANSFORMADOR - CELDAS |

**13. SISTEMA SANITARIO**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| SISTEMA SANITARIO | INSTALACIONES SANITARIAS | ACCESORIOS SANITARIOS - BRIDAS |
| | | DESATOROS - EQUIPOS DE DESATORO |
| | | DISPOSITIVOS ELÉCTRICOS - SECADORES DE MANO |
| | | GRIFERÍAS - FLUXÓMETROS |
| | | GRIFERÍAS - GRIFERÍA NO TEMPORIZADA |
| | | GRIFERÍAS - GRIFERÍA TEMPORIZADA |
| | | INODOROS - ACCESORIOS |
| | | INODOROS - LLAVE DE CIERRE GENERAL |
| | | INODOROS - PULSADOR DE DESCARGA FLUXÓMETRO |
| | | INODOROS - TASA DE INODORO |
| | | INODOROS - TUBO DE ABASTO |
| | | INODOROS - VÁLVULA DE CIERRE |
| | | LAVATORIOS - ACCESORIOS |
| | | OTROS EQUIPOS SANITARIOS - OTROS |
| | | POZO DE AGUA - LIMPIEZA |
| | | POZO DE SÉPTICO - LIMPIEZA |
| | | POZOS TANQUES Y CISTERNAS - CISTERNAS DE AGUA |
| | | POZOS TANQUES Y CISTERNAS - TANQUES ELEVADOS DE AGUA |
| | | REDES DE AGUA - ALIMENTADORES DE AGUA |
| | | REDES DE DESAGÜE - MONTANTES |
| | | SUMIDEROS - LIMPIEZA |
| | | URINARIOS - SISTEMA DE DESCARGA |
| | | URINARIOS - TRAMPAS Y/O AFINES |

**14. VIDRIOS Y MAMPARAS**

| Grupo | Unidad | Sub Unidad |
|-------|---------|------------|
| VIDRIOS Y MAMPARAS | VIDRIOS | VIDRIO CRUDO - LAMINADO DE VIDRIOS |
| | | VIDRIO CRUDO - PAVONADOS |
| | | VIDRIO TEMPLADO - ESPEJOS |
| | | VIDRIO TEMPLADO - MAMPARAS |
| | | VIDRIO TEMPLADO - MUROS CORTINA |
| | | VIDRIO TEMPLADO - PUERTAS |
| | | VIDRIOS - LIMPIEZA |

### 11.3. Funcionalidad de Solicitud de Atención de Incidencias

El sistema debe permitir la creación y gestión de solicitudes de atención de incidencias con las siguientes funcionalidades:

#### 11.3.1. Acceso al Módulo de Solicitud

El sistema debe proporcionar:
- Módulo "Solicitud de Atención de Incidencia" accesible desde el menú principal
- Botón "Nueva Solicitud" o "Crear Incidencia" visible y destacado
- Pantalla principal con historial de solicitudes previas del usuario
- Interfaz intuitiva y responsiva para crear solicitudes

#### 11.3.2. Funcionalidad de Tipo de Solicitud

El sistema debe incluir:
- Lista desplegable con los tipos de solicitud disponibles:
  - Mantenimiento
  - Suministros
- Campo obligatorio
- Gestión administrativa de tipos de solicitud (crear, modificar, eliminar) a nivel administrador
- Validación de selección antes de continuar

#### 11.3.3. Funcionalidad de Categorización Dinámica (Nivel 1)

El sistema debe proporcionar:
- Lista desplegable de **CATEGORÍA** (Nivel 1) filtrada según el tipo de solicitud
- Categorías incluidas:
  - ÁREAS VERDES
  - CERRAJERÍA
  - HVAC
  - SISTEMA ELÉCTRICO
  - SISTEMA SANITARIO
  - VIDRIOS Y MAMPARAS
  - Y otras según catálogo de servicios
- Campo obligatorio
- Actualización dinámica al cambiar el tipo de solicitud
- Gestión administrativa del catálogo de categorías

#### 11.3.4. Funcionalidad de Subcategorización Dinámica (Nivel 2)

El sistema debe incluir:
- Lista desplegable de **UNIDAD DE MTTO** (Nivel 2) filtrada dinámicamente según la categoría seleccionada
- Ejemplos de filtrado dinámico:
  - Si CATEGORÍA = ÁREAS VERDES → Mostrar: JARDINERÍA, MACETEROS
  - Si CATEGORÍA = CERRAJERÍA → Mostrar: CARPINTERÍA ALUMINIO, CARPINTERÍA DE MADERA, CARPINTERÍA METÁLICA
  - Si CATEGORÍA = HVAC → Mostrar: AIRE ACONDICIONADO, EQUIPOS DE EXTRACCIÓN DE AIRE, EQUIPOS DE VENTILACIÓN
- Campo obligatorio
- Actualización automática al cambiar la categoría
- **Importante**: Este es el último nivel de categorización visible para el usuario

#### 11.3.5. Funcionalidad de Descripción de Incidencia

El sistema debe proporcionar:
- Campo de texto libre para descripción detallada de la incidencia
- Campo obligatorio con validación de contenido
- Límite mínimo de caracteres (sugerido: 20 caracteres)
- Análisis automático del texto mediante IA para:
  - Extracción de palabras clave
  - Detección de nivel de urgencia
  - Asignación automática de criticidad
- Mensaje de error si el usuario intenta enviar sin descripción

#### 11.3.6. Funcionalidad de Carga de Imágenes

El sistema debe incluir:
- Área de carga de imágenes con drag & drop o selector de archivos
- Validaciones:
  - Formatos permitidos: PNG, JPG
  - Tamaño máximo por imagen: 10 MB
  - Cantidad mínima: 1 imagen (obligatorio)
  - Cantidad máxima: 3 imágenes
- Vista previa de imágenes cargadas
- Opción de eliminar imágenes antes de enviar
- Mensajes de error claros para archivos que no cumplan las validaciones
- Indicador visual de progreso de carga

#### 11.3.7. Validación Integral del Formulario

El sistema debe validar antes de permitir el envío:
- Tipo de solicitud seleccionado
- Categoría (Nivel 1) seleccionada
- Unidad de MTTO (Nivel 2) seleccionada
- Descripción ingresada con mínimo de caracteres
- Al menos 1 imagen cargada correctamente
- Mensaje de error específico para cada campo faltante
- Resaltado visual de campos incompletos

#### 11.3.8. Asignación Automática de Criticidad

El sistema debe incluir funcionalidad de análisis inteligente para:
- Analizar automáticamente la descripción ingresada
- Detectar palabras clave de emergencia (urgente, crítico, emergencia, peligro, falla total, etc.)
- Asignar automáticamente uno de tres niveles de criticidad:
  - **Alta**: Emergencias, fallas críticas que requieren atención inmediata
  - **Media**: Problemas que afectan operaciones pero no son emergencias
  - **Baja**: Solicitudes de mantenimiento preventivo o mejoras
- Método: Sistema Híbrido (Reglas Determinísticas + Inteligencia Artificial)
- Mostrar el nivel de criticidad asignado al usuario antes de confirmar
- Permitir revisión por Service Desk FM después del envío
- Ver sección 11.14 para detalles técnicos de implementación

#### 11.3.9. Generación Automática de Código de Servicio/Ticket

El sistema debe proporcionar:
- Generación automática de código único al crear la solicitud
- Formato: SRV-AAAA-NNNN
  - SRV: Prefijo de Servicio
  - AAAA: Año actual
  - NNNN: Número secuencial
- Ejemplo: SRV-2026-0001
- Contador secuencial que se reinicia cada año
- Campo de solo lectura
- Visualización del código generado inmediatamente después del envío

#### 11.3.10. Sistema de Notificaciones Automáticas

El sistema debe enviar notificaciones automáticas según el nivel de criticidad:

**Para Criticidad Alta**:
- Notificación inmediata a Supervisor FM por correo electrónico
- Notificación inmediata a Supervisor FM por WhatsApp
- Notificación a Service Desk FM por correo electrónico
- Indicador visual de "URGENTE" en la bandeja

**Para Criticidad Media o Baja**:
- Notificación a Service Desk FM por correo electrónico
- Sin notificación por WhatsApp

**Contenido de las Notificaciones**:
- Código de servicio generado
- Nivel de criticidad
- Tipo de solicitud
- Categoría y Unidad de MTTO
- Descripción resumida
- Cliente/Sede
- Enlace directo a la solicitud en el sistema

#### 11.3.11. Registro Automático de Información

El sistema debe registrar automáticamente:
- Fecha y hora exacta de creación de la solicitud
- Usuario solicitante (usuario logueado)
- Cliente y sede asociados al usuario
- Estado inicial: "Nuevo"
- Nivel de criticidad asignado
- Código de servicio generado
- Historial completo de la solicitud desde su creación

#### 11.3.12. Confirmación de Envío

El sistema debe mostrar:
- Mensaje de confirmación de envío exitoso
- Código de servicio asignado destacado
- Resumen de la solicitud creada
- Nivel de criticidad asignado
- Tiempo estimado de atención (según SLA)
- Opción de imprimir o descargar comprobante
- Enlace para seguimiento de la solicitud

#### 11.3.13. Gestión Administrativa del Catálogo

El sistema debe permitir (solo usuarios administradores):
- Crear nuevos tipos de solicitud
- Agregar, modificar o eliminar categorías (Nivel 1)
- Agregar, modificar o eliminar unidades de MTTO (Nivel 2)
- Configurar relaciones entre tipos, categorías y unidades
- Gestionar palabras clave para detección de criticidad
- Configurar plantillas de notificación
- Definir SLAs por categoría o criticidad

### 11.4. Generación de Código de Servicio/Ticket

**Formato Sugerido**: SRV-AAAA-NNNN
- **SRV**: Prefijo de Servicio
- **AAAA**: Año actual (2026)
- **NNNN**: Número secuencial (0001, 0002, etc.)

**Ejemplo**: SRV-2026-0001

**Reglas**:
- Código autogenerado al crear la solicitud
- Único en el sistema
- Campo de solo lectura
- Se reinicia el contador cada año

### 11.5. Niveles de Criticidad y Notificaciones

| Nivel de Criticidad | Descripción | Notificación |
|---------------------|-------------|--------------|
| **Alta** | Emergencias, fallas críticas, riesgos de seguridad | Supervisor + Service Desk FM (Correo + WhatsApp) |
| **Media** | Problemas que afectan operaciones normales | Service Desk FM (Correo) |
| **Baja** | Mantenimiento preventivo, mejoras, suministros | Service Desk FM (Correo) |

**Palabras Clave para Criticidad Alta** (ejemplos):
- Emergencia
- Urgente
- Crítico
- Falla total
- Peligro
- Riesgo
- Sin funcionamiento
- Inoperativo

### 11.6. Campos del Formulario de Solicitud

| Campo | Tipo | Obligatorio | Descripción |
|-------|------|-------------|-------------|
| **Código de Servicio** | Texto (autogenerado) | Sí | Código único de la solicitud (SRV-AAAA-NNNN) |
| **Tipo de Solicitud** | Lista desplegable | Sí | Mantenimiento / Suministros |
| **Categoría** | Lista desplegable | Sí | **CATEGORIA (Nivel 1)** - VISIBLE AL USUARIO |
| **Unidad de MTTO** | Lista desplegable | Sí | **UNIDAD DE MTTO (Nivel 2)** - VISIBLE AL USUARIO |
| **Descripción** | Texto libre | Sí | Descripción detallada de la incidencia |
| **Imágenes** | Archivo (PNG, JPG) | Sí | Mínimo 1, máximo 3 imágenes (10MB cada una) |
| **Criticidad** | Texto (autogenerado) | Sí | Alta / Media / Baja (asignado por IA) |
| **Fecha de Solicitud** | Fecha/Hora | Sí | Fecha y hora de creación (automático) |
| **Usuario Solicitante** | Texto | Sí | Usuario logueado que crea la solicitud |
| **Cliente/Sede** | Texto | Sí | Cliente y sede donde ocurre la incidencia |
| **Estado** | Lista | Sí | Nuevo / En Proceso / Atendido / Cerrado |



**El formulario muestra ÚNICAMENTE 2 campos de categorización**:
- **Categoría** (Nivel 1): Primera lista desplegable
- **Unidad de MTTO** (Nivel 2): Segunda lista desplegable (filtrada según la categoría seleccionada)

**NO existe un tercer campo** para SUB UNIDAD DE MTTO en la interfaz del usuario.

El catálogo completo de 3 niveles (sección 11.2.1) se mantiene para referencia administrativa, pero el usuario solo interactúa con 2 niveles.

### 11.7. Gestión de Categorías a Nivel Administrador

**Permisos**: Solo el **Superadministrador** puede gestionar las categorías de mantenimiento.

**Funcionalidades**:
- **Crear**: Agregar nuevas categorías o unidades de MTTO
- **Modificar**: Editar nombres o descripciones de categorías existentes
- **Eliminar**: Eliminar categorías que no se utilizan (validar que no tengan solicitudes asociadas)

**Campos de Categoría en la Base de Datos**:
- Código de Categoría (autogenerado)
- Tipo de Solicitud (Mantenimiento/Suministros)
- Nivel (Categoría/Unidad/Sub Unidad)
- Nombre de la Categoría
- Categoría Padre (para nivel 2 y 3)
- **Visible para Usuario** (Sí/No) - Define si el nivel es seleccionable en la interfaz
- Estado (Activo/Inactivo)



**En Base de Datos**: Se almacenan los 3 niveles completos del catálogo
- Nivel 1: CATEGORIA
- Nivel 2: UNIDAD DE MTTO
- Nivel 3: SUB UNIDAD DE MTTO

**En la Interfaz del Usuario**: Solo se muestran 2 niveles
- Campo 1: **CATEGORIA** (Lista desplegable)
- Campo 2: **UNIDAD DE MTTO** (Lista desplegable en cascada)
- ❌ NO existe un tercer campo para SUB UNIDAD DE MTTO

**Uso del Catálogo Completo**:
- **Para Usuarios**: Ver y seleccionar solo 2 niveles (CATEGORIA y UNIDAD DE MTTO)
- **Para Administradores**: Ver los 3 niveles completos para planificación y referencia técnica
- **Para Reportes**: Utilizar toda la información de 3 niveles para análisis detallado
- **Para Mantenimiento**: El equipo técnico puede consultar el nivel 3 para información específica

**Configuración del Campo "Visible para Usuario"**:
- Nivel 1 (CATEGORIA): Visible para Usuario = **Sí**
- Nivel 2 (UNIDAD DE MTTO): Visible para Usuario = **Sí**
- Nivel 3 (SUB UNIDAD DE MTTO): Visible para Usuario = **No**
- Visible para Usuario (Sí/No) - Solo las columnas amarillas (CATEGORIA y UNIDAD DE MTTO) son visibles

**Estructura en Base de Datos**:
- El sistema mantiene los 3 niveles completos en la base de datos para referencia técnica
- Solo los niveles 1 (CATEGORIA) y 2 (UNIDAD DE MTTO) se muestran al usuario en listas desplegables
- El nivel 3 (SUB UNIDAD DE MTTO) se mantiene en el catálogo maestro para consultas administrativas y reportes técnicos

### 11.8. Validaciones del Módulo

- **Tipo de Solicitud**: Debe seleccionarse antes de mostrar categorías
- **Categoría Completa**: Los 2 niveles obligatorios deben completarse (CATEGORIA y UNIDAD DE MTTO)
- **Listas en Cascada**: La lista de UNIDAD DE MTTO solo muestra opciones relacionadas con la CATEGORIA seleccionada
- **Descripción Obligatoria**: No se permite enviar solicitud sin descripción
- **Imágenes Obligatorias**: Mínimo 1 imagen, máximo 3 imágenes
- **Formato de Imágenes**: Solo PNG y JPG permitidos
- **Tamaño de Imágenes**: Máximo 10MB por imagen
- **Campos Obligatorios**: Sistema valida antes de permitir el envío
- **Código Único**: El código de servicio debe ser único en el sistema
- **Solo 2 Niveles**: El usuario NUNCA debe ver un tercer nivel de categorización (SUB UNIDAD DE MTTO)

### 11.9. Notificaciones Automáticas

**Al Crear la Solicitud**:
1. **Al Usuario**: Confirmación de solicitud creada con código de servicio
2. **Al Equipo FM**: Notificación según criticidad
   - **Alta**: Correo + WhatsApp a Supervisor y Service Desk
   - **Media/Baja**: Correo a Service Desk

**Contenido del Correo**:
- Código de servicio
- Tipo de solicitud
- Categoría (Nivel 1)
- Unidad de MTTO (Nivel 2)
- Descripción
- Nivel de criticidad
- Usuario solicitante
- Cliente/Sede
- Link para ver las imágenes

### 11.10. Auditoría del Módulo

El sistema debe registrar en auditoría:
- Fecha y hora de creación de la solicitud
- Usuario que creó la solicitud
- Nivel de criticidad asignado
- Categorías seleccionadas
- Cambios de estado de la solicitud
- Imágenes cargadas (nombre, tamaño, fecha)
- Notificaciones enviadas (destinatario, fecha, hora)
- Cambios en las categorías de mantenimiento (administrador)

### 11.11. Funcionalidades de Búsqueda

- Búsqueda por Código de Servicio
- Búsqueda por Tipo de Solicitud
- Búsqueda por Categoría/Sub Categoría
- Búsqueda por Nivel de Criticidad
- Búsqueda por Estado
- Búsqueda por Fecha de Solicitud (rango)
- Búsqueda por Usuario Solicitante
- Búsqueda por Cliente/Sede
- Filtros combinados

### 11.12. Sistema de Asignación Automática de Criticidad

**Objetivo**: Clasificar automáticamente las solicitudes de incidencia en tres niveles de criticidad (Alta, Media, Baja) para priorizar la atención del equipo de FM.

**Método**: Sistema Híbrido que combina:
1. **Reglas por Palabras Clave** (primera validación)
2. **Inteligencia Artificial GPT-4o-mini de OpenAI** (casos ambiguos)

#### 11.12.1. Clasificación por Palabras Clave

El sistema analiza la descripción de la incidencia buscando palabras clave predefinidas. Si encuentra coincidencia, asigna criticidad automáticamente.

**Tabla de Palabras Clave por Criticidad**:

| Criticidad | Palabras Clave |
|------------|----------------|
| **ALTA** | emergencia, urgente, crítico, peligro, riesgo, falla total, inoperativo, sin funcionamiento, incendio, inundación, corto circuito, fuga de gas, colapso, derrumbe, personas atrapadas, accidente, lesionado, amenaza, evacuación, sin agua, sin luz, explosión |
| **MEDIA** | fallo, malogrado, averiado, no funciona, problema, deficiente, irregular, intermitente, ruido extraño, goteo, fisura, atascado, bloqueado, obstruido, desgaste, sobrecalentamiento, lentitud, demora |
| **BAJA** | mantenimiento preventivo, revisión, inspección, limpieza, cambio programado, suministro, solicitud de material, mejora, optimización, actualización, solicitud, requerimiento, pedido, instalación nueva, cambio estético, pintura, jardinería |

**Gestión de Palabras Clave**:
- El **Superadministrador** puede agregar, editar o eliminar palabras clave
- Puede activar/desactivar palabras temporalmente
- El sistema registra todas las modificaciones en auditoría

#### 11.12.2. Clasificación por Inteligencia Artificial

**Cuándo se activa**: Solo cuando NO se encuentra ninguna palabra clave en la descripción.

**Modelo utilizado**: GPT-4o-mini de OpenAI

**Datos analizados por la IA**:
- Descripción de la incidencia
- Categoría seleccionada (ej: HVAC, SISTEMA ELÉCTRICO)
- Unidad de MTTO seleccionada (ej: AIRE ACONDICIONADO)
- Tipo de solicitud (Mantenimiento/Suministros)

**Resultado**: La IA responde con: ALTA, MEDIA o BAJA

**Fallback**: Si la IA no está disponible o falla, el sistema asigna criticidad **MEDIA** por defecto.

#### 11.12.3. Flujo del Sistema

1. Usuario envía solicitud con descripción
2. Sistema busca palabras clave en la descripción
3. **¿Encuentra palabra clave?**
   - **SÍ**: Asigna criticidad según palabra clave → Fin
   - **NO**: Envía datos a GPT-4o-mini → Asigna criticidad según respuesta de IA → Fin

#### 11.12.4. Validación Manual

- **Service Desk FM** puede revisar y modificar la criticidad asignada automáticamente
- El sistema registra en auditoría: criticidad original, criticidad modificada, método usado (Reglas/IA/Manual), usuario que modificó

#### 11.12.5. Configuración del Sistema

**Parámetros Configurables**:
- Activar/desactivar uso de Inteligencia Artificial
- Criticidad por defecto en caso de error (recomendado: MEDIA)
- Gestión de palabras clave por criticidad

**Auditoría**:
- Método utilizado (Reglas/IA)
- Criticidad asignada
- Fecha y hora
- Modificaciones manuales

### 11.13. Gestión y Verificación de Criticidad

**Propósito**: Gestionar el ordenamiento automático de solicitudes según criticidad y permitir la verificación manual de solicitudes de alta prioridad antes de la coordinación con proveedores.

#### 11.13.1. Funcionalidad de Ordenamiento Automático

**Descripción**: Una vez asignada la criticidad mediante el sistema híbrido (sección 11.12), el sistema organiza automáticamente la bandeja de solicitudes.

**Orden de Prioridad**:
1. **Criticidad Alta** (primer lugar en la lista)
2. **Criticidad Media** (segundo lugar)
3. **Criticidad Baja** (tercer lugar)

**Criterios Adicionales de Ordenamiento**:
- Dentro del mismo nivel de criticidad, ordenar por fecha y hora de creación (más recientes primero)
- Las solicitudes en estado "Nuevo" aparecen antes que las "En Proceso"

**Visualización**:
- **Criticidad Alta**: Indicador rojo, icono de urgencia
- **Criticidad Media**: Indicador amarillo, icono de atención
- **Criticidad Baja**: Indicador verde, icono normal

#### 11.13.2. Tabla de Clasificación de Términos por Criticidad

Esta tabla define los términos clave que el sistema utiliza para clasificar solicitudes y los tiempos de atención esperados.

| Nivel de Urgencia | Atención | Término en la Descripción | Observación |
|-------------------|----------|---------------------------|-------------|
| **Alta** | Inmediata | Caído (ej. "sistema caído") | Servicio o sistema detenido |
| **Alta** | Inmediata | Falla | Error que afecta la operación |
| **Alta** | Inmediata | Bloqueo | Usuario o proceso detenido |
| **Alta** | Inmediata | Emergencia | Requiere atención inmediata |
| **Alta** | Inmediata | Incendio | Requiere atención inmediata |
| **Alta** | Inmediata | Fuego | Requiere atención inmediata |
| **Alta** | Inmediata | Humo | Requiere atención inmediata |
| **Alta** | Inmediata | Corte | Interrupción de energía, red o servicio |
| **Alta** | Inmediata | Crítico | Impacto mayor |
| **Alta** | Inmediata | Urgente | Marcado explícitamente, atención inmediata |
| **Alta** | Inmediata | Sin acceso | Imposibilidad de ingresar |
| **Alta** | Inmediata | Interrupción | Corte parcial o total |
| **Alta** | Inmediata | Pérdida (de datos/servicio) | Datos/servicios comprometidos |
| **Alta** | Inmediata | Paralizado | Operación detenida totalmente |
| **Alta** | Inmediata | Averías | En equipos críticos (Ej. ascensor) |
| **Alta** | Pronto | Observación | Recomendación: ITSE, Auditoría, CC, INDECI |
| **Alta** | Inmediata | Riesgo | Riesgo inminente |
| **Alta** | Inmediata | Filtración | Cualquier tipo de filtración de agua |
| **Media** | Pronto | Retraso | Afecta tiempos, pero no detiene |
| **Media** | Pronto | Alerta | Señal preventiva |
| **Media** | Pronto | Inestable | Servicio funciona con fallas |
| **Media** | Pronto | Incidencia | Requiere solución, pero no crítica |
| **Media** | Pronto | Revisión | Necesita validación |
| **Media** | Pronto | Advertencia | Riesgo potencial |
| **Media** | Pronto | Pendiente | En espera de acción |
| **Media** | Pronto | Plaga | Reporte de plagas |
| **Media** | Pronto | No enfría | Aire acondicionado |
| **Baja** | Programable | Consulta | Pregunta sin impacto operativo |
| **Baja** | Programable | Soporte | Asistencia planificable |
| **Baja** | Programable | Mantenimiento | Preventivo o programado |
| **Baja** | Programable | Mejora | Cambio para optimizar |
| **Baja** | Programable | Solicitud | Pedido administrativo/técnico |
| **Baja** | Programable | Actualización | Cambio de versión/configuración |
| **Baja** | Programable | Configuración | Ajuste planificado |
| **Baja** | Programable | Capacitación | Formación o entrenamiento |
| **Baja** | Programable | Requerimiento | Solicitud general |

**Tiempos de Atención Esperados**:
- **Inmediata**: Atención en menos de 1 hora
- **Pronto**: Atención en el mismo día (máximo 8 horas)
- **Programable**: Atención dentro de 24-72 horas

**Gestión de Términos**:
- El **Superadministrador** puede agregar, editar o eliminar términos
- Puede activar/desactivar términos temporalmente
- Puede cambiar el nivel de criticidad asociado a un término
- El sistema registra todas las modificaciones en auditoría

#### 11.13.3. Verificación Obligatoria para Criticidad Alta

**Regla de Negocio**: Las solicitudes con criticidad ALTA requieren verificación obligatoria por Service Desk FM o Supervisor de MTTO antes de iniciar coordinación con proveedores.

**Roles Autorizados para Verificar**:
- Service Desk FM
- Supervisor de MTTO

**Notificación Automática**:
- **Cuando**: Se crea una solicitud con criticidad ALTA
- **Destinatarios**: Service Desk FM + Supervisor de MTTO
- **Medios**: Correo electrónico + WhatsApp

**Proceso de Verificación**:
1. Usuario revisa la solicitud en detalle
2. Valida descripción, imágenes, categoría y nivel de criticidad
3. Decide si la criticidad asignada es correcta
4. Si NO es correcta: modifica la criticidad (ver sección 11.13.5)
5. Si es correcta: aprueba y puede iniciar coordinación con proveedores

**Validaciones**:
- El sistema NO permite asignar proveedores a solicitudes de criticidad ALTA sin verificación
- Solo solicitudes de criticidad **ALTA** requieren verificación obligatoria
- Solicitudes de criticidad **MEDIA** y **BAJA** pueden pasar directamente a coordinación

#### 11.13.4. Interfaz de Bandeja de Solicitudes

**Descripción**: Pantalla principal donde Service Desk FM y Supervisor de MTTO visualizan todas las solicitudes ordenadas por criticidad.

**Elementos de la Interfaz**:

**Filtros Disponibles**:
- Nivel de criticidad (Alta/Media/Baja)
- Estado (Nuevo/En Proceso/Atendido/Cerrado)
- Tipo de solicitud (Mantenimiento/Suministros)
- Categoría
- Fecha de creación (rango)
- Cliente/Sede
- Usuario solicitante

**Columnas de la Lista**:
- Código de servicio (SRV-AAAA-NNNN)
- Indicador visual de criticidad (color + icono)
- Tipo de solicitud
- Categoría + Unidad de MTTO
- Descripción (resumen)
- Cliente/Sede
- Fecha de creación
- Estado
- Asignado a (proveedor/técnico)
- Acciones (Ver detalle, Modificar criticidad, Asignar)

**Indicadores Visuales**:
- **Rojo + Icono de Alerta**: Criticidad Alta, requiere verificación
- **Amarillo + Icono de Atención**: Criticidad Media
- **Verde + Icono Normal**: Criticidad Baja
- **Badge "Requiere Verificación"**: Para solicitudes ALTA sin verificar

**Contador de Solicitudes**:
- Total de solicitudes
- Solicitudes por criticidad (Alta: X, Media: Y, Baja: Z)
- Solicitudes pendientes de verificación

#### 11.13.5. Cambio Manual de Criticidad

**Descripción**: Funcionalidad que permite a Service Desk FM y Supervisor de MTTO modificar manualmente la criticidad asignada automáticamente.

**Roles Autorizados**:
- Service Desk FM
- Supervisor de MTTO

**Acceso**:
- Desde la bandeja de solicitudes (botón "Modificar Criticidad")
- Desde la vista de detalle de la solicitud

**Formulario de Cambio**:

| Campo | Tipo | Obligatorio | Descripción |
|-------|------|-------------|-------------|
| **Criticidad Original** | Texto (solo lectura) | - | Criticidad asignada por el sistema |
| **Método Original** | Texto (solo lectura) | - | Reglas / IA / Manual |
| **Nueva Criticidad** | Lista desplegable | Sí | Alta / Media / Baja |
| **Justificación** | Texto libre | No | Razón del cambio (opcional, recomendado) |

**Opciones de Cambio Permitidas**:
- De Alta a Media
- De Alta a Baja
- De Media a Alta
- De Media a Baja
- De Baja a Alta
- De Baja a Media

**Validaciones**:
- El usuario debe tener rol de Service Desk FM o Supervisor de MTTO
- No se puede cambiar la criticidad de solicitudes cerradas
- El sistema debe solicitar confirmación antes de aplicar el cambio

**Acciones del Sistema al Cambiar Criticidad**:
1. Actualiza el campo de criticidad en la solicitud
2. Reordena la bandeja de solicitudes según nueva criticidad
3. Registra en auditoría (ver campos abajo)
4. Si el cambio es de Alta a Media/Baja: envía notificación al usuario solicitante
5. Si el cambio es de Media/Baja a Alta: envía notificación a Service Desk + Supervisor

**Campos de Auditoría**:
- Código de solicitud
- Criticidad original
- Método de asignación original (Reglas/IA)
- Nueva criticidad
- Usuario que realizó el cambio
- Rol del usuario
- Fecha y hora del cambio
- Justificación ingresada
- IP del usuario (opcional)

#### 11.13.6. Notificaciones del Proceso

| Evento | Destinatarios | Medios |
|--------|---------------|--------|
| Nueva solicitud criticidad ALTA | Service Desk FM + Supervisor MTTO | Correo + WhatsApp |
| Nueva solicitud criticidad MEDIA | Service Desk FM | Correo |
| Nueva solicitud criticidad BAJA | Service Desk FM | Correo |
| Cambio de criticidad (Alta → Media/Baja) | Usuario solicitante | Correo |
| Cambio de criticidad (Media/Baja → Alta) | Service Desk FM + Supervisor MTTO | Correo + WhatsApp |
| Asignación a proveedor/técnico | Proveedor/Técnico asignado | Correo + WhatsApp |
| Solicitud Alta sin verificar >2 horas | Supervisor de MTTO | WhatsApp |

#### 11.13.7. Reglas de Negocio

- **RN-11.13.1**: Solo solicitudes de criticidad ALTA requieren verificación obligatoria antes de coordinación con proveedores
- **RN-11.13.2**: El sistema ordena automáticamente las solicitudes por criticidad (Alta > Media > Baja) y dentro del mismo nivel por fecha de creación
- **RN-11.13.3**: Solo Service Desk FM y Supervisor de MTTO pueden modificar manualmente la criticidad
- **RN-11.13.4**: Todos los cambios manuales de criticidad quedan registrados en auditoría con usuario, fecha y justificación
- **RN-11.13.5**: El sistema NO permite asignar proveedores a solicitudes de criticidad ALTA sin verificación previa
- **RN-11.13.6**: Si una solicitud de criticidad ALTA no es verificada en 2 horas, el sistema envía alerta al Supervisor de MTTO
- **RN-11.13.7**: Los términos de la tabla de clasificación son configurables solo por el Superadministrador
## 12. Módulo de Solicitud de Cotización

**Propósito**: Gestionar el proceso completo de solicitud, recepción y análisis de cotizaciones de proveedores para la atención de incidencias. Permite a Service Desk FM y Supervisor de MTTO seleccionar proveedores, al área de Compras coordinar las cotizaciones, y a los proveedores cargar sus propuestas a través del Portal de Proveedores.

### 12.1. Selección de Proveedores

**Descripción**: Funcionalidad que permite a Service Desk FM y Supervisor de MTTO seleccionar uno o más proveedores para solicitar cotización.

**Roles Autorizados**:
- Service Desk FM
- Supervisor de MTTO

**Criterios de Selección**:
- Especialidad del proveedor (debe coincidir con la categoría de la incidencia)
- Disponibilidad del proveedor (activo en el sistema)
- Histórico de desempeño (calificación, cumplimiento de plazos)
- Cobertura geográfica (sede del cliente)

**Opciones del Sistema**:
- Selección múltiple de proveedores (mínimo 1, recomendado 3)
- Filtros por especialidad, ubicación, calificación
- Vista de historial de desempeño de cada proveedor
- Opción de derivar a Compras si requiere gestión especializada

**Derivación a Compras**:
- **Cuándo**: Servicios especializados o de alto monto
- **Acción**: Cambia estado a "En Cotización - Compras"
- **Notificación Automática**: Sistema envía correo a Compras con:
  - Código de solicitud
  - Descripción de incidencia
  - Categoría y Unidad de MTTO
  - Cliente y sede
  - Criticidad
  - **Enlace de carga de cotización** (para compartir con proveedores)

### 12.2. Generación de Enlaces de Cotización

**Descripción**: Sistema genera enlaces únicos para que cada proveedor cargue su cotización.

**Características del Enlace**:
- URL única por proveedor y por solicitud
- Formato: `https://proveedores.fm.com/cotizacion/{token}`
- Token de seguridad único
- Acceso directo sin login (o con login si el proveedor ya tiene cuenta)

**Generación Automática**:
- Se genera al seleccionar proveedores
- Se incluye en correo manual enviado por Compras
- Enlace expira según fecha límite de respuesta

**Seguridad**:
- Token único no reutilizable
- Solo el proveedor asignado puede acceder
- Expira automáticamente después de fecha límite

### 12.3. Portal de Proveedores - Carga de Cotización

**Descripción**: Interfaz en Portal de Proveedores para que proveedores carguen sus cotizaciones.

**Acceso**:
- Mediante enlace único recibido por correo
- Portal independiente: `https://proveedores.fm.com`
- Autenticación automática con token o login manual

**Formulario de Carga de Cotización**:

| Campo | Tipo | Obligatorio | Validaciones | Descripción |
|-------|------|-------------|--------------|-------------|
| **Archivo de Cotización** | Archivo | Sí | PDF, XLS, XLSX, DOC, DOCX; Max 10MB | Documento con la propuesta |
| **Monto Total** | Numérico | Sí | Mayor a 0, máximo 2 decimales | Monto total cotizado |
| **Moneda** | Lista desplegable | Sí | Soles (PEN) / Dólares (USD) | Moneda de cotización |
| **Tiempo de Entrega** | Numérico | Sí | Mayor a 0, en días | Días para completar servicio |
| **Validez de Cotización** | Numérico | Sí | Mayor a 0, en días | Días de vigencia de la propuesta |
| **Observaciones** | Texto libre | No | Máximo 500 caracteres | Comentarios adicionales |

**Validaciones al Cargar**:
- Validación de formato de archivo permitido
- Validación de tamaño máximo (10 MB)
- Escaneo antivirus del archivo
- Monto debe ser numérico y mayor a 0
- Tiempo de entrega debe ser numérico

**Acciones del Sistema**:
- Al cargar exitosamente: notifica a Service Desk FM y Compras
- Marca estado de cotización como "Recibida"
- Permite al proveedor ver confirmación de carga exitosa
- Bloquea edición después de enviar (requiere contacto con FM para cambios)

### 12.4. Bandeja de Cotizaciones para FM/Compras

**Descripción**: Interfaz para que Service Desk FM, Supervisor de MTTO y Compras visualicen y comparen cotizaciones recibidas.

**Vista de Lista de Cotizaciones**:

**Filtros Disponibles**:
- Por solicitud (código SRV-AAAA-NNNN)
- Por proveedor
- Por estado (Pendiente/Recibida/Aprobada/Rechazada)
- Por fecha de solicitud
- Por criticidad de la incidencia
- Derivadas a Compras (Sí/No)

**Columnas de la Vista**:
- Código de solicitud
- Descripción de incidencia (resumen)
- Proveedores solicitados vs proveedores que respondieron
- Montos cotizados (comparativa)
- Tiempos de entrega
- Estado de cada cotización
- Fecha límite de respuesta
- Acciones (Ver detalle, Aprobar, Rechazar)

**Vista de Comparación**:
- Tabla comparativa lado a lado de todas las cotizaciones
- Columnas: Proveedor, Monto, Moneda, Tiempo Entrega, Validez
- Destacado visual del menor monto y menor tiempo
- Acceso a archivos de cotización de cada proveedor
- Histórico de desempeño del proveedor

### 12.5. Análisis y Aprobación de Cotización

**Descripción**: Funcionalidad para que FM seleccione y apruebe la mejor cotización.

**Roles Autorizados**:
- Service Desk FM
- Supervisor de MTTO
- Compras (si fue derivado)

**Proceso de Aprobación**:

**Requisito Previo**: Debe haber al menos 1 cotización cargada

**Análisis Disponible**:
- Comparación de montos (convertidos a misma moneda si aplica)
- Comparación de tiempos de entrega
- Histórico de desempeño de proveedores
- Calificaciones de servicios anteriores

**Aprobación**:
- Selección del proveedor ganador
- Campo opcional: Justificación de selección
- Confirmación de aprobación
- Sistema marca automáticamente las demás cotizaciones como "Rechazadas"

**Acciones del Sistema al Aprobar**:
1. Actualiza estado de cotización a "Aprobada"
2. Rechaza automáticamente las demás cotizaciones de la misma solicitud
3. Genera **enlace de programación de servicio** único para el proveedor aprobado
4. Envía notificación automática al proveedor aprobado con:
   - Confirmación de aprobación
   - Monto aprobado
   - **Link de programación**
   - Indicación: "La recepción del servicio debe ser en un plazo máximo de 3 días calendario"
5. Envía notificación a proveedores no seleccionados (cotizaciones rechazadas)
6. Registra en auditoría

### 12.6. Campos del Módulo de Cotización

| Campo | Tipo | Obligatorio | Descripción |
|-------|------|-------------|-------------|
| **Código de Solicitud** | Texto (referencia) | Sí | Código de la solicitud de incidencia (SRV-AAAA-NNNN) |
| **Proveedores Seleccionados** | Lista múltiple | Sí | Proveedores a los que se solicita cotización |
| **Estado de Cotización** | Lista | Sí | Pendiente / En Proceso / Recibida / Aprobada / Rechazada |
| **Derivado a Compras** | Sí/No | Sí | Indica si requiere gestión de Compras |
| **Fecha de Solicitud** | Fecha/Hora | Sí | Fecha en que se solicita cotización |
| **Fecha Límite de Respuesta** | Fecha | Sí | Plazo para recibir cotizaciones |
| **Enlace de Carga** | URL (autogenerado) | Sí | Link único para cada proveedor |
| **Archivo de Cotización** | Archivo | Sí | Documento cargado por el proveedor |
| **Monto Cotizado** | Numérico | Sí | Monto total de la cotización |
| **Moneda** | Lista | Sí | Soles (PEN) / Dólares (USD) |
| **Tiempo de Entrega** | Numérico | Sí | Días estimados para completar el servicio |
| **Validez de Cotización** | Numérico | Sí | Días de validez de la propuesta |
| **Observaciones Proveedor** | Texto libre | No | Comentarios adicionales del proveedor |
| **Proveedor Seleccionado** | Lista | No | Proveedor aprobado (después del análisis) |
| **Fecha de Aprobación** | Fecha/Hora | No | Fecha en que se aprueba la cotización |
| **Usuario que Aprueba** | Texto | No | Service Desk FM o Supervisor que aprueba |
| **Justificación de Selección** | Texto libre | No | Razón por la cual se eligió ese proveedor |

### 12.7. Notificaciones del Módulo de Cotización

| Evento | Destinatarios | Medio | Tipo |
|--------|---------------|-------|------|
| Solicitud derivada a Compras | Área de Compras | Correo | Automático |
| Solicitud de cotización a proveedor | Proveedores seleccionados | Correo | **Manual** (por Compras) |
| Proveedor carga cotización | Service Desk FM + Compras | Correo | Automático |
| Cotización aprobada (incluye link programación) | Proveedor seleccionado | Correo | Automático |
| Cotización rechazada | Proveedores no seleccionados | Correo | Automático |
| Plazo de cotización próximo a vencer (24h) | Proveedores sin respuesta | Correo | Automático |

### 12.8. Validaciones del Módulo de Cotización

- Debe haber al menos 1 proveedor seleccionado para solicitar cotización
- El enlace de carga de cotización es único y expira después de la fecha límite de respuesta
- Solo el proveedor asignado puede acceder a su enlace de carga
- No se puede aprobar una cotización sin que haya sido cargada por el proveedor
- El sistema debe validar que el archivo de cotización tenga formato permitido (PDF, Excel, Word)
- Archivo debe pasar escaneo antivirus antes de almacenarse
- Al aprobar una cotización, el sistema automáticamente rechaza las demás cotizaciones de la misma solicitud
- Validación de campos numéricos (monto > 0, tiempo entrega > 0)

### 12.9. Reglas de Negocio del Módulo de Cotización

- **RN-12.1**: Si el servicio requiere especialización, debe derivarse obligatoriamente a Compras
- **RN-12.2**: El enlace de carga de cotización es único por proveedor y por solicitud
- **RN-12.3**: Las cotizaciones vencidas (fuera de fecha límite) quedan marcadas como "Expiradas" automáticamente
- **RN-12.4**: Solo Service Desk FM, Supervisor de MTTO y Compras pueden aprobar cotizaciones
- **RN-12.5**: Al aprobar una cotización, el sistema genera automáticamente el enlace de programación de servicio
- **RN-12.6**: El monto cotizado debe registrarse en la moneda original (PEN o USD) para posterior conversión si es necesario
- **RN-12.7**: El proveedor no puede editar ni eliminar su cotización después de enviarla
- **RN-12.8**: La notificación manual a proveedores (por Compras) se realiza fuera del sistema

### 12.10. Auditoría del Módulo de Cotización

- Fecha y hora de solicitud de cotización
- Proveedores seleccionados
- Usuario que solicita cotización
- Derivación a Compras (si aplica)
- Fecha de carga de cada cotización
- Proveedor que carga cotización
- Monto cotizado y moneda
- Fecha de aprobación/rechazo
- Usuario que aprueba/rechaza
- Justificación de selección (opcional)

---

## 13. Módulo de Programación de Servicio

**Propósito**: Gestionar la programación de fechas de inicio de servicio por parte de los proveedores aprobados. Permite al proveedor definir el tipo de servicio (nacional o importación), registrar fechas de inicio, y al Supervisor de MTTO validar y coordinar la programación final. (SOLICITUD DE COTIZACION Y PROGRAMACION DE SERVICIO)

### 13.1. Generación de Enlace de Programación

**Descripción**: Sistema genera automáticamente un enlace único para que el proveedor aprobado programe la fecha de inicio del servicio.

**Generación Automática**:
- Se genera al aprobar una cotización
- Formato: `https://proveedores.fm.ruwaytech.com/programacion/{token}`
- Token único de seguridad
- Incluido en correo de notificación de aprobación

**Contenido del Correo de Aprobación**:
- Confirmación de aprobación de cotización
- Código de solicitud
- Monto aprobado
- **Link de programación de servicio**
- Indicación importante: "La recepción del servicio debe ser en un plazo máximo de 3 días calendario de aprobada la cotización"

**Seguridad del Enlace**:
- Token único por proveedor y por solicitud
- Solo el proveedor aprobado puede acceder
- Expira después de 30 días de emitido
- Acceso directo sin login o con credenciales del proveedor

### 13.2. Portal de Proveedores - Formulario de Programación

**Descripción**: Interfaz en Portal de Proveedores donde el proveedor selecciona tipo de servicio y fecha de inicio.

**Acceso**:
- Mediante enlace único recibido por correo
- Portal: `https://proveedores.fm.ruwaytech.com`
- Autenticación automática con token o login manual

**Formulario de Programación**:

| Campo | Tipo | Obligatorio | Validaciones | Descripción |
|-------|------|-------------|--------------|-------------|
| **Tipo de Servicio** | Lista desplegable | Sí | Nacional / Importación | Define restricción de plazo |
| **Fecha de Inicio Propuesta** | Calendario (fecha) | Sí | Ver validaciones por tipo | dd/mm/yyyy |
| **Observaciones** | Texto libre | No | Máximo 500 caracteres | Comentarios sobre la programación |

**Validaciones por Tipo de Servicio**:

**Si es NACIONAL**:
- Fecha propuesta NO puede exceder 3 días calendario desde fecha de aprobación de cotización
- Fecha no puede ser anterior a fecha actual
- Sistema calcula automáticamente plazo máximo (Fecha aprobación + 3 días calendario)
- Muestra mensaje: "Plazo máximo: {fecha calculada}"

**Si es IMPORTACIÓN**:
- Sistema libera restricción de 3 días
- Permite seleccionar cualquier fecha futura
- Recomienda justificar el plazo en campo observaciones
- Muestra mensaje: "Sin restricción de plazo - Importación"

**Comportamiento del Sistema**:
- Al seleccionar tipo "Nacional": Bloquea fechas posteriores a 3 días calendario
- Al seleccionar tipo "Importación": Habilita calendario completo
- Valida que fecha no sea anterior a hoy
- Permite campo de observaciones para justificar plazos

### 13.3. Validación de Programación por Supervisor MTTO

**Descripción**: Funcionalidad que permite al Supervisor de MTTO revisar y aprobar/rechazar la programación propuesta por el proveedor.

**Rol Autorizado**:
- Supervisor de MTTO

**Notificación Automática**:
- **Cuándo**: Proveedor envía fecha propuesta
- **Destinatario**: Supervisor de MTTO
- **Medio**: Correo electrónico
- **Contenido**: Código de solicitud, proveedor, tipo de servicio, fecha propuesta, link al sistema

**Interfaz de Validación**:

**Vista de Detalle**:
- Código de solicitud
- Descripción de la incidencia
- Proveedor asignado
- Monto aprobado
- Tipo de servicio (Nacional/Importación)
- Fecha propuesta por proveedor
- Observaciones del proveedor
- Plazo máximo (si es nacional)
- Cliente y sede

**Opciones del Supervisor**:
- **Aprobar**: Da VB a la programación
- **Rechazar**: Solicita nueva fecha al proveedor
- **Campo obligatorio si rechaza**: Motivo del rechazo

**Acciones al Aprobar**:
- Actualiza estado a "Programación Validada"
- Permite continuar con coordinación final
- Notifica al proveedor de la aprobación
- Habilita campo de "Fecha Confirmada"

**Acciones al Rechazar**:
- Actualiza estado a "Programación Rechazada"
- Notifica al proveedor con motivo de rechazo
- Reabre formulario de programación para el proveedor
- Proveedor debe proponer nueva fecha

### 13.4. Funcionalidad de Coordinación Final y Confirmación de Fecha

**Propósito**: Permitir el registro de la fecha definitiva del servicio después de la coordinación manual entre Supervisor MTTO y proveedor.

**Nota Importante**: La coordinación de detalles operativos, punto de contacto en sede y requisitos especiales se realiza **fuera del sistema** mediante correo electrónico o WhatsApp. El sistema solo registra el resultado final de esta coordinación.

#### 13.4.1. Funcionalidad de Registro de Fecha Confirmada

El sistema debe proporcionar:
- Campo "Fecha Confirmada" para registrar la fecha definitiva de inicio de servicio
- Formato de fecha: dd/mm/yyyy
- Calendario visual para selección de fecha
- Validación automática: la fecha no puede ser anterior al día actual
- Campo opcional para observaciones o detalles adicionales
- Botón "Confirmar Fecha de Servicio"

#### 13.4.2. Validaciones del Sistema

El sistema debe validar:
- Fecha confirmada no sea anterior a la fecha actual
- Fecha confirmada sea coherente con el plazo del servicio
- Confirmación de que se ha completado la coordinación manual
- Campos obligatorios estén completos

#### 13.4.3. Acciones Automáticas al Confirmar Fecha

El sistema debe ejecutar automáticamente:

**1. Actualización de Estado**:
- Cambiar estado del servicio a "Servicio Programado"
- Registrar fecha y hora de confirmación
- Registrar usuario que confirmó (Supervisor de MTTO)

**2. Generación de Notificaciones**:
- **Al Cliente**: Correo electrónico con información del servicio programado (fecha, hora, proveedor, tipo de servicio)
- **Al Proveedor**: Correo de confirmación final con detalles del servicio

**3. Programación de Recordatorios Automáticos**:
- **24 horas antes del servicio**: Envío de recordatorio por correo electrónico y WhatsApp a todas las partes
- **2 horas antes del servicio**: Envío de recordatorio por WhatsApp al proveedor y supervisor

**4. Registro de Auditoría**:
- Usuario que confirmó la fecha
- Fecha y hora de confirmación
- Fecha programada del servicio
- Cambio de estado registrado

### 13.5. Campos del Módulo de Programación

| Campo | Tipo | Obligatorio | Descripción |
|-------|------|-------------|-------------|
| **Código de Solicitud** | Texto (referencia) | Sí | Código de la solicitud de incidencia |
| **Proveedor Asignado** | Texto (referencia) | Sí | Proveedor aprobado en cotización |
| **Enlace de Programación** | URL (autogenerado) | Sí | Link único para programar servicio |
| **Tipo de Servicio** | Lista | Sí | Nacional / Importación |
| **Fecha de Aprobación Cotización** | Fecha/Hora | Sí | Fecha en que se aprobó la cotización |
| **Plazo Máximo (Nacional)** | Fecha (calculado) | - | Fecha aprobación + 3 días calendario |
| **Fecha Propuesta por Proveedor** | Fecha | Sí | Fecha que el proveedor propone |
| **Formato de Fecha** | - | - | dd/mm/yyyy |
| **Observaciones Proveedor** | Texto libre | No | Comentarios sobre la programación |
| **Estado de Programación** | Lista | Sí | Pendiente / Propuesta / Validada / Rechazada / Confirmada |
| **Validado por** | Texto (usuario) | No | Supervisor que valida |
| **Fecha de Validación** | Fecha/Hora | No | Cuándo se validó |
| **Requiere Reprogramación** | Sí/No | - | Indica si se rechazó la fecha |
| **Motivo de Rechazo** | Texto libre | Sí (si rechaza) | Razón del rechazo |
| **Fecha Confirmada** | Fecha | Sí | Fecha final coordinada |
| **Usuario que Confirma** | Texto | Sí | Supervisor que confirma |
| **Fecha de Confirmación** | Fecha/Hora | Sí | Cuándo se confirmó |

### 13.6. Notificaciones del Módulo de Programación

| Evento | Destinatarios | Medio | Tipo |
|--------|---------------|-------|------|
| Cotización aprobada (incluye link programación) | Proveedor aprobado | Correo | Automático |
| Proveedor propone fecha | Supervisor de MTTO | Correo | Automático |
| Programación validada | Proveedor | Correo | Automático |
| Programación rechazada | Proveedor | Correo | Automático |
| Coordinación manual de fecha | Proveedor | Correo/WhatsApp | **Manual** |
| Fecha confirmada | Proveedor + Cliente | Correo | Automático |
| Recordatorio 24h antes del servicio | Proveedor + Supervisor MTTO | Correo + WhatsApp | Automático |
| Recordatorio 2h antes del servicio | Proveedor + Supervisor MTTO | WhatsApp | Automático |

### 13.7. Validaciones del Módulo de Programación

- El enlace de programación solo está activo después de aprobar la cotización
- Solo el proveedor aprobado puede acceder al enlace de programación
- Para servicios **Nacionales**: La fecha propuesta NO puede exceder 3 días calendario desde la aprobación de cotización
- Para servicios de **Importación**: No hay restricción de tiempo, pero debe justificarse el plazo en observaciones
- El Supervisor de MTTO debe validar la programación antes de que el servicio inicie
- No se puede confirmar una programación sin la aprobación del Supervisor de MTTO
- El sistema debe validar que la fecha propuesta no sea anterior a la fecha actual
- La fecha confirmada queda bloqueada y solo puede modificarse con aprobación del Supervisor de MTTO

### 13.8. Reglas de Negocio del Módulo de Programación

- **RN-13.1**: La recepción del servicio debe ser en un plazo máximo de 3 días calendario de aprobada la cotización (solo para servicios nacionales)
- **RN-13.2**: Para servicios de importación, se libera la restricción de 3 días calendario
- **RN-13.3**: El enlace de programación es único por proveedor y expira después de 30 días de emitido
- **RN-13.4**: Solo el Supervisor de MTTO puede validar o rechazar programaciones propuestas
- **RN-13.5**: Si la programación es rechazada, el proveedor recibe notificación y debe proponer nueva fecha
- **RN-13.6**: El sistema envía recordatorios automáticos 24h y 2h antes del inicio del servicio programado
- **RN-13.7**: La coordinación manual (correo/WhatsApp) entre Supervisor y proveedor es externa al sistema
- **RN-13.8**: El Supervisor de MTTO debe registrar manualmente la fecha confirmada en el sistema después de coordinar



### 13.9. Auditoría del Módulo de Programación

- Fecha de emisión del enlace de programación
- Proveedor que accede al enlace
- Tipo de servicio seleccionado (Nacional/Importación)
- Fecha propuesta por proveedor
- Usuario (Supervisor) que valida/rechaza
- Fecha y hora de validación/rechazo
- Motivo de rechazo (si aplica)
- Fecha confirmada final
- Cambios en la fecha confirmada (si hay reprogramaciones)
- Usuario que confirma la fecha final
- Notificaciones enviadas

---

## 14. Portal de Proveedores

**Propósito**: Proporcionar una interfaz web independiente para que los proveedores puedan cargar cotizaciones, programar servicios y gestionar sus asignaciones de manera segura y eficiente.

### 14.1. Características del Portal de Proveedores

**URL del Portal**: `https://proveedores.fm.ruwaytech.com`

**Arquitectura**:
- Portal web independiente del sistema FM interno
- Diseño responsive (accesible desde PC, tablet y móvil)
- Interfaz en español
- Acceso mediante enlace directo desde correos o login tradicional

**Tecnología**:
- Front-end separado del Portal de Clientes
- API REST para comunicación con sistema FM interno
- Certificado SSL obligatorio (HTTPS)
- Autenticación mediante tokens

### 14.2. Seguridad y Acceso

**Autenticación**:
- Login con usuario (email del proveedor) y contraseña
- Opción de acceso directo mediante enlace con token temporal (cotizaciones y programaciones)
- Recuperación de contraseña mediante correo electrónico
- Obligación de cambiar contraseña cada 3 meses (ver sección 3.1)

**Permisos**:
- Cada proveedor solo ve sus propias solicitudes asignadas
- No puede ver cotizaciones de otros proveedores
- No puede ver información de clientes (solo sede y tipo de incidencia)
- No puede modificar cotizaciones o programaciones después de enviarlas (requiere contacto con FM)

**Seguridad**:
- Certificado SSL (HTTPS)
- Enlaces con token único de un solo uso
- Sesión expira después de 30 minutos de inactividad
- Registro de accesos en auditoría

### 14.3. Funcionalidades Disponibles en el Portal

#### 14.3.1. Dashboard Principal

**Elementos**:
- Resumen de solicitudes asignadas
- Cotizaciones pendientes de carga
- Programaciones pendientes de confirmar
- Servicios en ejecución
- Historial de servicios completados

**Indicadores**:
- Cotizaciones pendientes (número)
- Programaciones por confirmar (número)
- Servicios próximos (en 48h)
- Alertas de vencimiento de plazo

#### 14.3.2. Módulo de Cotizaciones

**Funcionalidades**:
- Ver solicitudes de cotización recibidas
- Cargar archivo de cotización (PDF, Excel, Word)
- Ingresar monto, moneda, tiempo de entrega
- Ver estado de cotización (Pendiente, Aprobada, Rechazada)
- Historial de cotizaciones enviadas

**Campos Visibles**:
- Código de solicitud
- Descripción de la incidencia
- Categoría y Unidad de MTTO
- Sede del cliente
- Fecha límite de respuesta
- Estado de cotización

#### 14.3.3. Módulo de Programación de Servicios

**Funcionalidades**:
- Acceder a solicitudes con cotización aprobada
- Seleccionar tipo de servicio (Nacional/Importación)
- Proponer fecha de inicio de servicio
- Ver validación del Supervisor de MTTO
- Ver fecha confirmada final
- Recibir notificaciones de recordatorios

**Campos Visibles**:
- Código de solicitud
- Descripción del servicio
- Monto aprobado
- Plazo máximo (si es nacional)
- Estado de programación
- Fecha propuesta
- Fecha confirmada

#### 14.3.4. Perfil del Proveedor

**Funcionalidades**:
- Ver datos del proveedor (RUC, razón social, contacto)
- Actualizar datos de contacto (email, teléfono, WhatsApp)
- Cambiar contraseña
- Ver histórico de servicios realizados
- Descargar certificados de desempeño (si aplica)

### 14.4. Integración con Sistema FM Interno

**Sincronización**:
- Todas las acciones en el Portal de Proveedores se sincronizan en tiempo real con el sistema FM interno
- Las notificaciones generadas desde FM llegan automáticamente al portal
- Los cambios de estado se reflejan instantáneamente

**API REST**:
- Endpoints seguros para carga de cotizaciones
- Endpoints para programación de servicios
- Endpoints para consulta de solicitudes asignadas
- Autenticación mediante API Key y tokens JWT

### 14.5. Notificaciones desde el Portal

**Medios**:
- Correo electrónico
- Notificaciones push en el portal (cuando el proveedor está logueado)
- WhatsApp (para recordatorios de servicios)

**Eventos**:
- Nueva solicitud de cotización asignada
- Cotización aprobada
- Cotización rechazada
- Recordatorio de plazo de cotización próximo a vencer
- Solicitud de programación disponible
- Programación validada/rechazada
- Recordatorio de servicio próximo (24h y 2h antes)

### 14.6. Auditoría del Portal de Proveedores

- Accesos al portal (login exitoso/fallido)
- IP de acceso
- Cotizaciones cargadas
- Programaciones registradas
- Modificaciones de perfil
- Descarga de documentos
- Tiempo de sesión

### 14.7. Reglas de Negocio del Portal de Proveedores

- **RN-14.1**: El Portal de Proveedores es independiente del Portal de Clientes y del sistema FM interno
- **RN-14.2**: Cada proveedor solo puede acceder a sus propias solicitudes y cotizaciones
- **RN-14.3**: Los enlaces con token expiran después de 30 días de emitidos
- **RN-14.4**: El proveedor debe cambiar su contraseña cada 3 meses (ver sección 3.1)
- **RN-14.5**: El portal debe ser accesible 24/7 con disponibilidad mínima de 99%
- **RN-14.6**: Todos los archivos cargados deben pasar validación antivirus antes de almacenarse
- **RN-14.7**: El proveedor no puede eliminar cotizaciones o programaciones después de enviarlas


## 15. Módulo de Cotización Formal para Cliente

**Propósito**: Gestionar la elaboración, cálculo de FEE y envío de cotizaciones formales a clientes (internos y externos), incluyendo el proceso de aprobación y posterior solicitud de emisión de Orden de Compra (OC).

### 15.1. Descripción General del Módulo

El módulo de Cotización Formal para Cliente permite al Facility Manager (FM) elaborar cotizaciones basadas en las cotizaciones recibidas de proveedores, aplicar márgenes de FEE según el tipo de cliente, y gestionar el proceso de aprobación hasta la emisión de la Orden de Compra.

**Características principales**:
- Gestión de cotizaciones para clientes internos y externos
- Cálculo automático de FEE según tipo de cliente y parámetros contractuales
- Diferenciación de flujos de aprobación según tipo de cliente
- Generación de formato especial de cotización en formato LNT (para obras menores)
- Integración con sistema de emisión de Orden de Compra (OC)
- Trazabilidad completa del proceso de cotización

### 15.2. Acceso al Módulo de Cotizaciones

#### 15.2.1. Ingreso al Sistema

**Proceso**:
1. FM ingresa al sistema con sus credenciales
2. FM accede al módulo de "Cotizaciones" desde el menú principal
3. Sistema valida permisos del usuario (solo FM y roles autorizados)

**Roles con Acceso**:
- Facility Manager (FM)
- Gerente de FM
- Supervisor FM
- Gerente General (solo visualización)

#### 15.2.2. Visualización de Relación de Cotizaciones

**Funcionalidad del Sistema**:
- Sistema muestra automáticamente la relación completa de cotizaciones pendientes y en proceso
- Listado incluye cotizaciones provenientes del módulo de Solicitud de Cotización (Módulo 12)
- Vista organizada por estado y antigüedad

**Campos Visibles en el Listado**:

| Campo | Tipo | Descripción |
|-------|------|-------------|
| **Código de Solicitud** | Texto | Código único de la solicitud de atención |
| **Código de Cotización** | Texto | Código autogenerado para la cotización |
| **Cliente** | Texto | Nombre del cliente |
| **Tipo de Cliente** | Lista | Interno / Externo |
| **Sede** | Texto | Ubicación de la sede del cliente |
| **Descripción de Incidencia** | Texto | Breve descripción del servicio solicitado |
| **Proveedor Seleccionado** | Texto | Proveedor cuya cotización fue aprobada |
| **Monto Proveedor** | Número | Monto de la cotización aprobada del proveedor |
| **Moneda** | Lista | S/. o $ |
| **Estado** | Lista | Pendiente / En Elaboración / Enviada / Aprobada / Rechazada |
| **Fecha de Creación** | Fecha | Fecha en que se creó la cotización |
| **Fecha de Envío** | Fecha | Fecha en que se envió al cliente |

### 15.3. Proceso de Elaboración de Cotización

#### 15.3.1. Selección de Cotización a Elaborar

**Funcionalidad**:
- FM selecciona de la lista la cotización a revisar y elaborar
- Sistema abre la ficha completa de la cotización
- Sistema muestra toda la información de la solicitud original y cotización de proveedor aprobada

**Información Disponible**:
- Datos del cliente y sede
- Descripción completa de la incidencia
- Categoría y subcategoría del servicio
- Cotización del proveedor aprobada (monto, plazo, alcance)
- Historial de la solicitud

#### 15.3.2. Elaboración de Cotización por FM

**Proceso**:
1. FM revisa la cotización del proveedor aprobada
2. FM elabora la cotización formal para el cliente
3. FM ingresa o valida los siguientes datos:

**Campos del Formulario de Cotización**:

| Campo | Tipo | Obligatorio | Descripción |
|-------|------|-------------|-------------|
| **Descripción del Servicio** | Texto largo | Sí | Descripción detallada del servicio a cotizar |
| **Alcance del Servicio** | Texto largo | Sí | Detalle del alcance incluido en la cotización |
| **Monto Base (Proveedor)** | Número | Sí | Monto de la cotización del proveedor |
| **Moneda** | Lista | Sí | S/. o $ |
| **Plazo de Ejecución** | Número | Sí | Días calendario para completar el servicio |
| **Observaciones** | Texto libre | No | Comentarios adicionales sobre la cotización |

### 15.4. Cálculo Automático de FEE

#### 15.4.1. Diferenciación por Tipo de Cliente

**Funcionalidad del Sistema**:
- Sistema identifica automáticamente si el cliente es **Interno** o **Externo**
- Según el tipo de cliente, el sistema aplica diferentes reglas de cálculo de FEE

#### 15.4.2. Cliente Externo: Visualización de Monto y Margen de FEE Contractual

**Proceso para Cliente Externo**:

1. **Sistema muestra automáticamente**:
   - Campo de visualización: "Monto y Margen de FEE Contractual"
   - Monto del FEE establecido en el contrato con el cliente
   - Porcentaje de margen de FEE contractual
   - Este campo es de solo lectura (no editable por FM)

2. **FM coloca el FEE**:
   - FM puede ajustar el FEE dentro del rango permitido
   - Sistema valida que no exceda el margen contractual
   - Si FM intenta exceder el margen, sistema muestra alerta

3. **Sistema realiza el cálculo del FEE**:
   - Fórmula para Cliente Externo: 
     ```
     Monto Total = Monto Base Proveedor + FEE + IGV
     ```
   - Sistema calcula automáticamente el monto total
   - Sistema muestra desglose completo

**Campos Calculados Automáticamente**:

| Campo | Fórmula | Descripción |
|-------|---------|-------------|
| **Monto Base** | Monto Proveedor | Cotización aprobada del proveedor |
| **FEE (S/. o $)** | Monto Base × % FEE | Monto del FEE aplicado |
| **Subtotal** | Monto Base + FEE | Subtotal antes de IGV |
| **IGV (18%)** | Subtotal × 0.18 | Impuesto General a las Ventas |
| **Monto Total** | Subtotal + IGV | Monto final de la cotización |

#### 15.4.3. Cliente Interno: Cálculo Directo de FEE

**Proceso para Cliente Interno**:

1. **Sistema omite la validación de FEE contractual**
   - Para clientes internos no aplica restricción de margen contractual
   - FM tiene mayor flexibilidad para establecer el FEE

2. **FM coloca el FEE**:
   - FM ingresa el porcentaje o monto de FEE a aplicar
   - Campo editable sin restricciones de margen contractual

3. **Sistema realiza el cálculo del FEE**:
   - Fórmula para Cliente Interno:
     ```
     Monto Total = Monto Base Proveedor + FEE
     ```
   - Para clientes internos, el IGV puede no aplicarse según configuración
   - Sistema calcula y muestra el desglose

**Validaciones para Cliente Interno**:
- FEE debe ser mayor a 0
- El monto total debe ser razonable (alertas si excede 200% del monto base)
- Sistema registra justificación si el FEE es mayor al 50%

#### 15.4.4. Generación Automática de Documento de Cotización

**Propósito**: El sistema debe generar automáticamente el documento formal de cotización en formato Excel con el diseño estándar de la empresa, incluyendo todos los cálculos, desglose de costos y condiciones comerciales.

**Formato Disponible**:
- **Excel (.xlsx)**: Formato editable y oficial para envío al cliente

**Momento de Generación**:
- Después de que FM complete todos los campos de la cotización
- Antes de enviar la cotización al cliente
- El documento se genera haciendo clic en botón "Generar Documento" o "Vista Previa"

**Diseño del Documento de Cotización**:

El documento debe seguir el formato estándar mostrado a continuación:

![Formato de Cotización de Servicio](assets/cotizacion-de-servicio.png)

**Componentes del Documento** (según imagen de referencia):
- Encabezado con logo y datos de la empresa
- Información del cliente (RUC, dirección, contacto)
- Detalle de la solicitud y servicio
- Tabla de costos y cantidades
- Desglose financiero (Subtotal, FEE, IGV, Total)
- Condiciones comerciales (plazo, forma de pago, validez)
- Observaciones
- Firma del FM y datos de contacto

**Diferenciación por Tipo de Cliente**:
- **Cliente Externo**: Incluye campo "Margen FEE Contractual" de referencia
- **Cliente Interno**: Omite referencia a margen contractual

**Funcionalidades del Sistema para Generación del Documento**:

1. **Vista Previa**:
   - Botón "Vista Previa" que muestra el documento antes de generar
   - Permite al FM revisar el formato y contenido
   - No genera archivo, solo muestra visualización

2. **Generación de Excel**:
   - Botón "Generar Excel"
   - Sistema utiliza plantilla predefinida de Excel (configurada en Datos Maestros 10.15)
   - Rellena automáticamente todos los campos dinámicos
   - Aplica formato de celdas, bordes y estilos según plantilla
   - Genera archivo .xlsx descargable

3. **Almacenamiento Automático**:
   - El documento generado se almacena automáticamente en el sistema
   - Se vincula con el registro de cotización
   - Se mantiene versión del documento
   - Se registra en auditoría (fecha, hora, usuario que generó)

4. **Adjuntar al Correo**:
   - El documento Excel generado se adjunta automáticamente al correo de envío
   - El documento queda disponible para descarga en el Portal de Clientes

**Plantilla de Cotización (Datos Maestros)**:
- La plantilla debe configurarse en el **Módulo 10.15 - Plantillas de Documentos**
- Código de Plantilla: **COTIZ**
- Formato: Excel (.xlsx)
- Campos dinámicos marcados con [tags] que el sistema reemplaza automáticamente

**Validaciones de Generación**:
- Todos los campos obligatorios deben estar completos antes de generar
- El logo de la empresa debe estar configurado en Datos Maestros
- La plantilla debe estar activa en el sistema
- Los cálculos de FEE e IGV deben ser correctos

**Reglas de Negocio para Generación de Documentos**:
- **RN-15.11**: El documento solo puede generarse si todos los cálculos están completos
- **RN-15.12**: Cada vez que se genera un documento, se crea una nueva versión si hubo cambios
- **RN-15.13**: El documento Excel es la versión oficial para envío al cliente
- **RN-15.14**: Una vez generado y enviado, el documento queda bloqueado para edición
- **RN-15.15**: Una vez generado y enviado, el documento queda bloqueado para edición

**Auditoría de Generación de Documentos**:
- Fecha y hora de generación
- Usuario que generó el documento
- Versión del documento
- Descarga del documento (quién y cuándo)

### 15.5. Envío de Cotización a Clientes

#### 15.5.1. Preparación de Cotización para Envío

**Funcionalidad del Sistema**:

1. **FM revisa la cotización completa**:
   - Verifica todos los cálculos
   - Revisa descripción y alcance
   - Confirma montos y plazos

2. **Generación de Formato Especial (Obras Menores)**:
   - **Nota importante**: Para obras menores, FM brindará un formato especial en la LNT (Línea de Negocio Tercerizada)
   - Sistema debe permitir adjuntar documentos adicionales
   - Formatos predefinidos disponibles para descarga

3. **FM ejecuta acción "Enviar Cotización"**:
   - Sistema valida que todos los campos obligatorios estén completos
   - Sistema genera documento PDF de la cotización
   - Sistema registra fecha y hora de envío

#### 15.5.2. Envío Automático por Correo

**Funcionalidad del Sistema**:
- Sistema envía automáticamente correo electrónico a clientes con la cotización
- Destinatarios según tipo de cliente:
  - **Cliente Externo**: Correo registrado del representante del cliente
  - **Cliente Interno**: Correo del personal autorizado para aprobar cotizaciones

**Contenido del Correo**:

**Asunto**: "Cotización [Código de Cotización] - [Descripción del Servicio]"

**Cuerpo del Correo**:
```
Estimado(a) [Nombre del Cliente],

Por medio del presente, le hacemos llegar la cotización solicitada para el siguiente servicio:

Código de Cotización: [Código]
Descripción: [Descripción del Servicio]
Sede: [Nombre de la Sede]
Monto Total: [Moneda] [Monto Total]
Plazo de Ejecución: [Días] días calendario

Adjunto encontrará el documento completo de la cotización con el detalle y alcance del servicio.

Para aprobar la cotización, por favor ingrese al sistema a través del siguiente enlace:
[Enlace al Portal de Clientes]

Quedamos atentos a sus comentarios.

Atentamente,
[Nombre del FM]
Facility Manager
```

**Archivos Adjuntos**:
- PDF de la cotización formal
- Formato especial LNT (si aplica para obras menores)
- Documentos técnicos adicionales (si corresponde)

### 15.6. Proceso de Aprobación de Cotización

#### 15.6.1. Aprobación por Cliente Externo

**Proceso**:

1. **Cliente Externo accede al Portal de Clientes**:
   - Cliente recibe correo con enlace de acceso
   - Cliente ingresa al portal con sus credenciales
   - Sistema muestra la cotización pendiente de aprobación

2. **Revisión de Cotización**:
   - Cliente visualiza el detalle completo de la cotización
   - Puede descargar el PDF de la cotización
   - Puede revisar alcance, montos y plazos

3. **Cliente aprueba cotización en el sistema**:
   - Cliente hace clic en botón "Aprobar Cotización"
   - Sistema solicita confirmación de la aprobación
   - Sistema registra fecha, hora y usuario que aprobó

4. **Notificación Automática**:
   - Sistema envía notificación automática al FM
   - FM recibe correo informando que la cotización fue aprobada
   - Estado cambia a "Aprobada"

#### 15.6.2. Aprobación por Personal Autorizado (Cliente Interno)

**Proceso**:

1. **Personal Autorizado accede al sistema**:
   - Usuario con permisos de aprobación ingresa al sistema interno
   - Accede al módulo de aprobación de cotizaciones
   - Sistema muestra cotizaciones pendientes de aprobación

2. **Revisión de Cotización**:
   - Personal autorizado revisa la cotización internamente
   - Valida que esté dentro del presupuesto aprobado
   - Puede solicitar ajustes si es necesario

3. **Personal autorizado aprueba las cotizaciones en el sistema**:
   - Usuario hace clic en "Aprobar"
   - Sistema solicita confirmación
   - Opción de agregar comentarios de aprobación

4. **Notificación**:
   - Sistema notifica al FM de la aprobación
   - Estado cambia a "Aprobada"

**Roles con Permiso de Aprobación (Cliente Interno)**:
- Gerente General
- Gerente de FM
- Jefe de Área solicitante
- Controller (según monto)

### 15.7. Gestión de FEE Adicional y Solicitud de Orden de Compra (OC)

#### 15.7.1. Colocación de FEE Adicional (Paso 13 y 15)

**Funcionalidad**:

1. **FM coloca el FEE** (después de aprobación inicial):
   - En algunos casos, después de la aprobación, FM debe ajustar o confirmar el FEE final
   - Sistema muestra nuevamente el campo de margen de FEE contractual
   - FM confirma o ajusta el FEE para la emisión de OC

2. **Sistema muestra el campo de margen de FEE contractual**:
   - Campo de referencia con el margen establecido en el contrato
   - Validación automática de límites

3. **FM coloca el FEE final**:
   - FM ingresa el FEE definitivo
   - Sistema recalcula el monto total si hubo ajustes

4. **Sistema realiza el cálculo del FEE**:
   - Cálculo final con el FEE confirmado
   - Generación del monto definitivo para la OC

#### 15.7.2. Envío de Cotización para Emisión de Orden de Compra (OC)

**Proceso Final**:

1. **FM envía cotización solicitando emisión de OC**:
   - FM ejecuta acción "Solicitar Emisión de OC"
   - Sistema genera formato de cotización para OC
   - Incluye código de correlativo para OC

2. **Generación de Formato de Cotización por Proveedor**:
   - Sistema debe elaborar el formato de cotización por proveedor según formato predefinido
   - Incluye todos los detalles de la cotización aprobada
   - Monto final con FEE aplicado
   - Términos y condiciones

3. **Sistema envía solicitud al área de Compras/Procurement**:
   - Notificación automática al área de Compras
   - Adjunta cotización aprobada y formato para OC
   - Compras procede con la emisión de la Orden de Compra

4. **Trazabilidad**:
   - Sistema registra fecha de solicitud de OC
   - Estado cambia a "En Proceso de OC"
   - Se crea vínculo entre cotización y OC

### 15.8. Estados de la Cotización Formal

| Estado | Descripción | Acciones Disponibles |
|--------|-------------|----------------------|
| **Pendiente** | Cotización creada pero no elaborada | Elaborar, Editar, Eliminar |
| **En Elaboración** | FM está trabajando en la cotización | Editar, Guardar borrador, Enviar |
| **Enviada** | Cotización enviada al cliente | Ver, Enviar recordatorio, Cancelar |
| **Aprobada** | Cliente aprobó la cotización | Solicitar OC, Ver detalle |
| **Rechazada** | Cliente rechazó la cotización | Ver motivo, Renegociar, Cerrar |
| **En Proceso de OC** | Solicitud de OC enviada a Compras | Ver estado OC, Seguimiento |
| **OC Emitida** | Orden de Compra generada | Ver OC, Imprimir, Archivar |
| **Cancelada** | Cotización cancelada | Solo visualización |

### 15.9. Campos del Formulario de Cotización Formal

| Campo | Tipo | Obligatorio | Editable | Descripción |
|-------|------|-------------|----------|-------------|
| **Código de Cotización** | Texto (autogenerado) | Sí | No | Código único de cotización |
| **Código de Solicitud** | Texto (referencia) | Sí | No | Código de la solicitud original |
| **Cliente** | Lista desplegable | Sí | No | Cliente seleccionado |
| **Tipo de Cliente** | Lista | Sí | No | Interno / Externo |
| **Sede** | Lista desplegable | Sí | Sí | Sede del cliente |
| **Descripción del Servicio** | Texto largo | Sí | Sí | Detalle del servicio |
| **Alcance del Servicio** | Texto largo | Sí | Sí | Alcance incluido |
| **Proveedor Seleccionado** | Texto (referencia) | Sí | No | Proveedor cuya cotización se aprobó |
| **Monto Base Proveedor** | Número | Sí | No | Monto de cotización del proveedor |
| **Moneda** | Lista | Sí | Sí | S/. o $ |
| **% FEE** | Número | Sí | Sí | Porcentaje de FEE a aplicar |
| **Monto FEE** | Número (calculado) | Sí | No | Monto del FEE en moneda |
| **Margen FEE Contractual** | Número (referencia) | Condicional | No | Solo para clientes externos |
| **Subtotal** | Número (calculado) | Sí | No | Monto Base + FEE |
| **IGV (18%)** | Número (calculado) | Sí | No | Impuesto calculado |
| **Monto Total** | Número (calculado) | Sí | No | Monto final de cotización |
| **Plazo de Ejecución** | Número | Sí | Sí | Días calendario |
| **Observaciones** | Texto libre | No | Sí | Comentarios adicionales |
| **Estado** | Lista | Sí | No | Estado actual de la cotización |
| **Fecha de Creación** | Fecha/Hora | Sí | No | Fecha de creación |
| **Fecha de Envío** | Fecha/Hora | Condicional | No | Fecha de envío a cliente |
| **Fecha de Aprobación** | Fecha/Hora | Condicional | No | Fecha de aprobación por cliente |
| **Usuario que Aprobó** | Texto | Condicional | No | Usuario que aprobó (cliente) |
| **Código de OC** | Texto | Condicional | No | Código de Orden de Compra generada |

### 15.10. Notificaciones del Módulo

| Evento | Destinatarios | Medio | Tipo |
|--------|---------------|-------|------|
| Cotización elaborada | FM (confirmación) | Correo | Automático |
| Cotización enviada a cliente | Cliente (externo/interno) | Correo | Automático |
| Cotización aprobada | FM | Correo + Notificación interna | Automático |
| Cotización rechazada | FM | Correo + Notificación interna | Automático |
| Recordatorio de cotización pendiente | Cliente | Correo | Manual (FM) |
| Solicitud de OC enviada | Área de Compras | Correo + Notificación interna | Automático |
| OC emitida | FM + Cliente | Correo | Automático |

### 15.11. Validaciones del Módulo

- El monto total de la cotización debe ser mayor a 0
- Para clientes externos, el FEE no puede exceder el margen FEE contractual establecido
- Todos los campos obligatorios deben estar completos antes de enviar la cotización
- La cotización solo puede ser enviada si el FM tiene permisos suficientes
- No se puede editar una cotización después de ser aprobada por el cliente
- El porcentaje de IGV es parametrizable pero por defecto es 18%
- Para obras menores, es obligatorio adjuntar el formato especial LNT
- El plazo de ejecución debe ser coherente con el plazo ofrecido por el proveedor
- Si el FEE supera el 50% del monto base, se requiere justificación escrita

### 15.12. Reglas de Negocio del Módulo

- **RN-15.1**: El FM debe elaborar la cotización formal basándose en la cotización de proveedor aprobada
- **RN-15.2**: Para clientes externos, el sistema debe validar que el FEE no exceda el margen FEE contractual
- **RN-15.3**: Para clientes internos, el FEE es flexible pero requiere aprobación de Gerencia si supera el 50%
- **RN-15.4**: El sistema debe calcular automáticamente el FEE, subtotal, IGV y monto total
- **RN-15.5**: La cotización solo puede ser aprobada por el cliente o personal autorizado (según tipo de cliente)
- **RN-15.6**: Una vez aprobada la cotización, se debe generar la solicitud de OC automáticamente o manualmente según configuración
- **RN-15.7**: Para obras menores, es obligatorio utilizar el formato especial LNT
- **RN-15.8**: El sistema debe permitir el envío de recordatorios al cliente si no ha respondido en 3 días
- **RN-15.9**: Las cotizaciones aprobadas quedan bloqueadas y no pueden editarse sin autorización de Gerencia
- **RN-15.10**: El código de cotización debe seguir el formato: COT-[Año]-[Mes]-[Correlativo]

### 15.13. Formato Especial para Obras Menores (LNT)

**Descripción**:
Para servicios clasificados como "Obras Menores", el FM debe proporcionar un formato especial de cotización en la LNT (Línea de Negocio Tercerizada).

**Características del Formato LNT**:
- Plantilla predefinida en Excel o PDF
- Incluye campos específicos para obras menores
- Detalle de partidas y metrados
- Especificaciones técnicas
- Cronograma de ejecución
- Garantías y penalidades

**Funcionalidad del Sistema**:
- Sistema identifica automáticamente si el servicio es "Obra Menor"
- Alerta al FM que debe adjuntar formato LNT
- Validación obligatoria del archivo adjunto antes de envío
- Plantilla descargable desde el sistema

### 15.14. Integración con Módulo de Orden de Compra (OC)

**Flujo de Integración**:

1. **Cotización Aprobada** → Estado cambia a "Aprobada"
2. **FM solicita emisión de OC** → Sistema genera formato de cotización por proveedor
3. **Sistema envía solicitud a Compras** → Notificación automática con datos necesarios
4. **Compras emite OC** → Código de OC se registra en la cotización
5. **Vínculo Cotización-OC** → Trazabilidad completa del proceso

**Datos Transferidos a la OC**:
- Proveedor seleccionado
- Monto total aprobado
- Descripción y alcance del servicio
- Plazo de ejecución
- Términos de pago
- Contacto del proveedor

### 15.15. Auditoría del Módulo

El sistema debe registrar en auditoría:

- Fecha y hora de creación de cotización
- Usuario (FM) que creó la cotización
- Cambios realizados en la cotización (antes de envío)
- Fecha y hora de envío al cliente
- Fecha y hora de aprobación/rechazo
- Usuario (cliente) que aprobó o rechazó
- Motivo de rechazo (si aplica)
- Ajustes de FEE realizados
- Fecha de solicitud de OC
- Código de OC generada
- Notificaciones enviadas (destinatario, fecha, hora)
- Accesos al detalle de la cotización
- Descargas de documentos

### 15.16. Reportes del Módulo

**Reportes Disponibles**:

1. **Reporte de Cotizaciones por Estado**:
   - Filtrado por estado (Pendiente, Enviada, Aprobada, etc.)
   - Período de tiempo
   - Exportable a Excel

2. **Reporte de Cotizaciones por Cliente**:
   - Listado de todas las cotizaciones por cliente
   - Montos totales
   - Tasas de aprobación

3. **Reporte de FEE Aplicado**:
   - Comparativa de FEE por tipo de cliente
   - Promedio de FEE aplicado
   - Análisis de rentabilidad

4. **Reporte de Cotizaciones Pendientes**:
   - Cotizaciones sin respuesta del cliente
   - Días transcurridos desde envío
   - Alertas de seguimiento

5. **Reporte de Conversión a OC**:
   - Cotizaciones aprobadas vs OC emitidas
   - Tiempo promedio de conversión
   - Estado de OC

---

## 16. ENVIO DE INFORMACION PARA EMISION DE ORDEN DE COMPRA - COSTO

### 16.1. Objetivo del Módulo

Gestionar el flujo completo de solicitud y emisión de Órdenes de Compra (OC) desde FM hacia el área de Compras, asegurando la trazabilidad, validación y notificación de todos los documentos obligatorios requeridos para el proceso de compra. El sistema debe automatizar las notificaciones entre áreas y permitir el seguimiento en tiempo real del estado de cada OC.

### 16.2. Flujo del Proceso

#### 16.2.1. Inicio del Proceso

**Funcionalidad FM**: Sistema genera alerta automática

- **Trigger**: Service Desk genera Código de Engagement en SQLPED
- **Acción del Sistema**: FM detecta automáticamente la generación del engagement y notifica al Service Desk
- **Notificación**: Correo automático al Service Desk informando que se ha generado un engagement válido en SQLPED

#### 16.2.2. Validación de Datos y Documentos

**Funcionalidad FM**: Service Desk adjunta información e ingresa al sistema

1. **Captura de Datos**:
   - Código de Engagement SQLPED
   - Sustento de Ingresos y Gastos
   - Cotización debidamente aprobada por cliente y proveedor
   
2. **Validación del Sistema**:
   - Verifica que el código de engagement sea válido
   - Confirma que la cotización esté aprobada
   - Valida que todos los documentos obligatorios estén adjuntos

3. **Regla de Negocio**:
   - Si tiene engagement SQLPED → Monto límite: 50,000 o más soles (contenido legal)
   - Si NO tiene engagement SQLPED → Monto límite: 5000 a MÁS MM Y GOJO (solo Mantenimiento Mayor y Gastos Operativos de Obras)

**Notificación Simple** (no es funcionalidad FM directa):
- Sistema valida que el documento tenga los documentos obligatorios adjuntos
- **Acción**: Si NO están completos → Gateway de decisión: ¿Documentos obligatorios adjuntos?
  - **NO**: Genera alerta y envía notificación al Service Desk para completar documentos

#### 16.2.3. Envío de Documentos a Compras

**Funcionalidad FM**: Sistema envía documentos y notifica automáticamente

1. **Proceso de Envío**:
   - Sistema compila todos los documentos: Engagement, Cotización, Sustentos
   - Genera paquete de información completo
   - Adjunta enlace de ingreso al sistema para consulta

2. **Envío Automático**:
   - Sistema envía correo a Compras con:
     - Documentos adjuntos comprimidos
     - Enlace directo al sistema FM
     - Resumen de la solicitud (Monto, Proveedor, Plazo)

3. **Notificación**:
   - Compras recibe correo con alerta de nueva solicitud de OC
   - Notificación incluye prioridad según monto

#### 16.2.4. Generación de Orden de Compra

**Notificación Simple** (no es funcionalidad FM directa):
- Compras genera la OC en su sistema CSC
- FM recibe notificación de que la OC ha sido creada

**Funcionalidad FM**: Sistema registra y actualiza estado

1. **Registro de OC**:
   - Sistema muestra pantalla de consulta de estado
   - Compras comparte código de OC generado
   - Sistema actualiza estado de la solicitud: "OC Generada"

2. **Auditoría**:
   - Sistema registra:
     - Fecha y hora de generación de OC
     - Código de OC
     - Usuario de Compras que generó
     - Documentos asociados

#### 16.2.5. Selecciones CSC y Emisión Final

**Notificación Simple** (no es funcionalidad FM directa):
- Compras realiza selecciones internas en CSC (aprobaciones, revisiones)
- Genera las OC definitivas con todas las aprobaciones

**Funcionalidad FM**: Sistema recibe y procesa confirmación

1. **Recepción de OC Definitiva**:
   - Sistema solicita permiso para acceder a los archivos
   - Usuario autoriza acceso al sistema
   - Sistema descarga y almacena OC en formato PDF

2. **Validación de Formatos**:
   - Sistema valida que el archivo sea PDF
   - Verifica integridad del documento
   - Confirma que contenga código de OC válido

#### 16.2.6. Compra OC y Envío al Proveedor

**Funcionalidad FM**: Sistema emite OC y notifica

1. **Generación de Compra CSC**:
   - Sistema compara CSC, selecciona y emite la OC definitiva
   - Almacena OC en repositorio del sistema

2. **Emisión al Proveedor**:
   - Sistema envía OC como PdfService Chile
   - Notificación automática al proveedor vía correo
   - Enlace para descarga de OC
   - Confirmación de recepción requerida

#### 16.2.7. Notificación Final al Service Desk

**Funcionalidad FM**: Sistema notifica cierre del proceso

1. **Service Desk revisa la OC**:
   - Sistema notifica a Service Desk que OC ha sido enviada al proveedor
   - Service Desk puede consultar estado en tiempo real

2. **Cierre del Proceso**:
   - Sistema registra fecha y hora de envío al proveedor
   - Estado final: "OC Enviada a Proveedor"
   - Proceso completo registrado en auditoría

**Notificación Simple**:
- Sistema envía correo al proveedor confirmando envío de OC
- Requiere confirmación de recepción

### 16.3. Estados de la Orden de Compra

El sistema debe gestionar los siguientes estados:

1. **Engagement Generado**: SQLPED genera código de engagement
2. **Documentos en Validación**: Service Desk adjunta información
3. **Documentos Incompletos**: Falta documentación obligatoria (Alerta)
4. **Enviado a Compras**: Paquete completo enviado al área de Compras
5. **OC en Proceso**: Compras está generando la OC
6. **OC Generada**: Compras creó OC en CSC
7. **Selecciones CSC en Proceso**: Aprobaciones internas de Compras
8. **OC Definitiva Generada**: OC final con todas las aprobaciones
9. **OC Enviada a Proveedor**: Proveedor recibe OC vía PdfService
10. **Proceso Finalizado**: Proveedor confirma recepción

### 16.4. Pantallas del Módulo

#### 16.4.1. Pantalla de Solicitud de OC

**Campos**:
- Código de Engagement SQLPED (obligatorio)
- Adjuntar Sustento de Ingresos y Gastos (obligatorio)
- Adjuntar Cotización Aprobada (obligatorio, archivo)
- Monto Total (calculado desde cotización)
- Proveedor Seleccionado (desde cotización)
- Observaciones (opcional)

**Validaciones**:
- Código de engagement debe existir en SQLPED
- Monto debe cumplir reglas según tenga o no engagement
- Cotización debe estar en estado "Aprobada por Cliente"
- Todos los documentos obligatorios deben estar adjuntos

**Botones**:
- Guardar como Borrador
- Enviar a Compras (solo si validaciones pasan)
- Cancelar

#### 16.4.2. Pantalla de Seguimiento de OC

**Información Mostrada**:
- Código de Solicitud (generado por FM)
- Código de Engagement SQLPED
- Estado Actual (con indicador visual)
- Fecha de Solicitud
- Monto Total
- Proveedor
- Cliente
- Código de OC (cuando Compras lo genere)
- Fecha de Emisión de OC
- Documentos Asociados (con opción de descarga)

**Filtros**:
- Por Estado
- Por Fecha
- Por Proveedor
- Por Cliente
- Por Rango de Monto

**Acciones Disponibles**:
- Ver Detalle
- Descargar OC (cuando esté disponible)
- Ver Auditoría
- Imprimir Resumen

#### 16.4.3. Pantalla de Registro de OC (Compras)

**Campos** (solo accesible para rol Compras):
- Código de Solicitud FM (solo lectura)
- Código de OC CSC (obligatorio)
- Fecha de Generación (automática)
- Observaciones de Compras (opcional)
- Adjuntar OC Definitiva PDF (obligatorio)

**Validaciones**:
- Código de OC debe ser único
- Archivo debe ser formato PDF
- Tamaño máximo: 10 MB

**Botones**:
- Registrar OC
- Cancelar

### 16.5. Notificaciones Automáticas

#### 16.5.1. Notificación: Engagement Generado
- **Destinatarios**: Service Desk FM
- **Trigger**: Sistema detecta nuevo engagement en SQLPED
- **Contenido**:
  - Código de Engagement
  - Fecha de Generación
  - Enlace al sistema para adjuntar documentos

#### 16.5.2. Notificación: Documentos Incompletos
- **Destinatarios**: Service Desk FM
- **Trigger**: Validación detecta falta de documentos
- **Contenido**:
  - Lista de documentos faltantes
  - Enlace para completar información
  - Alerta de urgencia

#### 16.5.3. Notificación: Solicitud Enviada a Compras
- **Destinatarios**: Área de Compras
- **Trigger**: Service Desk envía solicitud completa
- **Contenido**:
  - Código de Solicitud
  - Resumen de la solicitud (Proveedor, Monto, Cliente)
  - Documentos adjuntos (ZIP)
  - Enlace al sistema FM
  - Plazo sugerido de respuesta

#### 16.5.4. Notificación: OC Generada
- **Destinatarios**: Service Desk FM, Gerente FM
- **Trigger**: Compras registra código de OC
- **Contenido**:
  - Código de OC CSC
  - Código de Solicitud FM
  - Fecha de Generación
  - Enlace para consulta

#### 16.5.5. Notificación: OC Enviada a Proveedor
- **Destinatarios**: Proveedor, Service Desk FM
- **Trigger**: Sistema envía OC definitiva
- **Contenido** (Proveedor):
  - OC en formato PDF
  - Código de OC
  - Instrucciones de confirmación
  - Enlace para descargar
  - Datos de contacto FM

**Contenido** (Service Desk):
  - Confirmación de envío
  - Proveedor destinatario
  - Fecha y hora de envío

### 16.6. Reglas de Negocio

#### 16.6.1. Montos y Engagements

1. **Con Engagement SQLPED**:
   - Monto mínimo: 50,000 soles
   - Requiere: Contenido legal obligatorio
   - Tipo: Compras de alto valor

2. **Sin Engagement SQLPED**:
   - Rango: 5,000 a MÁS soles
   - Solo aplica para: Mantenimiento Mayor (MM) y Gastos Operativos de Obras (GOJO)
   - Documentación simplificada

#### 16.6.2. Validación de Documentos Obligatorios

**Documentos Requeridos**:
1. Código de Engagement SQLPED válido (si aplica según monto)
2. Sustento de Ingresos y Gastos (obligatorio)
3. Cotización aprobada por cliente y proveedor (obligatorio)

**Regla**: Sistema NO permite envío a Compras si falta algún documento obligatorio

#### 16.6.3. Formatos Permitidos

- **Cotización**: PDF (máx. 10 MB)
- **Sustento de Ingresos y Gastos**: PDF, Excel (máx. 5 MB)
- **OC Definitiva**: Solo PDF (máx. 10 MB)

### 16.7. Integraciones

#### 16.7.1. Integración con SQLPED

**Tipo**: Lectura automática
**Frecuencia**: Tiempo real o cada 5 minutos
**Datos Obtenidos**:
- Código de Engagement
- Fecha de Generación
- Estado del Engagement
- Monto Asociado

**Acción del Sistema**:
- Detecta nuevo engagement
- Genera notificación automática
- Actualiza base de datos FM

#### 16.7.2. Integración con Sistema de Compras (CSC)

**Tipo**: Bidireccional
**Datos Enviados a CSC**:
- Código de Solicitud FM
- Proveedor
- Monto Total
- Documentos (ZIP)
- Plazo Sugerido

**Datos Recibidos desde CSC**:
- Código de OC
- Estado de OC
- Fecha de Generación
- OC Definitiva (PDF)

#### 16.7.3. Integración con PdfService Chile

**Tipo**: Envío de documentos
**Uso**: Emisión de OC al proveedor
**Funcionalidad**:
- Envío seguro de PDF
- Confirmación de entrega
- Registro de trazabilidad

### 16.8. Permisos por Rol

| Rol | Ver Solicitudes | Crear Solicitud | Registrar OC | Enviar a Proveedor | Ver Auditoría |
|-----|----------------|-----------------|--------------|-------------------|---------------|
| Gerente General | Sí | No | No | No | Sí |
| Gerente FM | Sí | No | No | Sí | Sí |
| Service Desk FM | Sí | Sí | No | No | No |
| Compras | Sí | No | Sí | No | No |
| Proveedor | Solo sus OC | No | No | No | No |

### 16.9. Auditoría del Módulo

El sistema debe registrar:

1. **Creación de Solicitud**:
   - Usuario que creó
   - Fecha y hora
   - Documentos adjuntos
   - Monto solicitado

2. **Validaciones**:
   - Resultado de cada validación
   - Documentos faltantes detectados
   - Intentos de envío rechazados

3. **Envío a Compras**:
   - Fecha y hora de envío
   - Usuario que envió
   - Destinatarios de la notificación
   - Documentos incluidos

4. **Registro de OC**:
   - Usuario de Compras que registró
   - Código de OC CSC
   - Fecha de registro
   - Archivo PDF adjunto

5. **Envío a Proveedor**:
   - Fecha y hora de envío
   - Proveedor destinatario
   - Confirmación de recepción
   - Método de envío (PdfService)

6. **Cambios de Estado**:
   - Cada cambio de estado con timestamp
   - Usuario responsable del cambio
   - Estado anterior y nuevo estado

### 16.10. Reportes del Módulo

#### 16.10.1. Reporte de Solicitudes de OC

**Filtros**:
- Período (fecha inicio - fecha fin)
- Estado
- Proveedor
- Cliente
- Rango de Monto

**Datos Mostrados**:
- Código de Solicitud
- Código de Engagement
- Fecha de Solicitud
- Proveedor
- Cliente
- Monto
- Estado Actual
- Código de OC (si existe)
- Días en proceso

**Exportable a**: Excel, PDF

#### 16.10.2. Reporte de Tiempo de Proceso

**Análisis**:
- Tiempo promedio desde solicitud hasta OC generada
- Tiempo promedio desde OC generada hasta envío a proveedor
- Identificación de cuellos de botella

**Datos Mostrados**:
- Código de Solicitud
- Fecha de Solicitud
- Fecha de Generación de OC
- Fecha de Envío a Proveedor
- Días en cada etapa
- Tiempo total del proceso

**Gráficos**:
- Diagrama de barras por etapa
- Tendencia mensual de tiempos

#### 16.10.3. Reporte de OC por Proveedor

**Filtros**:
- Proveedor
- Período
- Estado

**Datos Mostrados**:
- Proveedor
- Cantidad de OC emitidas
- Monto total
- Promedio por OC
- Estado de cada OC

**Exportable a**: Excel, PDF

#### 16.10.4. Reporte de Documentos Faltantes

**Objetivo**: Identificar solicitudes con documentación incompleta

**Datos Mostrados**:
- Código de Solicitud
- Fecha de Creación
- Documentos Faltantes
- Responsable (Service Desk)
- Días pendiente
- Estado

**Acción**: Permite enviar recordatorio masivo

### 16.11. Alertas del Sistema

#### 16.11.1. Alerta: Nuevo Engagement Detectado
- **Tipo**: Notificación automática
- **Destinatario**: Service Desk FM
- **Urgencia**: Normal
- **Acción Requerida**: Adjuntar documentos obligatorios

#### 16.11.2. Alerta: Documentos Incompletos
- **Tipo**: Advertencia
- **Destinatario**: Service Desk FM
- **Urgencia**: Alta
- **Acción Requerida**: Completar documentación

#### 16.11.3. Alerta: Solicitud Pendiente en Compras
- **Tipo**: Recordatorio
- **Destinatario**: Área de Compras
- **Frecuencia**: Cada 2 días si no hay avance
- **Acción Requerida**: Generar OC

#### 16.11.4. Alerta: OC Sin Enviar a Proveedor
- **Tipo**: Recordatorio
- **Destinatario**: Gerente FM
- **Frecuencia**: Si pasan más de 3 días desde generación de OC
- **Acción Requerida**: Autorizar envío a proveedor

### 16.12. Validaciones Adicionales

1. **Código de Engagement**:
   - Debe existir en sistema SQLPED
   - Debe estar activo
   - No debe estar asociado a otra solicitud de OC

2. **Cotización**:
   - Debe estar en estado "Aprobada"
   - Debe tener proveedor seleccionado
   - Monto debe coincidir con el sustento

3. **Monto vs Engagement**:
   - Si monto ≥ 50,000 → Debe tener engagement SQLPED
   - Si monto < 50,000 y es MM o GOJO → Puede NO tener engagement
   - Si no cumple reglas → Sistema rechaza

4. **Documentos**:
   - Tamaño máximo por archivo: 10 MB
   - Formatos permitidos según tipo de documento
   - No se permiten documentos corruptos o ilegibles

### 16.13. Consideraciones Técnicas

1. **Almacenamiento de Documentos**:
   - Documentos deben almacenarse en repositorio seguro
   - Backup automático diario
   - Retención mínima: 7 años

2. **Seguridad**:
   - Encriptación de documentos sensibles
   - Control de acceso por rol
   - Registro de todos los accesos a documentos

3. **Performance**:
   - Carga de documentos: máximo 30 segundos por archivo
   - Consulta de estado: tiempo de respuesta < 2 segundos
   - Generación de reportes: máximo 1 minuto

4. **Disponibilidad**:
   - Sistema debe estar disponible 24/7
   - Mantenimientos programados fuera de horario laboral
   - Notificación previa de mantenimientos

---

## 17. EMISION DE ORDEN DE COMPRA PARA GASTOS

### 17.1. Objetivo del Módulo

Gestionar el proceso completo de emisión de Órdenes de Compra (OC) para gastos operativos, garantizando la trazabilidad desde la generación del engagement en SQLPED hasta la notificación al proveedor y el registro del parte de ingresos. El sistema debe automatizar validaciones, notificaciones y el flujo de información entre Service Desk, FM, Compras CSC y Proveedores.

### 17.2. Flujo del Proceso

#### 17.2.1. Generación de Engagement en SQLPED

**Funcionalidad FM**: Sistema detecta y registra engagement

**Proceso**:

1. **Service Desk genera Código de Engagement en SQLPED**:
   - Service Desk emite el código de engagement en el sistema SQLPED
   - Sistema SQLPED valida y genera código único
   - Engagement queda registrado con sus datos asociados

2. **Sistema FM detecta nuevo Engagement**:
   - Sistema FM monitorea automáticamente SQLPED
   - Detecta nuevo engagement generado
   - Registra automáticamente en base de datos FM

3. **Notificación Automática**:
   - Sistema genera notificación automática al Service Desk
   - Correo confirmando que el engagement fue detectado por FM
   - Se habilita el proceso de carga de documentos

**Datos Capturados del Engagement**:
- Código de Engagement SQLPED
- Fecha de generación
- Monto asociado
- Tipo de servicio
- Estado del engagement

#### 17.2.2. Validación de Documentos Obligatorios

**Funcionalidad FM**: Service Desk adjunta documentación y FM valida

**Proceso**:

1. **Service Desk adjunta información al sistema**:
   - Código de Engagement SQLPED (obligatorio)
   - Sustento de Ingresos y Gastos (obligatorio)
   - Cotización aprobada por cliente y proveedor (obligatorio)

2. **FM valida la documentación**:
   - Sistema presenta lista de documentos obligatorios
   - FM revisa cada documento adjuntado
   - Verifica que la información sea correcta y completa
   - Valida que los documentos correspondan al engagement

3. **Validación del Sistema**:
   - Código de engagement debe existir en SQLPED
   - Todos los documentos obligatorios deben estar adjuntos
   - Formatos de archivos deben ser válidos (PDF, Excel según tipo)
   - Cotización debe estar en estado "Aprobada"

4. **Gateway de Decisión: ¿Documentos obligatorios adjuntos?**:
   - **SÍ**: Sistema permite continuar al siguiente paso
   - **NO**: Sistema genera alerta y notifica a Service Desk
     - Detalla qué documentos faltan
     - Bloquea el avance hasta completar documentación
     - Envía correo de recordatorio

**Reglas de Validación**:
- Documentos en formato PDF (máximo 10 MB por archivo)
- Sustento de Ingresos debe coincidir con monto de engagement
- Cotización debe tener firmas de aprobación (cliente y proveedor)
- Documentos no deben tener más de 30 días de antigüedad

#### 17.2.3. Aprobaciones Respectivas

**Funcionalidad FM**: Sistema gestiona aprobaciones internas

**Proceso**:

1. **FM realiza aprobaciones con sus respectivas validaciones**:
   - FM revisa el paquete completo de documentos
   - Valida montos, plazos y condiciones
   - Verifica coherencia entre documentos
   - Aprueba o solicita correcciones

2. **Niveles de Aprobación** (según monto):
   - **Monto < 50,000**: Aprobación de FM
   - **Monto ≥ 50,000**: Aprobación de FM + Gerente FM
   - **Monto ≥ 100,000**: FM + Gerente FM + Gerente General

3. **Sistema registra aprobaciones**:
   - Fecha y hora de cada aprobación
   - Usuario aprobador
   - Observaciones o comentarios
   - Nivel de aprobación cumplido

4. **Notificación de Aprobaciones**:
   - Sistema notifica a cada aprobador en cadena
   - Envío automático a siguiente nivel tras cada aprobación
   - Alerta si aprobación está pendiente más de 24 horas

#### 17.2.4. Envío de Datos a Compras CSC

**Funcionalidad FM**: Sistema compila y envía información a Compras

**Proceso**:

1. **FM envía la información (data) a Compras CSC**:
   - Sistema compila todos los documentos aprobados
   - Genera paquete de información completo
   - Incluye resumen ejecutivo de la solicitud

2. **Información Enviada a Compras**:
   - Código de Engagement SQLPED
   - Documentos obligatorios (Sustento, Cotización)
   - Resumen de aprobaciones obtenidas
   - Monto total autorizado
   - Proveedor seleccionado
   - Plazo de ejecución
   - Observaciones de FM

3. **Envío Automático**:
   - Sistema envía correo a Compras CSC con:
     - Documentos adjuntos (ZIP comprimido)
     - Enlace al sistema FM para consulta
     - Datos de contacto de FM
     - Prioridad según monto y urgencia

4. **Notificación al Sistema**:
   - Sistema notifica a FM confirmación de envío
   - Estado cambia a "Enviado a Compras"
   - Se registra fecha y hora de envío

#### 17.2.5. Compras Sube la OC al Sistema

**Funcionalidad FM**: Compras CSC genera OC y la registra en FM, con validación especial para Venta Empresa

**Proceso General**:

1. **Compras CSC genera la Orden de Compra**:
   - Compras recibe la información de FM
   - Genera OC en su sistema CSC
   - OC incluye código único CSC

2. **Compras CSC sube la OC al sistema FM**:
   - Compras accede al módulo de registro de OC en FM
   - Ingresa código de OC CSC
   - Adjunta archivo PDF de la OC definitiva
   - Registra fecha de emisión

3. **Validación del Sistema FM**:
   - Verifica que el archivo sea formato PDF
   - Valida que el código de OC sea único
   - Confirma que contenga firma digital o sello de Compras
   - Tamaño máximo: 10 MB

4. **Sistema almacena la OC**:
   - OC se guarda en repositorio del sistema
   - Se vincula automáticamente con el engagement correspondiente
   - Estado cambia a "OC Generada"

---

#### 17.2.5.1. Validación Especial: Venta Empresa

**Funcionalidad FM**: Sistema detecta y valida automáticamente cotizaciones de empresas proveedoras registradas

**Descripción**:
El sistema debe procesar automáticamente las cotizaciones recibidas por correo electrónico de empresas proveedoras registradas en el módulo de Venta Empresa, validando la información, autorizando compras dentro de límites establecidos y gestionando aprobaciones cuando se excedan los montos permitidos.

**Empresas de Venta Empresa**:
- El sistema permite configurar múltiples empresas proveedoras
- Ejemplos: Sodimac, Promart, Maestro, Cassinelli, etc.
- Lista configurable desde el módulo de Datos Maestros

**Proceso de Validación**:

##### 1. Detección Automática de Correos de Venta Empresa

**Funcionalidad**:
- Sistema monitorea bandeja de entrada de correos FM
- Detecta correos de empresas Venta Empresa registradas
- Valida asunto del correo con palabra clave: **"Atención"**

**Criterios de Detección**:
- **Remitente**: Debe ser dominio de correo de empresa registrada en el sistema
- **Asunto**: Debe contener la palabra clave configurada (por defecto: **"Atención"**)
- **Formato**: Correo debe tener estructura de cotización estándar según plantilla configurada

**Acción del Sistema**:
- Si detecta correo válido → Inicia proceso de extracción de datos
- Si no cumple criterios → Correo se trata como correspondencia normal

##### 2. Extracción Automática de Información del Correo

**Funcionalidad**: Sistema extrae automáticamente la siguiente información del correo

**Datos Extraídos**:

1. **Número de Cotización**:
   - Formato configurable según empresa proveedora
   - Ejemplos: VE-XXXXXX (Promart), X-XXXXXXX-X (Sodimac), COT-XXXXX (otros)
   - Sistema detecta formato automáticamente según patrón configurado
   - Campo obligatorio para identificación única

2. **Venta Empresa Emisora**:
   - Sistema identifica automáticamente la empresa proveedora
   - Se determina por dominio del remitente configurado en el sistema
   - También puede identificarse por logo, footer o firma del correo

3. **Sucursal de Venta Empresa**:
   - Ubicación de la tienda/sucursal/sede del proveedor
   - Dato obtenido del campo "Local", "Sucursal", "Tienda" o "Despacho" en cotización
   - Campo configurable según formato de cada empresa

4. **Persona Encargada de Gestionar la Compra**:
   - Nombre completo del usuario técnico FM
   - Ejemplo: YAMIL ADRIAN PIERRE CUBAS JIMENEZ, ARTURO MIRO ROJAS RUIZ
   - Campo: "Persona encargada" o "DNI de encargado"

5. **Descripción de los Items**:
   - Tabla completa con:
     - SKU / Código de Producto
     - Descripción del producto
     - Cantidad
     - Precio Unitario Neto
     - Total por Item
   - Sistema captura cada línea de la tabla de productos

6. **Monto Total (incluido IGV)**:
   - Monto total de la cotización con IGV incluido
   - Formato: S/ XXX.XX o $ XXX.XX según moneda
   - Campo: "TOTAL", "Monto Total" o "Total a Pagar" en la cotización

7. **Usuario FM Destinatario del Correo**:
   - Usuario FM al cual va dirigido el correo
   - Opciones: Victor, Ana, Marco (u otros FM registrados)
   - Sistema identifica por campo "Para:" o "Generado por:"

**Validaciones de Extracción**:
- Todos los campos obligatorios deben ser extraídos correctamente
- Si falta información crítica → Sistema genera alerta y solicita revisión manual
- Monto debe ser numérico y mayor a 0
- Número de cotización debe ser único (no duplicado en sistema)

##### 3. Validación de Persona Encargada y Monto

**Funcionalidad**: Sistema valida dos campos críticos antes de aprobar

**Campo 1: Validación de Persona Encargada**

1. **Sistema verifica si la persona encargada está registrada**:
   - Consulta base de datos de usuarios técnicos FM registrados
   - Compara nombre completo o DNI con lista de usuarios autorizados

2. **Resultado de Validación**:
   - **PERSONA REGISTRADA**: Sistema continúa con validación de monto
   - **PERSONA NO REGISTRADA**: Sistema rechaza automáticamente y notifica:
     - Al FM destinatario del correo
     - Motivo: "Persona encargada no está registrada en el sistema"
     - Acción requerida: Registrar usuario o solicitar cambio de responsable

**Campo 2: Validación de Monto por Comprar**

**Regla de Negocio**:
- **Límite autorizado**: S/. 200 por compra
- **Frecuencia**: Máximo 1 compra autorizada automáticamente al mes por FM para cada usuario técnico

**Proceso de Validación**:

1. **Si Monto ≤ S/. 200 Y usuario no ha excedido intentos del mes**:
   - Sistema aprueba automáticamente la compra
   - Envía correo de aprobación a Venta Empresa emisora
   - Registra compra en historial del usuario técnico
   - Estado: "Aprobada Automáticamente"
   - Descuenta 1 intento libre del mes para ese usuario

2. **Si Monto > S/. 200 O usuario ya excedió intentos del mes**:
   - Sistema NO aprueba automáticamente
   - Inicia proceso de aprobación manual
   - Notifica al validador FM correspondiente

**Condiciones de Rechazo Automático**:
- Monto supera S/. 200 en una sola compra
- Usuario técnico ya realizó su compra mensual autorizada
- Acumulado mensual del usuario supera el límite configurado

##### 4. Proceso de Aprobación Manual (cuando se exceden límites)

**Funcionalidad**: Sistema solicita aprobación del FM validador

**Proceso**:

1. **Sistema identifica que se requiere aprobación manual**:
   - Por monto superior a S/. 200
   - Por intentos libres agotados del usuario técnico

2. **Sistema notifica al validador FM correspondiente**:
   
   **Notificación mediante Llamada Automática** (opcional según configuración):
   - Sistema realiza llamada automática al FM aprobador
   - Mensaje de voz: "Tiene una solicitud de aprobación de Venta Empresa pendiente"
   - Informa: Número de cotización, monto, usuario solicitante

   **Notificación por WhatsApp**:
   - Sistema envía mensaje de WhatsApp al usuario FM aprobador
   - **Contenido del mensaje**:
   ```
   🔔 SOLICITUD DE APROBACIÓN - VENTA EMPRESA
   
   Cotización: [Nro Cotización]
   Empresa: [Sodimac/Promart]
   Sucursal: [Nombre Sucursal]
   Usuario Técnico: [Nombre Persona Encargada]
   Monto Total: S/ [Monto con IGV]
   
   Motivo de Aprobación:
   [X] Monto supera S/. 200
   [X] Usuario agotó intentos del mes
   
   Por favor, ingrese al sistema para aprobar o rechazar:
   [Enlace al Sistema]
   ```

   **Notificación en el Sistema**:
   - Alerta en panel del FM aprobador
   - Badge de notificación pendiente
   - Enlace directo a la solicitud

3. **FM aprobador ingresa al sistema**:
   - Accede al módulo de "Aprobaciones Venta Empresa"
   - Visualiza detalle completo de la cotización
   - Revisa:
     - Datos de la cotización (items, montos)
     - Historial del usuario técnico solicitante
     - Justificación de la compra (si fue cargada)
     - Documentos adjuntos

4. **FM aprobador toma decisión**:
   
   **Opción A: APROBAR**
   - FM hace clic en botón "Aprobar Venta Empresa"
   - Sistema solicita confirmación
   - Sistema registra aprobación con:
     - Fecha y hora
     - Usuario aprobador
     - Observaciones (opcional)
   - Sistema envía correo de aprobación a Venta Empresa emisora
   - Estado cambia a: "Aprobada por FM"
   
   **Opción B: RECHAZAR**
   - FM hace clic en botón "Rechazar"
   - Sistema solicita motivo de rechazo (obligatorio)
   - Sistema registra rechazo
   - Sistema envía notificación al usuario técnico
   - Sistema envía correo a Venta Empresa cancelando solicitud
   - Estado cambia a: "Rechazada"

##### 5. Aprobación Automática (cuando cumple límites)

**Funcionalidad**: Sistema aprueba sin intervención manual

**Condiciones para Aprobación Automática**:
- Persona encargada está registrada en sistema ✓
- Monto ≤ S/. 200 ✓
- Usuario técnico NO ha agotado su intento mensual ✓

**Proceso**:

1. **Sistema valida todas las condiciones**:
   - Verifica persona encargada registrada
   - Confirma monto dentro de límite
   - Valida intentos disponibles del mes

2. **Sistema genera aprobación automática**:
   - Crea registro de aprobación
   - Marca como "Aprobada Automáticamente"
   - Descuenta intento mensual del usuario técnico

3. **Sistema envía correo de aprobación a Venta Empresa**:
   
   **Asunto**: "Aprobación de Cotización [Nro Cotización] - Panorama BPO"
   
   **Cuerpo del Correo**:
   ```
   Estimado equipo de [Nombre Empresa Proveedora],
   
   Por medio del presente, confirmamos la aprobación de la siguiente cotización:
   
   Número de Cotización: [Nro Cotización]
   Sucursal: [Nombre Sucursal]
   Persona Encargada: [Nombre Usuario Técnico]
   Monto Total: S/ [Monto con IGV]
   
   La compra ha sido aprobada automáticamente por el sistema.
   El usuario encargado procederá con la adquisición de los productos detallados.
   
   Detalle de Items:
   [Tabla con SKU, Descripción, Cantidad, Monto]
   
   Atentamente,
   Sistema FM - Panorama BPO
   ```

4. **Sistema notifica al usuario FM destinatario**:
   - Correo de confirmación de aprobación automática
   - Enlace para consultar la cotización aprobada
   - Recordatorio de límite mensual restante

##### 6. Adjuntar Correos al Código de Servicio

**Funcionalidad**: Sistema vincula correos con sustentos de ingresos y gastos

**Proceso**:

1. **Sistema identifica código de servicio asociado**:
   - Extrae código de servicio del sustento de ingresos y gastos
   - Busca código en base de datos de solicitudes activas

2. **Sistema adjunta correos de Venta Empresa**:
   - Correo original de cotización de la empresa proveedora
   - Correo de aprobación enviado por sistema
   - Cualquier correo adicional relacionado al asunto

3. **Sistema organiza adjuntos**:
   - Crea carpeta digital con código de servicio
   - Almacena todos los correos relacionados
   - Indexa por fecha y tipo de correo
   - Permite descarga en lote

4. **Trazabilidad**:
   - Sistema registra:
     - Fecha de adjunto
     - Usuario que realizó la vinculación
     - Tipo de documento (cotización, aprobación, etc.)
   - Historial disponible en auditoría

**Reglas de Adjuntos**:
- Correos se adjuntan en formato .eml o PDF
- Mantener formato original para evidencia
- Incluir todos los archivos adjuntos del correo (imágenes, PDFs)
- No permitir eliminación de correos adjuntos (solo lectura)

##### 7. Panel de Control de Venta Empresa

**Funcionalidad**: Dashboard para gestión de cotizaciones Venta Empresa

**Información Mostrada**:

**Resumen General**:
- Total de cotizaciones recibidas en el mes
- Total aprobadas automáticamente
- Total pendientes de aprobación
- Total rechazadas
- Monto acumulado del mes

**Por Usuario Técnico**:
- Nombre del usuario
- Intentos utilizados en el mes
- Intentos disponibles
- Monto acumulado de compras aprobadas
- Última compra realizada

**Lista de Cotizaciones**:
- Número de Cotización
- Fecha de Recepción
- Empresa Proveedora (nombre de la empresa)
- Usuario Técnico
- Monto
- Estado (Aprobada Automática, Pendiente, Aprobada Manual, Rechazada)
- FM Aprobador (si aplica)
- Acciones (Ver detalle, Aprobar, Rechazar)

**Filtros Disponibles**:
- Por Estado
- Por Empresa Proveedora (lista dinámica según empresas registradas)
- Por Usuario Técnico
- Por Rango de Fechas
- Por Rango de Monto
- Por FM Aprobador

##### 8. Configuración de Parámetros de Venta Empresa

**Funcionalidad**: Configuración de límites y reglas

**Parámetros Configurables**:

1. **Monto Límite para Aprobación Automática**:
   - Valor por defecto: S/. 200
   - Editable por Gerente FM
   - Aplica para todos los usuarios técnicos

2. **Intentos Mensuales por Usuario**:
   - Valor por defecto: 1 compra al mes
   - Editable por Gerente FM
   - Puede ser diferente por usuario o rol

3. **FM Aprobadores**:
   - Lista de FM autorizados para aprobar
   - Asignación de usuarios técnicos a cada FM aprobador
   - Configuración de métodos de notificación (correo, WhatsApp, llamada)

4. **Empresas de Venta Empresa**:
   - Lista de empresas proveedoras registradas (configurable)
   - Ejemplos: Sodimac, Promart, Maestro, Cassinelli, etc.
   - Dominios de correo autorizados por empresa
   - Palabras clave en asunto para detección
   - Formato de número de cotización por empresa
   - Campos personalizados según plantilla de cada empresa

5. **Usuarios Técnicos Registrados**:
   - Lista de personas autorizadas para solicitar compras
   - Nombre completo y DNI
   - FM aprobador asignado
   - Límites personalizados (si aplica)

**Pantalla de Configuración**:
- Accesible solo para Gerente FM y Administrador
- Cambios requieren confirmación
- Sistema registra historial de cambios de configuración
- Cambios aplican desde el día siguiente (o inmediatamente según configuración)

##### 9. Validaciones Adicionales para Venta Empresa

1. **Validación de Duplicados**:
   - Número de cotización debe ser único
   - Sistema rechaza si cotización ya fue procesada
   - Alerta si hay cotización similar en últimos 7 días

2. **Validación de Vigencia**:
   - Cotización no debe tener más de 30 días de antigüedad
   - Sistema verifica fecha de emisión en correo
   - Rechaza automáticamente si está vencida

3. **Validación de Formato de Correo**:
   - Correo debe tener estructura válida de cotización
   - Debe contener tabla de productos
   - Debe incluir monto total
   - Si falta información → Requiere revisión manual

4. **Validación de Moneda**:
   - Sistema acepta solo Soles (S/.)
   - Si cotización está en dólares → Solicita conversión manual
   - Tipo de cambio configurable en sistema

##### 10. Reportes de Venta Empresa

**Reporte 1: Compras por Usuario Técnico**
- Período seleccionable
- Total de compras por usuario
- Monto acumulado por usuario
- Comparativa mes a mes
- Exportable a Excel

**Reporte 2: Aprobaciones por FM**
- Cantidad de aprobaciones manuales por FM
- Tiempo promedio de aprobación
- Tasa de aprobación vs rechazo
- Exportable a Excel

**Reporte 3: Compras por Empresa Proveedora**
- Total de compras por cada empresa proveedora registrada
- Comparativa entre empresas (ej: Sodimac vs Promart vs Maestro)
- Sucursales más frecuentes por empresa
- Productos más solicitados por empresa
- Comparativa de montos por empresa
- Exportable a Excel

**Reporte 4: Tendencias Mensuales**
- Evolución de compras mes a mes
- Tendencia de montos
- Usuarios más activos
- Gráficos de tendencia

##### 11. Auditoría de Venta Empresa

El sistema debe registrar:

- Fecha y hora de recepción del correo
- Datos extraídos automáticamente
- Validaciones realizadas (persona encargada, monto)
- Resultado de validación (aprobada automática o requiere aprobación)
- Usuario FM aprobador (si aplica)
- Fecha y hora de aprobación/rechazo
- Motivo de rechazo (si aplica)
- Correo de aprobación enviado (fecha, destinatario)
- Correos adjuntados al código de servicio
- Cambios de configuración de parámetros
- Accesos al panel de Venta Empresa
- Descargas de reportes

#### 17.2.6. Sistema Notifica a FM

**Funcionalidad FM**: Notificación automática de OC generada

**Proceso**:

1. **Sistema detecta que OC ha sido cargada**:
   - Trigger automático al registrar OC en sistema
   - Sistema genera notificación inmediata

2. **El Sistema notifica a FM**:
   - Correo automático a FM con:
     - Código de OC CSC generado
     - Código de Engagement asociado
     - Monto de la OC
     - Proveedor
     - Enlace para descargar OC en PDF
     - Estado actual

3. **FM recibe notificación**:
   - FM puede visualizar la OC desde el sistema
   - Tiene acceso a descargar el PDF
   - Puede consultar detalles completos

4. **Registro de Notificación**:
   - Sistema registra fecha y hora de envío
   - Confirma lectura de correo
   - Registra accesos a la OC

#### 17.2.7. Envío de Documentación al Proveedor vía Email

**Funcionalidad FM**: Sistema envía OC al proveedor automáticamente

**Proceso**:

1. **Sistema prepara el envío al proveedor**:
   - Genera formato PDF de la OC
   - Compila documentos adicionales si corresponde
   - Prepara correo con plantilla predefinida

2. **Sistema envía la documentación vía email al proveedor**:
   - Correo automático al proveedor registrado
   - Adjunta OC en formato PDF
   - Incluye instrucciones de confirmación

**Contenido del Correo al Proveedor**:

**Asunto**: "Orden de Compra [Código OC] - [Nombre del Servicio]"

**Cuerpo del Correo**:
```
Estimado Proveedor,

Por medio del presente, le notificamos que se ha emitido la siguiente Orden de Compra:

Código de OC: [Código OC CSC]
Código de Engagement: [Código Engagement]
Descripción: [Descripción del Servicio]
Monto Total: [Moneda] [Monto]
Plazo de Ejecución: [Días] días calendario

Adjunto encontrará el documento oficial de la Orden de Compra.

Por favor, confirme la recepción de este correo y su aceptación de la OC ingresando al sistema a través del siguiente enlace:
[Enlace al Portal de Proveedores]

Quedamos atentos a su confirmación.

Atentamente,
Área de Compras
Panorama BPO
```

3. **Notificación de Envío**:
   - Sistema notifica a FM que OC fue enviada al proveedor
   - Registra fecha y hora de envío
   - Estado cambia a "OC Enviada a Proveedor"

#### 17.2.8. Sistema Envía Documentación al Proveedor en el Sistema

**Funcionalidad FM**: Portal de Proveedores recibe OC

**Proceso**:

1. **Sistema habilita OC en Portal de Proveedores**:
   - OC queda disponible en portal del proveedor
   - Proveedor accede con sus credenciales
   - Visualiza OC completa con todos los detalles

2. **Proveedor revisa la OC en el sistema**:
   - Descarga PDF de la OC
   - Revisa términos y condiciones
   - Consulta detalle del servicio solicitado

3. **Proveedor confirma recepción y aceptación**:
   - Proveedor hace clic en "Confirmar Recepción"
   - Sistema solicita confirmación de aceptación de términos
   - Proveedor ingresa observaciones (opcional)

4. **Sistema registra confirmación**:
   - Fecha y hora de confirmación del proveedor
   - Usuario del proveedor que confirmó
   - Estado cambia a "OC Confirmada por Proveedor"

5. **Notificación de Confirmación**:
   - Sistema notifica a FM que proveedor confirmó OC
   - Sistema notifica a Compras CSC
   - Se registra en auditoría

#### 17.2.9. Generación de Parte de Ingresos

**Funcionalidad FM**: Relación OC con Parte de Ingresos

**Proceso**:

1. **Sistema relaciona OC con Parte de Ingresos**:
   - Una vez confirmada la OC por el proveedor
   - Sistema genera automáticamente correlación: **OC = Parte de Ingresos**
   - Código de Parte de Ingresos se genera basado en código de OC

2. **Registro de Parte de Ingresos**:
   - Sistema crea registro de Parte de Ingresos
   - Vincula con OC correspondiente
   - Estado inicial: "Pendiente de Ingreso"

3. **Información del Parte de Ingresos**:
   - Código de OC CSC
   - Código de Parte de Ingresos (autogenerado)
   - Proveedor
   - Monto esperado
   - Fecha estimada de ingreso
   - Descripción de productos/servicios

4. **Notificación**:
   - Sistema notifica a Logística/Almacén
   - Notifica a FM sobre parte de ingreso generado
   - Queda en espera de recepción física

### 17.3. Estados de la Orden de Compra para Gastos

El sistema debe gestionar los siguientes estados:

1. **Engagement Detectado**: Sistema FM detectó engagement en SQLPED
2. **Documentos en Carga**: Service Desk está adjuntando documentación
3. **Documentos Incompletos**: Falta documentación obligatoria (Alerta)
4. **En Validación FM**: FM está revisando documentos
5. **En Proceso de Aprobación**: Esperando aprobaciones según nivel
6. **Aprobado**: Todas las aprobaciones obtenidas
7. **Enviado a Compras**: Información enviada a Compras CSC
8. **OC en Proceso CSC**: Compras está generando OC
9. **OC Generada**: Compras cargó OC en sistema FM
10. **OC Enviada a Proveedor**: OC enviada vía email y portal
11. **OC Confirmada por Proveedor**: Proveedor aceptó OC
12. **Parte de Ingresos Generado**: Sistema generó parte de ingresos
13. **Proceso Finalizado**: OC completada y cerrada

### 17.4. Pantallas del Módulo

#### 17.4.1. Pantalla de Registro de Engagement y Documentos

**Campos**:
- Código de Engagement SQLPED (obligatorio, validado con SQLPED)
- Fecha de Generación Engagement (solo lectura, automático)
- Monto del Engagement (solo lectura, automático desde SQLPED)
- Tipo de Servicio (lista desplegable)
- Adjuntar Sustento de Ingresos y Gastos (obligatorio, PDF/Excel)
- Adjuntar Cotización Aprobada (obligatorio, PDF)
- Proveedor (desde cotización, solo lectura)
- Observaciones (opcional, texto libre)

**Validaciones**:
- Código de engagement debe existir en SQLPED
- Documentos en formato PDF o Excel según tipo
- Tamaño máximo por archivo: 10 MB
- Cotización debe estar firmada y aprobada
- Monto sustento debe coincidir con monto engagement

**Botones**:
- Guardar como Borrador
- Enviar a Validación FM
- Cancelar

#### 17.4.2. Pantalla de Validación y Aprobación (FM)

**Información Mostrada**:
- Código de Engagement SQLPED
- Código de Solicitud FM (generado)
- Service Desk que cargó información
- Fecha de Carga
- Monto Total
- Proveedor
- Lista de Documentos Adjuntos (con vista previa)
- Estado Actual

**Acciones Disponibles**:
- Descargar Documentos
- Validar Documentos (marca como validados)
- Solicitar Correcciones (regresa a Service Desk)
- Aprobar (si FM tiene autoridad según monto)
- Enviar a Aprobación Superior (si monto requiere)
- Rechazar (con motivo obligatorio)

**Validaciones**:
- Todos los documentos deben estar validados antes de aprobar
- Observaciones obligatorias si se solicitan correcciones
- Motivo obligatorio si se rechaza

#### 17.4.3. Pantalla de Carga de OC (Compras CSC)

**Campos** (solo accesible para rol Compras):
- Código de Solicitud FM (solo lectura)
- Código de Engagement (solo lectura)
- Código de OC CSC (obligatorio, único)
- Fecha de Emisión OC (obligatorio)
- Adjuntar OC en PDF (obligatorio)
- Monto OC (obligatorio, debe coincidir con solicitud)
- Términos de Pago (lista desplegable)
- Plazo de Entrega (número de días)
- Observaciones de Compras (opcional)

**Validaciones**:
- Código de OC debe ser único en el sistema
- Archivo debe ser formato PDF
- Tamaño máximo: 10 MB
- Monto OC debe coincidir con monto aprobado (±2% tolerancia)
- Fecha de emisión no puede ser futura

**Botones**:
- Registrar OC
- Guardar Borrador
- Cancelar

#### 17.4.4. Pantalla de Seguimiento de OC

**Filtros**:
- Por Estado
- Por Fecha de Solicitud
- Por Proveedor
- Por Rango de Monto
- Por Código de Engagement
- Por Código de OC

**Información Mostrada** (tabla):
- Código de Solicitud FM
- Código de Engagement
- Código de OC CSC
- Estado Actual (con indicador de color)
- Fecha de Solicitud
- Fecha de OC Generada
- Proveedor
- Monto
- Días en Proceso
- Responsable Actual

**Acciones Disponibles**:
- Ver Detalle Completo
- Descargar OC (si existe)
- Descargar Documentos
- Ver Auditoría
- Imprimir Resumen
- Exportar a Excel

#### 17.4.5. Portal de Proveedores - Visualización de OC

**Información Mostrada** (vista proveedor):
- Código de OC
- Fecha de Emisión
- Monto Total
- Descripción del Servicio
- Plazo de Ejecución
- Términos de Pago
- Condiciones Especiales
- Contacto de Compras
- Documentos Adjuntos (OC en PDF)

**Acciones Disponibles**:
- Descargar OC en PDF
- Confirmar Recepción
- Aceptar Términos
- Agregar Observaciones
- Ver Historial de OC

**Validaciones**:
- Proveedor debe confirmar recepción en máximo 48 horas
- Sistema envía recordatorio si no confirma en 24 horas
- Aceptación de términos es obligatoria para continuar

### 17.5. Notificaciones Automáticas

#### 17.5.1. Notificación: Engagement Detectado
- **Destinatarios**: Service Desk FM
- **Trigger**: Sistema detecta nuevo engagement en SQLPED
- **Contenido**:
  - Código de Engagement
  - Monto asociado
  - Enlace para cargar documentos
  - Lista de documentos obligatorios

#### 17.5.2. Notificación: Documentos Incompletos
- **Destinatarios**: Service Desk FM
- **Trigger**: FM solicita correcciones o faltan documentos
- **Contenido**:
  - Código de Solicitud
  - Lista de documentos faltantes o con errores
  - Observaciones de FM
  - Enlace para completar

#### 17.5.3. Notificación: Aprobación Pendiente
- **Destinatarios**: Aprobadores (Gerente FM, Gerente General según nivel)
- **Trigger**: Solicitud enviada a aprobación
- **Contenido**:
  - Código de Solicitud
  - Monto a aprobar
  - Proveedor
  - Enlace para revisar y aprobar
  - Resumen de documentos

#### 17.5.4. Notificación: Solicitud Aprobada y Enviada a Compras
- **Destinatarios**: Área de Compras CSC
- **Trigger**: Solicitud aprobada y enviada
- **Contenido**:
  - Código de Solicitud FM
  - Código de Engagement
  - Proveedor
  - Monto autorizado
  - Documentos adjuntos (ZIP)
  - Enlace al sistema FM
  - Plazo sugerido de emisión de OC

#### 17.5.5. Notificación: OC Generada
- **Destinatarios**: FM, Service Desk, Gerente FM
- **Trigger**: Compras registra OC en sistema
- **Contenido**:
  - Código de OC CSC
  - Código de Solicitud FM
  - Código de Engagement
  - Fecha de Emisión
  - Monto OC
  - Enlace para descargar OC

#### 17.5.6. Notificación: OC Enviada a Proveedor
- **Destinatarios**: Proveedor
- **Trigger**: Sistema envía OC
- **Contenido**:
  - Código de OC
  - Monto
  - Descripción del servicio
  - OC en PDF adjunta
  - Enlace al portal de proveedores
  - Instrucciones de confirmación
  - Plazo para confirmar recepción

#### 17.5.7. Notificación: Proveedor Confirmó OC
- **Destinatarios**: FM, Compras CSC
- **Trigger**: Proveedor confirma recepción y aceptación
- **Contenido**:
  - Código de OC
  - Proveedor
  - Fecha y hora de confirmación
  - Observaciones del proveedor (si las hay)

#### 17.5.8. Notificación: Parte de Ingresos Generado
- **Destinatarios**: Logística/Almacén, FM
- **Trigger**: Sistema genera parte de ingresos
- **Contenido**:
  - Código de Parte de Ingresos
  - Código de OC asociado
  - Proveedor
  - Descripción de productos/servicios
  - Fecha estimada de ingreso
  - Enlace para registrar recepción

### 17.6. Reglas de Negocio

#### 17.6.1. Validación de Engagement

1. **Engagement Válido**:
   - Debe existir en sistema SQLPED
   - Debe estar activo
   - No debe estar asociado a otra solicitud de OC
   - Fecha de generación no mayor a 90 días

2. **Montos y Límites**:
   - Monto mínimo para generar OC: S/. 500
   - Monto máximo sin aprobación gerencial: S/. 50,000
   - Montos superiores requieren aprobaciones escalonadas

#### 17.6.2. Documentación Obligatoria

**Documentos Requeridos**:
1. Código de Engagement SQLPED válido
2. Sustento de Ingresos y Gastos actualizado (máximo 30 días)
3. Cotización aprobada por cliente y proveedor con firmas

**Regla**: Sistema NO permite avanzar sin documentación completa

#### 17.6.3. Aprobaciones Escalonadas

1. **Monto < S/. 50,000**:
   - Aprobación: FM
   - Tiempo máximo: 24 horas

2. **Monto S/. 50,000 - S/. 100,000**:
   - Aprobación: FM + Gerente FM
   - Tiempo máximo: 48 horas

3. **Monto > S/. 100,000**:
   - Aprobación: FM + Gerente FM + Gerente General
   - Tiempo máximo: 72 horas

**Regla**: Si se excede el tiempo, sistema envía escalamiento automático

#### 17.6.4. Confirmación de Proveedor

- Proveedor debe confirmar recepción en máximo 48 horas
- Sistema envía recordatorio a las 24 horas
- Si no confirma en 48 horas, sistema alerta a FM
- FM puede marcar como "Confirmada manualmente" con justificación

#### 17.6.5. Generación de Parte de Ingresos

- Sistema genera automáticamente parte de ingresos al confirmar OC
- Relación 1:1 entre OC y Parte de Ingresos
- Código de Parte de Ingresos formato: PI-[AñoMes]-[Correlativo]
- Parte de Ingresos queda pendiente hasta recepción física

#### 17.6.6. Formatos Permitidos

- **Sustento de Ingresos y Gastos**: PDF, Excel (máx. 5 MB)
- **Cotización**: PDF (máx. 10 MB)
- **OC Definitiva**: Solo PDF (máx. 10 MB)

### 17.7. Integraciones

#### 17.7.1. Integración con SQLPED

**Tipo**: Lectura automática en tiempo real

**Frecuencia**: Cada 5 minutos o en tiempo real (webhook)

**Datos Obtenidos**:
- Código de Engagement
- Fecha de Generación
- Monto Asociado
- Estado del Engagement
- Tipo de Servicio
- Cliente/Sede

**Acción del Sistema**:
- Detecta nuevo engagement
- Valida que no esté duplicado
- Genera notificación automática
- Actualiza base de datos FM
- Crea registro de solicitud inicial

#### 17.7.2. Integración con Sistema de Compras (CSC)

**Tipo**: Bidireccional

**FM → CSC** (envío de solicitudes):
- Código de Engagement
- Documentos obligatorios
- Aprobaciones obtenidas
- Datos del proveedor
- Monto autorizado

**CSC → FM** (respuesta con OC):
- Código de OC CSC
- Fecha de Emisión
- OC en formato PDF
- Estado de la OC
- Términos y condiciones

**Método de Integración**:
- API REST o SOAP
- Autenticación OAuth 2.0
- Notificaciones mediante webhooks
- Backup manual si API no disponible

#### 17.7.3. Integración con Portal de Proveedores

**Tipo**: Publicación automática

**Datos Publicados**:
- OC completa en PDF
- Términos y condiciones
- Instrucciones de confirmación
- Contactos de Compras

**Funcionalidades**:
- Descarga de OC
- Confirmación de recepción
- Aceptación de términos
- Carga de observaciones

### 17.8. Auditoría del Módulo

El sistema debe registrar en auditoría:

- Fecha y hora de detección de engagement
- Usuario (Service Desk) que cargó documentos
- Cambios en documentos adjuntos
- Usuario (FM) que validó documentos
- Aprobadores y fechas de cada aprobación
- Fecha de envío a Compras CSC
- Usuario (Compras) que cargó OC
- Fecha de envío de OC a proveedor
- Fecha y hora de confirmación del proveedor
- Generación de parte de ingresos
- Accesos a documentos (quién y cuándo)
- Descargas de OC (usuario, fecha, hora)
- Modificaciones de estado
- Notificaciones enviadas (destinatario, fecha, hora)

### 17.9. Reportes del Módulo

#### 17.9.1. Reporte de OC por Estado

**Filtros**:
- Estado
- Rango de Fechas
- Proveedor
- Rango de Monto

**Datos Mostrados**:
- Código de Solicitud FM
- Código de Engagement
- Código de OC CSC
- Estado Actual
- Proveedor
- Monto
- Días en Proceso
- Responsable Actual

**Exportable a**: Excel, PDF

#### 17.9.2. Reporte de Tiempo de Proceso

**Análisis**:
- Tiempo promedio desde engagement hasta OC generada
- Tiempo promedio desde OC generada hasta confirmación de proveedor
- Identificación de cuellos de botella por etapa

**Datos Mostrados**:
- Etapa del Proceso
- Tiempo Promedio
- Tiempo Mínimo
- Tiempo Máximo
- Cantidad de Casos
- Porcentaje del Total

**Gráficos**:
- Diagrama de barras por etapa
- Tendencia mensual de tiempos
- Comparativa por proveedor

#### 17.9.3. Reporte de Aprobaciones Pendientes

**Filtros**:
- Aprobador
- Rango de Montos
- Antigüedad (días pendientes)

**Datos Mostrados**:
- Código de Solicitud
- Fecha de Solicitud
- Monto
- Proveedor
- Aprobador Pendiente
- Días Pendiente
- Nivel de Urgencia

**Acciones**:
- Enviar recordatorio individual
- Enviar recordatorio masivo
- Escalar a superior

#### 17.9.4. Reporte de OC por Proveedor

**Filtros**:
- Proveedor
- Período
- Estado

**Datos Mostrados**:
- Proveedor
- Cantidad de OC emitidas
- Monto total
- Promedio por OC
- Tiempo promedio de confirmación
- Estado de cada OC

**Exportable a**: Excel, PDF

#### 17.9.5. Reporte de Partes de Ingresos Pendientes

**Objetivo**: Identificar partes de ingreso generados pero no recepcionados

**Datos Mostrados**:
- Código de Parte de Ingresos
- Código de OC Asociado
- Proveedor
- Fecha de Generación
- Días Pendiente
- Monto
- Estado

**Acciones**:
- Notificar a Logística
- Marcar como recepcionado
- Ver detalle

### 17.10. Alertas del Sistema

#### 17.10.1. Alerta: Nuevo Engagement Detectado
- **Tipo**: Notificación automática
- **Destinatario**: Service Desk FM
- **Urgencia**: Normal
- **Acción Requerida**: Cargar documentos obligatorios en 24 horas

#### 17.10.2. Alerta: Documentos Incompletos
- **Tipo**: Advertencia
- **Destinatario**: Service Desk FM
- **Urgencia**: Alta
- **Acción Requerida**: Completar documentación de inmediato

#### 17.10.3. Alerta: Aprobación Pendiente
- **Tipo**: Recordatorio
- **Destinatario**: Aprobador correspondiente
- **Frecuencia**: Diaria hasta que se apruebe
- **Acción Requerida**: Revisar y aprobar/rechazar

#### 17.10.4. Alerta: Tiempo de Aprobación Excedido
- **Tipo**: Escalamiento
- **Destinatario**: Superior del aprobador + Gerente FM
- **Trigger**: Se excedió tiempo máximo de aprobación
- **Acción Requerida**: Intervención inmediata

#### 17.10.5. Alerta: OC Generada
- **Tipo**: Información
- **Destinatario**: FM, Service Desk
- **Urgencia**: Normal
- **Acción Requerida**: Revisar OC generada

#### 17.10.6. Alerta: Proveedor No Confirmó OC
- **Tipo**: Advertencia
- **Destinatario**: FM
- **Trigger**: 24 horas sin confirmación de proveedor
- **Acción Requerida**: Contactar al proveedor

#### 17.10.7. Alerta: Parte de Ingresos Pendiente
- **Tipo**: Recordatorio
- **Destinatario**: Logística/Almacén, FM
- **Frecuencia**: Cada 3 días
- **Acción Requerida**: Recepcionar productos/servicios

### 17.11. Validaciones Adicionales

1. **Código de Engagement**:
   - Debe existir en sistema SQLPED
   - Debe estar activo
   - No debe estar asociado a otra solicitud
   - Antigüedad máxima: 90 días

2. **Sustento de Ingresos y Gastos**:
   - Formato PDF o Excel
   - Tamaño máximo: 5 MB
   - Fecha de elaboración no mayor a 30 días
   - Monto debe coincidir con engagement (±2% tolerancia)

3. **Cotización Aprobada**:
   - Debe estar en estado "Aprobada"
   - Debe contener firmas de cliente y proveedor
   - Formato PDF
   - Tamaño máximo: 10 MB
   - Vigencia no vencida

4. **OC Generada por Compras**:
   - Código único (no duplicado)
   - Formato PDF obligatorio
   - Monto debe coincidir con aprobado (±2% tolerancia)
   - Debe contener sello/firma de Compras
   - Tamaño máximo: 10 MB

5. **Confirmación de Proveedor**:
   - Debe realizarse dentro de 48 horas
   - Usuario del proveedor debe estar registrado
   - Aceptación de términos obligatoria

### 17.12. Consideraciones Técnicas

1. **Almacenamiento de Documentos**:
   - Repositorio seguro con backup automático
   - Versionado de documentos
   - Retención mínima: 7 años
   - Encriptación de archivos sensibles

2. **Seguridad**:
   - Autenticación de usuarios por rol
   - Control de acceso granular
   - Registro de todos los accesos
   - Auditoría completa de acciones

3. **Performance**:
   - Carga de documentos: máximo 30 segundos
   - Consulta de estado: tiempo de respuesta < 2 segundos
   - Generación de reportes: máximo 1 minuto
   - Notificaciones en tiempo real (< 5 segundos)

4. **Disponibilidad**:
   - Sistema disponible 24/7
   - Mantenimientos programados fuera de horario laboral
   - Notificación previa de mantenimientos (48 horas)
   - Plan de contingencia ante caídas

5. **Integraciones**:
   - Monitoreo de conexión con SQLPED cada 5 minutos
   - Reintentos automáticos en caso de fallo (3 intentos)
   - Alertas a TI si integración falla
   - Modo manual disponible si API no funciona

## 18. EJECUCIÓN DE TRABAJO / ENTREGA DEL BIEN

### 18.1. Objetivo del Módulo

Gestionar la ejecución de trabajos y entrega de bienes, desde la coordinación de fechas de inicio hasta el cierre final, controlando la documentación obligatoria según el tipo de trabajo, automatizando notificaciones y asegurando la trazabilidad completa del proceso.

### 18.2. Flujo del Proceso

#### 18.2.1. Coordinación y Solicitud de Documentos

1. **Supervisor de MTTO coordina fecha de inicio**: Revisa solicitud, contacta proveedor, valida disponibilidad cliente/sede
2. **Sistema determina documentos obligatorios** según tipo de trabajo (ver tabla en 18.2.2)
3. **Sistema envía mail al proveedor** con lista de documentos requeridos, plazo de entrega y enlace al portal

**Plazos de Entrega de Documentos**:
- **Trabajos Menores - Bajo Riesgo**: 2 días hábiles
- **Trabajos de Alto Riesgo Programados**: 2 días hábiles
- **Emergencia**: 4 horas

#### 18.2.2. Tabla de Documentos Obligatorios según Tipo de Trabajo

| N° | DOCUMENTO | REVISIÓN | TRABAJOS MENORES | ALTO RIESGO | EMERGENCIA |
|----|-----------|----------|------------------|-------------|------------|
| 1 | Relación de Personal | CONTRALOR | ✓ | ✓ | ✓ |
| 2 | Certificado de Homologación | CONTRALOR | ✓ | ✓ | ✓ |
| 3 | Constancia SCTR (Salud y Pensión) | CONTRALOR | ✓ | ✓ | ✓ |
| 4 | Certificado de Operatividad de Equipos | SST | - | ✓ | ✓ |
| 5 | Procedimiento de Trabajo Seguro | SST | - | ✓ | ✓ |
| 6 | Carnet SST Terceros | CONTRALOR | ✓ | ✓ | ✓ |
| 7 | CV Documento de Prevencionista de Riesgo | SST | - | ✓ | ✓ |
| 8 | Certificado de Aptitud Médico | SST | - | ✓ | - |
| 9 | Certificado de Capacitación Trabajo Alto Riesgo | SST | - | ✓ | - |
| 10 | Registro de Entrega EPPS | SST | - | ✓ | - |
| 11 | IPERC Específico | SST | ✓ | ✓ | ✓ |
| 12 | Plan de Emergencia | SST | ✓ | ✓ | ✓ |
| 13 | Competencia de Trabajadores - CV Certificados | SST | - | ✓ | - |
| 14 | Hojas de Seguridad - MSDS | SST | ✓ | ✓ | ✓ |
| 15 | Carta de Autorización de Corte de Energía | SST | - | ✓ | ✓ |

**Leyenda**: ✓ Obligatorio | - No requerido | CONTRALOR: Revisión Contraloría | SST: Revisión Seguridad y Salud

**Total documentos obligatorios**: Menores (7), Alto Riesgo (15), Emergencia (11)

#### 18.2.3. Proveedor Carga Documentación

1. Proveedor accede al portal y visualiza lista de documentos requeridos
2. Carga cada documento (formato PDF, máximo 10 MB)
3. Sistema valida formato, tamaño y vigencia (si aplica)
4. Sistema muestra progreso: "X de Y documentos cargados"
5. Proveedor confirma envío → Sistema notifica a Supervisor y SSDMA

#### 18.2.4. Supervisor y SSDMA Validan Documentación

1. **Supervisor revisa documentación**: Verifica completitud y vigencia
2. **SSDMA valida documentos SST**: Checklist de seguridad (charla, personal autorizado, EPPs, permisos especiales)
3. **Gateway de Decisión: ¿Es correcto?**
   - **SÍ**: Supervisor confirma fecha de inicio → Estado: "Fecha de Inicio Confirmada"
   - **NO**: SSDMA registra observaciones (Crítica/Media/Leve) → Proveedor debe subsanar

**Observaciones Críticas**: Bloquean inicio del servicio hasta subsanación

#### 18.2.5. Ejecución del Servicio

1. **Inicio de ejecución**: Sistema registra fecha/hora de inicio y activa contador de 48 horas
2. **Alertas progresivas de cierre**:
   - A las 24 horas: Primera alerta al Supervisor
   - A las 40 horas: Alerta de urgencia
   - A las 48 horas: Alerta crítica al Supervisor y Gerente FM

#### 18.2.6. Cierre del Servicio

1. **Proveedor carga documentación de cierre**:
   - Acta de Conformidad firmada por cliente
   - Orden de Trabajo cerrada
   - Evidencias fotográficas (mínimo 3)
   - Documentación geolocalizable (si aplica)
   - Certificados de Prueba/Garantía (si aplica)
2. **Supervisor valida documentación de cierre**: Revisa acta, valida alcance, aprueba o solicita correcciones
3. **Sistema cierra el ticket**: Estado final "Cerrado", genera reporte, archiva documentación

---

### 18.3. Flujo de Entrega del Bien

#### 18.3.1. Vía Email

1. Service Desk coordina fecha de entrega con proveedor
2. Proveedor envía información para ingreso (guía de remisión, factura, certificados)
3. Service Desk valida documentación de ingreso
4. **Gateway: ¿Es correcto?**
   - **SÍ**: Service Desk genera PI (Parte de Ingreso) y lo envía al almacén
   - **NO**: Proveedor debe corregir documentación
5. Almacén recepciona bien con PI

#### 18.3.2. Vía Puesta a Calle (CC - Centro de Costo/Cliente)

1. Supervisor coordina fecha de ejecución con cliente
2. Proveedor ejecuta servicio (instalación/puesta en marcha)
3. Sistema alerta plazo de 48 horas para cierre
4. Cliente comunica aprobación
5. Supervisor registra fecha de cierre y adjunta documentación
6. Sistema cierra el ticket

---

### 18.4. Estados del Servicio en Ejecución

1. **Coordinación de Inicio** | 2. **Documentación Solicitada** | 3. **Documentación en Carga** | 4. **Documentación en Revisión** | 5. **Documentación Observada** | 6. **Documentación Aprobada** | 7. **Fecha de Inicio Confirmada** | 8. **En Ejecución** | 9. **Pendiente de Cierre** | 10. **Alerta 48 Horas** | 11. **Documentación de Cierre en Revisión** | 12. **Aprobado por Cliente** | 13. **Cerrado** | 14. **Entrega Programada** (bienes) | 15. **En Tránsito** (bienes) | 16. **Recibido en Almacén** (bienes)

---

### 18.5. Pantallas del Módulo

#### 18.5.1. Pantalla de Coordinación de Inicio
- Campos: Código Servicio, Proveedor, Tipo de Trabajo, Fecha/Hora Estimada, Personal Asignado, Equipos, Observaciones
- Botones: Solicitar Documentación, Guardar Coordinación

#### 18.5.2. Portal de Proveedores - Carga de Documentos
- Información: Código Servicio, Tipo de Trabajo, Plazo de Entrega, Progreso (X de Y documentos)
- Formulario: Tipo de Documento, Adjuntar Archivo (PDF, 10 MB máx.), Fecha Vencimiento, Observaciones
- Validación: Solo PDF, tamaño máximo, fechas vigentes
- Botones: Cargar Documento, Enviar Documentación Completa

#### 18.5.3. Pantalla de Gestión de Documentos (Supervisor/SSDMA)
- Tabla: N°, Documento, Responsable Revisión, Estado (Pendiente/Cargado/Aprobado/Observado), Fecha Carga, Vencimiento, Acciones
- Filtros: Por Estado, Por Responsable (CONTRALOR/SST)
- Botones: Aprobar Todos, Enviar Observaciones

#### 18.5.4. Pantalla de Revisión SSDMA
- Checklist SST: Charla Seguridad, Personal Autorizado, EPPs Verificados, Permisos Especiales, Documentación Vigente
- Observaciones: Tipo (Crítica/Media/Leve), Descripción, Documentos Afectados, Acción Correctiva, Plazo, Evidencia Fotográfica
- Botones: Aprobar Documentación SST, Registrar Observación, Rechazar

#### 18.5.5. Pantalla de Seguimiento de Ejecución
- Información: Código, Estado Actual, Proveedor, Fechas (Inicio/Cierre Programada), Tiempo Transcurrido/Restante
- Timeline: Coordinación → Solicitud Docs → Carga → Aprobación → Inicio Ejecución → Cierre
- Acciones: Confirmar Inicio, Registrar Avance, Adjuntar Evidencias, Cargar Acta Conformidad, Cerrar Servicio

#### 18.5.6. Pantalla de Cierre de Servicio
- Documentación obligatoria: Acta Conformidad, OT Cerrada, Evidencias Fotográficas (mín. 3), Documentación Geolocalizable, Certificados
- Conformidad Cliente: ¿Dio conformidad? (Sí/No), Nombre Cliente, Observaciones
- Evaluación: Calidad, Cumplimiento Plazo, Atención Proveedor (1-5 estrellas)
- Botones: Cerrar Servicio, Guardar Borrador, Solicitar Correcciones

#### 18.5.7. Pantalla de Gestión de Entrega de Bienes
- Coordinación: Fecha/Hora Entrega, Punto Entrega, Responsable Recepción, Observaciones
- Documentos Ingreso: Guía Remisión, Factura, Certificados, Ficha Técnica, Garantía
- Parte de Ingreso: Generar PI, N° PI (autogenerado), Adjuntar al Expediente
- Botones: Confirmar Entrega, Generar PI, Notificar Almacén

---

### 18.6. Reglas de Negocio

1. **Documentación Obligatoria**: Sistema NO permite confirmar fecha de inicio sin documentación completa y aprobada según tipo de trabajo
2. **Vigencia de Documentos**: SCTR vigente durante ejecución; homologación activa; certificados de equipos y médicos no vencidos
3. **Observaciones Críticas**: Bloquean inicio; Medias permiten inicio con compromiso; Leves se subsanan durante ejecución
4. **Alerta 48 Horas**: Contador automático desde inicio; alertas a las 24, 40 y 48 horas; exceder plazo requiere justificación escrita
5. **Conformidad Cliente**: Acta firmada por cliente es obligatoria para cerrar servicio; sin conformidad NO se puede cerrar
6. **Parte de Ingreso (PI)**: Obligatorio para recepción de bienes; debe estar vinculado a OC; sin PI almacén NO recepciona

---

### 18.7. Consideraciones Técnicas

- **Almacenamiento**: Repositorio seguro, backup diario, versionado de documentos, retención 7 años, encriptación de docs sensibles
- **Seguridad**: Acceso por roles (Supervisor, SSDMA, Proveedor, Almacén), permisos granulares, registro de accesos, auditoría completa
- **Performance**: Carga docs < 30 seg, visualización < 3 seg, generación PI < 5 seg, consulta estado < 2 seg
- **Disponibilidad**: Sistema 24/7 (especialmente emergencias), mantenimientos fuera de horario laboral, notificación previa 48 horas
- **Notificaciones**: Envío en tiempo real (< 5 seg), múltiples canales (email, sistema, WhatsApp para urgentes), reintentos automáticos (3 intentos)

---

**Nota Final**: El módulo de Ejecución de Trabajo/Entrega del Bien es crítico para controlar la documentación obligatoria de seguridad según el tipo de trabajo (15 documentos para Alto Riesgo, 11 para Emergencia, 7 para Trabajos Menores), garantizar cumplimiento de plazos de cierre (48 horas) y asegurar la trazabilidad completa desde coordinación hasta cierre final.

---

## 19. EMISIÓN DE HES (Hoja de Entrada de Servicio)

### 19.1. Objetivo del Módulo

Gestionar la emisión de HES (Hoja de Entrada de Servicio) para formalizar la culminación de servicios ejecutados por proveedores, validando la documentación requerida y asegurando la notificación automática al proveedor. Este proceso es fundamental para el cierre administrativo y contable de los servicios prestados.

**Nota Importante**: Este módulo NO tiene integración con SAP. Toda la gestión es independiente dentro del sistema FM.

### 19.2. Flujo del Proceso

#### 19.2.1. Proveedor Entrega Documentación Requerida

1. Proveedor accede al Portal de Proveedores y navega a "Solicitud de HES"
2. Visualiza servicios completados pendientes de HES (filtros: Fecha, Cliente, Sede, Monto)
3. Selecciona servicio y carga documentos obligatorios según tipo de servicio

**Documentos Obligatorios**:

| N° | Documento | Formato | Obligatorio |
|----|-----------|---------|-------------|
| 1 | Ficha de Atención | PDF | Sí |
| 2 | Informe Técnico | PDF | Sí |
| 3 | Protocolo de Mantenimiento | PDF | Condicional* |
| 4 | Acta de Conformidad | PDF | Sí |
| 5 | Evidencias Fotográficas | JPG/PNG/PDF | Sí |
| 6 | Orden de Trabajo Cerrada | PDF | Sí |
| 7 | Reporte de Materiales Utilizados | PDF/Excel | Condicional* |
| 8 | Certificados de Prueba | PDF | Condicional* |

*Condicional: Según tipo de servicio (preventivo/correctivo, uso de materiales, alto riesgo)

**Validaciones**: Formato PDF, tamaño máximo 10 MB, nomenclatura con código de servicio

#### 19.2.2. Proveedor Solicita Emisión de HES

1. Proveedor revisa documentación cargada (progreso: "X de Y documentos cargados")
2. Completa formulario de solicitud con datos del servicio (solo lectura) y observaciones (opcional)
3. Hace clic en "Solicitar Emisión de HES"
4. Sistema genera número de solicitud y cambia estado a "Solicitud de HES en Revisión"
5. Sistema notifica al Service Desk

#### 19.2.3. Service Desk Valida la Documentación

1. Service Desk accede al módulo de Validación de HES (filtros: Estado, Proveedor, Fecha, Cliente)
2. Selecciona solicitud y accede a documentación cargada
3. Revisa cada documento con checklist:
   - Ficha de Atención completa y firmada
   - Informe Técnico detallado con hallazgos
   - Protocolo de Mantenimiento (si aplica)
   - Acta de Conformidad con firma del cliente
   - Evidencias fotográficas claras (mínimo 3: antes, durante, después)
   - Orden de Trabajo cerrada
   - Reporte de Materiales coincide con OC (si aplica)
   - Certificados de Prueba vigentes (si aplica)
4. Valida específicamente:
   - **Acta de Conformidad**: Firma cliente, fecha posterior a inicio, conformidad total
   - **Informe Técnico**: Actividades, hallazgos, coincide con OC, firmado
   - **Evidencias Fotográficas**: Mínimo 3, claras, muestran trabajo, fecha dentro del periodo
   - **Montos**: Materiales no exceden OC, coherencia con servicio
5. Marca cada documento como "Aprobado" o "Observado"

#### 19.2.4. Gateway de Decisión: ¿Es Correcto?

**CASO A: SÍ - Documentación Correcta**
- Todos los documentos aprobados, sin observaciones críticas, checklist completo
- Continúa a 19.2.5 (Service Desk emite HES)

**CASO B: NO - Documentación Incorrecta/Incompleta**
- Documentos faltantes, observaciones críticas, documentos no conformes
- Service Desk registra observaciones (tipo, descripción, plazo: 2 días hábiles)
- Sistema notifica al proveedor con lista de observaciones y enlace para corregir
- Proveedor corrige y reenvía (máximo 3 oportunidades; después requiere aprobación Supervisor)
- Regresa a revisión

#### 19.2.5. Service Desk Emite la HES

1. Service Desk accede a módulo de Emisión de HES
2. Sistema pre-llena datos automáticamente:
   - Número de HES (formato: HES-[Año]-[Mes]-[Correlativo])
   - Código de Servicio, OC, Proveedor, Cliente, Sede
   - Descripción, Fechas, Monto Total
3. Service Desk completa información adicional (opcional):
   - Observaciones, Área Solicitante, Centro de Costo, N° de PI, Anexos
4. Genera HES en PDF (plantilla estándar con logo Panorama BPO)
5. Revisa vista previa y confirma
6. Hace clic en "Emitir HES" → Estado: "HES Emitida"

#### 19.2.6. Service Desk Carga la HES al Sistema

1. Sistema almacena HES automáticamente (PDF en repositorio)
2. Vincula HES con: OC, Documentación del servicio, Acta de conformidad, PI (si aplica)
3. Actualiza estado: "HES Emitida y Registrada"
4. Marca servicio como "Listo para Facturación"

#### 19.2.7. Sistema Envía la HES vía Mail al Proveedor

1. Sistema genera correo automático con:
   - Asunto: "HES Emitida - [Número] - [Código Servicio]"
   - Datos de HES (número, servicio, OC, cliente, monto)
   - HES adjunta en PDF
   - Instrucciones: Facturar en 5 días hábiles con referencia a HES y OC
2. Registra envío (fecha, hora, destinatario, estado)
3. Notifica a Supervisor de MTTO y Gerente FM (si monto > umbral)
4. Estado final: "Proceso de HES Completado"

---

### 19.3. Estados de la Solicitud de HES

1. **Pendiente de Solicitud** | 2. **Documentación en Carga** | 3. **Solicitud en Revisión** | 4. **Documentación Observada** | 5. **Solicitud en Revisión (Corrección)** | 6. **Documentación Aprobada** | 7. **HES en Emisión** | 8. **HES Emitida** | 9. **HES Emitida y Registrada** | 10. **HES Enviada al Proveedor** | 11. **Proceso Completado** | 12. **Suspendida**

---

### 19.4. Pantallas del Módulo

#### 19.4.1. Portal de Proveedores - Solicitud de HES
- Lista de servicios completados (filtros: Estado HES, Cliente, Fechas, Monto)
- Formulario de solicitud: Datos servicio (solo lectura), Carga de documentos, Barra de progreso, Observaciones
- Botones: Cargar Documento, Guardar Borrador, Solicitar Emisión de HES

#### 19.4.2. Pantalla de Validación de HES (Service Desk)
- Información del servicio (código, proveedor, cliente, fecha, monto)
- Checklist de documentos (estado, ver/descargar, observaciones)
- Botones: Aprobar Documento, Observar Documento, Aprobar Todos, Solicitar Correcciones, Emitir HES

#### 19.4.3. Pantalla de Emisión de HES
- Datos pre-llenados (automáticos)
- Campos editables (observaciones, área, centro costo, PI, anexos)
- Vista previa de HES en PDF
- Botones: Generar Vista Previa, Emitir HES, Cancelar, Guardar Borrador

#### 19.4.4. Pantalla de Seguimiento de HES
- Filtros: Estado, Proveedor, Cliente, Fechas, Número HES
- Tabla: Número HES, Código Servicio, Proveedor, Cliente, Fecha Emisión, Monto, Estado, Días desde Emisión
- Acciones: Ver Detalle, Descargar PDF, Ver Documentación, Reenviar, Auditoría, Imprimir, Exportar Excel

---

### 19.5. Reglas de Negocio

1. **Documentación Obligatoria**: Sistema NO permite solicitar HES sin documentos obligatorios completos (5 siempre + 3 condicionales)
2. **Acta de Conformidad**: Debe tener firma cliente; sin acta NO se puede emitir HES
3. **Límite de Rechazos**: Máximo 3 oportunidades para corregir; después se suspende automáticamente
4. **Plazos**: Corrección en 2 días hábiles (ampliable a 5 máximo); recordatorio 1 día antes; vencimiento suspende solicitud
5. **Numeración HES**: Formato HES-[Año]-[Mes]-[Correlativo]; secuencial y única; no modificable una vez emitida
6. **Facturación**: Proveedor debe facturar en 5 días hábiles; recordatorio a los 3 días; referencia obligatoria a HES y OC
7. **Modificación HES**: Una vez emitida es inmutable; anulación requiere aprobación Gerente FM
8. **Vinculación OC**: HES debe estar vinculada a OC válida; monto no puede exceder OC (±2% tolerancia)

---

### 19.6. Consideraciones Técnicas

- **Almacenamiento**: Repositorio seguro, backup diario, formato PDF/A, retención 7 años, indexación por HES/OC/servicio/proveedor
- **Seguridad**: HES inmutables, solo lectura proveedores, control acceso por rol, auditoría completa
- **Performance**: Generación PDF < 10 seg, consulta < 2 seg, descarga < 5 seg, envío email < 30 seg
- **Sin SAP**: No hay integración; gestión exclusiva en FM; exportación manual a Excel si necesario
- **Trazabilidad**: Vinculación completa Solicitud → Cotización → OC → Ejecución → Cierre → HES

---

**Nota Final**: El módulo de Emisión de HES es crítico para el cierre administrativo de servicios. La correcta validación de documentación y emisión oportuna asegura el flujo de facturación y pago a proveedores. El sistema garantiza la inmutabilidad de las HES emitidas y mantiene una auditoría completa del proceso.


---

## 20. PRESENTACIÓN DE KPI's

### 20.1. Objetivo del Módulo

Proporcionar visualización y análisis de indicadores clave de rendimiento (KPI's) del sistema FM mediante reportes estándares predefinidos y dashboards personalizados. El módulo permite monitorear el desempeño de servicios, equipos y proveedores para facilitar la toma de decisiones basadas en datos.

### 20.2. Flujo del Proceso

#### 20.2.1. FM Ingresa al Sistema

1. Usuario FM accede al módulo "Reportes y KPI's"
2. Sistema valida permisos según rol (Gerente FM, Supervisor, Analista)
3. Sistema muestra dashboard principal con KPI's relevantes

#### 20.2.2. Ingresa al Módulo de Reportes

**Gateway de Decisión: ¿Para Nuevos KPI's?**

**Para nuevos KPI's debe ser configurado por FM.**

- **CASO A - KPI Estándar**: Usuario selecciona KPI de la lista de 23 predefinidos → Sistema permite visualizar reportes estándares
- **CASO B - Nuevo KPI**: Usuario crea dashboard personalizado → Sistema permite crear y sugerir reportes personalizados (Estilo Power BI + IA)

#### 20.2.3. Sistema Permite Visualizar Reportes Estándares

1. Usuario selecciona KPI estándar (ver Tabla en 20.3)
2. Sistema muestra gráfico principal con indicadores
3. Filtros disponibles: Periodo, Cliente, Sede, Proveedor, Categoría de Servicio, Tipo de Equipo
4. Acciones: Exportar (Excel/PDF), Guardar favorito, Compartir, Programar envío

#### 20.2.4. Sistema Permite Crear Reportes Personalizados (Estilo Power BI + IA)

1. **Usuario define reporte**: Nombre, descripción, categoría
2. **Usuario selecciona fuente de datos**: Servicios, OT's, Equipos, Preventivos, Proveedores, Tiempos, Costos, HES, Cotizaciones, OC's
3. **Usuario selecciona campos**:
   - Dimensiones: Fecha, Cliente, Sede, Proveedor, Tipo de Servicio, Estado, Categoría de Equipo
   - Métricas: Conteo, Suma, Promedio, Porcentaje, Cantidad
4. **Sistema sugiere gráficos según campos seleccionados** (IA analiza y recomienda visualizaciones)
5. **Usuario decide**:
   - Selecciona dashboard sugerido por IA
   - O diseña reporte visual manualmente (drag-and-drop)
6. Usuario guarda reporte personalizado

---

### 20.3. Catálogo de KPI's Estándares

El sistema FM incluye 23 KPI's predefinidos:

| N° | Nombre de indicador, KPI/OKR | Categorías | Lógica | Fórmula | Modo de Recaudación |
|----|------------------------------|------------|--------|---------|---------------------|
| 1 | **Cumplimiento del preventivo** | Preventivo | Compara los servicios preventivos programados versus los efectivamente ejecutados. | Ejecutados/Programados | Se obtiene de los registros de mantenimientos programados y ejecutados en el sistema. |
| 2 | **Cumplimiento de entregables (Preventivos)** | Preventivo | Mide el cumplimiento de la entrega de reportes, informes o entregables correspondientes a los mantenimientos preventivos. | Entregables emitidos/Entregables Programados | Se toma del control de entregas documentarias asociadas a cada mantenimiento preventivo. |
| 3 | **MTBF (Mean Time Between Failures)** | Equipos | Mide el tiempo promedio entre una falla y la siguiente, reflejando la confiabilidad del activo. | Tiempo total de funcionamiento/Número de fallas | Se calcula con base en los registros de fallas y reparaciones de los equipos. |
| 4 | **Tiempo medio de atención de Compras CSC** | Servicio | Promedio del tiempo que tarda el área de compras en atender un requerimiento o servicio. | Tiempo total de atención/Número de servicios adjudicados | Se obtiene del registro de solicitudes enviadas y fechas de atención de Compras CSC. |
| 5 | **MTTR (Mean Time To Repair)** | Equipos | Mide el tiempo promedio que tarda en repararse un equipo tras una falla. | Tiempo total de reparación/Número de fallas | Se obtiene del tiempo registrado entre inicio y fin de cada reparación. |
| 6 | **Disponibilidad de equipos** | Equipos | Indica el porcentaje de tiempo que un equipo está disponible para operar respecto al total de tiempo del periodo analizado. | (Tiempo operativo/(Tiempo operativo + Tiempo fuera de servicio))*100 | Se calcula a partir de los registros de operación y tiempos fuera de servicio. |
| 7 | **Ciclo del activo** | Equipos | Mide el tiempo que transcurre desde la adquisición hasta el retiro o reemplazo del activo. | Fecha de retiro - Fecha de adquisición | Se obtiene de las fechas de alta y baja registradas para cada equipo. |
| 8 | **Tiempo de vida del activo** | Equipos | Mide el tiempo de funcionamiento real del activo desde su puesta en marcha. | Fecha actual - Fecha de inicio de operación | Se calcula con las fechas de inicio de operación registradas en el sistema. |
| 9 | **Tiempo de envío de presupuesto** | Servicio | Mide el tiempo promedio que tarda en enviarse un presupuesto de Facilities Management al cliente. | Fecha de envío - Fecha de solicitud x cliente | Se obtiene de las fechas de solicitud y envío de presupuesto registradas. |
| 10 | **OEE (Overall Equipment Effectiveness)** | Equipos | Mide la eficiencia global del equipo considerando disponibilidad, rendimiento y calidad. | Disponibilidad * Rendimiento * Calidad | Se obtiene integrando tres fuentes del sistema: disponibilidad (horas operativas vs paradas), rendimiento (producción real vs esperada) y calidad (unidades buenas vs totales). La información se consolida automáticamente por equipo y periodo. |
| 11 | **Tasa de fallos o paros inesperados** | Equipos | Mide la frecuencia de fallas o detenciones no planificadas respecto al total de horas de operación. | (Número de fallas inesperadas/Horas totales de operación)*100 | Se calcula con base en los reportes de fallas y el total de horas operativas. |
| 12 | **Porcentaje de fallas no planificadas** | Equipos | Mide el porcentaje de fallas no previstas sobre el total de intervenciones. | (Fallas no planificadas/Total de intervenciones)*100 | Se obtiene del registro de órdenes de trabajo clasificadas como no planificadas. |
| 13 | **Cumplimiento de entrega de inventario de equipos** | Equipos | Mide el cumplimiento de la entrega del inventario físico o técnico de equipos. | (Locales intervenidos/Locales Programados)*100 | Se toma de los registros de entregas de inventario programadas y realizadas. |
| 14 | **Nivel de cumplimiento de Tiempo medio de llegada a sitio por Emergencias** | Servicio | Mide el cumplimiento del tiempo objetivo de llegada ante emergencias. | (Llegadas dentro del Tiempo objetivo/Total de emergencias)*100 | Se obtiene de los tiempos de llegada registrados en cada atención de emergencia. |
| 15 | **Nivel de cumplimiento de Tiempo medio de ejecución de Emergencias** | Servicio | Mide el cumplimiento del tiempo establecido para ejecutar las atenciones de emergencia. | (Ejecuciones dentro del Tiempo objetivo/Total de emergencias)*100 | Se toma del control de tiempos de ejecución registrados para servicios de emergencia. |
| 16 | **Nivel de cumplimiento de Tiempo medio de llegada a sitio para Correctivos normales** | Servicio | Mide el cumplimiento del tiempo objetivo de llegada para atenciones correctivas no urgentes. | (Llegadas dentro del Tiempo objetivo/Total de correctivos normales)*100 | Se obtiene del registro de tiempos de atención de servicios correctivos normales. |
| 17 | **Nivel de cumplimiento de Tiempo medio de ejecución de Correctivos normales** | Servicio | Mide el cumplimiento del tiempo establecido para ejecutar las órdenes correctivas. | (Ejecuciones dentro del Tiempo objetivo/Total de correctivos normales)*100 | Se calcula con base en los tiempos de ejecución de cada orden correctiva. |
| 18 | **Ratio de Confiabilidad** | Equipos | Mide la proporción de equipos que no presentaron fallas durante el periodo. | (N° de equipos sin fallas/Total de equipos)*100 | Se obtiene del conteo de equipos sin registros de fallas en el periodo. |
| 19 | **Ratio de OT's de Emergencia** | Servicio | Mide la proporción de órdenes de trabajo de emergencia respecto al total de órdenes emitidas. | (OTs de emergencia/Total de OTs)*100 | Se toma del registro de órdenes de trabajo clasificadas por tipo de atención. |
| 20 | **Ratio de averías repetidas** | Equipos | Mide la proporción de fallas reincidentes sobre el total de fallas registradas. | (Fallas repetidas/Total de fallas)*100 | Se obtiene comparando las fallas reportadas de un mismo equipo en un periodo. |
| 21 | **Nivel de cumplimiento de Tiempo medio de Finalización de OT's con conformidades y revisiones** | Servicio | Mide el cumplimiento del tiempo objetivo de cierre de OT's incluyendo revisión y conformidad. | (OTs finalizadas dentro del Tiempo objetivo/Total de OTs)*100 | Se obtiene de los tiempos de cierre registrados con validación y conformidad. |
| 22 | **Nivel de cumplimiento de Entrega de Liquidaciones de los servicios realizados** | Servicio | Mide el cumplimiento en la entrega de liquidaciones administrativas dentro del plazo establecido. | (Liquidaciones entregadas a Tiempo/Total de servicios realizados)*100 | Se obtiene del registro de entregas de liquidaciones con fecha límite y de envío. |
| 23 | **Evaluación de desempeño del proveedor** | Servicio | Mide el cumplimiento de indicadores de calidad, tiempo, seguridad y documentación del proveedor. | Σ(Ponderación * Cumplimiento de cada criterio) | Se calcula con base en la evaluación de desempeño registrada por cada proveedor. |

**Categorías de KPI's**:
- **Preventivo** (2 KPI's): N° 1-2
- **Equipos** (11 KPI's): N° 3, 5-8, 10-13, 18, 20
- **Servicio** (10 KPI's): N° 4, 9, 14-17, 19, 21-23

---

### 20.4. Pantallas del Módulo

#### 20.4.1. Dashboard Principal de KPI's
- Tarjetas con KPI's principales (Top 6 configurables)
- Gráfico de tendencia de KPI prioritario
- Alertas de KPI's fuera de rango
- Filtros globales: Periodo, Cliente, Sede

#### 20.4.2. Catálogo de KPI's Estándares
- Lista de 23 KPI's predefinidos
- Filtros: Por Categoría, Por Nombre, Por Favoritos
- Acciones: Ver Reporte, Agregar a Favoritos, Exportar, Compartir

#### 20.4.3. Pantalla de Visualización de KPI
- Valor actual destacado, comparación con periodo anterior
- Gráfico principal (tipo según KPI)
- Tabla de datos detallados, drill-down
- Botones: Exportar (Excel/PDF), Compartir, Programar Envío

#### 20.4.4. Lienzo de Diseño de Reportes Personalizados
- Panel izquierdo: Componentes (gráficos, tablas, KPI cards)
- Área central: Canvas drag-and-drop
- Panel derecho: Propiedades del componente
- IA sugiere 3-5 dashboards según campos seleccionados

---

### 20.5. Reglas de Negocio

1. **Configuración de KPI's Nuevos**: Solo Gerente FM o Administrador pueden crear KPI's nuevos
2. **Acceso a Reportes**:
   - Gerente FM: Acceso total
   - Supervisor: KPI's de Equipos y Servicio (limitado a sus clientes/sedes)
   - Analista: Reportes predefinidos (sin edición)
3. **Actualización de Datos**: KPI's estándares se actualizan cada hora; KPI's en tiempo real cada 15 minutos
4. **Retención**: Datos históricos de KPI's se conservan por 24 meses
5. **Exportación**: Excel máximo 100,000 filas; PDF máximo 50 páginas
6. **Compartir Dashboards**: Creador define permisos (lectura/edición/administración)
7. **Alertas**: Usuario puede configurar alertas personalizadas (máximo 10 activas por usuario)
8. **Programación**: Máximo 20 reportes programados por usuario; envío en horario nocturno (2:00-6:00 AM)

---

### 20.6. Consideraciones Técnicas

- **Performance**: Carga de dashboard < 3 segundos; generación de gráficos < 2 segundos
- **Almacenamiento**: Datos históricos 24 meses; reportes exportados 6 meses
- **Escalabilidad**: Soportar 100 usuarios concurrentes; hasta 500 dashboards personalizados
- **Seguridad**: Control de acceso por rol; exportaciones con marca de agua; auditoría completa
- **Interactividad**: Gráficos interactivos (zoom, pan, tooltips); drill-down; filtros globales
- **Responsividad**: Dashboards adaptables a tablets y smartphones

---

**Nota Final**: El módulo de Presentación de KPI's facilita la toma de decisiones estratégicas basadas en datos mediante 23 KPI's predefinidos y capacidad de crear dashboards personalizados con IA.

---

## 21. PROGRAMACIÓN DE MANTENIMIENTO Y ACTIVIDADES

### 21.1. Objetivo del Módulo

Gestionar la programación de mantenimientos preventivos y actividades de FM mediante un calendario visual, generar automáticamente códigos de servicio únicos para PAM's (Programa Anual de Mantenimiento), calendarizar tareas, elaborar Gantt de programación y generar OT's asociadas, asegurando trazabilidad completa desde planificación hasta cierre.

### 21.2. Flujo del Proceso

#### 21.2.1. Sistema Solicita Información de Actividad

1. **Sistema solicita**: Actividad, programación, fechas, recursos y personal
2. **FM accede al módulo** "Programación de Mantenimiento y Actividades"
3. **Sistema presenta formulario** con campos requeridos

#### 21.2.2. FM Registra Programación y Actividades

1. **FM completa información**:
   - Tipo de Actividad (Preventivo, Inspección, Calibración, Limpieza, etc.)
   - Cliente/Sede
   - Equipo/Activo (si aplica)
   - Frecuencia (Mensual, Trimestral, Semestral, Anual)
   - Fecha de Inicio Programada
   - Turno (Mañana, Tarde, Noche)
   - Recursos Necesarios (herramientas, materiales)
   - Personal Asignado (técnico, proveedor)
   - Observaciones

2. **Sistema recoge información del Event Code**:
   - Fecha programada
   - Cliente
   - Tienda/Sede
   - Turno
   - Tipo de mantenimiento
   - Código de equipo (si aplica)

3. **Sistema valida información**: Disponibilidad de recursos, conflictos de calendario, capacidad del personal

**Nota**: Modificable por Gerente de FM y FM

#### 21.2.3. Sistema Agrupa y Calendariza

1. **Sistema agrupa información en el día asignado**:
   - Agrupa por fecha
   - Agrupa por cliente/sede
   - Agrupa por turno
   - Agrupa por técnico/proveedor

2. **Sistema calendariza las actividades programadas**:
   - Asigna slot en calendario
   - Valida superposición de actividades
   - Genera alertas de conflictos

#### 21.2.4. Sistema Muestra Información en Calendario

**Opciones de Visualización**:

**A. Calendario con Vista Principal Mensual**:
- Vista mensual con actividades agrupadas por día
- Código de colores por tipo de actividad
- Indicadores de carga por día (bajo/medio/alto)
- Capacidad de filtrar por rango de fechas
- Filtros: Cliente, Sede, Tipo de Actividad, Técnico, Estado

**B. Vista Gantt de Programación de Mantenimientos**:
- Sistema elabora Gantt de programación
- Línea de tiempo con tareas programadas
- Visualización de dependencias
- Hitos importantes
- Progreso de ejecución

**Gateway de Decisión: Calendario o Gantt?**
- Usuario selecciona vista preferida
- Sistema alterna entre vistas sin perder datos

#### 21.2.5. Sistema Genera las OT's

**Generación Automática**:

1. **Código único PAM**: Formato PAM-[Año]-[Mes]-[Cliente]-[Correlativo] (ej: PAM-2026-02-CLIENTEX-001)

2. **Datos obligatorios de la OT**:
   - **Trazabilidad**: Quién creó, quién solicitó, fecha creación, fecha aprobación
   - **Asociaciones**: Incidencia (si aplica con mismo concepto), Grupo MTTO, Sub Grupo MTTO, Centro de Costo
   - **Clasificación**: Tipo (Preventivo/Correctivo), Criticidad (Normal default/Urgente/Emergencia)
   - **Asignaciones**: Cliente, Sede/Inmueble, Proveedor, Técnico
   - **Programación**: Fecha inicio calendarizada, duración estimada
   - **Estado inicial**: "Programada" (Estados: Operativo, En Proceso, Programada, Ejecutada, Con Atraso, Anulada)

3. **Módulo de Gestión de OT's**:
   - **Visualización**: Modo Kanban (columnas por estado) o Modo Listado (tabla 100% de OT's)
   - **Búsqueda y Filtros**: Por todas las variables (listas desplegables: estado, cliente, sede, proveedor, grupo MTTO, criticidad, fechas, etc.)
   - **Cálculo de tiempos**: Sistema calcula tiempo de atención (horas/minutos/días), indica dentro de tiempo o atrasada
   - **Alertas automáticas**: Por correo, SMS o WhatsApp según fecha programación, estado, atrasos, asignaciones
   - **Alertas personalizadas**: Configurables por usuario
   - **Validación**: Firma digital requerida para cierre
   - **Exportación**: Imprimible y exportable a PDF

4. **Fecha de inicio = Día de ejecución programado**

#### 21.2.6. Gestión de Cierre de Mantenimiento

1. **Técnico/Proveedor ejecuta mantenimiento** y registra en sistema:
   - Fecha y hora real de ejecución
   - Actividades realizadas
   - Hallazgos/Observaciones
   - Materiales utilizados
   - Evidencias fotográficas

2. **Supervisor valida cierre**:
   - Revisa documentación
   - Aprueba o solicita correcciones
   - Confirma conformidad

#### 21.2.7. Sistema Cambia el Status del Calendario

**Estados del Calendario**:
- **Programada**: Actividad creada, pendiente de ejecución
- **En Ejecución**: Técnico ha iniciado trabajo
- **Cerrado**: Actividad completada y validada
- **Culminado**: Proceso completo con documentación archivada
- **Reprogramada**: Cambio de fecha por motivo justificado
- **Cancelada**: Actividad anulada

Sistema actualiza automáticamente el color en calendario según estado.

---

### 21.3. Pantallas del Módulo

#### 21.3.1. Pantalla de Registro de Programación

**Campos**:
- Tipo de Actividad (dropdown: Preventivo, Inspección, Calibración, Limpieza, Otro)
- Cliente/Sede (búsqueda con autocompletado)
- Equipo/Activo (búsqueda vinculada a sede, opcional)
- Frecuencia (Única, Mensual, Trimestral, Semestral, Anual)
- Fecha de Inicio Programada (calendario)
- Hora Estimada (hora)
- Turno (Mañana: 6-14h, Tarde: 14-22h, Noche: 22-6h)
- Duración Estimada (horas)
- Recursos Necesarios (texto/checklist)
- Personal Asignado (búsqueda de técnicos/proveedores)
- Observaciones (texto largo)
- Recurrencia (si aplica: cada X días/semanas/meses, hasta fecha)

**Botones**: Guardar, Guardar y Crear OT, Cancelar

#### 21.3.2. Calendario Mensual de Mantenimiento

**Vista Principal**:
- Calendario mensual con días del mes
- Cada día muestra: Cantidad de actividades, Indicador de carga (verde/amarillo/rojo)
- Click en día → Muestra detalle de actividades programadas

**Filtros Laterales**:
- Rango de Fechas (desde/hasta)
- Cliente (múltiple selección)
- Sede (múltiple selección)
- Tipo de Actividad (múltiple selección)
- Técnico Asignado (múltiple selección)
- Estado (Programada, En Ejecución, Cerrado, Culminado)

**Código de Colores**:
- 🟦 Azul: Preventivo
- 🟩 Verde: Inspección
- 🟨 Amarillo: Calibración
- 🟪 Morado: Limpieza
- 🟧 Naranja: Otro

**Acciones Rápidas**: Crear Nueva Actividad, Ver Gantt, Exportar Calendario, Imprimir

#### 21.3.3. Vista Gantt de Programación

**Componentes**:
- Eje temporal horizontal (semanas/meses)
- Lista de actividades vertical (agrupadas por cliente/sede)
- Barras de duración de cada actividad
- Hitos (fechas críticas, vencimientos)
- Líneas de dependencia (si aplica)
- Indicador de progreso (% completado)

**Interactividad**:
- Arrastrar barras para reprogramar
- Zoom in/out en timeline
- Filtros dinámicos
- Export a PDF/imagen

**Botones**: Volver a Calendario, Ajustar Fechas, Guardar Cambios, Exportar

#### 21.3.4. Pantalla de Detalle de Actividad Programada

**Información**:
- Código PAM (solo lectura)
- Tipo de Actividad, Cliente/Sede, Equipo
- Fecha Programada vs Fecha Real (si ejecutada)
- Técnico Asignado, Recursos, Duración

**Documentación**:
- OT asociada (enlace)
- Protocolo de mantenimiento (adjunto)
- Evidencias fotográficas
- Informe de cierre

**Acciones**: Editar Programación, Reprogramar, Cancelar, Generar OT, Cerrar Actividad

#### 21.3.6. Módulo de Gestión de OT's

**Visualización Dual**:
- **Modo Kanban**: Columnas por estado (Programada, En Proceso, Ejecutada, Con Atraso, Anulada), tarjetas arrastrables, indicador de criticidad por color
- **Modo Listado**: Tabla con 100% de OT's, scroll infinito, ordenable por columnas

**Tabla de OT's** (Modo Listado):
- Código OT, Código PAM, Concepto, Estado, Criticidad, Cliente, Sede, Proveedor
- Grupo MTTO, Sub Grupo MTTO, Centro de Costo, Tipo (Preventivo/Correctivo)
- Fecha Creación, Fecha Programada, Fecha Aprobación
- Creado Por, Solicitado Por
- Tiempo de Atención (horas/minutos/días), Estado Temporal (Dentro de Tiempo/Atrasada)
- Acciones (Ver, Editar, Firmar, Exportar PDF, Anular)

**Filtros Avanzados** (panel lateral):
- Estado (múltiple), Criticidad (múltiple), Cliente (búsqueda), Sede (búsqueda)
- Proveedor (búsqueda), Grupo MTTO (lista), Sub Grupo MTTO (lista), Centro de Costo (lista)
- Tipo de Mantenimiento (Preventivo/Correctivo), Fechas (rango: creación, programación, aprobación)
- Creado Por (lista usuarios), Solicitado Por (lista usuarios)
- Estado Temporal (Dentro de Tiempo/Atrasada), Incidencia Asociada (Sí/No)

**Búsqueda Global**: Por cualquier campo, autocompletado, búsqueda inteligente

**Alertas Personalizadas**: Usuario configura alertas por fecha programación, cambio de estado, asignaciones, atrasos; canal: correo/SMS/WhatsApp

**Botones**: Crear OT Manual, Cambiar Vista (Kanban/Listado), Exportar Todo, Configurar Alertas

#### 21.3.7. Pantalla de Detalle de OT

**Información General**:
- Código OT, Código PAM (si aplica), Estado, Criticidad
- Incidencia Asociada (enlace, concepto heredado)

**Trazabilidad**:
- Creado Por, Solicitado Por, Fecha Creación, Fecha Aprobación

**Asociaciones**:
- Grupo MTTO, Sub Grupo MTTO, Centro de Costo
- Tipo de Mantenimiento, Cliente, Sede/Inmueble, Proveedor

**Programación**:
- Fecha Inicio Calendarizada, Duración Estimada
- Tiempo de Atención Calculado (horas/minutos/días), Estado: Dentro de Tiempo/Atrasada

**Firma Digital**: Sección para firma del responsable al cerrar

**Botones**: Editar, Firmar y Cerrar, Exportar a PDF, Imprimir, Anular OT

#### 21.3.5. Pantalla de Cierre de Mantenimiento

**Campos**:
- Código PAM (solo lectura)
- Fecha y Hora Real de Ejecución (obligatorio)
- Actividades Realizadas (checklist + texto)
- Hallazgos/Observaciones (texto largo)
- Materiales Utilizados (tabla: Material, Cantidad, Unidad)
- Próximo Mantenimiento Sugerido (fecha, opcional)
- Evidencias Fotográficas (mínimo 2, antes/después)
- Adjuntar Protocolo/Informe (PDF, obligatorio)

**Conformidad**:
- Estado del Equipo Post-Mantenimiento (Operativo, Con Observaciones, Requiere Reparación)
- Firma Digital del Técnico (obligatorio)
- Firma/Conformidad del Cliente (si aplica)

**Botones**: Guardar Borrador, Enviar a Validación, Cerrar Mantenimiento

---

### 21.4. Reglas de Negocio

1. **Generación de Códigos PAM**: Automática y secuencial; formato PAM-[Año]-[Mes]-[Cliente]-[Correlativo]; único e irrepetible
2. **Modificación de Programación**: Solo Gerente de FM y FM pueden crear/modificar; Técnicos solo pueden cerrar/ejecutar
3. **Conflictos de Calendario**: Sistema alerta si técnico tiene 2+ actividades en mismo turno/día; permite override con justificación
4. **Recurrencia Automática**: Sistema genera automáticamente próximas ocurrencias según frecuencia (mensual, trimestral, etc.) hasta 12 meses adelante
5. **Fecha de Inicio**: Debe ser = Día de ejecución programado en calendario; modificable hasta 24 horas antes
6. **Reprogramación**: Máximo 3 reprogramaciones por actividad; más requiere aprobación Gerente FM; debe registrarse motivo
7. **Cierre Obligatorio**: Actividades en estado "En Ejecución" deben cerrarse en 48 horas; alerta automática a Supervisor
8. **Validación de Recursos**: Sistema valida disponibilidad de recursos al programar; bloquea recursos asignados
9. **Estados de OT**: 6 estados posibles (Operativo, En Proceso, Programada, Ejecutada, Con Atraso, Anulada); transiciones controladas
10. **Criticidad por Default**: Nueva OT se crea con criticidad "Normal"; Urgente/Emergencia debe indicarse explícitamente
11. **Incidencias Asociadas**: Si OT proviene de incidencia, hereda el concepto automáticamente; asociación inmutable
12. **Firma Digital Obligatoria**: OT no puede cerrarse sin firma digital del responsable; firma registra usuario, fecha y hora
13. **Cálculo de Tiempos**: Sistema calcula automáticamente tiempo de atención desde fecha programada; marca como "Atrasada" si excede plazo
14. **Alertas Multicanal**: Usuario elige canal preferido (correo/SMS/WhatsApp); alertas se envían según configuración personal
15. **Grupos MTTO**: Grupo y Sub Grupo MTTO son obligatorios; deben existir en catálogo maestro; lista desplegable con búsqueda

---

### 21.5. Consideraciones Técnicas

- **Almacenamiento**: Calendario con retención 24 meses; tareas programadas archivadas 7 años; backup diario
- **Seguridad**: Acceso por rol (Gerente FM: full, FM: crear/editar, Técnico: ejecutar/cerrar, Supervisor: validar); auditoría completa
- **Performance**: Carga calendario < 2 seg; generación Gantt < 3 seg; filtros en tiempo real < 1 seg
- **Sincronización**: Calendario se actualiza cada 5 minutos; notificaciones en tiempo real; sincronización con calendarios externos (Outlook, Google Calendar) opcional
- **Notificaciones**: Recordatorios 24h antes de mantenimiento; alertas de conflictos; notificación de cierre pendiente; resumen semanal de programación
- **Escalabilidad**: Soportar hasta 10,000 actividades programadas simultáneamente; 200 técnicos activos; múltiples clientes y sedes

---

**Nota Final**: El módulo de Programación de Mantenimiento y Actividades centraliza la planificación de mantenimientos preventivos mediante calendario visual y Gantt, generando automáticamente códigos PAM únicos y OT's asociadas, asegurando control completo desde programación hasta cierre con trazabilidad total.


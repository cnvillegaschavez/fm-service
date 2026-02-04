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

### 4.9. Proceso de Registro de Cliente Nuevo

**Propósito**: Gestionar el flujo completo de registro de información de clientes nuevos, desde la solicitud de datos hasta el envío de la bienvenida, incluyendo validación de historial crediticio para clientes externos.

Este proceso involucra la colaboración entre FM, Cliente, Service Desk y opcionalmente CVC (Central de Verificación Crediticia) para clientes externos nuevos.

#### 4.9.1. Flujo del Proceso de Registro

**Paso 1: Solicitud de Datos (Proceso Manual)**
- **Actor**: FM
- **Acción**: FM envía solicitud de data de usuarios a registrar al cliente
- **Medio**: Correo electrónico
- **Sistema**: NO se registra en el sistema. Proceso completamente manual
- **Contenido de la Solicitud**: Formato Excel con campos requeridos

**Paso 2: Cliente Envía la Data Solicitada (Proceso Manual)**
- **Actor**: Cliente
- **Acción**: Cliente envía la data solicitada
- **Medio**: Correo electrónico
- **Formato**: Excel (plantilla enviada por FM)
- **Contenido**: Datos completos del cliente según formato estándar

**Paso 2.1: Validación de Historial Crediticio (Solo para Clientes Externos Nuevos)**
- **Actor**: FM
- **Acción**: Para clientes externos nuevos, FM solicita validación de historial crediticio a CVC
- **Proceso**: Manual, fuera del sistema
- **Información Enviada**: Datos del cliente en formato Excel
- **Propósito**: Verificar la solvencia crediticia del cliente antes de registrarlo

**Paso 3: Derivación de Data a Service Desk**
- **Actor**: FM
- **Acción**: FM deriva la data recibida del cliente a Service Desk
- **Medio**: Correo electrónico o comunicación interna
- **Sistema**: NO se registra en el sistema

**Paso 4: Service Desk Ingresa al Sistema**
- **Actor**: Service Desk FM
- **Acción**: Service Desk accede al módulo de Gestión de Clientes
- **Sistema**: Service Desk inicia sesión en el sistema FM

**Paso 5: Opción de Crear Cliente**
- **Actor**: Service Desk FM
- **Acción**: Service Desk selecciona la opción "Crear Cliente" o "Nuevo Cliente"
- **Sistema**: Sistema muestra el formulario de registro de cliente

**Paso 6: Service Desk Ingresa el RUC en la Barra de Búsqueda**
- **Actor**: Service Desk FM
- **Acción**: Service Desk ingresa el RUC del cliente en la barra de búsqueda
- **Sistema**: Sistema busca si el RUC ya existe en la base de datos
- **Propósito**: Validar si el cliente ya está registrado para evitar duplicados

**Paso 7: Service Desk Verifica la Data del Cliente**
- **Actor**: Service Desk FM
- **Acción**: Service Desk verifica la información del cliente
- **Sistema**: Sistema muestra los resultados de la búsqueda

**Decisión: ¿Cliente Existe?**

**Caso A: Cliente NO Existe**
- **Sistema**: No se encuentra ningún registro con ese RUC
- **Siguiente Paso**: Ir a **Paso 10 - Registrar al Cliente**

**Caso B: Cliente SÍ Existe**
- **Sistema**: Se encuentra un registro existente con ese RUC
- **Siguiente Paso**: Ir a **Paso 8 - Verificar si la Data es la Misma**

**Paso 8: Decisión - ¿Misma Data?**
- **Actor**: Service Desk FM
- **Acción**: Service Desk compara la data recibida con la data existente en el sistema
- **Opciones**:
  - **SÍ - La data es la misma**: Ir a **Paso 9 - Enviar Correo de Bienvenida**
  - **NO - La data es diferente**: Actualizar la data del cliente

**Paso 8.1: Service Desk Actualiza la Data (Si la data NO es la misma)**
- **Actor**: Service Desk FM
- **Acción**: Service Desk actualiza los campos modificados del cliente
- **Sistema**: 
  - Sistema registra los cambios en auditoría
  - Guarda la nueva información
  - Registra usuario y fecha de actualización
- **Siguiente Paso**: Ir a **Paso 9 - Enviar Correo de Bienvenida**

**Paso 9: Service Desk Envía Correo de Bienvenida**
- **Actor**: Service Desk FM
- **Acción**: Service Desk envía correo de bienvenida al cliente
- **Sistema**: Puede ser manual o mediante el sistema
- **Asunto del Correo**: "Bienvenido a Ruwaytech"
- **Siguiente Paso**: Ir a **Paso 11 - Sistema Envía Correo a Cliente**

**Paso 10: Service Desk Registra al Cliente (Si el cliente NO existe)**
- **Actor**: Service Desk FM
- **Acción**: Service Desk completa todos los campos del formulario de registro
- **Sistema**: 
  - Sistema genera automáticamente el Código de Cliente (RUC-CECO)
  - Valida que todos los campos obligatorios estén completos
  - Registra el nuevo cliente en la base de datos
  - Genera log de auditoría con usuario y fecha de creación
- **Datos a Registrar**:
  - RUC
  - Razón Social
  - Domicilio Fiscal
  - CECO
  - Tipo de Cliente (Público/Privado)
  - Clasificación (Interno/Externo)
  - Nacional/Extranjero
  - País
  - Email
  - Teléfono
  - WhatsApp
  - Representantes
  - Usuarios
  - Sucursales

**Paso 11: Sistema Envía Correo a Cliente (Proceso Automático)**
- **Actor**: Sistema
- **Acción**: Sistema envía automáticamente correo de bienvenida al cliente
- **Asunto**: "Bienvenido a Ruwaytech"
- **Destinatario**: Email del cliente registrado
- **Contenido**: 
  - Mensaje de bienvenida
  - Código de cliente generado
  - Instrucciones de acceso al portal (si aplica)
  - Información de contacto de FM
- **Fin del Proceso**

#### 4.9.2. Validación de Historial Crediticio (Clientes Externos Nuevos)

**Propósito**: Para clientes externos nuevos, es necesario validar su historial crediticio antes de proceder con el registro.

**Proceso:**
1. FM identifica que el cliente es externo y nuevo
2. FM solicita validación de historial crediticio a CVC (Central de Verificación Crediticia)
3. FM envía data del cliente en formato Excel
4. CVC realiza la validación (proceso externo)
5. CVC devuelve resultado a FM
6. Si la validación es exitosa, FM procede con el Paso 3 (derivar a Service Desk)
7. Si la validación falla, FM notifica al cliente y no procede con el registro

**Importante**: Este paso solo aplica para **clientes externos nuevos**.

#### 4.9.3. Formato de Data de Cliente

**Plantilla Excel para Solicitud de Datos:**

El formato Excel debe incluir las siguientes columnas:

| Campo | Descripción | Obligatorio |
|-------|-------------|-------------|
| RUC | Registro Único de Contribuyentes (11 dígitos) | Sí |
| Razón Social | Nombre completo o razón social del cliente | Sí |
| Domicilio Fiscal | Dirección completa del domicilio fiscal | Sí |
| CECO | Centro de Costos | Sí |
| Tipo de Cliente | Público o Privado | Sí |
| Clasificación | Interno o Externo | Sí |
| Nacional/Extranjero | Nacional o Extranjero | Sí |
| País | País del cliente | Sí |
| Email | Correo electrónico corporativo | Sí |
| Teléfono | Número de contacto principal | Sí |
| WhatsApp | Número de WhatsApp | No |
| Nombre Representante | Nombre del representante legal | Sí |
| Email Representante | Email del representante | Sí |
| Celular Representante | Celular del representante | Sí |
| Cargo Representante | Cargo del representante | Sí |

**Nota**: La plantilla puede incluir múltiples representantes y usuarios según la estructura del cliente.

#### 4.9.4. Roles Involucrados en el Proceso

| Rol | Responsabilidad |
|-----|-----------------|
| **FM (Facility Manager)** | Solicitar datos al cliente, coordinar validación crediticia (si aplica), derivar data a Service Desk |
| **Cliente** | Proporcionar información completa en formato Excel |
| **CVC (Central Verificación Crediticia)** | Validar historial crediticio para clientes externos nuevos |
| **Service Desk FM** | Ingresar o actualizar data en el sistema, enviar correo de bienvenida |
| **Sistema** | Validar datos, generar código de cliente, enviar correo automático de bienvenida |

#### 4.9.5. Correo de Bienvenida

**Asunto**: "Bienvenida e Instrucciones de Acceso"

**Estructura del Correo**:

```
Estimado(a) [Nombre del Usuario],

Le damos la cordial bienvenida a [Panorama BPO]. A partir de este momento, usted cuenta con un acceso institucional para el uso de la plataforma.

Por favor, siga las indicaciones a continuación para activar su cuenta:

Credenciales Iniciales de Acceso
• Correo institucional: [correo@cliente.pe]
• Contraseña temporal: [contraseña generada automáticamente]

Al ingresar por primera vez se le solicitará cambiar su contraseña. Para ello, recibirá un código de verificación en su correo institucional, el cual deberá ingresar para completar el proceso de actualización de credenciales.

Importante:
• El cambio de contraseña debe realizarse dentro de un plazo máximo de 24 horas desde el envío del correo.
• Si el plazo vence sin haber realizado el cambio, el sistema generará automáticamente una nueva opción para restablecer la contraseña.

En caso de presentar alguna dificultad con el acceso, por favor comuníquese con el área de soporte a través de:
Correo: soportefm@panoramabpo.com

Agradecemos su atención y le deseamos un excelente inicio.

Atentamente,
[Nombre / Cargo]
[Nombre de la Empresa]
```

**Campos Dinámicos del Correo**:
- **[Nombre del Usuario]**: Nombre completo del usuario registrado
- **[Panorama BPO]**: Nombre de la empresa (configurable en parámetros del sistema)
- **[correo@cliente.pe]**: Correo institucional asignado al usuario
- **[contraseña generada automáticamente]**: Contraseña temporal generada por el sistema
- **[Nombre / Cargo]**: Nombre y cargo del remitente (configurable)
- **[Nombre de la Empresa]**: Nombre de la empresa remitente

**Reglas del Sistema para Contraseñas Temporales**:

1. **Generación Automática**: El sistema debe generar una contraseña temporal aleatoria y segura
2. **Formato de Contraseña**: Debe incluir mayúsculas, minúsculas y números (mínimo 8 caracteres)
3. **Código de Verificación**: Al cambiar la contraseña, el sistema envía un código de verificación al correo institucional
4. **Plazo de 24 Horas**: El usuario tiene 24 horas para cambiar la contraseña temporal
5. **Vencimiento**: Si no cambia la contraseña en 24 horas:
   - La contraseña temporal se invalida
   - El sistema genera automáticamente una opción de restablecimiento
   - El usuario debe solicitar un nuevo código de acceso

**Envío del Correo**:
- **Automático**: El sistema envía el correo automáticamente después del registro exitoso del cliente
- **Manual**: Service Desk también puede enviar el correo manualmente desde el sistema
- **Registro**: El sistema debe registrar en auditoría la fecha y hora de envío del correo

**Información de Soporte**:
- **Correo de Soporte**: soportefm@panoramabpo.com (parametrizable en el sistema)
- **Disponibilidad**: Debe especificarse en el correo el horario de atención

#### 4.9.6. Validaciones del Proceso de Registro

- **RUC Único**: El sistema debe validar que no exista un RUC duplicado antes de permitir el registro
- **Campos Obligatorios**: Todos los campos marcados como obligatorios deben estar completos
- **Formato de Email**: Validar formato correcto de correo electrónico
- **Formato de RUC**: Validar que sea un RUC válido de 11 dígitos
- **Historial Crediticio**: Para clientes externos nuevos, debe existir validación de CVC antes del registro
- **Actualización de Data**: Si el cliente ya existe, se debe actualizar solo los campos modificados

#### 4.9.7. Auditoría del Proceso

El sistema debe registrar en auditoría:

- Fecha y hora de creación del cliente
- Usuario (Service Desk) que registró al cliente
- Fecha y hora de actualizaciones de data
- Usuario que realizó las actualizaciones
- Cambios específicos realizados (valor anterior y nuevo valor)
- Envío de correo de bienvenida (fecha, hora, destinatario)
- Búsquedas de RUC realizadas

#### 4.9.8. Notificaciones del Proceso

**Notificaciones Automáticas**:
1. **Al Cliente**: Correo de bienvenida con código de cliente
2. **A FM**: Notificación de cliente registrado exitosamente
3. **A Gerente de FM**: Resumen semanal de nuevos clientes registrados

**Notificaciones Manuales**:
1. FM notifica al cliente sobre solicitud de datos (correo)
2. FM notifica a CVC para validación crediticia (correo)
3. FM notifica a Service Desk para proceder con el registro (correo o comunicación interna)

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

### 9.10. Flujo del Proceso de Contrato

#### Paso 1: Solicitud de Contrato (Proceso Manual - Fuera del Sistema)
- **Actor**: FM
- **Acción**: FM solicita contrato al cliente por correo electrónico o comunicación directa
- **Sistema**: NO se registra en el sistema. Este paso es completamente manual
- **Estado**: No aplica (proceso externo al sistema)

#### Paso 2: Inicio del Registro - Inicio del Registro - Recepción de Contrato
- **Actor**: Cliente
- **Acción**: Después de la solicitud manual (Paso 1), el cliente tiene dos opciones:
  - **Opción A (Manual)**: Cliente envía contrato por correo → Gerente de FM crea el registro en el sistema y carga el contrato
  - **Opción B (Portal)**: Cliente crea el registro y carga el contrato directamente desde el Portal de Clientes
- **Sistema**: 
  - El contrato se registra por primera vez en el sistema (independientemente de la opción)
  - El Gerente de FM o el Cliente ingresan los datos generales del contrato (código, fechas, moneda, etc.)
  - Se genera el código de contrato automáticamente
  - Se carga el documento inicial
- **Notificación**: Sistema notifica a FM y Gerente de FM
- **Estado**: Recibido (primer estado en el sistema)

#### Paso 3: Revisión y Observaciones
- **Actor**: FM
- **Acción**: FM revisa el contrato y registra observaciones en el sistema
- **Sistema**: FM coloca observaciones en el sistema
- **Estado**: En Revisión → Con Observaciones

#### Paso 4: Envío de Observaciones al Cliente
- **Actor**: FM
- **Acción**: FM envía observaciones desde el sistema
- **Sistema**: 
  - Sistema envía email al cliente con las observaciones
  - Sistema notifica al cliente (email/sistema)
- **Estado**: Observaciones Enviadas

#### Paso 5: Recepción de Contrapropuesta
- **Actor**: Cliente
- **Acción**: Cliente tiene dos opciones:
  - **Opción A (Manual)**: Cliente envía contrapropuesta por correo → FM carga la contrapropuesta al sistema
  - **Opción B (Portal)**: Cliente carga la contrapropuesta directamente desde el Portal de Clientes
- **Sistema**: La contrapropuesta queda registrada en el sistema (independientemente de la opción)
- **Notificación**: Sistema notifica automáticamente a FM
- **Estado**: Contrapropuesta Recibida

#### Paso 6: Envío a Legal
- **Actor**: FM
- **Acción**: FM envía contrato a Legal (proceso manual - correo)
- **Sistema**: FM actualiza estado en el sistema
- **Notificación**: Sistema notifica a Legal
- **Estado**: En Revisión Legal

#### Paso 7: Observaciones de Legal
- **Actor**: Legal
- **Acción**: Legal envía observaciones y correcciones por correo (proceso manual)
- **Sistema**: FM registra las observaciones de Legal en el sistema
- **Estado**: Legal con Observaciones

#### Paso 8: Segunda Propuesta
- **Actor**: FM
- **Acción**: FM envía 2da propuesta al cliente
- **Sistema**: FM carga nueva versión del contrato
- **Notificación**: Sistema notifica al cliente
- **Estado**: Propuesta Enviada

#### Paso 9: Aceptación del Cliente
- **Actor**: Cliente
- **Acción**: Cliente acepta propuesta (proceso manual)
- **Sistema**: FM actualiza el estado en el sistema
- **Notificación**: Sistema notifica a Gerente de FM
- **Estado**: Aceptado

#### Paso 10: Habilitación de Firma Electrónica
- **Actor**: Sistema
- **Acción**: Sistema habilita automáticamente opción de firma electrónica
- **Notificación**: Sistema notifica a FM
- **Estado**: En Firma

#### Paso 11: Gestión de Firmas
- **Actor**: FM
- **Acción**: FM gestiona el proceso de firmas electrónicas
- **Sistema**: Sistema registra cada firma con validadores del sistema
- **Estado**: En Firma

#### Paso 12: Contrato Firmado
- **Actor**: Sistema
- **Acción**: Sistema valida que todas las firmas estén completadas
- **Notificación**: Sistema notifica a Gerente General
- **Estado**: Firmado

#### Paso 13: Envío Final al Cliente
- **Actor**: FM
- **Acción**: FM envía contrato firmado al cliente
- **Sistema**: Sistema archiva el contrato
- **Estado**: Finalizado

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
:

**Posibles Adiciones Futuras:**
- Catálogo de Departamentos/Provincias/Distritos
- Catálogo de Países
- Catálogo de Zonas Geográficas
- Días festivos y no laborables
- Horarios de operación
- Tarifas y costos estándar
- Categorías de equipos y subcategorías
- Tipos de mantenimiento
- Plantillas de documentos
- Configuración de firma electrónica

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

### 11.3. Flujo del Proceso de Solicitud de Atención

#### Paso 1: Usuario Ingresa al Sistema
- **Actor**: Usuario (Cliente, Empleado interno)
- **Acción**: Usuario accede al módulo de "Solicitud de Atención de Incidencia"
- **Sistema**: Sistema muestra la pantalla principal de creación de solicitud

#### Paso 2: Usuario Ingresa la Razón de Atención de Incidencia
- **Actor**: Usuario
- **Acción**: Usuario selecciona "Nueva Solicitud" o "Crear Incidencia"
- **Sistema**: Sistema muestra el formulario de solicitud

#### Paso 3: Sistema Muestra el Tipo de Solicitud
- **Actor**: Sistema
- **Acción**: Sistema presenta lista desplegable con los tipos de solicitud
- **Opciones**: Mantenimiento / Suministros

#### Paso 4: Usuario Selecciona el Tipo de Solicitud
- **Actor**: Usuario
- **Acción**: Usuario selecciona el tipo de solicitud desde la lista desplegable
- **Campo**: Obligatorio
- **Sistema**: El sistema permite crear, modificar, eliminar data de categoría a nivel administrador

#### Paso 5: Sistema Muestra Categorías de Acuerdo a Tipo
- **Actor**: Sistema
- **Acción**: Sistema filtra y muestra las categorías (Grupos de MTTO) disponibles según el tipo de solicitud seleccionado
- **Formato**: Lista desplegable dinámica

#### Paso 6: Usuario Selecciona la Categoría (Nivel 1)
- **Actor**: Usuario
- **Acción**: Usuario selecciona la CATEGORIA desde la lista desplegable
- **Ejemplo**: ÁREAS VERDES, CERRAJERÍA, HVAC, SISTEMA ELÉCTRICO, etc.
- **Campo**: Obligatorio
- **Nivel**: Nivel 1 de categorización (marcado en amarillo en el catálogo)

#### Paso 7: Sistema Muestra Lista de Opciones Seleccionables de Sub Categorías
- **Actor**: Sistema
- **Acción**: Sistema muestra las Unidades de MTTO correspondientes a la categoría seleccionada
- **Formato**: Lista desplegable dinámica
- **Filtrado**: Según la categoría seleccionada en el paso anterior

#### Paso 8: Usuario Selecciona la Unidad de MTTO (Nivel 2)
- **Actor**: Usuario
- **Acción**: Usuario selecciona la UNIDAD DE MTTO desde la lista desplegable filtrada
- **Ejemplo**: 
  - Si seleccionó ÁREAS VERDES: JARDINERÍA, MACETEROS
  - Si seleccionó CERRAJERÍA: CARPINTERÍA ALUMINIO, CARPINTERÍA DE MADERA, CARPINTERÍA METÁLICA
  - Si seleccionó HVAC: AIRE ACONDICIONADO, EQUIPOS DE EXTRACCIÓN DE AIRE, EQUIPOS DE VENTILACIÓN
- **Campo**: Obligatorio
- **Nivel**: Nivel 2 de categorización (marcado en amarillo en el catálogo)
- **Importante**: Este es el último nivel que el usuario selecciona. NO hay un tercer nivel para el usuario

#### Paso 9: Sistema Muestra Campo de Descripción
- **Actor**: Sistema
- **Acción**: Sistema habilita el campo de descripción de la incidencia
- **Validación**: El sistema extrae caracteres del campo de descripción (IA) para asociar con tabla de criticidad

#### Paso 10: Usuario Redacta la Descripción
- **Actor**: Usuario
- **Acción**: Usuario ingresa una descripción detallada de la incidencia
- **Campo**: Obligatorio, texto libre
- **Validación**: Sistema no debe permitir subir requerimientos sin descripción
- **Análisis**: El sistema analiza el texto para determinar nivel de criticidad

#### Paso 11: Sistema Exige Imágenes del Evento
- **Actor**: Sistema
- **Acción**: Sistema solicita al usuario cargar imágenes relacionadas con la incidencia
- **Formato**: PNG, JPG
- **Tamaño Máximo**: 10 MB por imagen
- **Validación**: Sistema no debe permitir subir requerimientos sin fotos

#### Paso 12: Usuario Sube las Imágenes
- **Actor**: Usuario
- **Acción**: Usuario carga las imágenes del evento
- **Campo**: Obligatorio (al menos 1 imagen)
- **Cantidad**: Máximo 3 imágenes
- **Validación**: El sistema valida formato y tamaño de archivo

#### Paso 13: Usuario Envía el Requerimiento
- **Actor**: Usuario
- **Acción**: Usuario presiona el botón "Enviar" o "Crear Solicitud"
- **Sistema**: Sistema valida que todos los campos obligatorios estén completos
- **Validación Final**: 
  - Tipo de solicitud seleccionado
  - Categoría completa (todos los niveles)
  - Descripción ingresada
  - Al menos 1 imagen cargada

#### Paso 14: Sistema Categoriza de Acuerdo a Tipo de Criticidad
- **Actor**: Sistema
- **Acción**: Sistema analiza la descripción y asigna automáticamente un nivel de criticidad/urgencia
- **Niveles de Criticidad**: 
  - **Alta**: Emergencias, fallas críticas que requieren atención inmediata
  - **Media**: Problemas que afectan operaciones pero no son emergencias
  - **Baja**: Solicitudes de mantenimiento preventivo o mejoras
- **Método**: Sistema Híbrido (Reglas Determinísticas + Inteligencia Artificial)
- **Proceso de Asignación**: Ver sección 11.14 para detalles técnicos de implementación

#### Paso 15: Sistema Envía la Solicitud a Equipo FM
- **Actor**: Sistema
- **Acción**: Sistema genera el ticket/código de servicio y notifica al equipo correspondiente
- **Código de Servicio**: Autogenerado por el sistema
- **Notificaciones**: 
  - **Criticidad Alta**: Notificación a Supervisor, Service Desk FM vía correo y WhatsApp (solo alta prioridad)
  - **Criticidad Media/Baja**: Notificación a Service Desk FM vía correo
- **Ticket Generado**: Sistema genera ticket o código de servicio
- **Fin del Proceso**

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

**Propósito**: Gestionar la programación de fechas de inicio de servicio por parte de los proveedores aprobados. Permite al proveedor definir el tipo de servicio (nacional o importación), registrar fechas de inicio, y al Supervisor de MTTO validar y coordinar la programación final.

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

### 13.4. Coordinación Final y Confirmación de Fecha

**Descripción**: Proceso de coordinación manual entre Supervisor MTTO y proveedor para confirmar detalles operativos finales.

**Coordinación Manual** (FUERA DEL SISTEMA):
- **Actor**: Supervisor de MTTO
- **Medio**: Correo electrónico o WhatsApp
- **Propósito**: Confirmar detalles operativos, punto de contacto en sede, requisitos especiales
- **Nota**: Esta coordinación es manual y no se registra automáticamente en el sistema

**Registro de Fecha Confirmada en el Sistema**:

**Actor**: Supervisor de MTTO

**Funcionalidad**: Registrar la fecha final coordinada

**Campo**:
- **Fecha Confirmada**: Fecha definitiva de inicio de servicio
- **Formato**: dd/mm/yyyy
- **Validación**: No puede ser anterior a hoy

**Acciones del Sistema al Confirmar Fecha**:
1. Actualiza estado a "Servicio Programado"
2. Registra fecha confirmada
3. Genera notificaciones:
   - Al cliente (información del servicio programado)
   - Al proveedor (confirmación final)
4. Programa recordatorios automáticos:
   - 24 horas antes del servicio: Correo + WhatsApp
   - 2 horas antes del servicio: WhatsApp
5. Registra en auditoría

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
| **Proveedor Asignado** | Texto (referencia) | Sí | Proveedor aprobado en cotización |
| **Enlace de Programación** | URL (autogenerado) | Sí | Link único para programar servicio |
| **Tipo de Servicio** | Lista | Sí | Nacional / Importación |
| **Fecha de Aprobación Cotización** | Fecha/Hora | Sí | Fecha en que se aprobó la cotización |
| **Fecha Propuesta por Proveedor** | Fecha | Sí | Fecha que el proveedor propone para inicio |
| **Formato de Fecha** | - | - | dd/mm/yyyy |
| **Plazo Máximo (Nacional)** | Cálculo automático | - | Fecha aprobación + 3 días calendario |
| **Observaciones Proveedor** | Texto libre | No | Comentarios del proveedor sobre la programación |
| **Estado de Programación** | Lista | Sí | Pendiente / Propuesta por Proveedor / Validada / Rechazada / Confirmada |
| **Validado por** | Texto (usuario) | No | Supervisor de MTTO que valida |
| **Fecha de Validación** | Fecha/Hora | No | Fecha en que se valida la programación |
| **Fecha Confirmada** | Fecha | No | Fecha final coordinada para inicio de servicio |
| **Requiere Reprogramación** | Sí/No | - | Indica si se rechazó la fecha propuesta |
| **Motivo de Rechazo** | Texto libre | No | Razón por la cual se rechazó la fecha |

### 13.4. Notificaciones del Proceso de Programación

| Evento | Destinatarios | Medio | Tipo |
|--------|---------------|-------|------|
| Cotización aprobada (incluye link programación) | Proveedor aprobado | Correo | Automático |
| Proveedor propone fecha | Supervisor de MTTO | Correo | Automático |
| Programación validada | Proveedor | Correo | Automático |
| Programación rechazada | Proveedor | Correo | Automático |
| Fecha confirmada | Proveedor + Cliente | Correo | Automático |
| Recordatorio 24h antes del servicio | Proveedor + Supervisor MTTO | Correo + WhatsApp | Automático |
| Recordatorio 2h antes del servicio | Proveedor + Supervisor MTTO | WhatsApp | Automático |
| Coordinación manual de fecha | Proveedor | Correo/WhatsApp | **Manual** |

### 13.5. Validaciones del Módulo de Programación

- El enlace de programación solo está activo después de aprobar la cotización
- Solo el proveedor aprobado puede acceder al enlace de programación
- Para servicios **Nacionales**: La fecha propuesta NO puede exceder 3 días calendario desde la aprobación de cotización
- Para servicios de **Importación**: No hay restricción de tiempo, pero debe justificarse el plazo
- El Supervisor de MTTO debe validar la programación antes de que el servicio inicie
- No se puede confirmar una programación sin la aprobación del Supervisor de MTTO
- El sistema debe validar que la fecha propuesta no sea anterior a la fecha actual

### 13.6. Reglas de Negocio del Módulo de Programación

- **RN-13.1**: La recepción del servicio debe ser en un plazo máximo de 3 días calendario de aprobada la cotización (solo para servicios nacionales)
- **RN-13.2**: Para servicios de importación, se libera la restricción de 3 días calendario
- **RN-13.3**: El enlace de programación es único por proveedor y expira después de 30 días de emitido
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
# PRACTICAS-TEST-1
TEST PARA PRACTICANTES

## OBJETIVO

Desarrollar una aplicación web de gestión de inventario utilizando:

* Supabase como base de datos y backend.
* HTML + CSS + JavaScript para el frontend.
* Supabase Client/API para conectar el dashboard con la base de datos.

El sistema debe permitir consultar, crear, editar y eliminar información de inventario.

Los practicantes pueden utilizar herramientas de IA / Vibe Coding, pero deben ser capaces de comprender y explicar el código desarrollado.

1. BASE DE DATOS

---

El sistema debe tener 3 tablas principales interconectadas.

## TABLA 1 — inventory

Representa el stock actual de cada artículo.

Campos:

* id
  Tipo sugerido: UUID / bigint
  Descripción: ID del registro.

* item_id
  Tipo sugerido: FK
  Descripción: Artículo asociado.

* quantity
  Tipo sugerido: integer
  Descripción: Cantidad actual disponible.

* location
  Tipo sugerido: text
  Descripción: Ubicación del inventario.

* min_stock
  Tipo sugerido: integer
  Descripción: Stock mínimo permitido.

* max_stock
  Tipo sugerido: integer
  Descripción: Stock máximo permitido.

* updated_at
  Tipo sugerido: timestamp
  Descripción: Última actualización.

## TABLA 2 — inventory_items

Contiene la información maestra de los artículos.

Campos:

* id
  Tipo sugerido: UUID / bigint
  Descripción: ID del artículo.

* sku
  Tipo sugerido: text
  Descripción: Código único del artículo.

* name
  Tipo sugerido: text
  Descripción: Nombre del artículo.

* description
  Tipo sugerido: text
  Descripción: Descripción del artículo.

* category
  Tipo sugerido: text
  Descripción: Categoría del artículo.

* weight
  Tipo sugerido: numeric
  Descripción: Peso.

* length
  Tipo sugerido: numeric
  Descripción: Largo.

* width
  Tipo sugerido: numeric
  Descripción: Ancho.

* height
  Tipo sugerido: numeric
  Descripción: Alto.

* price
  Tipo sugerido: numeric
  Descripción: Precio de venta.

* cost
  Tipo sugerido: numeric
  Descripción: Costo del artículo.

* supplier
  Tipo sugerido: text
  Descripción: Proveedor.

* created_at
  Tipo sugerido: timestamp
  Descripción: Fecha de creación.

## TABLA 3 — inventory_movements

Registra todos los movimientos realizados sobre el inventario.

Campos:

* id
  Tipo sugerido: UUID / bigint
  Descripción: ID del movimiento.

* item_id
  Tipo sugerido: FK
  Descripción: Artículo relacionado.

* inventory_id
  Tipo sugerido: FK
  Descripción: Registro de inventario afectado.

* movement_type
  Tipo sugerido: text
  Descripción: Entrada / Salida / Ajuste.

* quantity
  Tipo sugerido: integer
  Descripción: Cantidad involucrada en el movimiento.

* reason
  Tipo sugerido: text
  Descripción: Motivo del movimiento.

* status
  Tipo sugerido: text
  Descripción: Pendiente / Aprobado / Rechazado.

* created_at
  Tipo sugerido: timestamp
  Descripción: Fecha de creación.

* approved_at
  Tipo sugerido: timestamp
  Descripción: Fecha de aprobación.

* notes
  Tipo sugerido: text
  Descripción: Observaciones.

## RELACIONES

Las tablas deben estar correctamente relacionadas mediante Foreign Keys.

La estructura esperada es:

inventory_items
|
+------------- inventory
|
+------------- inventory_movements

La lógica esperada es:

1 artículo
->
1 registro de inventario
->
muchos movimientos

2. DASHBOARD

---

El practicante debe crear un dashboard en HTML que permita visualizar y gestionar la información del sistema.

El dashboard principal debe mostrar como mínimo:

* Total de artículos.
* Stock total.
* Artículos bajo el stock mínimo.
* Valor total del inventario.
* Movimientos recientes.

También debe existir una tabla principal de inventario que muestre información como:

* SKU
* Artículo
* Categoría
* Stock
* Costo
* Precio
* Proveedor
* Estado
* Acciones

El dashboard debe incluir:

* Búsqueda por artículo.
* Búsqueda por SKU.
* Filtro por categoría.
* Filtro por proveedor.
* Filtro por estado de stock.

Ejemplo:

[ Buscar artículo / SKU ]

Categoría: [ Todas ]
Proveedor: [ Todos ]
Stock:     [ Todos ]

---

## SKU | Artículo | Stock | Costo | Proveedor | Acciones

3. SISTEMA DE EDICIÓN

---

El usuario debe poder seleccionar un artículo y abrir un formulario para visualizar y modificar su información.

El formulario debe permitir editar:

* SKU
* Nombre
* Categoría
* Descripción
* Peso
* Largo
* Ancho
* Alto
* Precio
* Costo
* Proveedor

Ejemplo:

EDITAR ARTÍCULO

SKU:          [ ABC-001       ]
Nombre:       [ Motor X       ]
Categoría:    [ Motores       ]
Peso:         [ 25.5          ]
Largo:        [ 50            ]
Ancho:        [ 30            ]
Alto:         [ 40            ]
Precio:       [ 850           ]
Costo:        [ 600           ]
Proveedor:    [ Proveedor ABC ]

```
          [ Cancelar ] [ Guardar ]
```

El botón GUARDAR debe actualizar realmente la información almacenada en Supabase.

El sistema debe permitir como mínimo:

* Crear artículos.
* Editar artículos.
* Eliminar artículos.
* Ver información de los artículos.
* Crear registros de inventario.
* Modificar información del inventario.

4. SISTEMA DE MOVIMIENTOS

---

El dashboard debe tener una sección específica para administrar los movimientos del inventario.

Debe permitir visualizar:

* Fecha.
* SKU.
* Artículo.
* Tipo de movimiento.
* Cantidad.
* Motivo.
* Estado.

Ejemplo:

[ + NUEVO MOVIMIENTO ]

---

## Fecha | SKU | Artículo | Tipo     | Cantidad | Estado

07/09 | A01 | Motor X  | ENTRADA  | 20       | Aprobado
07/09 | A02 | Cable Y  | SALIDA   | 5        | Pendiente
--------------------------------------------------------

## CREAR MOVIMIENTO

Al crear un movimiento se debe poder seleccionar:

Artículo:
[ Motor X ]

Tipo:

( ) Entrada
( ) Salida
( ) Ajuste

Cantidad:
[ 10 ]

Motivo:
[ Compra de mercadería ]

Notas:
[........................................]

[ Crear movimiento ]

5. BONUS — WORKFLOW DE APROBACIÓN

---

Esta es una funcionalidad adicional para los practicantes que quieran obtener puntos extra.

Los movimientos NO deberían modificar inmediatamente el stock.

El flujo esperado es:

Usuario
|
v
CREA MOVIMIENTO
|
v
PENDIENTE
|
+-------------------+
|                   |
v                   v
APROBAR             RECHAZAR
|                   |
v                   v
Actualiza           No modifica
inventario          inventario

## EJEMPLO

Stock actual:

Motor X
Stock: 100

Un usuario solicita:

Tipo: SALIDA
Cantidad: 20

El sistema registra:

Movimiento #125
Tipo: SALIDA
Cantidad: 20
Estado: PENDIENTE

El stock debe continuar siendo:

Stock: 100

Si un administrador presiona APROBAR:

Stock: 100
|
| -20
v
Stock: 80

El movimiento cambia a:

Estado: APROBADO

Si el administrador presiona RECHAZAR:

Estado: RECHAZADO

El stock permanece:

Stock: 100

6. PUNTUACIÓN

---

PUNTAJE BASE: 100 PUNTOS

Base de datos correctamente implementada       15 puntos

Relaciones entre tablas                         15 puntos

Dashboard funcional                             15 puntos

CRUD de artículos                               15 puntos

Gestión de inventario                            10 puntos

Registro de movimientos                          10 puntos

Diseño / UI / UX                                 10 puntos

Validaciones y manejo de errores                 10 puntos

TOTAL                                            100 puntos

BONUS: HASTA 20 PUNTOS ADICIONALES

Workflow de aprobación                           +10 puntos

Actualización automática del stock                +5 puntos

Buenas prácticas / seguridad / RLS                +5 puntos

PUNTAJE MÁXIMO                                   120 puntos

7. NIVELES DE EVALUACIÓN

---

NIVEL BÁSICO

La aplicación funciona y permite realizar las operaciones principales.

NIVEL INTERMEDIO

La aplicación funciona correctamente y las tablas y relaciones están bien implementadas.

NIVEL AVANZADO

La aplicación funciona, tiene validaciones, filtros, buen UX y maneja correctamente los movimientos.

NIVEL SOBRESALIENTE

La aplicación implementa workflow de aprobación, actualización correcta del stock, seguridad/RLS y manejo adecuado de errores.

8. RESTRICCIONES

---

NO se proporcionará el SQL completo de la base de datos.

El practicante debe interpretar los requerimientos y crear la estructura de Supabase.

Se permite utilizar:

* ChatGPT.
* Claude.
* Gemini.
* Cursor.
* GitHub Copilot.
* Otras herramientas de IA.
* Vibe Coding.

Sin embargo, el practicante debe poder explicar:

* Cómo funciona la base de datos.
* Cómo están relacionadas las tablas.
* Cómo se conecta el frontend con Supabase.
* Cómo funcionan las operaciones CRUD.
* Cómo se registra un movimiento.
* Cómo se actualiza el stock.
* Qué medidas de seguridad implementó.

9. TIEMPO

---

Tiempo recomendado de desarrollo:

6–8 HORAS

El objetivo no es solamente evaluar si el practicante puede producir una interfaz visualmente atractiva.

Se evaluará principalmente:

* Capacidad para entender requerimientos.
* Capacidad para estructurar una base de datos.
* Capacidad para conectar frontend y backend.
* Capacidad para resolver problemas.
* Capacidad para utilizar IA de manera efectiva.
* Capacidad para entender y modificar el código generado.
* Calidad del resultado final.
* Buenas prácticas de desarrollo.

10. ENTREGA

---

El practicante deberá entregar:

1. Link al proyecto funcionando.

2. Link o acceso al proyecto de Supabase.

3. Código fuente del proyecto.

4. README explicando:

   * Arquitectura.
   * Tablas.
   * Relaciones.
   * Funcionamiento.
   * Tecnologías utilizadas.
   * Funcionalidades implementadas.

5. Si implementó funcionalidades BONUS:

   * Explicar cómo funciona el workflow.
   * Explicar cómo se actualiza el stock.
   * Explicar las medidas de seguridad implementadas.

## OBJETIVO FINAL

El objetivo del test es identificar a los practicantes que no solamente pueden generar una interfaz bonita, sino que son capaces de construir un sistema funcional conectado a una base de datos real.

Se valorará especialmente la capacidad de convertir un requerimiento de negocio en:

REQUERIMIENTO
|
v
BASE DE DATOS
|
v
BACKEND / SUPABASE
|
v
FRONTEND
|
v
WORKFLOW
|
v
SISTEMA FUNCIONAL

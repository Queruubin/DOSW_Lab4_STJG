# 📄 Requerimientos del Sistema

## 1. Lista general de requerimientos

El sistema de Bankify tiene los siguientes requerimientos (descripción a alto nivel):

### 1.1 Requerimientos funcionales

El sistema de Bankify debe tener la capacidad de:

1.  [cite_start]Permitir la autenticación de usuarios (operadores y clientes) mediante usuario y contraseña[cite: 47].
2.  [cite_start]Permitir a los supervisores la gestión de clientes (crear, activar, inactivar y actualizar)[cite: 48].
3.  [cite_start]Permitir a los asesores la gestión de cuentas bancarias (crear, activar, inactivar y actualizar)[cite: 50].
4.  [cite_start]Permitir realizar depósitos a cuentas, tanto por el dueño de la cuenta como por usuarios externos[cite: 53].
5.  [cite_start]Permitir a los clientes consultar el saldo actual de sus cuentas[cite: 52].

### 1.2 Requerimientos no funcionales

El sistema de Bankify debe tener:

1.  [cite_start]Validación de cuentas: Los números deben tener exactamente 10 dígitos y no contener caracteres especiales[cite: 40].
2.  [cite_start]Regla de negocio: Los dos primeros dígitos deben corresponder al código de un banco registrado (ej. 01)[cite: 41].
3.  [cite_start]Interoperabilidad: Los reportes para la DIAN deben generarse en formato JSON[cite: 35].
4.  [cite_start]Portabilidad: Los reportes para los clientes deben generarse en formato PDF[cite: 35].
5.  [cite_start]Seguridad: Solo los usuarios con el rol de "Asesor" o "Supervisor" pueden realizar cambios en estados de cuentas o clientes[cite: 51].

## 2. Diagramas de caso de uso

### 2.1 Requerimiento Funcional 1

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-03 |
| **Nombre del requerimiento** | Gestión de Cuentas (Crear Cuenta) |
| **Descripción** | El sistema debe permitir registrar nuevas cuentas bancarias asociadas a un cliente, validando las reglas de negocio. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, Bankify debe tener previamente bancos registrados y un cliente activo. El Asesor debe estar logueado. |
| **Actor** | [cite_start]Asesor [cite: 51] |
| **Flujo principal** | 1. El Asesor selecciona la opción "Crear Cuenta".<br>2. El sistema solicita el número de cuenta y el cliente asociado.<br>3. El sistema valida que el número tenga 10 dígitos y el prefijo del banco sea correcto.<br>4. El sistema confirma la creación exitosa. |
| **Diagrama de caso de uso** | *(Pega aquí el enlace a tu imagen en /docs/uml/)* |
| **Poscondiciones** | Se espera como resultado que la cuenta quede registrada en el sistema con estado activo. |

### 2.2 Requerimiento Funcional 2

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-04 |
| **Nombre del requerimiento** | Realizar Depósito |
| **Descripción** | El sistema debe permitir el ingreso de dinero a una cuenta específica de forma controlada. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, la cuenta destino debe existir y estar activa en el sistema. |
| **Actor** | [cite_start]Cliente (Dueño) o Usuario Externo [cite: 53] |
| **Flujo principal** | 1. El actor solicita realizar un depósito.<br>2. El sistema pide el número de cuenta destino y el monto.<br>3. El sistema valida que la cuenta exista.<br>4. El sistema suma el monto al saldo y confirma la transacción. |
| **Diagrama de caso de uso** | *(Pega aquí el enlace a tu imagen en /docs/uml/)* |
| **Poscondiciones** | Se espera como resultado que el saldo de la cuenta destino aumente en el valor depositado. |

### 2.3 Requerimiento Funcional 3

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-05 |
| **Nombre del requerimiento** | Consulta de Saldo |
| **Descripción** | El sistema debe permitir a un cliente ver el dinero disponible en sus cuentas. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, el cliente debe haberse autenticado correctamente. |
| **Actor** | [cite_start]Cliente [cite: 52] |
| **Flujo principal** | 1. El Cliente selecciona la opción de ver saldo.<br>2. El sistema busca la información de la cuenta en base de datos.<br>3. El sistema muestra el saldo actual en pantalla. |
| **Diagrama de caso de uso** | *(Pega aquí el enlace a tu imagen en /docs/uml/)* |
| **Poscondiciones** | Se espera como resultado que el cliente conozca su saldo (el estado del sistema no cambia). |

## 3. Preguntas

**a. ¿Identifica algún requerimiento que deba detallarse más? ¿cuál (es)?**
Sí, el **RF-04 (Depósitos)**. No se especifica si hay topes máximos de dinero por transacción, ni si el sistema debe generar un comprobante digital de la transacción para el usuario externo.

**b. ¿Existen requerimientos que se contradigan entre sí? ¿cuál(es)?**
Podría haber conflicto entre la **Autenticación (RF-01)** y los **Depósitos (RF-04)**. El sistema exige autenticación general, pero permite que "otros usuarios" (externos) hagan depósitos. No queda claro si un usuario externo debe registrarse solo para depositar o si esa función es pública.

**c. Si tuviera que dar una prioridad a los requerimientos, ¿cuáles deberían ser los 2 más importantes?**
1.  **Gestión de Cuentas (RF-03):** Es el núcleo del negocio; sin cuentas creadas y validadas, no hay operaciones posibles.
2.  **Realizar Depósitos (RF-04):** Es la forma principal en que entra dinero al banco ("fondeo"), lo cual es crítico para una primera versión.

**d. ¿Existe algún requerimiento que no debería realizarse?**
No necesariamente eliminarse, pero la **Generación de Reportes PDF/JSON** podría posponerse para una segunda iteración, ya que no bloquea la operatividad básica (crear cuentas y mover dinero) de la versión MVP.
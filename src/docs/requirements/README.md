# 📄 Requerimientos del Sistema

## 1. Lista general de requerimientos

El sistema de Bankify tiene los siguientes requerimientos (descripción a alto nivel):

### 1.1 Requerimientos funcionales

El sistema de Bankify debe tener la capacidad de:

1.  Permitir la autenticación de usuarios (operadores y clientes) mediante usuario y contraseña.
2.  Permitir a los supervisores la gestión de clientes (crear, activar, inactivar y actualizar).
3.  Permitir a los asesores la gestión de cuentas bancarias (crear, activar, inactivar y actualizar).
4.  Permitir realizar depósitos a cuentas, tanto por el dueño de la cuenta como por usuarios externos.
5.  Permitir a los clientes consultar el saldo actual de sus cuentas.

### 1.2 Requerimientos no funcionales

El sistema de Bankify debe tener:

1.  Validación: Los números de cuenta deben tener exactamente 10 dígitos y no contener caracteres especiales.
2.  Regla de Negocio: Los dos primeros dígitos de la cuenta deben corresponder a un banco registrado.
3.  Interoperabilidad: Los reportes para la DIAN deben generarse en formato JSON.
4.  Portabilidad: Los reportes para los clientes deben generarse en formato PDF.
5.  Usabilidad: La interfaz debe ser intuitiva para operaciones simples.

## 2. Diagramas de caso de uso

### 2.1 Requerimiento Funcional 1

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-03 |
| **Nombre del requerimiento** | Gestión de Cuentas (Crear Cuenta) |
| **Descripción** | El sistema debe permitir registrar nuevas cuentas bancarias asociadas a un cliente. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, Bankify debe tener bancos registrados y el cliente debe existir. El Asesor debe estar logueado. |
| **Actor** | Asesor |
| **Flujo principal** | 1. El Asesor selecciona la opción "Crear Cuenta".<br>2. El sistema solicita los datos (número, cliente).<br>3. El sistema valida longitud (10 dígitos) y prefijo bancario.<br>4. El sistema confirma la creación. |
| **Diagrama de caso de uso** | *(Pega aquí tu imagen/link de la carpeta uml)* |
| **Poscondiciones** | Se espera como resultado que la cuenta quede registrada y activa en el sistema. |

### 2.2 Requerimiento Funcional 2

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-04 |
| **Nombre del requerimiento** | Realizar Depósito |
| **Descripción** | El sistema debe permitir ingresar dinero a una cuenta de forma controlada. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, la cuenta destino debe existir y estar activa. |
| **Actor** | Cliente (Propietario) o Usuario Externo |
| **Flujo principal** | 1. El actor selecciona depositar dinero.<br>2. El sistema pide el número de cuenta y el monto.<br>3. El sistema valida que la cuenta exista.<br>4. El sistema suma el monto al saldo y confirma. |
| **Diagrama de caso de uso** | *(Pega aquí tu imagen/link de la carpeta uml)* |
| **Poscondiciones** | Se espera como resultado que el saldo de la cuenta aumente en el valor depositado. |

### 2.3 Requerimiento Funcional 3

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-05 |
| **Nombre del requerimiento** | Consulta de Saldo |
| **Descripción** | El sistema debe permitir a un cliente ver su dinero disponible. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, el cliente debe haberse autenticado correctamente. |
| **Actor** | Cliente |
| **Flujo principal** | 1. El Cliente selecciona la opción de ver saldo.<br>2. El sistema recupera la información de la base de datos.<br>3. El sistema muestra el saldo en pantalla. |
| **Diagrama de caso de uso** | *(Pega aquí tu imagen/link de la carpeta uml)* |
| **Poscondiciones** | Se espera como resultado que el cliente visualice su saldo (el estado del sistema no cambia). |

## 3. Preguntas

**a. ¿Identifica algún requerimiento que deba detallarse más? ¿cuál (es)?**
Sí, el **RF-04 (Depósitos)**. No se especifica si hay topes máximos de dinero por transacción, ni si se requiere comprobante.

**b. ¿Existen requerimientos que se contradigan entre sí? ¿cuál(es)?**
Posiblemente **Autenticación (RF-01)** vs **Depósitos (RF-04)**. Si un externo deposita, ¿debe loguearse? El RF-01 dice que el sistema requiere usuario y contraseña, pero el depósito externo suele ser público.

**c. Si tuviera que dar una prioridad a los requerimientos, ¿cuáles deberían ser los 2 más importantes?**
1. **RF-03 Gestión de Cuentas:** Sin cuentas no hay banco.
2. **RF-04 Realizar Depósitos:** Es necesario para que entre dinero al sistema.

**d. ¿Existe algún requerimiento que no debería realizarse?**
Los reportes (PDF/JSON) podrían posponerse para una segunda fase, ya que no son vitales para la operación básica de cuentas.
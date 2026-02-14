# Requerimientos del Sistema

## 1. Lista general de requerimientos

El sistema de Bankify tiene los siguientes requerimientos (descripción a alto nivel):

### 1.1 Requerimientos funcionales

El sistema de Bankify debe tener la capacidad de:

1.  Permitir la autenticación de usuarios y clientes mediante credenciales (RF-01).
2.  Permitir a los supervisores la gestión de clientes (crear, inactivar, actualizar) (RF-02).
3.  Permitir a los asesores la gestión de cuentas bancarias (crear, inactivar, actualizar) (RF-03).
4.  Permitir realizar depósitos a cuentas, tanto por el titular como por terceros (RF-04).
5.  Permitir a los clientes consultar el saldo disponible en sus cuentas (RF-05).

### 1.2 Requerimientos no funcionales

El sistema de Bankify debe tener:

1.  Validación de longitud: Los números de cuenta deben tener exactamente 10 dígitos.
2.  Regla de Negocio: Los dos primeros dígitos deben corresponder al código de un banco registrado (ej. 01).
3.  Seguridad: Las contraseñas no deben guardarse en texto plano.
4.  Interoperabilidad: Los reportes para la DIAN deben generarse en formato JSON.
5.  Portabilidad: Los reportes para clientes deben generarse en formato PDF.

## 2. Diagramas de caso de uso

### 2.1 Requerimiento Funcional 1

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-03 |
| **Nombre del requerimiento** | Gestión de Cuentas (Crear Cuenta) |
| **Descripción** | El sistema debe permitir registrar nuevas cuentas bancarias asociadas a un cliente, validando las reglas de negocio. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, el cliente debe existir y el asesor debe estar autenticado. |
| **Actor** | Asesor |
| **Flujo principal** | 1. El Asesor selecciona la opción "Crear Cuenta".<br>2. El sistema solicita datos (número, cliente).<br>3. El sistema valida longitud y prefijo.<br>4. El sistema confirma la creación. |
| **Diagrama de caso de uso** | [Inserte imagen del diagrama aquí] |
| **Poscondiciones** | Se espera como resultado que la cuenta quede activa en el sistema. |

### 2.2 Requerimiento Funcional 2

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-04 |
| **Nombre del requerimiento** | Realizar Depósito |
| **Descripción** | El sistema debe permitir el ingreso de dinero a una cuenta específica de forma controlada. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, la cuenta destino debe existir y estar activa. |
| **Actor** | Cliente (Propietario) o Usuario Externo |
| **Flujo principal** | 1. El actor solicita depositar e ingresa cuenta y monto.<br>2. El sistema valida que la cuenta exista.<br>3. El sistema suma el monto al saldo actual.<br>4. El sistema confirma la transacción exitosa. |
| **Diagrama de caso de uso** | [Inserte imagen del diagrama aquí] |
| **Poscondiciones** | Se espera como resultado que el saldo de la cuenta aumente. |

### 2.3 Requerimiento Funcional 3

| Campo | Descripción |
| :--- | :--- |
| **ID** | RF-05 |
| **Nombre del requerimiento** | Consulta de Saldo |
| **Descripción** | El sistema debe permitir a un cliente ver el dinero disponible en sus cuentas. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, el cliente debe haberse autenticado correctamente. |
| **Actor** | Cliente |
| **Flujo principal** | 1. El Cliente selecciona la opción de ver saldo.<br>2. El sistema busca la información en la base de datos.<br>3. El sistema muestra el saldo en pantalla. |
| **Diagrama de caso de uso** | [Inserte imagen del diagrama aquí] |
| **Poscondiciones** | Se espera como resultado que el cliente conozca su saldo (el estado no cambia). |

## 3. Preguntas

**a. ¿Identifica algún requerimiento que deba detallarse más? ¿cuál (es)?**
Sí, el **RF-04 (Depósitos)**. No se especifica si hay topes máximos de dinero por transacción, ni si el sistema debe generar un comprobante digital obligatorio.

**b. ¿Existen requerimientos que se contradigan entre sí? ¿cuál(es)?**
Potencialmente **Autenticación (RF-01)** vs **Depósitos (RF-04)**. Si un externo deposita, ¿debe loguearse? El sistema exige autenticación general, pero permite depósitos de terceros, lo cual suele ser una función pública en cajeros/corresponsales.

**c. Si tuviera que dar una prioridad a los requerimientos, ¿cuáles deberían ser los 2 más importantes?**
1. **Gestión de Cuentas (RF-03):** Es el núcleo del negocio; sin cuentas, no hay banco.
2. **Realizar Depósitos (RF-04):** Es crítico para el fondeo de las cuentas y la operación financiera inicial.

**d. ¿Existe algún requerimiento que no debería realizarse?**
La generación de reportes (PDF/JSON) podría posponerse para una segunda fase (iteración), ya que no bloquea la operatividad básica transaccional.
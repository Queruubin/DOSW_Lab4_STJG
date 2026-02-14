# 📄 Requerimientos del Sistema

## 1. Lista general de requerimientos

El sistema de Bankify tiene los siguientes requerimientos (descripción a alto nivel):

### 1.1 Requerimientos funcionales
El sistema de Bankify debe tener la capacidad de:

1. [cite_start]**RF-01 Autenticación:** Permitir el acceso mediante usuario y contraseña para operadores y clientes[cite: 47].
2. [cite_start]**RF-02 Gestión de Clientes:** Permitir a los supervisores crear, activar, inactivar y actualizar la información de los clientes[cite: 48].
3. [cite_start]**RF-03 Gestión de Cuentas:** Permitir a los asesores crear, activar, inactivar y actualizar cuentas bancarias[cite: 50].
4. [cite_start]**RF-04 Transacciones de Depósito:** Permitir realizar depósitos de dinero a una cuenta, tanto por el propietario como por terceros[cite: 53].
5. [cite_start]**RF-05 Consulta de Saldo:** Permitir a los clientes consultar el saldo actual de sus cuentas registradas[cite: 52].

### 1.2 Requerimientos no funcionales
El sistema de Bankify debe tener:

1. [cite_start]**RNF-01 Integridad de Datos:** Los números de cuenta deben tener exactamente 10 dígitos numéricos y no incluir caracteres especiales[cite: 40].
2. [cite_start]**RNF-02 Regla de Negocio Bancaria:** Los dos primeros dígitos de la cuenta deben corresponder a un banco registrado (ej: 01->Bancolombia)[cite: 41].
3. [cite_start]**RNF-03 Interoperabilidad (DIAN):** Los reportes tributarios para la DIAN deben generarse exclusivamente en formato JSON[cite: 35].
4. [cite_start]**RNF-04 Portabilidad (Clientes):** Los reportes tributarios para los clientes deben generarse en formato PDF[cite: 35].
5. [cite_start]**RNF-05 Usabilidad:** La interfaz debe permitir realizar operaciones simples de forma intuitiva para clientes finales[cite: 29].

## 2. Diagramas de caso de uso

### 2.1 Requerimiento Funcional 1: Gestión de Cuentas (Crear)

| Campo | Descripción |
|---|---|
| **ID** | RF-03 |
| **Nombre del requerimiento** | Gestión de Cuentas (Crear Cuenta) |
| **Descripción** | El sistema debe permitir registrar nuevas cuentas bancarias asociadas a un cliente. |
| **Precondiciones** | El cliente debe estar previamente registrado y activo en el sistema. El asesor debe estar autenticado. |
| **Actor** | Asesor |
| **Flujo principal** | 1. El Asesor selecciona la opción de "Crear Nueva Cuenta".<br>2. El sistema solicita los datos de la cuenta (número, tipo).<br>3. El Asesor ingresa la información.<br>4. El sistema valida que el número tenga 10 dígitos y el prefijo bancario sea correcto.<br>5. El sistema confirma la creación de la cuenta. |
| **Diagrama de caso de uso** | *(Debes subir tu imagen a docs/uml y poner el link aquí. Ej: `![Diagrama RF03](../uml/rf03_diagram.png)`)* |
| **Poscondiciones** | La cuenta queda registrada en estado "Activa" o "Pendiente". |

### 2.2 Requerimiento Funcional 2: Realizar Depósito

| Campo | Descripción |
|---|---|
| **ID** | RF-04 |
| **Nombre del requerimiento** | Realizar Depósito |
| **Descripción** | El sistema debe permitir ingresar dinero a una cuenta específica de forma controlada. |
| **Precondiciones** | La cuenta destino debe existir y estar activa. |
| **Actor** | Cliente (Propietario) / Usuario Externo |
| **Flujo principal** | 1. El Actor selecciona la opción "Depositar".<br>2. El sistema solicita el número de cuenta destino y el monto.<br>3. El Actor ingresa los datos.<br>4. El sistema verifica que la cuenta exista y sea válida.<br>5. El sistema suma el monto al saldo actual y confirma la transacción. |
| **Diagrama de caso de uso** | *(Inserta tu link de imagen aquí)* |
| **Poscondiciones** | El saldo de la cuenta destino aumenta en el valor depositado. |

### 2.3 Requerimiento Funcional 3: Consulta de Saldo

| Campo | Descripción |
|---|---|
| **ID** | RF-05 |
| **Nombre del requerimiento** | Consulta de Saldo |
| **Descripción** | El sistema debe mostrar la información financiera actual de la cuenta del cliente. |
| **Precondiciones** | El cliente debe estar autenticado en el sistema. |
| **Actor** | Cliente |
| **Flujo principal** | 1. El Cliente selecciona la cuenta que desea consultar.<br>2. El sistema recupera la información financiera de la base de datos.<br>3. El sistema muestra en pantalla el saldo disponible. |
| **Diagrama de caso de uso** | *(Inserta tu link de imagen aquí)* |
| **Poscondiciones** | Ninguna (el estado del sistema no cambia). |

## 3. Preguntas

**a. ¿Identifica algún requerimiento que deba detallarse más? ¿cuál (es)?**
Sí, el requerimiento de "Realizar depósitos" (RF-04). No se especifica si hay límites máximos o mínimos de dinero por transacción, ni si se requiere algún tipo de soporte o comprobante de la transacción.

**b. ¿Existen requerimientos que se contradigan entre sí? ¿cuál(es)?**
Potencialmente el de "Depósitos por otros usuarios" vs "Autenticación". Si un usuario externo (no cliente) quiere depositar, ¿necesita credenciales? El sistema dice que requiere autenticación (RF-01), pero los depósitos pueden ser hechos por terceros (RF-04), lo cual podría generar conflicto si no se define un acceso público limitado.

**c. Si tuviera que dar una prioridad a los requerimientos, ¿cuáles deberían ser los 2 más importantes?**
1. **Gestión de Cuentas (RF-03):** Sin cuentas creadas y validadas, el negocio no existe.
2. **Realizar Depósitos (RF-04):** Es la funcionalidad principal para que el dinero ingrese al sistema y el modelo de negocio funcione.
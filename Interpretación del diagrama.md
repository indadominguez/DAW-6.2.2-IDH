# Interpretación del diagrama
El diagrama muestra el proceso completo de validación del usuario cuando inserta su tarjeta en el cajero automático, ingresando su PIN y seleccionando la opción de sacar dinero. Incluye las verificaciones de la autenticidad de la tarjeta, la validez del PIN y la disponibilidad de saldo.

## Descripción de Elementos
- Usuario: Interactúa con el cajero.
- Interfaz_Cajero: Muestra mensajes y recibe del usuario.
- Control_Validacion: Gestiona la autenticidad de la tarjeta y la validación del PIN.
- Control_Transaccion: Procesa los retiros de dinero.
- Tarjeta: Representa la información de la tarjeta insertada.
- Cuenta: Contiene el saldo y la información asociada a la tarjeta.

## Interpretación del diagrama
**1. Inserción de la Tarjeta:**
- El usuario inserta la tarjeta.
- La interfaz envía la solicitud para verificar la tarjeta.
  
**2. Verificación de la Tarjeta:**
- Solicita validar la autenticidad de la tarjeta.
  La tarjeta puede ser válida o inválida.
- Si la tarjeta es inválida:
  - Termina el proceso.
- Si la tarjeta es válida:
  - Solicita al usuario que ingrese el PIN.
    
**3. Ingreso y Verificación del PIN:**
- Loop Hasta 3 Intentos:
  - Ingresa el PIN.
  - Solicita la verificación del PIN.
  - Valida el PIN ingresado.
  - Puede ser correcto o incorrecto.
- Si el PIN es incorrecto:
  - Permite reintentar hasta 3 veces.
- Si los intentos se exceden:
  - Finaliza la sesión.
    
**4. Selección de Operaciones:**
- Si el PIN es correcto:
  - Menú de Operaciones.
  - Selecciona la opción.

**5. Procesamiento de la Transacción:**
- Solicita el procesamiento del retiro.
- Verifica si hay suficiente saldo.
- Saldo suficiente o Saldo insuficiente.
  
**6. Resultado de la Transacción:**
- Si hay saldo suficiente:
  - Realiza el retiro y confirma la operación.
  - Entrega el dinero.
- Si hay saldo insuficiente:
  - Permite elegir otra operación o finalizar.
    
**7. Fin de la Operación:**
- Solicita retirar la tarjeta.
  - El flujo termina y el sistema vuelve al estado inicial.

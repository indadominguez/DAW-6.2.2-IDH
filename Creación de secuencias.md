# Creación de Secuencias
## Clases Estereotipadas a partir de los casos de uso (CU: Sacar dinero y CU: Validación usuario)
**Interfaces:**

- Interfaz_Cajero (Interfaz gráfica del cajero para el usuario).

**Control:**

- Control_Transaccion (Gestiona las operaciones de transacción).
- Control_Validacion (Gestiona la autenticación del usuario).

**Entidad:**

- Tarjeta (Entidad que representa la tarjeta del usuario).
- Cuenta (Entidad que representa la cuenta bancaria asociada).

## Diagrama de Secuencias Básico
- He buscado una manera de poder poner el código mucho más correcto en md, para que se entienda mejor a la hora de ver que hace cada paso
```plantuml
@startuml
actor Usuario
boundary Interfaz_Cajero
control Control_Validacion
control Control_Transaccion
entity Tarjeta
entity Cuenta

Usuario -> Interfaz_Cajero: Insertar Tarjeta
Interfaz_Cajero -> Control_Validacion: Verificar Tarjeta
Control_Validacion -> Tarjeta: Validar Autenticidad
Tarjeta --> Control_Validacion: Respuesta (Válida o Inválida)

alt Tarjeta Válida
Interfaz_Cajero -> Usuario: Solicitar PIN
Usuario -> Interfaz_Cajero: Ingresar PIN
Interfaz_Cajero -> Control_Validacion: Verificar PIN
Control_Validacion -> Tarjeta: Validar PIN
Tarjeta --> Control_Validacion: Respuesta (Correcto o Incorrecto)

alt PIN Correcto  
    Interfaz_Cajero -> Usuario: Mostrar Menú de Operaciones  
    Usuario -> Interfaz_Cajero: Seleccionar Sacar Dinero  
    Interfaz_Cajero -> Control_Transaccion: Procesar Retiro  
    Control_Transaccion -> Cuenta: Verificar Saldo  
    Cuenta --> Control_Transaccion: Respuesta (Suficiente o Insuficiente)  
    
    alt Saldo Suficiente  
        Control_Transaccion -> Cuenta: Realizar Retiro  
        Cuenta --> Control_Transaccion: Confirmación  
        Control_Transaccion -> Interfaz_Cajero: Entregar Dinero  
    else Saldo Insuficiente  
        Interfaz_Cajero -> Usuario: Saldo Insuficiente  
    end  

else PIN Incorrecto  
    Interfaz_Cajero -> Usuario: PIN Incorrecto  
end  
else Tarjeta Inválida
Interfaz_Cajero -> Usuario: Tarjeta Inválida
end

Interfaz_Cajero -> Usuario: Retirar Tarjeta
@enduml
```

![image](https://github.com/user-attachments/assets/67b1ef72-1468-424d-a2bc-f92aea133daa)

## Diagrama de Secuencia Final
```plantuml
@startuml
actor Usuario
boundary Interfaz_Cajero
control Control_Validacion
control Control_Transaccion
entity Tarjeta
entity Cuenta

Usuario -> Interfaz_Cajero: Insertar Tarjeta
Interfaz_Cajero -> Control_Validacion: Verificar Tarjeta
Control_Validacion -> Tarjeta: Validar Autenticidad
Tarjeta --> Control_Validacion: Respuesta (Válida o Inválida)

alt Tarjeta Válida
Interfaz_Cajero -> Usuario: Solicitar PIN
loop Hasta 3 Intentos
Usuario -> Interfaz_Cajero: Ingresar PIN
Interfaz_Cajero -> Control_Validacion: Verificar PIN
Control_Validacion -> Tarjeta: Validar PIN
Tarjeta --> Control_Validacion: Respuesta (Correcto o Incorrecto)

    alt PIN Correcto  
        Interfaz_Cajero -> Usuario: Mostrar Menú de Operaciones  
        Usuario -> Interfaz_Cajero: Seleccionar Sacar Dinero  
        Interfaz_Cajero -> Control_Transaccion: Procesar Retiro  
        Control_Transaccion -> Cuenta: Verificar Saldo  
        Cuenta --> Control_Transaccion: Respuesta (Suficiente o Insuficiente)  
        
        alt Saldo Suficiente  
            Control_Transaccion -> Cuenta: Realizar Retiro  
            Cuenta --> Control_Transaccion: Confirmación  
            Control_Transaccion -> Interfaz_Cajero: Entregar Dinero  
        else Saldo Insuficiente  
            Interfaz_Cajero -> Usuario: Saldo Insuficiente  
        end  
        break  
    else PIN Incorrecto  
        Interfaz_Cajero -> Usuario: PIN Incorrecto  
    end  
end  

alt Intentos Excedidos  
    Interfaz_Cajero -> Usuario: Tarjeta Bloqueada  
end  
else Tarjeta Inválida
Interfaz_Cajero -> Usuario: Tarjeta Inválida
end

Interfaz_Cajero -> Usuario: Retirar Tarjeta
@enduml
```
![image](https://github.com/user-attachments/assets/f2385401-2705-45cc-aeb4-cd48010494b8)

# 06. Drivers arquitectónicos

Un driver se selecciona porque modifica la estructura, las dependencias o una decisión relevante. No todos los requisitos funcionales necesitan convertirse en drivers.

| ID | Driver | Origen trazable | Decisión de arquitectura | Compromiso o validación |
|---|---|---|---|---|
| DA01 | Soportar crecimiento durante campañas. | AC03 | Backend sin estado exclusivo de instancia; sesiones y carritos persistentes; posibilidad de varias instancias. | Mayor costo y presión sobre base de datos; validar con carga. |
| DA02 | Mantener tiempos de respuesta con concurrencia. | AC01, RF01, RF04 | Paginación, índices y consultas acotadas; llamadas externas fuera de transacciones de compra. | Medir antes de introducir caché. |
| DA03 | Proteger cuentas, datos y operaciones. | AC04, RF08, RF10, RF15 | Usuarios controla identidad y roles; cada módulo verifica propiedad; auditoría crítica. | Probar autorización por recurso, no solo ocultar botones. |
| DA04 | Procesar pagos externos confiablemente. | RC04, RF09, AC06 | Adaptador de pago, idempotencia, notificaciones verificadas y conciliación. | La transacción local no abarca al proveedor; manejar estados intermedios. |
| DA05 | Comunicar web y backend mediante REST. | RC01, RC03 | API en presentación que valida y delega casos de uso. | No exponer consultas directas a la base. |
| DA06 | Facilitar mantenimiento con tres capas. | RC06, AC05, DP01 | Monolito modular con presentación → negocio → datos; proveedores detrás de adaptadores. | Se despliega como una unidad inicial; los módulos no son microservicios. |
| DA07 | Evitar sobreventa y mantener pedidos coherentes. | RF05, RF14, RF16, AC06, DP03 | Transacción local de pedido y reservas, versión de stock y conciliación ERP. | El ERP multicanal requiere un contrato adicional. |
| DA08 | Conservar operación ante fallos de envío o facturación. | RC05, RC08, RF12, RF13, AC02 | Estados separados, tareas persistentes y reintentos idempotentes. | Consistencia eventual; pueden verse estados pendientes. |

**Prioridad propuesta:** DA03, DA04 y DA07 protegen la compra; DA05 y DA06 determinan la estructura obligatoria; DA01, DA02 y DA08 guían capacidad y recuperación. Todos aparecen en la [arquitectura inicial](../arquitectura/arquitectura-inicial.md).

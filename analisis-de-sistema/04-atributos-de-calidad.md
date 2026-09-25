# 04. Atributos de calidad

Escenario central: una campaña aumenta las consultas y compras simultáneas. Las cifras son **metas propuestas para validar**, no mediciones de una aplicación existente. Deben ajustarse con el negocio y el presupuesto.

| ID | Atributo | Estímulo y entorno | Respuesta y medida propuesta | Verificación prevista |
|---|---|---|---|---|
| AC01 | Rendimiento | 300 usuarios concurrentes consultan 10 000 productos y modifican carritos durante 15 minutos. | Percentil 95 de catálogo y carrito ≤ 2 s, con menos del 1 % de errores internos. Los proveedores externos se miden aparte. | Prueba de carga con 80 % de consultas y 20 % de cambios de carrito. |
| AC02 | Disponibilidad | Falla temporalmente facturación o envío durante una campaña. | El catálogo continúa y los pedidos pagados conservan su estado; las tareas fallidas quedan pendientes. Meta mensual del servicio propio: 99,5 % de sondas exitosas cada minuto. | Sondas de salud y prueba de indisponibilidad de cada proveedor. |
| AC03 | Escalabilidad | La concurrencia crece de 300 a 600 usuarios con la misma mezcla de operaciones. | Con dos instancias de backend, sostener p95 ≤ 2 s y errores internos < 1 %, si la base de datos tiene capacidad. | Comparar ambas configuraciones y reportar límites de CPU, conexiones y base. |
| AC04 | Seguridad | Un cliente o seller intenta usar recursos ajenos, o llega una notificación de pago inválida. | Rechazar el 100 % de casos de la matriz de pruebas sin devolver datos ni cambiar estados; auditar sin secretos. | Pruebas por rol, propietario, sesión ausente y firma inválida. |
| AC05 | Mantenibilidad | Se sustituye el proveedor de envío. | El cambio se limita al adaptador, configuración y pruebas de contrato; no modifica catálogo, carrito ni web si el contrato interno se mantiene. | Revisión de dependencias y pruebas con dos adaptadores simulados. |
| AC06 | Consistencia | Dos clientes compran la última unidad y la pasarela repite su notificación. | Solo una reserva obtiene la unidad; stock ≥ 0; cada pago se aplica una vez y produce como máximo una solicitud lógica de comprobante. | Prueba concurrente y repetición de eventos con fallos intermedios. |

## Consecuencias para el diseño

- AC01: paginación, índices y consultas acotadas; estudiar caché solo si las mediciones lo requieren.
- AC02: timeouts, tareas persistentes y reintentos controlados para servicios externos.
- AC03: sesión y carrito fuera de la memoria exclusiva de una instancia.
- AC04: autenticación, autorización por propiedad, cifrado en tránsito y minimización de datos.
- AC05: límites entre capas y contratos para proveedores.
- AC06: transacciones locales, actualizaciones condicionadas de stock e idempotencia.

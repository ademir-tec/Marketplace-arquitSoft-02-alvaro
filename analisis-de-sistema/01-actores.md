# 01. Actores del sistema

Un actor es una persona o sistema externo que interactúa con el marketplace. Los módulos internos y la base de datos no son actores.

| ID | Actor | Tipo | Necesidades e interacción | Límite de acceso |
|---|---|---|---|---|
| ACT01 | Cliente | Humano | Buscar productos, consultar información y stock, gestionar carrito, registrar dirección, comprar, pagar y consultar pedidos y comprobantes. | Solo modifica su carrito y consulta sus propias compras y datos. |
| ACT02 | Seller | Humano | Registrar, actualizar y consultar sus productos; mantener stock cuando no lo administra un ERP; consultar sus ventas y preparar entregas. | Solo accede a productos y líneas de venta que le pertenecen. |
| ACT03 | Administrador | Humano | Registrar, actualizar, habilitar y desactivar sellers; supervisar cuentas y actividad de la plataforma. | Sus acciones administrativas deben estar autorizadas y auditadas. |
| ACT04 | Pasarela de pago | Sistema externo | Recibir solicitudes de pago, procesar operaciones y notificar su resultado. | Intercambia identificadores, importe, moneda y estados; no recibe acceso general a pedidos. |
| ACT05 | Servicio de envío | Sistema externo | Registrar entregas y proporcionar identificadores de seguimiento y estados. | Recibe únicamente los datos necesarios para entregar el pedido. |
| ACT06 | Servicio de facturación | Sistema externo | Generar comprobantes de pedidos pagados y devolver su referencia. | Recibe los datos fiscales y de compra necesarios para emitir el comprobante. |
| ACT07 | ERP | Sistema externo | Proporcionar información de productos y stock de sellers integrados. | La sincronización se limita al seller y sus productos. |

Los siete actores aparecen en el ejercicio 03. La profundidad técnica de facturación y ERP no está definida en la guía; esta propuesta documenta responsabilidades iniciales sin seleccionar proveedores.

Un visitante puede explorar el catálogo sin iniciar sesión. Para la primera versión se propone exigir una cuenta de cliente al confirmar un pedido. Cliente, seller y administrador son roles; la autorización debe verificarse en el backend.

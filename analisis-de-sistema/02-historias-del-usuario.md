# 02. Historias de usuario

HU01–HU06 mantienen las necesidades del ejemplo de la guía. HU07–HU13 completan las interacciones identificadas en el caso. Los criterios son condiciones propuestas para poder verificar cada historia durante la implementación.

| ID | Historia de usuario | Criterios de aceptación |
|---|---|---|
| HU01 | Como cliente, quiero buscar y consultar productos, para encontrar el producto que necesito. | Al buscar por nombre o categoría se muestran coincidencias activas; el detalle incluye seller, precio y disponibilidad; si no hay resultados se informa sin error. |
| HU02 | Como seller, quiero registrar y gestionar mis productos, para ofrecerlos a los clientes. | Un seller habilitado registra productos con nombre, categoría y precio positivo; puede actualizar y listar únicamente sus productos; el stock nunca es negativo. |
| HU03 | Como cliente, quiero gestionar los productos de mi carrito, para preparar los productos que deseo comprar. | Puede agregar, cambiar cantidad o eliminar líneas; las cantidades son positivas; se recalcula el total y se informa que agregar al carrito no reserva stock. |
| HU04 | Como cliente, quiero realizar un pedido con los productos de mi carrito, para completar mi compra. | Se exige dirección válida y carrito no vacío; se revalidan precios y stock; se genera un identificador y se conserva el detalle por seller; si falla la reserva no se inicia el pago. |
| HU05 | Como administrador, quiero gestionar los sellers de la plataforma, para administrar a los vendedores registrados. | Puede registrar, actualizar y desactivar sellers; un seller desactivado no publica ni recibe nuevas compras; sus pedidos previos se conservan. |
| HU06 | Como cliente, quiero consultar mis pedidos y su estado, para conocer el estado de mis compras. | Se listan solo sus pedidos; el detalle muestra líneas, importes, pago y entregas; no puede abrir pedidos ajenos cambiando un identificador. |
| HU07 | Como cliente, quiero pagar mi pedido mediante una pasarela externa, para confirmar mi compra de forma segura. | El importe proviene del pedido; el resultado se verifica con el proveedor; una notificación repetida no duplica el pago ni sus efectos; un rechazo se informa al cliente. |
| HU08 | Como cliente, quiero registrarme e iniciar sesión, para acceder a mis compras de forma personal. | Se rechaza un correo duplicado; credenciales inválidas no inician sesión; el registro público no permite asignarse el rol administrador o seller. |
| HU09 | Como seller, quiero consultar mis ventas y registrar su preparación, para atender los pedidos que me corresponden. | Solo ve sus líneas de pedidos pagados y datos de entrega necesarios; marca preparación sin modificar líneas de otro seller; no puede marcar un pedido como pagado. |
| HU10 | Como cliente, quiero consultar el seguimiento de mis entregas, para conocer el avance del envío. | Un pedido puede mostrar varios envíos; cada uno incluye seller, estado y referencia; una demora del proveedor no borra el último estado conocido. |
| HU11 | Como cliente, quiero consultar el comprobante de mi compra, para contar con una constancia del pago. | Se solicita después del pago confirmado; se muestra el comprobante disponible o emisión pendiente; no se emite otra vez por recibir el mismo evento. |
| HU12 | Como seller integrado con un ERP, quiero sincronizar mis productos y stock, para mantener actualizada mi oferta. | Se valida la identidad del seller y el formato; una repetición no crea otro producto; una actualización antigua no reemplaza una versión reciente. |
| HU13 | Como administrador, quiero consultar el registro de acciones críticas, para investigar cambios e incidencias. | Se registra quién, qué recurso, cuándo y resultado en cambios de sellers, pagos y stock; solo usuarios autorizados consultan la auditoría. |

Las historias de integración se expresan desde el beneficiario humano. Los sistemas externos participan como actores de soporte y no toman decisiones de negocio del marketplace.

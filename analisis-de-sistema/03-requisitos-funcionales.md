# 03. Requisitos funcionales

Cada requisito describe una función del sistema. Los permisos y controles también forman parte del comportamiento verificable.

| ID | Requisito funcional | Historia de origen | Módulo responsable |
|---|---|---|---|
| RF01 | Permitir buscar productos activos por nombre y categoría, con resultados paginados. | HU01 | Catálogo |
| RF02 | Mostrar nombre, descripción, categoría, precio, seller y disponibilidad del producto. | HU01 | Catálogo |
| RF03 | Permitir a sellers habilitados registrar, listar y actualizar sus productos y, cuando corresponda, su stock manual. | HU02 | Catálogo |
| RF04 | Permitir agregar, modificar cantidades y eliminar líneas del carrito, calculando su total. | HU03 | Carrito |
| RF05 | Crear un pedido desde el carrito, validar dirección, recalcular importes y conservar precio y seller de cada línea. | HU04 | Pedidos |
| RF06 | Listar los pedidos del cliente autenticado y mostrar sus estados. | HU06 | Pedidos |
| RF07 | Permitir al administrador registrar, actualizar, habilitar y desactivar sellers, conservando su historial de ventas. | HU05 | Sellers |
| RF08 | Mostrar el detalle de un pedido solo a su cliente, al administrador autorizado y, limitado a sus líneas, al seller correspondiente. | HU04, HU06, HU09 | Pedidos |
| RF09 | Iniciar el pago de un pedido mediante la pasarela y verificar resultado, importe, moneda e identificador antes de actualizarlo. | HU07 | Pedidos |
| RF10 | Registrar clientes, autenticar usuarios y aplicar permisos por rol y propiedad del recurso. | HU08 | Usuarios |
| RF11 | Permitir a un seller consultar sus ventas pagadas y registrar la preparación de sus líneas. | HU09 | Pedidos |
| RF12 | Solicitar el envío de cada grupo de líneas preparado, guardar su referencia y actualizar su seguimiento. | HU09, HU10 | Pedidos |
| RF13 | Solicitar un comprobante tras confirmar el pago y permitir al cliente consultar su referencia o estado. | HU11 | Pedidos |
| RF14 | Sincronizar productos y stock con el ERP del seller integrado, validando versiones y registrando el resultado. | HU12 | Catálogo |
| RF15 | Registrar y permitir consultar, con autorización administrativa, acciones críticas sobre sellers, pagos y stock. | HU13 | Usuarios y módulos emisores |
| RF16 | Reservar stock al crear el pedido, consumir la reserva al confirmar el pago y liberarla ante rechazo definitivo o vencimiento. | HU04, HU07 | Catálogo y Pedidos |

## Relación de historias y requisitos

| Historia | Requisitos relacionados |
|---|---|
| HU01 | RF01, RF02 |
| HU02 | RF03 |
| HU03 | RF04 |
| HU04 | RF05, RF08, RF16 |
| HU05 | RF07 |
| HU06 | RF06, RF08 |
| HU07 | RF09, RF16 |
| HU08 | RF10 |
| HU09 | RF08, RF11, RF12 |
| HU10 | RF12 |
| HU11 | RF13 |
| HU12 | RF14 |
| HU13 | RF15 |

## Reglas propuestas para el flujo de compra

1. Los precios y permisos se validan en el backend; no se confía en valores enviados por el navegador.
2. El carrito no reserva inventario. La confirmación revalida productos y habilitación de sellers.
3. La reserva de todas las líneas y la creación del pedido son atómicas en la base local. Si una línea no tiene stock, se revierte la operación completa.
4. La llamada a la pasarela ocurre después de guardar el pedido pendiente, fuera de la transacción de base de datos. Cada intento usa una clave de idempotencia.
5. La respuesta del navegador no confirma el pago. El backend verifica una notificación autenticada o consulta al proveedor; procesa cada resultado una sola vez.
6. Ante un timeout, el pago queda pendiente de conciliación. No se inicia otro cobro mientras el resultado anterior sea desconocido.
7. Si llega un pago aprobado después de expirar la reserva, el pedido pasa a revisión; la resolución manual o devolución debe definirse con el negocio.
8. Pago, preparación, envío y facturación tienen estados separados. Un fallo de facturación o envío no revierte un pago confirmado.
9. Cada producto tiene una fuente de inventario: manual o ERP. Para esta propuesta, el ERP comunica stock físico versionado y las reservas locales se descuentan al calcular disponibilidad. El protocolo de conciliación multicanal debe acordarse antes de producción.

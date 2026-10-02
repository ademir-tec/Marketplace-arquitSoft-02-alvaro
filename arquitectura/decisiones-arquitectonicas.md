# Decisiones arquitectónicas

## Resumen solicitado

| ADR | Decisión | Drivers asociados | Resultado esperado |
|---|---|---|---|
| **ADR-001** | Adoptar un monolito modular. | DA01 - Escalabilidad y DA06 - Mantenibilidad. | Organizar el backend en los módulos Catálogo, Carrito, Pedidos, Pagos y Usuarios. |
| **ADR-002** | Aplicar Clean Architecture. | DA06 - Mantenibilidad. | Separar Dominio, Aplicación, Infraestructura y Presentación. |
| **ADR-003** | Definir una estrategia de caché. | DA02 - Rendimiento. | Usar caché en consultas frecuentes y medibles. |
| **ADR-004** | Integrar pagos mediante interfaces y adaptadores. | DA04 - Pago externo. | Definir un contrato de pago y un adaptador para la pasarela externa. |

Las decisiones se registran como **aceptadas para el diseño inicial**. Su implementación y sus métricas se validarán en iteraciones posteriores.

## ADR-001: monolito modular

**Contexto.** El marketplace debe crecer durante campañas y permitir cambios aislados, pero el equipo y el alcance académico no justifican la operación distribuida de microservicios.

**Decisión.** Desplegar inicialmente un solo backend y dividir su código por capacidades del negocio: Catálogo, Carrito, Pedidos, Pagos y Usuarios. Cada módulo conserva una responsabilidad clara y expone operaciones definidas; no modifica directamente los datos internos de otro módulo.

**Consecuencias.** El despliegue y las transacciones locales son simples, y el backend completo puede replicarse detrás de un balanceador cuando sea necesario. El escalamiento sigue siendo conjunto y una falla grave puede afectar toda la instancia. Los límites modulares permitirán extraer una capacidad solamente si la medición futura lo justifica.

## ADR-002: Clean Architecture

**Contexto.** DA06 exige que los cambios en interfaz, persistencia o proveedores externos no obliguen a reescribir reglas de negocio.

**Decisión.** Separar el sistema en Dominio, Aplicación, Infraestructura y Presentación. Las dependencias de código apuntan al Dominio. Los contratos requeridos por los casos de uso se definen hacia el interior y se implementan mediante adaptadores externos.

**Consecuencias.** Las reglas se prueban sin navegador, base de datos ni pasarela real; también se pueden sustituir adaptadores desde una raíz de composición. A cambio, se incorporan interfaces, mapeos y configuración explícita. La [auditoría del boilerplate](auditoria-boilerplate.md) confirma este patrón en el proyecto de referencia.

## ADR-003: estrategia de caché

**Contexto.** El catálogo concentra lecturas y puede recibir alta concurrencia durante campañas. Los datos de stock y los estados de compra requieren mayor actualidad que las descripciones de producto.

**Decisión.** Aplicar caché selectiva a consultas frecuentes del catálogo, con claves que incluyan filtros y paginación, tiempo de vida limitado, métricas de aciertos y una política de invalidación al actualizar productos. No almacenar en caché autorizaciones, carritos, pagos ni decisiones de stock como fuente definitiva.

**Consecuencias.** Se reduce la carga de lectura y la latencia del catálogo. Existe riesgo de datos temporalmente desactualizados, por lo que la compra debe revalidar precio y stock contra la fuente autoritativa. El tiempo de vida se fijará después de medir tráfico y tolerancia del negocio.

## ADR-004: pagos mediante puertos y adaptadores

**Contexto.** La pasarela es externa, puede fallar o cambiar y maneja una operación crítica. El Dominio no debe depender del SDK ni del formato de un proveedor.

**Decisión.** Definir un contrato de procesamiento de pagos en el núcleo y colocar la traducción al proveedor en un adaptador de Infraestructura. Usar identificadores idempotentes, validar las notificaciones entrantes y consultar el estado antes de repetir una operación con resultado incierto.

**Consecuencias.** Se puede probar con un simulador y reemplazar la pasarela sin alterar los casos de uso. El adaptador debe mantener mapeos, autenticación, manejo de errores y conciliación. Un timeout no se interpreta automáticamente como rechazo o aprobación.

## Trazabilidad

| Driver | Decisión principal | Documento relacionado |
|---|---|---|
| DA01 - Escalabilidad | ADR-001 | [Estilo arquitectónico](estilo-arquitectonico.md) |
| DA02 - Rendimiento | ADR-003 | [Drivers arquitectónicos](../analisis-de-sistema/06-driver-arquitectonicos.md) |
| DA04 - Pago externo | ADR-004 | [Arquitectura inicial](arquitectura-inicial.md#flujo-de-compra-y-manejo-de-fallos) |
| DA06 - Mantenibilidad | ADR-001 y ADR-002 | [Enfoque Clean Architecture](enfoque/enfoque-arquitectonico.md) |

# 05. Restricciones

Se distingue lo indicado por la guía de las decisiones adoptadas para esta propuesta. Una tecnología presentada como ejemplo conceptual no se convierte automáticamente en una obligación.

| ID | Restricción | Origen | Consecuencia arquitectónica |
|---|---|---|---|
| RC01 | La solución debe ser accesible desde un navegador web. | Ejercicio 07 | Incorporar una aplicación web en presentación. |
| RC02 | El proyecto debe utilizar Git y un repositorio GitHub. | Ejercicios 01 y 07 | Versionar los documentos en una estructura compartida. |
| RC03 | Frontend y backend deben comunicarse mediante API REST. | Ejercicio 07 | Definir recursos HTTP, validaciones y errores consistentes. |
| RC04 | El pago se procesa mediante una pasarela externa. | Ejercicio 07 | Usar un adaptador y no almacenar datos completos de tarjeta. |
| RC05 | La entrega se integra con un servicio externo de envío. | Ejercicio 07 | Mantener referencias y estados de envío independientes del pago. |
| RC06 | El diseño inicial debe organizarse en tres capas. | Ejercicio 09 | Separar presentación, lógica de negocio y datos. |
| RC07 | El análisis se entrega en Markdown y el diagrama en Mermaid o Draw.io. | Herramientas y ejercicio 10 | Mantener documentación legible y versionable; se usa Mermaid. |
| RC08 | Incluir ERP y facturación en el análisis de integraciones. | Actores del ejercicio 03 | Representar contratos externos sin inventar proveedor. |

## Decisiones propuestas sujetas a validación

| ID | Decisión | Justificación y límite |
|---|---|---|
| DP01 | Backend como monolito modular y base relacional. | Simplifica el trabajo académico y permite transacciones locales; no obliga a un motor específico. |
| DP02 | Un pago por pedido y posibles entregas por seller. | Admite carrito multivendedor sin implementar liquidación financiera en esta etapa. |
| DP03 | Un único origen de stock por producto: manual o ERP. | Evita dos autoridades editando el dato; la conciliación ERP queda por acordar. |
| DP04 | Prototipo futuro con datos ficticios y entornos de prueba. | Evita datos o cobros reales durante la validación académica. |

La guía no define presupuesto, proveedor cloud, pasarela concreta, lenguaje ni motor de base de datos. Tampoco fija una meta de concurrencia: las cifras de calidad son propuestas. Las dos horas corresponden a la duración del laboratorio, no a un SLA.

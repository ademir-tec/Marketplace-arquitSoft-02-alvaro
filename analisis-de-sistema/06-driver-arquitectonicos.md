# 06. Drivers arquitectónicos

Un driver arquitectónico representa un problema relevante del sistema que requiere una decisión de arquitectura. Para el marketplace se definen los siguientes drivers:

| Driver | Problema que plantea | Decisión que responde |
|---|---|---|
| **DA01 - Escalabilidad** | Aumentarán los usuarios durante las campañas comerciales. | Monolito modular con posibilidad de escalamiento horizontal. |
| **DA02 - Rendimiento** | Habrá alta concurrencia de usuarios consultando productos y realizando compras. | Incorporar caché y optimizar la comunicación y el procesamiento. |
| **DA03 - Seguridad** | El sistema administra datos sensibles de usuarios y operaciones de compra. | Implementar autenticación y autorización. |
| **DA04 - Pago externo** | El marketplace debe comunicarse con una pasarela de pago. | Realizar la integración mediante una API y adaptadores. |
| **DA05 - API REST** | El frontend y el backend deben comunicarse mediante REST. | Separar la interfaz y el backend mediante una API REST. |
| **DA06 - Mantenibilidad** | Los cambios no deben afectar innecesariamente a otros módulos. | Aplicar modularidad y Clean Architecture. |

Estas decisiones se representan en la [arquitectura inicial](../arquitectura/arquitectura-inicial.md).

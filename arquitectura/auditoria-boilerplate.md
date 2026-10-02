# Auditoría del boilerplate de Clean Architecture

## Propósito

El Paso 01 de la Guía 03 solicita clonar, abrir, ejecutar y analizar el repositorio base. Esta auditoría registra la evidencia obtenida sin incorporar el boilerplate al repositorio del caso ni desarrollar funcionalidad nueva.

## Proyecto revisado

| Elemento | Evidencia |
|---|---|
| Repositorio | <https://github.com/devlizbethjaico/boilerplate.git> |
| Revisión analizada | `9291c71` (`main`) |
| Aplicación | Marketplace de productos para mascotas con Angular 18 |
| Entorno usado | Node.js `v24.21.0` y npm `11.19.0` |
| Instalación | `npm install` completado |

La instalación informó 55 vulnerabilidades en dependencias (7 bajas, 18 moderadas, 28 altas y 2 críticas). No se ejecutó `npm audit fix --force` porque podría introducir cambios incompatibles y el objetivo del laboratorio es analizar la arquitectura existente.

## Correspondencia entre carpetas y capas

| Capa | Evidencia en `src/app` | Responsabilidad observada |
|---|---|---|
| Dominio | `dominio/modelos` y `dominio/contratos` | Entidades, reglas de negocio e interfaces requeridas por el núcleo. |
| Aplicación | `aplicacion/*.caso-uso.ts` | Coordina consultas, carrito y registro de compra mediante contratos del dominio. |
| Infraestructura | `infraestructura` | Implementa repositorios, pagos y notificaciones con memoria, HTTP, Niubiz, WhatsApp o consola. |
| Presentación | `presentacion` | Componentes y estado de interfaz en Angular. |
| Composición | `app.config.ts` | Selecciona implementaciones concretas y las conecta con los casos de uso. |

## Regla de dependencia verificada

La dirección de las dependencias apunta hacia el núcleo:

```text
Presentación ──> Aplicación ──> Dominio
      │                           ▲
      └──────────────┐            │
                     ▼            │
               Infraestructura ───┘
```

- Los modelos del dominio son TypeScript puro y no importan Angular ni mecanismos de persistencia.
- Los casos de uso importan modelos y contratos del dominio; no conocen adaptadores concretos.
- Los adaptadores implementan interfaces definidas por el dominio.
- Los `InjectionToken` de Angular viven en Infraestructura, fuera del dominio.
- `app.config.ts` es la raíz de composición: allí se elige memoria o HTTP, pago simulado o Niubiz, y consola o WhatsApp.

## Flujo observado: registrar una compra

1. El componente de carrito invoca `RegistrarCompraCasoUso.ejecutar()`.
2. El caso de uso verifica que el carrito tenga elementos y consulta reglas de stock del dominio.
3. `Carrito` calcula el total con comisión e IGV definidos en el dominio.
4. El caso de uso cobra mediante `ProcesadorPagos`, sin conocer al proveedor concreto.
5. Tras aprobarse el pago, `Producto` descuenta stock y `Pedido` valida su creación.
6. Los contratos `RepositorioProductos` y `RepositorioPedidos` persisten el resultado.
7. `NotificadorCliente` envía la confirmación mediante el adaptador configurado.

## Verificación ejecutada

| Comando | Resultado |
|---|---|
| `npm run pruebas` | Correcto: 16 pruebas del dominio aprobadas en 100 ms, sin Angular ni navegador. |
| `npm run build` | Correcto: compilación de producción generada en `dist/marketplace-limpio`. |

Las pruebas ofrecen evidencia mecánica de independencia: su configuración compila Dominio, Aplicación y adaptadores en memoria sin iniciar Angular. El resultado confirma la organización del ejemplo; no demuestra por sí solo los atributos de calidad del marketplace propuesto.

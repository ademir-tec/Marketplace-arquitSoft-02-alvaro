# Marketplace de productos para mascotas

## Integrante

Alvaro Ademir Ayala Arango.

## Descripción

Proyecto académico de un marketplace donde diferentes sellers ofrecen alimentos, accesorios y otros productos para mascotas. Los clientes consultan el catálogo, preparan un carrito, realizan pedidos y consultan sus compras. El administrador gestiona a los vendedores y controla el acceso a la plataforma.

Este repositorio desarrolla los diez ejercicios de la **Guía 02: análisis del caso y diseño inicial de la arquitectura en capas de un marketplace**. Contiene análisis y diseño; todavía no implementa una aplicación ejecutable ni integraciones reales.

## Caso de estudio

GoPet se utiliza como referencia funcional indicada por la guía: <https://www.gopet.pe/>. La arquitectura propuesta no pretende describir su implementación interna.

## Curso

- Arquitectura de Software, IS-488
- Docente: Ing. Lizbeth Jaico Quispe
- Semestre: 2026-II
- Laboratorios: 02

## Comprensión del negocio — ejercicio 02

La empresa necesita reunir la oferta de varios vendedores de productos para mascotas en un solo canal de compra. Sin una plataforma común, el cliente debe consultar ofertas por separado y la empresa tiene dificultades para coordinar disponibilidad, pedidos y entregas.

La solución centraliza el catálogo y el proceso de compra, conservando la propiedad de cada producto y venta por seller. Facilita la búsqueda y compra para el cliente, ofrece un canal de venta para los sellers y permite al administrador controlar la participación de vendedores.

**Flujo principal:** buscar producto → revisar disponibilidad → preparar carrito → registrar dirección → crear pedido → pagar → coordinar entrega → consultar estado y comprobante.

### Alcance y supuestos de la propuesta

- Se incluyen cuentas y roles, catálogo, carrito, pedidos, gestión de sellers e integraciones previstas con pago, envío, facturación y ERP.
- Un carrito puede contener productos de varios sellers. Un pedido conserva el seller de cada línea y puede tener una entrega por seller.
- Para reducir el alcance inicial, el pago cubre el pedido completo. La distribución del dinero entre sellers, devoluciones, promociones y recomendaciones quedan para una iteración posterior.
- Se propone reservar stock antes del pago. La duración de la reserva y la fuente de stock de cada seller deben acordarse antes de implementar.
- Las metas numéricas de calidad son objetivos académicos propuestos, no resultados medidos ni compromisos de proveedores.
- No se fija lenguaje, framework ni motor de base de datos. Node.js y PostgreSQL aparecen como ejemplos conceptuales en la guía, no como requisitos obligatorios del caso.

## Estructura — ejercicio 01

```text
Marketplace-arquitSoft-02-alvaro/
├── analisis-de-sistema/
│   ├── 01-actores.md
│   ├── 02-historias-del-usuario.md
│   ├── 03-requisitos-funcionales.md
│   ├── 04-atributos-de-calidad.md
│   ├── 05-restricciones.md
│   └── 06-driver-arquitectonicos.md
├── arquitectura/
│   ├── arquitectura-inicial.md
│   ├── marketplace-archify.json
│   └── marketplace-arquitectura.html
├── .gitignore
└── README.md
```

Se conserva la estructura de la imagen del ejercicio 01 (página 6). La guía alterna posteriormente rutas como `análisis-del-sistema`, `requisitos` y `docs/arquitectura`; aquí se mantienen documentos únicos para evitar versiones contradictorias.

## Desarrollo de los ejercicios

| Ejercicio | Entregable |
|---|---|
| 01. Configuración del repositorio | Este README, estructura y `.gitignore` |
| 02. Comprender el negocio | Sección anterior de este README |
| 03. Actores | [Actores](analisis-de-sistema/01-actores.md) |
| 04. Historias de usuario | [Historias y criterios](analisis-de-sistema/02-historias-del-usuario.md) |
| 05. Requisitos funcionales | [Requisitos y trazabilidad](analisis-de-sistema/03-requisitos-funcionales.md) |
| 06. Atributos de calidad | [Escenarios de calidad](analisis-de-sistema/04-atributos-de-calidad.md) |
| 07. Restricciones | [Restricciones y decisiones](analisis-de-sistema/05-restricciones.md) |
| 08. Drivers arquitectónicos | [Drivers y consecuencias](analisis-de-sistema/06-driver-arquitectonicos.md) |
| 09. Arquitectura en capas | [Responsabilidades por capa](arquitectura/arquitectura-inicial.md#responsabilidades-por-capa) |
| 10. Diagrama final | [Vista gráfica en GitHub](arquitectura/marketplace-arquitectura.png), [diagrama Mermaid](arquitectura/arquitectura-inicial.md#diagrama-de-arquitectura) y [HTML interactivo para descargar](arquitectura/marketplace-arquitectura.html) |

## Cómo revisar y versionar

Leer los documentos de análisis en orden y después la arquitectura. GitHub muestra directamente la vista PNG y representa el bloque Mermaid al abrir el Markdown. En VS Code puede utilizarse la extensión **Markdown Preview Mermaid Support**, indicada en la guía. GitHub muestra el código fuente de los archivos HTML por seguridad; para explorar la versión Archify se debe descargar `marketplace-arquitectura.html` y abrirlo en un navegador.

Los siguientes comandos son una referencia para registrar y publicar la entrega una vez revisada; su presencia no significa que ya se hayan ejecutado:

```bash
git status
git add README.md .gitignore analisis-de-sistema arquitectura
git commit -m "docs: desarrollar analisis y arquitectura inicial del marketplace"
git push origin HEAD
```

## Fuente

`GUIA-AS-002.pdf`, proporcionada para el laboratorio, especialmente las páginas 6–14. Las políticas de stock, estados, autorizaciones y métricas detalladas se desarrollan aquí como propuesta académica y requieren validación con el negocio.

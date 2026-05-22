# NexSmart Ecosystem - TEST Repository

Bienvenido al repositorio centralizado de documentación y pruebas del ecosistema **NexSmart**. Este repositorio contiene las guías de despliegue, arquitectura y uso de cada uno de los microservicios que componen la plataforma.

## 🌟 Visión General
NexSmart es una plataforma de e-commerce y logística de última generación construida bajo una arquitectura de microservicios distribuida, utilizando **.NET 10**, **Docker** y principios de **Domain-Driven Design (DDD)**.

## 🏗️ Estructura del Ecosistema

| Componente | Descripción | Rol |
| :--- | :--- | :--- |
| [🚀 Gateway](./NexSmartGateway/README.md) | Punto de entrada único y documentador. | Orquestador |
| [📂 Central](./NexSmartCENTRAL/README.md) | BDs (SQL, PG) y Proxy Nginx compartido. | Infraestructura |
| [👤 Usuarios](./NexSmartUsuarios/README.md) | Gestión de identidades y clientes. | Microservicio |
| [📦 Catálogo](./NexSmartCatalogo/README.md) | Productos, stock e imágenes. | Microservicio |
| [🛒 Órdenes](./NexSmartOrdenes/README.md) | Corazón transaccional y ventas. | Microservicio |
| [🏷️ Promociones](./NexSmartPromociones/README.md) | Cupones, reglas y descuentos. | Microservicio |
| [💳 Pagos](./NexSmartPagos/README.md) | Integración bancaria y créditos. | Microservicio |
| [🚚 Envíos](./NexSmartEnvios/README.md) | Logística y rastreo en tiempo real. | Microservicio |

## 🛠️ Guía de Inicio Rápido

Para levantar el entorno completo de desarrollo en local, sigue este orden:

1. **Infraestructura Base**:
   Levanta `NexSmartCENTRAL` primero para tener las bases de datos y la red compartida listas.
2. **Microservicios de Soporte**:
   Levanta `Usuarios`, `Catalogo` y `Promociones`.
3. **Core Transaccional**:
   Levanta `Ordenes`, `Pagos` y `Envios`.
4. **Punto de Acceso**:
   Levanta `NexSmartGateway` para exponer todo el sistema.

## 🔒 Seguridad y Datos Sensibles
> [!IMPORTANT]
> Este es un repositorio de **PRUEBA**. Todos los archivos README han sido sanitizados para eliminar credenciales reales, IPs privadas y tokens de producción. Utiliza siempre las variables de entorno configuradas con tus propios valores locales.

---
© 2026 NexSmart - Orientado a la excelencia técnica.

# NexSmart Envíos

Microservicio dedicado a la logística, seguimiento de paquetes y gestión de flotas de entrega.

## Descripción
`NexSmartEnvios` gestiona todo el proceso posterior a la compra: desde la asignación de una guía de rastreo hasta la confirmación de entrega en el domicilio del cliente.

## Tecnologías Utilizadas
- **Runtime**: .NET 10 (Minimal API)
- **Base de Datos**: PostgreSQL 16
- **Real-time**: Soporte para WebSockets / SignalR para seguimiento en vivo.

## Instalación / Despliegue

### Pasos de Despliegue
1. **Docker Build**:
   ```bash
   docker build -t nexsmart-envios:latest -f deploy/Dockerfile .
   ```
2. **Docker Compose**:
   ```bash
   cd deploy/
   docker-compose up -d
   ```

## Uso
- Generación de guías de rastreo.
- Actualización de estados de envío (En preparación, En camino, Entregado).
- Integración con servicios de mensajería externos (Placeholders).

## Dependencias con otros servicios
- **Depende de**: `NexSmartOrdenes` (para saber qué enviar y a dónde).
- **Informa a**: `NexSmartUsuarios` o el Gateway para mostrar el estado al cliente final.

## Arquitectura (DDD)
- **Domain**: Entidades `Envio`, `Ruta` y `EstadoEnvio`.
- **Application**: Lógica de asignación de logística.
- **Infrastructure**: Integraciones con APIs de mapas y persistencia en PostgreSQL.
- **Api**: Webhooks y endpoints de consulta de estado.

## Para desarrolladores junior 💡
Este servicio es el **Camioncito de Reparto**:
- Su trabajo empieza cuando la venta ya terminó.
- Se asegura de que el paquete no se pierda y sepa exactamente en qué parte del mapa está.
- Es como el "Uber" interno del sistema: le dice al cliente: "Tu pedido está a 5 minutos de tu casa".

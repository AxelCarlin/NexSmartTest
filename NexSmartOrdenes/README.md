# NexSmart Órdenes

El corazón transaccional del ecosistema NexSmart, responsable de la creación y gestión de pedidos.

## Descripción
Este microservicio orquestra el flujo principal de venta: recibe el carrito de compras, valida disponibilidad, aplica promociones y coordina el pago antes de confirmar la transacción.

## Tecnologías Utilizadas
- **Runtime**: .NET 10
- **Base de Datos**: SQL Server 2022
- **Patrones**: Saga Pattern (simplificado) para consistencia entre servicios.

## Instalación / Despliegue

### Pasos de Despliegue
1. **Build**:
   ```bash
   docker build -t nexsmart-ordenes:latest -f deploy/Dockerfile .
   ```
2. **Despliegue**:
   ```bash
   cd deploy/
   docker-compose up -d
   ```

## Uso
- Creación de nuevas órdenes de compra.
- Historial de pedidos por usuario.
- Cambio de estados de la orden (Pendiente, Pagada, Cancelada).

## Dependencias con otros servicios
Es el **gran orquestador**:
1. Llama a `NexSmartUsuarios` para validar al comprador.
2. Consulta a `NexSmartCatalogo` para reservar stock.
3. Pregunta a `NexSmartPromociones` por descuentos.
4. Delega a `NexSmartPagos` el cobro.
5. Avisa a `NexSmartEnvios` una vez pagada.

## Arquitectura (DDD)
- **Domain**: Lógica de cálculo de totales y estados de pedidos. Es la capa más crítica.
- **Application**: Orquestación de llamadas a otros microservicios.
- **Infrastructure**: Repositorios SQL y clientes HTTP para comunicación inter-service.
- **Api**: Endpoints de checkout.

## Para desarrolladores junior 💡
Este servicio es el **Cajero Central**:
- Es el que toma tu lista de compras, suma todo, resta los descuentos y te da el ticket.
- Es el "pegamento" de todo el sistema; si este servicio falla, no hay ventas.
- Su trabajo es hablar con todos los demás departamentos para que la compra sea exitosa.

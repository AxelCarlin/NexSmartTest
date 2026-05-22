# NexSmart Promociones

Microservicio especializado en la gestión de campañas de marketing, cupones de descuento y reglas de negocio promocionales.

## Descripción
El Hub de Promociones permite aplicar lógica dinámica de descuentos sobre las órdenes. Puede gestionar descuentos por categoría, cupones temporales y promociones automáticas basadas en el carrito del usuario.

## Tecnologías Utilizadas
- **Runtime**: .NET 10
- **Base de Datos**: PostgreSQL 16 (vía NexSmartCENTRAL)
- **Persistencia**: Dapper / EF Core
- **Mensajería**: Soporte para eventos de dominio.

## Instalación / Despliegue

### Pasos de Despliegue
1. **Build**:
   ```bash
   docker build -t nexsmart-promociones:latest -f deploy/Dockerfile .
   ```
2. **Up**:
   ```bash
   cd deploy/
   docker-compose up -d
   ```

## Uso
- Validación de cupones de descuento.
- Aplicación de reglas "X por Y" (ej. 2x1).
- Listado de promociones vigentes.

## Dependencias con otros servicios
- **Se comunica con**: `NexSmartCatalogo` para validar a qué productos aplica un descuento.
- **Es consultado por**: `NexSmartOrdenes` antes de finalizar un pago para calcular el total real.

## Arquitectura (DDD)
- **Domain**: Reglas de negocio complejas (Strategy Pattern para distintos tipos de descuentos).
- **Application**: Orquestación de aplicación de cupones.
- **Infrastructure**: Acceso a PostgreSQL y servicios de tiempo para vigencia.
- **Api**: Endpoints de validación rápida.

## Para desarrolladores junior 💡
Este servicio es el **Calculador de Ofertas** de la tienda:
- Es como esa persona en la caja que sabe qué cupones pasan y cuáles ya expiraron.
- No guarda productos, solo guarda "reglas": "Si alguien compra esto, quítale un 10%".
- Trabaja muy de cerca con el Carrito de Compras para que el cliente siempre vea el mejor precio posible.

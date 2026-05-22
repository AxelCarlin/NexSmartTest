# NexSmart Pagos

Microservicio responsable de la integración con pasarelas de pago externas y la gestión de créditos internos de clientes.

## Descripción
`NexSmartPagos` aísla la complejidad de las transacciones financieras. Maneja la comunicación con servicios como Stripe, PayPal o Terminales Bancarias, asegurando que el dinero sea procesado de forma segura.

## Tecnologías Utilizadas
- **Runtime**: .NET 10
- **Base de Datos**: PostgreSQL 16 (para logs de transacciones de alta velocidad).
- **Seguridad**: Implementación de estándares de encriptación para datos sensibles.

## Instalación / Despliegue

### Pasos de Despliegue
1. **Compilar**:
   ```bash
   docker build -t nexsmart-pagos:latest -f deploy/Dockerfile .
   ```
2. **Levantar**:
   ```bash
   cd deploy/
   docker-compose up -d
   ```

## Uso
- Procesamiento de cargos a tarjetas.
- Gestión de monederos electrónicos / crédito NexSmart.
- Conciliación de pagos exitosos o fallidos.

## Dependencias con otros servicios
- **Depende de**: `NexSmartCENTRAL` (Logs y Persistencia).
- **Es llamado por**: `NexSmartOrdenes` (durante el proceso de checkout).

## Arquitectura (DDD)
- **Domain**: Entidades de `Transaccion`, `MetodoPago` y validadores financieros.
- **Application**: Adaptadores para distintos proveedores de pago.
- **Infrastructure**: Implementación de SDKs externos (ej. Stripe) y acceso a BD.
- **Api**: Webhooks para recibir confirmaciones de bancos.

## Para desarrolladores junior 💡
Este servicio es la **Terminal Bancaria y la Caja Fuerte**:
- Es el único lugar que toca "dinero" (virtualmente).
- Su misión es hablar con los bancos y regresar una respuesta simple: "Aprobado" o "Rechazado".
- Está muy protegido y guarda un registro (log) de cada intento de pago para que siempre haya cuentas claras.

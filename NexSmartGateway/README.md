# NexSmart Gateway

API Gateway robusto y centralizado construido con **.NET 10** y **YARP (Yet Another Reverse Proxy)**. Actúa como el punto de entrada único para todo el ecosistema de microservicios NexSmart, gestionando el enrutamiento, la resiliencia y la documentación unificada.

## Descripción
Este servicio es la puerta de enlace que orquesta el tráfico hacia los distintos microservicios. Implementa políticas de reintento, cortocircuitos (Circuit Breaker) y ofrece un hub de documentación interactivo para todos los desarrolladores.

## Tecnologías Utilizadas
- **Runtime**: .NET 10
- **Reverse Proxy**: YARP
- **Documentación**: Scalar (OpenAPI)
- **Resiliencia**: Polly
- **Caching**: Output Cache nativo de .NET

## Instalación / Despliegue

### Requisitos
- Docker y Docker Compose
- Red compartida `nexsmart_shared_network` levantada (ver `NexSmartCENTRAL`)

### Pasos de Despliegue
1. **Construir la imagen**:
   ```bash
   docker build -t nexsmart-gateway:latest -f deploy/Dockerfile .
   ```
2. **Levantar el servicio**:
   ```bash
   cd deploy/
   docker-compose up -d
   ```

## Uso
Una vez iniciado, el Gateway está disponible en el puerto configurado (ej. `http://localhost:80`).
- **Hub de Documentación**: Accede a `/` para ver la interfaz de Scalar con todos los microservicios mapeados.
- **Rutas de API**: Las peticiones son redirigidas según el prefijo:
  - `/docs/usuarios/*` -> Identidad y Usuarios
  - `/docs/catalogo/*` -> Catálogo de Productos
  - `/docs/promociones/*` -> Hub de Promociones
  - ...y así sucesivamente.

## Dependencias con otros servicios
El Gateway es el **consumidor principal** de los servicios:
- `NexSmartUsuarios`: Para validación de identidad.
- `NexSmartCatalogo`, `NexSmartPromociones`, `NexSmartEnvios`, `NexSmartOrdenes`, `NexSmartPagos`: Para orquestación de datos.

## Arquitectura (Resumen DDD)
Aunque el Gateway se enfoca en infraestructura, sigue un patrón de **Layered Architecture** simplificado:
- **API Layer**: Expone los endpoints de documentación y el proxy.
- **Infrastructure Layer**: Configuraciones de YARP y políticas de Polly.

## Para desarrolladores junior 💡
Imagina que el sistema NexSmart es un gran restaurante. El **Gateway** es el **recepcionista** (Host). 
- Los clientes (Frontend/App) solo hablan con él.
- Él sabe exactamente en qué mesa (microservicio) está cada plato.
- Si una cocina (servicio) está muy lenta, él avisa y gestiona la espera (Polly/Circuit Breaker).
- No tienes que saber las direcciones IP de cada microservicio, solo la dirección del Gateway.

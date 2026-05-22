# NexSmart Catálogo

Microservicio encargado de la gestión integral del catálogo de productos e inventarios del ecosistema NexSmart.

## Descripción
Este servicio gestiona el ciclo de vida de los productos, categorías, precios y niveles de existencias. Está optimizado para búsquedas rápidas y manejo de imágenes de productos.

## Tecnologías Utilizadas
- **Runtime**: .NET 10
- **Base de Datos**: SQL Server 2022
- **Almacenamiento**: Local Storage / Cloud Storage para imágenes.
- **Patrones**: CQRS (simplificado) y DDD.

## Instalación / Despliegue

### Pasos de Despliegue
1. **Construir Imagen**:
   ```bash
   docker build -t nexsmart-catalogo:latest -f deploy/Dockerfile .
   ```
2. **Despliegue**:
   ```bash
   cd deploy/
   docker-compose up -d
   ```

## Uso
Endpoints disponibles para:
- Listado y búsqueda de productos.
- Gestión de inventario (Stock).
- CRUD de categorías y catálogos.

## Dependencias con otros servicios
- **Depende de**: `NexSmartCENTRAL` (Persistencia).
- **Es consumido por**: `NexSmartOrdenes` (para obtener precios y disponibilidad) y `NexSmartPromociones` (para aplicar descuentos a productos específicos).

## Arquitectura (DDD)
- **Domain**: Entidades `Producto`, `Categoria` y `Stock`.
- **Application**: Lógica de gestión de inventarios y comandos de actualización de precios.
- **Infrastructure**: Repositorios SQL y servicios de manejo de archivos.
- **Api**: Exposición de catálogo a través del Gateway.

## Para desarrolladores junior 💡
Imagina que este servicio es el **Estante y el Almacén** de la tienda:
- Sabe cuántas piezas quedan de cada cosa.
- Tiene la etiqueta del precio y la foto de cada artículo.
- Si una orden se genera, este servicio es el que dice: "Sí tengo este producto, aquí está su precio".
- Es el servicio que más tráfico suele recibir porque todos quieren ver qué hay para comprar.

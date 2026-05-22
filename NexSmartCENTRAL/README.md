# NexSmart Central Infrastructure

Repositorio central de infraestructura que orquesta los servicios compartidos y el balanceo de carga para todo el ecosistema NexSmart.

## Descripción
`NexSmartCENTRAL` es el núcleo de persistencia y enrutamiento externo. Provee las instancias compartidas de bases de datos y un servidor Nginx configurado como buscador de servicios (Service Discovery manual) y terminación de dominios.

## Componentes
- **SQL Server 2022 (LTS)**: Base de datos relacional principal para la mayoría de los microservicios.
- **PostgreSQL 16**: Utilizado por servicios específicos que requieren persistencia orientada a objetos o relacional ligera.
- **Nginx**: Proxy inverso que mapea subdominios (ej. `apicatalogo.midominio.com`) a los contenedores internos.
- **Shared Network**: Red `nexsmart_shared_network` que permite la comunicación entre contenedores de distintos repositorios.

## Instalación / Despliegue

### Requisitos
- Docker y Docker Compose
- Puertos `80`, `1433` y `5432` disponibles.

### Pasos de Despliegue
1. **Iniciar Infraestructura**:
   ```bash
   docker-compose up -d
   ```
2. **Ejecutar Migraciones Globales (Opcional)**:
   Si tienes scripts de seed, utilízalos:
   ```bash
   ./seed-all.sh
   ```

## Uso
Una vez arriba, los microservicios pueden conectarse a las bases de datos usando el nombre de host del contenedor:
- SQL Server: `sqlserver_central,1433`
- PostgreSQL: `postgres_central:5432`

El archivo `nginx.conf` ya viene pre-configurado para redirigir tráfico de dominios específicos a los puertos `8080` de cada microservicio en la red compartida.

## Arquitectura
Este repositorio sigue un patrón de **Infrastructure as Code (IaC)** simplificado mediante Docker Compose, centralizando la configuración de red y volúmenes persistentes.

## Para desarrolladores junior 💡
Piensa en `CENTRAL` como los **cimientos y servicios públicos** de una colonia:
- Es la planta de luz y agua (Bases de datos) que todos usan.
- Es la caseta de vigilancia (Nginx) que sabe a qué casa mandar a cada visitante.
- Sin `CENTRAL`, los microservicios no tienen dónde guardar información ni cómo ser encontrados desde internet. Siempre debe ser el **primer** repositorio en levantarse.

# NexSmart Usuarios

Microservicio especializado en la gestión de identidades, perfiles de usuario y gestión de clientes dentro del ecosistema NexSmart.

## Descripción
Este servicio es el responsable de mantener la verdad absoluta sobre quiénes son los usuarios del sistema y qué permisos poseen. Utiliza un enfoque de **Minimal API** en .NET 10 para ofrecer un rendimiento excepcional.

## Tecnologías Utilizadas
- **Runtime**: .NET 10
- **Base de Datos**: SQL Server 2022 (vía NexSmartCENTRAL)
- **Persistencia**: Entity Framework Core
- **Arquitectura**: DDD (Domain-Driven Design)

## Instalación / Despliegue

### Pasos de Despliegue
1. **Compilar y Contenerizar**:
   ```bash
   docker build -t nexsmart-usuarios:latest -f deploy/Dockerfile .
   ```
2. **Levantar junto con su Job de BD**:
   ```bash
   cd deploy/
   docker-compose up -d
   ```

## Uso
Expone endpoints para:
- Registro y autenticación de usuarios.
- Gestión de perfiles y roles.
- Consulta de datos de cliente para otros servicios.

## Dependencias con otros servicios
- **Depende de**: `NexSmartCENTRAL` (Base de Datos).
- **Es consumido por**: `NexSmartGateway`, `NexSmartOrdenes` (para validar el cliente).

## Arquitectura (DDD)
Sigue una estructura de cuatro capas:
1. **Domain**: Contiene la lógica pura de negocio, la entidad `Usuario` y reglas de validación.
2. **Application**: Casos de uso (RegistrarUsuario, ActualizarPerfil).
3. **Infrastructure**: Implementación de repositorios y acceso a SQL Server.
4. **Api**: Endpoints y configuración de inyección de dependencias.

## Para desarrolladores junior 💡
Este microservicio es el **Libro de Registros** de la empresa. 
- Es el primer lugar donde alguien "toca la puerta" para entrar al sistema.
- Su única misión es saber quién es quién y asegurarse de que no haya impostores.
- Todos los demás servicios le preguntan: "¿Este ID de usuario realmente existe?".

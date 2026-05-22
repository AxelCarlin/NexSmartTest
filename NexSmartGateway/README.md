# NexSmartGateway

**API Gateway** - Puerta de entrada centralizada para acceder a todos los microservicios de NexSmart.

## ¿Qué es una API Gateway?

Una API Gateway es un servidor que actúa como intermediario entre los clientes (aplicaciones frontend, móviles, etc.) y los microservicios internos de una arquitectura. En lugar de que las aplicaciones se comuniquen directamente con cada microservicio, todas las peticiones pasan primero por la API Gateway.

### Beneficios de usar una API Gateway:

- **Punto de entrada único**: Una sola URL para acceder a todos los microservicios
- **Enrutamiento inteligente**: Dirige automáticamente cada petición al microservicio correcto
- **Autenticación centralizada**: Valida credenciales una sola vez
- **Rate limiting y seguridad**: Protege los microservicios de accesos no autorizados
- **Abstracción**: Los clientes no necesitan conocer dónde están los microservicios

---

## Acceso a Microservicios: Comparativa

### ❌ **Sin API Gateway** (Acceso Directo)

Deberías conectarte directamente a cada microservicio:

```
https://ms-usuarios.your-domain.com/api/usuarios
https://ms-productos.your-domain.com/api/productos
https://ms-pedidos.your-domain.com/api/pedidos
```

**Desventajas:**
- Múltiples URLs a mantener
- Exposición directa de microservicios
- Cada servicio maneja su propia autenticación
- Mayor complejidad en el cliente

---

### ✅ **Con API Gateway** (Recomendado)

A través de **NexSmartGateway**:

```
https://your-domain.com/api/usuarios
https://your-domain.com/api/productos
https://your-domain.com/api/pedidos
```

**Ventajas:**
- Una sola URL base: `https://your-domain.com`
- La API Gateway enruta internamente a los microservicios correspondientes
- Autenticación centralizada
- Mayor seguridad y control

---

## Ejemplos de Uso

### 1. **Obtener Lista de Usuarios**

**Endpoint:**
```
GET https://your-domain.com/api/usuarios
```

**Solicitud cURL:**
```bash
curl -X GET "https://your-domain.com/api/usuarios" \
  -H "Content-Type: application/json"
```

**Respuesta:**
```json
{
  "status": 200,
  "data": [
    {
      "id": 1,
      "nombre": "Nombre Ejemplo",
      "email": "ejemplo@your-domain.com"
    },
    {
      "id": 2,
      "nombre": "Usuario Prueba",
      "email": "prueba@your-domain.com"
    }
  ]
}
```

---

### 2. **Obtener Usuarios con Filtros**

**Endpoint:**
```
GET https://your-domain.com/api/usuarios?estado=activo
```

**Solicitud cURL:**
```bash
curl -X GET "https://your-domain.com/api/usuarios?estado=activo" \
  -H "Content-Type: application/json"
```

---

### 3. **Crear un Nuevo Usuario**

**Endpoint:**
```
POST https://your-domain.com/api/usuarios
```

**Solicitud cURL:**
```bash
curl -X POST "https://your-domain.com/api/usuarios" \
  -H "Content-Type: application/json" \
  -d '{
    "nombre": "Nombre Apellido",
    "email": "usuario@your-domain.com",
    "telefono": "0000000000"
  }'
```

**Respuesta:**
```json
{
  "status": 201,
  "message": "Usuario creado exitosamente",
  "data": {
    "id": 3,
    "nombre": "Nombre Apellido",
    "email": "usuario@your-domain.com"
  }
}
```

---

### 4. **Ejemplo en JavaScript/Fetch**

```javascript
// Obtener usuarios
fetch('https://your-domain.com/api/usuarios')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

// Crear un usuario
fetch('https://your-domain.com/api/usuarios', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    nombre: 'Nuevo Usuario',
    email: 'nuevo@your-domain.com'
  })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

---

## Documentación Interactiva

Accede a la documentación detallada de los endpoints usando **Scalar**:

- **Microservicio de Usuarios:**
  - Acceso Directo: https://ms-usuarios.your-domain.com/scalar/v1
  - A través del Gateway: https://your-domain.com/api/usuarios/docs

---

## Estructura del Proyecto

```
NexSmartGateway/
├── Program.cs              # Configuración principal
├── appsettings.json        # Configuración de microservicios
├── Controllers/            # Controladores que enrutan solicitudes
├── Middleware/             # Middlewares de autenticación y logging
├── Properties/             # Configuración del proyecto
└── Dockerfile              # Imagen Docker para desplegar
```

---

## Comenzar Rápidamente

### Requisitos:
- .NET 8.0 o superior
- Docker (opcional)

### Instalación Local:

```bash
# Clonar el repositorio
git clone https://github.com/AxelCarlin/NexSmartGateway.git
cd NexSmartGateway

# Restaurar dependencias
dotnet restore

# Ejecutar el servidor
dotnet run

# La API estará disponible en: http://localhost:5000
```

### Usar con Docker:

```bash
# Construir imagen
docker build -t nexsmart-gateway .

# Ejecutar contenedor
docker run -p 5000:80 nexsmart-gateway
```

---

## Resumen

| Aspecto | Acceso Directo | Con API Gateway |
|--------|----------------|-----------------|
| **URL base** | https://ms-usuarios.your-domain.com | https://your-domain.com |
| **Estructura** | /api/usuarios | /api/usuarios |
| **Autenticación** | Por microservicio | Centralizada |
| **Mantenimiento** | Complejo | Simple |
| **Seguridad** | Menor | Mayor |

**Recomendación:** Siempre usa **NexSmartGateway** para acceder a los microservicios.

---

## Contacto

Para más información sobre los microservicios y su implementación, consulta la documentación específica de cada servicio en su respectiva URL Scalar.

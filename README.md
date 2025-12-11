# 🚗 Sistema de Recaudos de Vehículos - Backend API

API REST para la gestión y consulta de recaudos de vehículos desarrollada como parte del reto técnico de F2X.

## 📋 Datos de la Aplicación

- **Nombre**: Sistema de Recaudos de Vehículos - Backend API
- **Versión**: 1.0.0
- **Descripción**: API REST que permite importar, consultar y generar reportes de recaudos de vehículos desde una API externa, con almacenamiento en SQL Server.

## 🛠 Tecnologías

- **.NET 9.0** - Framework del servidor
- **ASP.NET Core** - Web API REST
- **Entity Framework Core 9.0.9** - ORM para acceso a datos
- **Swashbuckle.AspNetCore 9.0.6** - Documentación OpenAPI/Swagger
- **SQL Server** - Motor de base de datos

## 📂 Estructura del Proyecto

```
reto2/
├── Controllers/                # Capa de Presentación
│   └── RecaudosController.cs
├── Services/                   # Capa de Lógica de Negocio
│   ├── RecaudoService.cs
│   └── ExternalApiService.cs
├── Data/                       # Capa de Datos
│   └── ApplicationDbContext.cs
├── Models/
│   └── Recaudo.cs
├── Program.cs
└── appsettings.json
```

## 🏗 Arquitectura

La aplicación implementa una arquitectura de 3 capas:

### Capa de Presentación
- Controllers (RecaudoController.cs)

### Capa de Lógica de Negocio
- Services (RecaudoService, ExternalApiService)
- Implementación de reglas de negocio
- Validaciones y transformaciones de datos

### Capa de Datos
- ApplicationDbContext (Entity Framework)
- Modelos (Recaudo)
- Acceso a SQL Server

### Patrones de Diseño Implementados
- Repository Pattern (a través de DbContext)
- Service Layer Pattern
- Dependency Injection
- DTO Pattern (para comunicación con API externa)

## 🚀 Instalación y Configuración

### Prerrequisitos

- [.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
- SQL Server
- Visual Studio 2022 o Visual Studio Code
- Git

### 1. Clonar el Repositorio

```bash
git clone https://github.com/keinerst77/retobackend.git
cd retobackend/reto2
```

### 2. Configurar Cadena de Conexión

Edita el archivo `appsettings.json` con tus credenciales de SQL Server:

**Opción A: Windows Authentication (Recomendado para desarrollo local)**
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=reto_keiner;Integrated Security=true;TrustServerCertificate=True;MultipleActiveResultSets=true;"
  }
}
```

**Opción B: SQL Authentication**
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=reto_keiner;User Id=tu_usuario;Password=tu_password;TrustServerCertificate=True;MultipleActiveResultSets=true;Encrypt=False;"
  }
}
```

> **Nota**: Si usas SQL Server Express, el servidor típicamente es `localhost\SQLEXPRESS`

### 3. Crear la Base de Datos

Abre SQL Server Management Studio y ejecuta:

```sql
CREATE DATABASE reto_keiner;
GO

USE reto_keiner;
GO

-- El esquema y tabla se crean automáticamente con Entity Framework
```

### 4. Aplicar Migraciones

En la terminal, dentro de la carpeta `reto2`:

```bash
dotnet restore
dotnet ef database update
```

Si no tienes Entity Framework CLI instalado:

```bash
dotnet tool install --global dotnet-ef
```

### 5. Ejecutar el Backend

```bash
dotnet run
```

El servidor estará disponible en:
- **API**: http://localhost:PUERTO
- **Swagger UI**: http://localhost:PUERTO/swagger/index.html

## 📖 Uso de la API

### Importar Datos

1. Ve a Swagger UI: http://localhost:PUERTO/swagger/index.html
2. Ejecuta el endpoint: `POST /api/Recaudos/importar`
3. Esto importará todos los datos desde el 31 de mayo de 2024

## 📊 Endpoints Principales

Consulta la documentación completa en Swagger UI: http://localhost:PUERTO/swagger/index.html

```
GET    /api/Recaudos                          # Obtener todos los recaudos
GET    /api/Recaudos/estacion/{estacion}      # Filtrar por estación
GET    /api/Recaudos/fecha/{fecha}            # Filtrar por fecha
GET    /api/Recaudos/rango                    # Filtrar por rango de fechas
POST   /api/Recaudos/importar                 # Importar datos desde API externa
POST   /api/Recaudos/importar/{fecha}         # Importar fecha específica
GET    /api/Recaudos/reporte-mensual          # Generar reporte mensual
GET    /api/Recaudos/reporte-estaciones       # Reporte agrupado por estación
```

## 🧪 Probar la API

### Con Swagger UI
1. Ve a http://localhost:PUERTO/swagger/index.html
2. Prueba directamente desde la interfaz


## 🐛 Solución de Problemas

### Error de conexión a la base de datos

**Error**: `Cannot connect to SQL Server`

**Solución**:
- Verifica que SQL Server esté corriendo
- Revisa la cadena de conexión en `appsettings.json`
- Asegúrate de tener permisos en la base de datos

### Error de CORS

Si conectas desde un frontend en otro puerto, asegúrate de configurar CORS en `Program.cs`.

### No se pueden aplicar migraciones

**Solución**:
```bash
# Instalar herramienta EF
dotnet tool install --global dotnet-ef

# Crear migración inicial
dotnet ef migrations add InitialCreate

# Aplicar migración
dotnet ef database update
```

## 🔗 Repositorio Frontend

Para visualizar los datos, puedes usar el frontend Angular:
- **Repositorio**: https://github.com/keinerst77/retoangular.git

## 📝 Notas Importantes

- La API externa requiere que las consultas sean de fechas con más de 2 días de anterioridad
- Los datos se importan desde el 31 de mayo de 2024 en adelante
- La tabla de base de datos se crea automáticamente con Entity Framework
- El reporte mensual ejecuta la agrupación en el servidor (SQL Server)

## 👨‍💻 Desarrollado por

**Keiner Arenas**

Para el reto de F2X

# Coders & IA Community - Backend

Repositorio backend en PHP para el portal **Coders & IA**. Conexión a MySQL, endpoints REST, seguridad y modelado de la base de datos.  
Esta es la API RESTful para la comunidad de **Coders & IA**, construida desde cero con **PHP puro** y **MySQL**, adoptando una arquitectura profesional y patrones de diseño modernos para garantizar un código limpio, seguro y escalable.

El objetivo es dar soporte al portal web, la aplicación móvil y futuros bots multicanal, gestionando la autenticación, recursos, eventos, comunidad y funcionalidades de IA.

---

## 🚀 Características Principales

- **Arquitectura Profesional**: A pesar de usar PHP puro, la estructura separa la lógica de negocio (Services), el acceso a datos (Models) y el control de peticiones (Controllers).
- **Seguridad Integral**: Implementa autenticación con JWT, hashing de contraseñas con `bcrypt`, y sentencias preparadas (PDO) para una protección robusta.
- **Stack Moderno y Controlado**: Utiliza **PHP 8.2+** y **MySQL**, gestionando las dependencias de desarrollo con **Composer**.
- **API Documentada**: Sigue la especificación **OpenAPI 3.0** para una documentación clara y precisa de todos los endpoints.
- **Entorno Contenerizado**: Configuración lista para usar con **Docker**, garantizando un entorno de desarrollo consistente y aislado.

---

## 🛠️ Stack Tecnológico

| Categoría         | Tecnología                                                              |
| :---------------- | :---------------------------------------------------------------------- |
| **Core** | PHP 8.2+ con tipado estricto, Composer, PSR-12 |
| **Framework** | **Ninguno (PHP Puro / Vanilla)** |
| **Base de Datos** | **MySQL 8.0+** |
| **Acceso a Datos**| **PDO (PHP Data Objects)** con sentencias preparadas |
| **API & Auth** | REST, OpenAPI 3.0, JWT (JSON Web Tokens) |
| **Caching** | OPcache (incluido en PHP), Redis (Opcional para escalar) |
| **Contenedores** | Docker, Docker Compose |
| **Testing** | PHPUnit |

---

## 📁 Estructura del Proyecto

El proyecto sigue una arquitectura modular y orientada a servicios para facilitar la mantenibilidad y escalabilidad.

```

api/
├── app/
│   ├── Controllers/    # Reciben peticiones HTTP y coordinan la respuesta.
│   ├── Models/         # Representan las entidades y la interacción con la BD.
│   ├── Services/       # Contienen la lógica de negocio pura y centralizada.
│   ├── Middleware/     # Lógica que se ejecuta ANTES del controlador (ej: auth).
│   ├── Validators/     # Clases dedicadas a validar los datos de entrada.
│   └── Utils/          # Clases y funciones de ayuda reutilizables.
├── config/             # Archivos de configuración de la aplicación (BD, JWT, etc.).
├── database/
│   ├── migrations/     # (Opcional) Para versionado de la BD con herramientas.
│   ├── seeds/          # Scripts para poblar la BD con datos iniciales.
│   └── schema.sql      # Script SQL para la creación inicial de la estructura.
├── public/
│   ├── index.php       # Punto de entrada ÚNICO de todas las peticiones.
│   └── .htaccess       # Reglas de reescritura para el enrutador.
├── storage/
│   ├── logs/           # Logs de errores y de la aplicación.
│   ├── uploads/        # Archivos subidos por los usuarios.
│   └── cache/          # Almacenamiento de caché de archivos.
├── tests/
│   ├── Unit/           # Pruebas para clases aisladas (Services, Utils).
│   └── Integration/    # Pruebas que verifican la interacción entre componentes.
├── docs/
│   ├── openapi.yaml    # Especificación formal de la API.
│   └── postman_collection.json # Colección para pruebas manuales con Postman.
├── docker/
│   ├── Dockerfile      # Define la imagen del contenedor de PHP.
│   └── docker-compose.yml # Orquesta los servicios (PHP, MySQL).
├── composer.json       # Dependencias del proyecto (solo desarrollo).
├── .env.example        # Plantilla para variables de entorno.
└── README.md

````

---

## 🚀 Instalación y Puesta en Marcha

### Prerrequisitos

- Git  
- Docker y Docker Compose

### Instalación con Docker (Recomendado)

1. **Clonar el repositorio**

   ```bash
   git clone [URL_DEL_REPO]
   cd api
````

2. **Configurar variables de entorno**
   Crea tu archivo `.env` a partir del ejemplo y configúralo con tus credenciales de la base de datos MySQL.

   ```bash
   cp .env.example .env
   ```

3. **Instalar dependencias de desarrollo**
   Este comando utiliza la imagen de PHP de Docker para instalar dependencias como PHPUnit.

   ```bash
   docker-compose run --rm composer install
   ```

4. **Levantar los servicios**
   Esto iniciará los contenedores de PHP y MySQL.

   ```bash
   docker-compose up -d
   ```

5. **Crear la Base de Datos**
   Ejecuta el script `schema.sql` para crear las tablas en tu base de datos MySQL.

   ```bash
   docker-compose exec -T mysql mysql -uTU_USUARIO -pTU_PASSWORD TU_BASE_DE_DATOS < database/schema.sql
   ```

   *(Reemplaza los valores con los que definiste en tu archivo `.env`)*

La API ahora estará disponible en `http://localhost:8080` (o el puerto que configures).

---

## 🏛️ Arquitectura y Flujo de Petición

El flujo de una petición típica sigue este camino para mantener el código organizado:

1. **`public/index.php`**: Recibe todas las peticiones gracias a `.htaccess`.
2. **Router**: Un enrutador simple (a crear en `core/` o similar) analiza la URL y el método HTTP.
3. **Middleware**: El router ejecuta los `Middleware` relevantes (ej. `AuthMiddleware`) para verificar permisos.
4. **Controller**: Si el middleware pasa, se llama al método del `Controller` correspondiente.
5. **Validator**: El controlador usa una clase de `Validators` para limpiar y validar los datos de entrada.
6. **Service**: El controlador delega toda la lógica de negocio a una clase en `Services`.
7. **Model**: El servicio interactúa con uno o más `Models` para acceder o modificar los datos en la base de datos a través de PDO.
8. **Response**: El controlador recibe el resultado del servicio y utiliza una utilidad de `Response` para enviar la respuesta JSON estandarizada al cliente.

---

## 🗺️ Roadmap

✅ **Fase 1: Setup y Autenticación (Semanas 1-2)**

* Configuración del proyecto y entorno Docker.
* Creación del esquema de la base de datos en `schema.sql`.
* Implementación del módulo de autenticación (Registro, Login, JWT).
* Definición de la API base con OpenAPI.

📋 **Próximos Módulos (En Desarrollo)**

* **Fase 2: Módulos Core (Semanas 3-6)**: Desarrollo de los módulos de Recursos, Calendario, Comunidad y Repositorios.
* **Fase 3: IA y Optimización (Semanas 7-8)**: Implementación de búsqueda semántica, recomendaciones y mejoras de rendimiento.
* **Fase 4: Despliegue (Semanas 9-10)**: Puesta en producción, configuración de monitoreo y documentación final.

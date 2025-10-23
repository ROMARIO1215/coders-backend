# Coders & IA Community - Backend
Repositorio backend en PHP para el portal Coders &amp; IA. Conexión a MySQL, endpoints REST, seguridad y modelado de la BD.


Esta es la API RESTful para la comunidad de Coders & IA. Ha sido construida desde cero con PHP puro y MySQL, adoptando una arquitectura profesional y patrones de diseño modernos para garantizar un código limpio, seguro y escalable.El objetivo es dar soporte al portal web, la aplicación móvil y futuros bots multicanal 1, gestionando la autenticación, recursos, eventos, comunidad y funcionalidades de IA2.🚀 Características PrincipalesArquitectura Profesional: A pesar de usar PHP puro, la estructura separa la lógica de negocio (Services), el acceso a datos (Models) y el control de peticiones (Controllers)3.Seguridad Integral: Implementa autenticación con JWT 4, hashing de contraseñas con bcrypt5, y sentencias preparadas (PDO) para una protección robusta.Stack Moderno y Controlado: Utiliza PHP 8.2+ 6y MySQL, gestionando las dependencias de desarrollo con Composer7.API Documentada: Sigue la especificación OpenAPI 3.0 para una documentación clara y precisa de todos los endpoints8.Entorno Contenerizado: Configuración lista para usar con Docker, garantizando un entorno de desarrollo consistente y aislado9.🛠️ Stack TecnológicoCategoríaTecnologíaCorePHP 8.2+ con tipado estricto 10, Composer 11, PSR-12 12FrameworkNinguno (PHP Puro / Vanilla)Base de DatosMySQL 8.0+Acceso a DatosPDO (PHP Data Objects) con sentencias preparadasAPI & AuthREST, OpenAPI 3.0 13, JWT (JSON Web Tokens) 14CachingOPcache 15 (incluido en PHP), Redis 16 (Opcional para escalar)ContenedoresDocker, Docker Compose 17TestingPHPUnit 18📁 Estructura del ProyectoEl proyecto sigue una arquitectura modular y orientada a servicios para facilitar la mantenibilidad y escalabilidad19.api/
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
🚀 Instalación y Puesta en MarchaPrerrequisitosGitDocker y Docker ComposeInstalación con Docker (Recomendado)Clonar el repositorioBashgit clone [URL_DEL_REPO]
cd api
Configurar variables de entornoCrea tu archivo .env a partir del ejemplo y configúralo con tus credenciales de la base de datos MySQL.Bashcp .env.example .env
Instalar dependencias de desarrolloEste comando utiliza la imagen de PHP de Docker para instalar dependencias como PHPUnit.Bashdocker-compose run --rm composer install
Levantar los serviciosEsto iniciará los contenedores de PHP y MySQL.Bashdocker-compose up -d
Crear la Base de DatosEjecuta el script schema.sql para crear las tablas en tu base de datos MySQL.Bashdocker-compose exec -T mysql mysql -uTU_USUARIO -pTU_PASSWORD TU_BASE_DE_DATOS < database/schema.sql
(Reemplaza los valores con los que definiste en tu archivo .env)La API ahora estará disponible en http://localhost:8080 (o el puerto que configures).🏛️ Arquitectura y Flujo de PeticiónEl flujo de una petición típica sigue este camino para mantener el código organizado:public/index.php: Recibe todas las peticiones gracias a .htaccess.Router: Un enrutador simple (a crear en core/ o similar) analiza la URL y el método HTTP.Middleware: El router ejecuta los Middleware relevantes (ej. AuthMiddleware) para verificar permisos.Controller: Si el middleware pasa, se llama al método del Controller correspondiente.Validator: El controlador usa una clase de Validators para limpiar y validar los datos de entrada.Service: El controlador delega toda la lógica de negocio a una clase en Services.Model: El servicio interactúa con uno o más Models para acceder o modificar los datos en la base de datos a través de PDO.Response: El controlador recibe el resultado del servicio y utiliza una utilidad de Response para enviar la respuesta JSON estandarizada al cliente.

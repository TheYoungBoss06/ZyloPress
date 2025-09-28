# ZyloPress

## English Version

**ZyloPress** is a professional, secure, and modular backend framework for **Zylo**, inspired by Express.js, ready for production use. It includes routing, middleware, authentication, database integration, HAST helpers, error handling, caching, and automatic API documentation.

### Features

- **HTTP Server**: GET, POST, PUT, DELETE with async/await support  
- **Modular Routing**: Organize routes by modules (`/users`, `/products`)  
- **Security Middlewares**:  
  - CORS  
  - Helmet  
  - CSRF  
  - Rate limiting  
  - JWT authentication  
  - Bcrypt password hashing  
  - Input validation  
- **Database**: PostgreSQL pool, secure queries  
- **Logging**: Request and error logging  
- **HAST Helpers**: Safe HTML generation for frontend Zylo integration  
- **Error Handling**: Centralized middleware for structured errors  
- **Caching**: Optional cache middleware per route  
- **API Documentation**: Automatic generation of API docs in JSON, accessible via `/docs` endpoint  
- **Testing Support**: Unit and E2E test helpers  
- **CI/CD Ready**: Scripts for lint, tests, documentation, and deployment

### Project Structure

zylopress/
├── zylopress.zylo # Main app() with routes, middleware, errors, cache, docs
├── router.zylo # Router class for modular routes
├── middleware.zylo # Security + errorHandler + cache
├── security/
│ ├── jwt.zylo
│ ├── bcrypt.zylo
├── utils.zylo # Logger, validator, HAST helpers
├── db/
│ └── pool.zylo
├── docs/ # Generated API documentation
└── tests/ # Unit and E2E tests

pgsql
Copiar código

### Usage Example

```zylo
import zylopress from "../zylo-press/zylopress"

var app = zylopress()

app.use(middleware.helmet())
app.use(middleware.cors())
app.use(middleware.rateLimit({ window: 60, max: 100 }))
app.use(middleware.logger())

app.get("/users", async (req, res) => {
    var users = await db.query("SELECT * FROM users")
    res.json(users)
})

app.post("/login", async (req, res) => {
    var { email, password } = req.body
    var user = await db.query("SELECT * FROM users WHERE email = $1", [email])
    if (!user) return res.status(404).json({ error: "User not found" })
    if (!bcrypt.compare(password, user.password)) return res.status(401).json({ error: "Invalid password" })
    var token = jwt.sign({ id: user.id, role: user.role }, "secret", { expiresIn: "1h" })
    res.json({ token })
})

app.listen(3000, () => show.log("ZyloPress server running on port 3000"))
Versión en Español
ZyloPress es un framework profesional, seguro y modular para Zylo, inspirado en Express.js, listo para producción. Incluye rutas, middlewares, autenticación, integración con base de datos, helpers HAST, manejo de errores, cache y documentación automática de API.

Funcionalidades
Servidor HTTP: GET, POST, PUT, DELETE con soporte async/await

Rutas modulares: Organiza rutas por módulos (/users, /products)

Middlewares de seguridad:

CORS

Helmet

CSRF

Rate limiting

Autenticación JWT

Hashing de contraseñas con Bcrypt

Validación de entradas

Base de datos: Pool de PostgreSQL y consultas seguras

Logging: Registro de peticiones y errores

HAST Helpers: Generación segura de HTML para frontend Zylo

Manejo de errores: Middleware centralizado para errores estructurados

Cache: Middleware de cache opcional por ruta

Documentación de API: Generación automática en JSON, accesible en /docs

Soporte de testing: Helpers para unit y E2E tests

Preparado para CI/CD: Scripts de lint, tests, documentación y despliegue

Estructura del Proyecto
bash
Copiar código
zylopress/
├── zylopress.zylo          # Función app() con rutas, middlewares, errores, cache, docs
├── router.zylo             # Clase Router para rutas modulares
├── middleware.zylo         # Middlewares de seguridad + errorHandler + cache
├── security/
│   ├── jwt.zylo
│   ├── bcrypt.zylo
├── utils.zylo              # Logger, validator, helpers HAST
├── db/
│   └── pool.zylo
├── docs/                   # Documentación de API generada
└── tests/                  # Unit y E2E tests
Ejemplo de Uso
zylo
Copiar código
import zylopress from "../zylo-press/zylopress"

var app = zylopress()

app.use(middleware.helmet())
app.use(middleware.cors())
app.use(middleware.rateLimit({ window: 60, max: 100 }))
app.use(middleware.logger())

app.get("/users", async (req, res) => {
    var users = await db.query("SELECT * FROM users")
    res.json(users)
})

app.post("/login", async (req, res) => {
    var { email, password } = req.body
    var user = await db.query("SELECT * FROM users WHERE email = $1", [email])
    if (!user) return res.status(404).json({ error: "Usuario no encontrado" })
    if (!bcrypt.compare(password, user.password)) return res.status(401).json({ error: "Contraseña inválida" })
    var token = jwt.sign({ id: user.id, role: user.role }, "secret", { expiresIn: "1h" })
    res.json({ token })
})

app.listen(3000, () => show.log("Servidor ZyloPress corriendo en puerto 3000"))
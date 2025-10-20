# Node.js Project Structure (DevSecOps Perspective)

## 1. Root-level Files
| File | Description |
|------|--------------|
| **`package.json`** | Declares the Node.js project, dependencies, and scripts for running, testing, and building. Key for reproducible environments in CI/CD. |
| **`Dockerfile`** | Defines how the backend service is built and executed in a container — critical for the *Build* and *Release* stages. |
| **`.env`** | Holds environment variables (database URI, JWT secret, etc.). **Must be protected** — never store real secrets in Git. |
| **`.gitignore`** | Lists files and folders excluded from version control (`node_modules/`, `.env`, logs, etc.). |
| **`ejemplos/transporttypes.json`** | Example JSON dataset, possibly used for local testing or populating the database. |

---

## 2. `src/` Folder
Contains all the backend source code — application logic, database models, routes, and service layers.

### 📁 `models/`
Defines Mongoose **schemas and models** representing MongoDB collections (e.g., `UserModel`, `ActivityModel`, `TransportTypeModel`).  
Responsible for database structure and validation.

> 🧩 Uses **Mongoose** as the ODM (Object Data Modeling) library to communicate with MongoDB.

### 📁 `routes/`
Defines the **API endpoints** of the backend (e.g., `/auth`, `/users`, `/activities`).  
Each file typically maps an Express router to controller or service logic.

### 📁 `services/`
Implements the **business logic** for each feature (authentication, user management, transport types, etc.).  
Services act as the intermediary between routes and models.

### 📁 `services/utils/`
Contains helper modules shared across the project:
- **`Factory.js`** — Factory pattern utilities.
- **`OxygenError.js`** — Centralized error handling class.
- **`Tokens.js`** — JWT token generation and validation.
- **`UserAuth.js`** — Authentication helper for Express middleware.

#### 📁 `validators/`
Houses data validation functions (input sanitization, schema validation before DB operations).

### 📄 `service.js`
Entry point of the backend — likely initializes Express, connects to MongoDB via Mongoose, and loads routes dynamically.

---

## 3. MongoDB Integration
The backend connects to MongoDB using the **Mongoose** library, which provides:
- Schema-based modeling for MongoDB documents.
- Query building and validation.
- Middleware hooks for pre/post operations.

> 💡 Example connection pattern (from `service.js` or similar):

```js
const mongoose = require('mongoose');
mongoose.connect(process.env.MONGO_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true
});
```

---

## 4. DevSecOps Considerations
- **Static code analysis** (ESLint, SonarQube) targets `src/` to enforce quality and detect vulnerabilities.  
- **Unit tests** (e.g., Jest) can validate routes and services independently.  
- **Secrets scanning** and **container image scanning** ensure secure CI/CD pipelines.  
- The `Dockerfile` encapsulates dependencies and environment configuration for deployment.

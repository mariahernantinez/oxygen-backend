# OxygenService Backend

## Descripción
**OxygenService** es el servicio backend de la aplicación Oxygen8.  
Está desarrollado en **Node.js** con **Express**, y proporciona las APIs necesarias para la gestión de usuarios, autenticación, actividades y tipos de transporte, utilizando **MongoDB** como base de datos.

El código está organizado en capas bien definidas: modelos, servicios, rutas y utilidades.

---

## ⚙️ Tecnologías principales

- **Node.js** v20.x  
- **Express** (framework web principal)
- **Mongoose** (ODM para MongoDB)
- **JWT (jsonwebtoken)** para autenticación
- **bcrypt / bcryptjs** para encriptación de contraseñas
- **dotenv** para configuración de variables de entorno
- **morgan** para logging de peticiones

## Ejecución local

### Instalar dependencias
```bash
npm install
```

### Configurar entorno
Crea un archivo `.env` en la raíz con el siguiente contenido (o adapta al entorno real):

```bash
PORT=8000
MONGODB_URI=mongodb://localhost:27017/oxygen
JWT_SECRET=supersecretkey
```

### Ejecutar el servidor
```bash
npm start
```
El backend quedará disponible en [http://localhost:8000](http://localhost:8000)

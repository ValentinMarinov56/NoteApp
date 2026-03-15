# NoteApp

Simple backend service for creating, reading, updating and deleting notes.  
Built with Node.js, Express and MongoDB and includes user authentication.

## 🧱 Tech Stack

- **Node 18+ / Express 5** – REST API framework  
- **MongoDB / Mongoose** – NoSQL persistence  
- **JWT** – Token‑based authentication  
- **bcrypt** – Password hashing  
- **ESLint** – Linting (with @stylistic plugin)  
- **Supertest / node:test** – API testing  
- **Docker & Docker‑Compose** (optional)

## 📁 Project structure

```
NoteApp/
├── app.js                   # Express application
├── index.js                 # Server entry point
├── package.json             # Node dependencies & scripts
├── mongo.js                 # (optional) connection helper
├── controllers/             # Express routers
│   ├── login.js
│   ├── notes.js
│   └── users.js
├── models/
│   ├── note.js
│   └── user.js
├── utils/
│   ├── config.js
│   ├── logger.js
│   └── middleware.js
└── tests/                   # integration tests
    ├── note_api.test.js
    └── test_helper.js
```

## ✅ Features

- **Notes API**  
  - `GET /api/notes` – list all notes (populates note owner)  
  - `GET /api/notes/:id` – fetch single note  
  - `POST /api/notes` – create note (requires valid JWT)  
  - `PUT /api/notes/:id` – update content/important flag  
  - `DELETE /api/notes/:id` – delete note

- **User management**  
  - `POST /api/users` – register new user (username must be unique)  
  - `GET /api/users` – list users with their notes

- **Authentication**  
  - `POST /api/login` – receive JWT after providing username & password  
  - Token is required in `Authorization: Bearer <token>` header for note creation

- **Middleware**  
  - Request logging, unknown endpoint, error handling (validation, JWT, etc.)

- **Tests**  
  - Comprehensive API tests with Supertest and in‑memory MongoDB config  
  - Helper utilities for initial data and database state checks

## 📦 Installation

```bash
# clone repository
git clone <repo-url>
cd NoteApp

# install dependencies
npm install
```

## 🚀 Running the app

### Local

1. Create `.env` with the following variables (example values):

   ```
   MONGODB_URI=mongodb://localhost:27017/noteapp
   TEST_MONGODB_URI=mongodb://localhost:27017/noteapp-test
   PORT=3001
   SECRET=your‑jwt‑secret‑≥16‑chars
   ```

2. Start development server:

   ```bash
   npm run dev
   ```

   Production mode:

   ```bash
   npm start
   ```

3. API listens on `http://localhost:3001` by default.

### With Docker

```bash
docker compose up --build
```

*(Adjust `docker-compose.yml` if added – not present in repository by default.)*

## 🧪 Testing

```bash
npm test
```

Tests reset the database and close the Mongo connection automatically.

## 📋 Scripts

| Command       | Description                       |
|---------------|-----------------------------------|
| `npm run dev` | start server with `--watch` for development |
| `npm start`   | launch in production              |
| `npm test`    | run tests (NODE_ENV=test)         |
| `npm run lint`| run ESLint                        |

## 📚 API Examples

```http
POST /api/login
Content-Type: application/json

{ "username": "root", "password": "salainen" }
```

```http
POST /api/notes
Authorization: Bearer <token>
Content-Type: application/json

{ "content": "Remember the milk", "important": true }
```

## 🔧 Configuration

Environment variables are managed in `utils/config.js`.

- `MONGODB_URI` – production database
- `TEST_MONGODB_URI` – used when `NODE_ENV=test`
- `PORT` – server port
- `SECRET` – JWT signing key

## 📄 License

This project is available under the MIT License. See LICENSE file for details.

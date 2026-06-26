# CogniDispatch Admin Service

The **Admin Service** is a microservice inside the **CogniDispatch** platform. It provides administrative features, database seeding, telemetry controls, and system statistics for managing dispatcher and vendor entities.

## 🚀 Technology Stack
*   **Runtime**: Node.js (v18+)
*   **Web Framework**: Express.js
*   **Security Headers**: Helmet
*   **Cross-Origin Request Sharing**: CORS
*   **Shared Modules**: Local file reference to `shared` (DB Adapter, utilities, seed data)

---

## 📁 Repository Structure
```
├── controllers/          # Express route controllers (admin logic)
├── shared/               # Shared logic (database connection, seeds, mocks)
│   ├── dbAdapter.js      # MongoDB/CosmosDB adapter
│   ├── seed.js           # DB seeding script
│   └── data/             # Sample JSON datasets
├── Dockerfile            # Multi-stage production container build
├── package.json          # Node dependencies
└── server.js             # Service entrypoint
```

---

## ⚙️ Environment Variables & Config
When running, this service expects the following configuration:

| Variable | Description | Default |
| :--- | :--- | :--- |
| `PORT` | Listening TCP Port for the service | `5004` |
| `MONGODB_URI_FILE` | Path to file containing Cosmos DB connection string (when Key Vault Secrets Store CSI is used) | *None* |
| `JWT_SECRET_FILE` | Path to file containing JWT token secret | *None* |

---

## 🛣️ API Endpoints

All routes are prefixed with `/api/admin`.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| **GET** | `/api/admin/health` | Service health status check |
| **POST** | `/api/admin/seed` | Seed or reset default database collections (Users, Vendors, Dispatches) |
| **GET** | `/api/admin/stats` | View cluster aggregates and platform throughput |

---

## 🛠️ Local Development

### 1. Prerequisite Installations
*   Node.js (v18 or higher)
*   A running local MongoDB instance (or Cosmos DB emulator)

### 2. Startup Commands
From the service root:
```bash
# Install dependencies
npm install

# Run the development server
npm start
```
The server will start listening at `http://localhost:5004/`.

---

## 🐳 Docker Container Build

Build and tag the production container image locally:
```bash
docker build -t cogniregistry.azurecr.io/cogni-admin-service:latest .
```

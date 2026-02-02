
# 🛒 Supermarket – Full-Stack E-commerce Application

Modern supermarket web app with customer shopping + admin panel.

- **Frontend**: React 19 + TypeScript + Vite  
- **Backend**:  Python Flask + SQLAlchemy (SQLite) + JWT  
- **Features**: product catalog, cart, checkout, order history, admin CRUD (products/categories/orders/users)

## 🎯 Quick Start – Fastest Way (Docker)

```bash
# 1. Start backend (port 3000)
docker pull dotcoms/supermarket-backend:latest
docker run -d -p 3000:3000 dotcoms/supermarket-backend:latest

# 2. Start frontend (port 80)
docker pull dotcoms/supermarket-frontend:latest
docker run -d -p 80:80 dotcoms/supermarket-frontend:latest
```

→ Open http://localhost

> The Docker images already contain seeded test data.

Test accounts (all passwords: `Test123!`):

| Role     | Email                |
|----------|----------------------|
| Admin    | admin@test.com       |
| Manager  | manager@test.com     |
| Customer | customer@test.com    |

## 🚀 Quick Start – Local Development

### Prerequisites

- Node.js 18+ / npm
- Python 3.11+
- Git

### Step-by-step

```bash
# 1. Clone repository
git clone <your-repo-url>
cd supermarket

# 2. Backend
cd backend-py
python -m venv venv
source venv/bin/activate     # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Optional: fresh database + test data
rm database.sqlite           # or supermarket.db – whatever your config uses
python seed_database.py

# Start backend
python -m src.main
# → http://localhost:3000
```

```bash
# 3. Frontend (in new terminal)
cd ../frontend
npm install
npm run dev
# → http://localhost:5173
```

Frontend expects backend at `http://localhost:3000`

## 🛠️ Tech Stack

| Layer      | Technologies                              |
|------------|-------------------------------------------|
| Frontend   | React 19, TypeScript, Vite, React Router 7, Zustand, Axios |
| Backend    | Python 3.11, Flask, SQLAlchemy, JWT, Flask-CORS |
| Database   | SQLite (file-based)                       |
| Deployment | Docker (separate images per layer)        |

## ✨ Main Features

**Customer**
- Browse & search products
- Category navigation
- Cart & checkout
- Order history
- Profile

**Admin / Manager**
- Dashboard (stats, low-stock alerts)
- Product CRUD
- Category management
- Order status management
- User role management

## 🔐 Test Credentials

All environments use the same test accounts:

| Role     | Email                | Password   |
|----------|----------------------|------------|
| Admin    | admin@test.com       | Test123!   |
| Manager  | manager@test.com     | Test123!   |
| Customer | customer@test.com    | Test123!   |

## 📁 Project Structure (simplified)

```
supermarket/
├── frontend/                # React + Vite app
│   ├── src/
│   │   ├── api/
│   │   ├── components/
│   │   ├── features/
│   │   ├── store/ (Zustand)
│   │   └── routes/
│   └── vite.config.ts
│
├── backend-py/              # Flask API
│   ├── src/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── routes/
│   │   └── main.py
│   ├── public/uploads/
│   ├── seed_database.py
│   └── requirements.txt
```

## 📌 Important Backend API Endpoints

**Auth**
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET  /api/auth/me`

**Products**
- `GET  /api/products`
- `GET  /api/products/:id`
- `POST /api/products` (admin)
- `PUT  /api/products/:id` (admin)
- `DELETE /api/products/:id` (admin)

**Orders**
- `GET  /api/orders` (own orders)
- `POST /api/orders`
- `PUT  /api/orders/:id/status` (admin/manager)

**Admin only**
- `GET  /api/users`
- `PUT  /api/users/:id/role`
- `DELETE /api/users/:id`

(Full list available in original backend README)

## 🔄 Reset & Re-seed Database

```bash
cd backend-py
rm database.sqlite
python seed_database.py
```

Includes:
- 60 categories (12 parents + subcategories)
- 62 products (some low/out-of-stock for testing)
- 5 realistic orders in different states

## ⚙️ Environment Variables (backend)

| Name         | Description                  | Required? | Default    |
|--------------|------------------------------|-----------|------------|
| `PORT`       | Server port                  | no        | 3000       |
| `JWT_SECRET` | Secret for signing tokens    | **yes**   | —          |
| `DB_STORAGE` | SQLite file path             | no        | `./database.sqlite` |
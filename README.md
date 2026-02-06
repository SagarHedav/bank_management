# Bank Management System (PERN)

Full‑stack Bank Management System built with:
- React (Create React App) in `client/`
- Node.js + Express API in `server/`
- PostgreSQL (Neon) database

Live API: [[API base](https://bank-management-system-ivbu.onrender.com)]/ 
Live Frontend: [[Frontend URL](https://bank-management-system-1-xj5k.onrender.com)] 

## 🧭 Project Structure
```
.
├── client/                          # React frontend (CRA)
│   ├── src/components/              # UI components
│   └── src/utils/api.js             # API helper (uses REACT_APP_API_URL)
├── server/                          # Express API
│   ├── app.js                       # Routes/controllers/middleware
│   ├── database.js                  # pg Pool + env config
│   └── database-setup/              # SQL helpers for schema/seed
├── render.yaml                      # Render config (API)
├── neon-db-init.sql                 # Optional seed helpers
└── README.md                        # This file
```

## ⚙️ Environment Variables

Server (`server/.env`)
```
# Prefer a single DATABASE_URL on Render/Neon
DATABASE_URL=postgresql://USER:PASSWORD@HOST:PORT/DB
# or individual variables for local dev
DB_USER=postgres
DB_PASSWORD=postgres
DB_HOST=localhost
DB_PORT=5433
DB_NAME=BANK
# Optional CORS front-end origin
FRONTEND_URL=https://your-frontend.onrender.com
NODE_ENV=production
```

Client (`client/.env`)
```
REACT_APP_API_URL=https://your-api.onrender.com
```

## ▶️ Local Development
- Terminal 1 (API)
  ```bash
  cd server && npm install && npm run dev
  ```
  Runs on http://localhost:5000

- Terminal 2 (Frontend)
  ```bash
  cd client && npm install && npm start
  ```
  CRA dev server on http://localhost:3000

## 🚀 Deployment (Render)
API (Web Service)
- Root Directory: `server`
- Build Command: `npm ci`
- Start Command: `node app.js`
- Health Check Path: `/ping`
- Env: set `DATABASE_URL`, remove custom `PORT`

Frontend (Static Site)
- Build Command: `npm ci && npm run build`
- Publish Directory: `client/build`
- Set `REACT_APP_API_URL` in environment

## 🔌 API Overview
Auth
- POST `/customer/login`
- POST `/employee/login`
- POST `/manager/login`

Resources
- Customers: GET `/customer`, POST `/customer`, PUT `/customer/:customer_id`, DELETE `/customer/:customer_id`
- Employees: GET `/employee`, POST `/employee`, PUT `/employee/:emp_id`, DELETE `/employee/:username`
- Branches: GET `/branch`, POST `/branch`, PUT `/branch/:branch_id`, DELETE `/branch/:branch_id`
- Accounts: GET `/accounts`, GET `/accounts/:customer_id`, POST `/accounts`, DELETE `/accounts/:account_id`
- Transactions: GET `/transaction/:customer_id`, POST `/transaction`

Health/Debug
- GET `/ping` (liveness)
- GET `/health` (DB check)
- GET `/debug/tables` (introspection)

## 🗃️ Database Notes (Neon)
- `server/database.js` uses `DATABASE_URL` if present; otherwise individual vars.
- SSL is enabled for production. Ensure Neon requires SSL or set appropriately.
- Seeding: you can use `neon-db-init.sql` or the SQL append scripts you ran.

## 🔐 Security & CORS
- CORS allows your `FRONTEND_URL` and any `*.onrender.com` origin.
- Parameterized queries with `pg`.
- Basic input validation and error handling.

## 🖼️ Demo Screenshots


![Home](demo/home.png)
![Customer Dashboard](demo/customer-dashboard.png)
![Accounts](demo/accounts.png)
![Transactions](demo/transactions.png)
![Admin Employee](demo/admin-employee.png)
![Admin Manager](demo/admin-branches.png)
![Customer Management](demo/customer-control.png)
![Employee Management](demo/employee-control.png)
![Branch Management](demo/branch-control.png)


## 📝 Scripts
Root shortcuts (optional):
```bash
npm run dev        # cd server && npm run dev
npm start          # cd server && npm start
```

## 🙌 Credits
Built by Sagar Hedav


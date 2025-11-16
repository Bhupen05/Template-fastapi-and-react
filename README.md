# Farm Stack Full-Stack Template

Simple template for spinning up the Farm Stack backend (FastAPI) and frontend (React) with Docker.

## Contents
- `Farm-Stack-Backend-Template/`
- `Farm-Stack-Frontend-Template/`
- `install-backend.bat`

## Prerequisites
- Docker Desktop 4.30+
- Node.js 20+
- Python 3.10+
- Git Bash or PowerShell

## Quick start

```bash
# clone repo
git clone https://github.com/your-org/farm-stack-template.git
cd farm-stack-template
```

```powershell
# start everything
docker compose up --build
```

Backend runs at `http://localhost:10001`, frontend at `http://localhost:3000`.

## Backend (FastAPI + MongoDB + MySQL + Redis)
1. Copy `.env.example` to `.env` and set secrets (JWT, DB credentials, SMTP).
2. Ensure Docker services `redis`, `mongodb`, and `mysql` are up.
3. Develop locally:
   ```bash
   cd Farm-Stack-Backend-Template
   python -m venv .venv && .venv\Scripts\activate
   pip install -r requirements.txt
   uvicorn server:app --reload --host 0.0.0.0 --port 10001
   ```

## Frontend (React + Vite)
1. Install deps:
   ```bash
   cd Farm-Stack-Frontend-Template
   npm install
   ```
2. Run dev server:
   ```bash
   npm run dev -- --host 0.0.0.0 --port 3000
   ```

## Useful commands
- `docker compose down -v` – stop stack and remove volumes.
- `pytest` – backend tests.
- `npm run test` – frontend tests.
- `install-backend.bat` – Windows shortcut to install backend requirements.

## Project structure
```📦Farm-Stack-Backend-Template
 ┣
 ┣ 📂api                 ⊙ This is Base API folder
 ┃ ┣ 📂db                ⊙ Demo DB configuration
 ┃ ┃ ┗ 📜__init__.py
 ┃ ┣ 📂extensions        ⊙ Extension Folder. Make Extensions Here
 ┃ ┃ ┣ 📂discord
 ┃ ┃ ┃ ┗ 📜discordBot.py  
 ┃ ┃ ┗ 📂etc             
 ┃ ┣ 📂models            ⊙ This is Models folder to Store Schema of Objects
 ┃ ┃ ┗ 📜Room.py         
 ┃ ┣ 📂socket            ⊙ Base Folder for Sockets 
 ┃ ┃ ┗ 📜__init__.py     ⊙ You can Configure more Socket events in this. 
 ┃ ┗ 📂versions          ⊙ Manage API version in this.
 ┃ ┃ ┣ 📂v1              ⊙ Version 1 File Development goes here
 ┃ ┃ ┃ ┣ 📂room          ⊙ Files Related to Room Management Goes here
 ┃ ┃ ┃ ┃ ┗ 📜root.py     ⊙ Root File for Rooms management
 ┃ ┃ ┃ ┗ 📜__init__.py   ⊙ This is API Version 1 Base File 
 ┃ ┃ ┣ 📂v2              ⊙ Version 2 Api files Goes here 
 ┃ ┃ ┃ ┗ 📜__init__.py   ⊙ This Is Demo Of Version 2 Configuration
 ┃ ┃ ┗ 📜__init__.py     ⊙ This is Base file Of API Version Management Add New Versions Using This
 ┣ 📂static              ⊙ This is Static Folder to Store Static Files
 ┃ ┗ 📜socket.io.min.js  ⊙ Dont remove this File It is needed For Long Polling
 ┣ 📜bind.py             ⊙ It Binds API , Socket You Can Configure Middlewares in this File or JWT configuration
 ┣ 📜devices.db          ⊙ This is Sqlite database for the default room Management example
 ┣ 📜req.txt             ⊙ Install these Packages
 ┣ 📜server.py           ⊙ Configure Port in this
 ┗ 📜z.bat               ⊙ Auto Start Script for Windows after venv configuration```

 ```📦Farm-Stack-Frontend-Template
 ┣
 ┣ 📂public              ⊙ Static assets served by Vite
 ┃ ┗ 📜favicon.svg
 ┣ 📂src                 ⊙ Main React source code
 ┃ ┣ 📂components        ⊙ Shared UI components
 ┃ ┃ ┣ 📜Header.tsx
 ┃ ┃ ┗ 📜Footer.tsx
 ┃ ┣ 📂pages             ⊙ Route-level pages
 ┃ ┃ ┣ 📜Dashboard.tsx
 ┃ ┃ ┗ 📜Settings.tsx
 ┃ ┣ 📂hooks             ⊙ Custom React hooks
 ┃ ┣ 📂services          ⊙ API utilities for backend calls
 ┃ ┣ 📂styles            ⊙ Global and module CSS files
 ┃ ┣ 📜App.tsx           ⊙ Root React component
 ┃ ┗ 📜main.tsx          ⊙ Entry point rendered by Vite
 ┣ 📜index.html          ⊙ HTML shell
 ┣ 📜package.json        ⊙ NPM scripts and deps
 ┣ 📜tsconfig.json       ⊙ TypeScript config
 ┗ 📜vite.config.ts      ⊙ Vite dev/build config
 ```

## Conventions
- Use feature branches: `git checkout -b feature/<name>`.
- Submit PRs with lint + test results.
- Keep README in sync when adding services.

## Troubleshooting
| Issue | Fix |
| --- | --- |
| Mongo hostname error | Set `MONGO_SERVER_URL=mongodb://mongodb:27017` |
| MySQL driver missing | Install `mysqlclient` or switch to `PyMySQL` |
| Ports inaccessible | Map explicitly (`10001:10001`, `3000:3000`) |

Happy hacking!
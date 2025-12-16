# AkuBantu
Pengembangan layanan rekomendasi learning path untuk mahasiswa Indonesia berbasis knowledge-based recommender dengan metode Human-Centered Design — panduan singkat untuk menjalankan proyek ini secara lokal dan menyiapkannya untuk deployment.

**Ringkasan struktur**
- **backend/**: server Python (Flask) dan API.
- **frontend/**: aplikasi web (Vite + React).
- `Procfile`, `railway.toml`: konfigurasi deployment.
- `requirements.txt` (root) dan `backend/requirements.txt`: dependency Python.

**Prasyarat**
- Python 3.10 (atau 3.9+); pip.
- Node.js (v18+) dan npm/yarn untuk frontend.
- Git (opsional).

**Pengaturan environment**
- Salin `backend/.env.example` (jika ada) menjadi `backend/.env` dan isi variabel yang dibutuhkan.
- Atau buat file environment di `backend/.env` berisi variabel penting seperti:

```env
OPENAI_API_KEY=your_openai_key
MAIL_USERNAME=you@example.com
MAIL_PASSWORD_APP=app_password_for_mail
MIDTRANS_SERVER_KEY=midtrans_server_key
MIDTRANS_CLIENT_KEY=midtrans_client_key
MIDTRANS_IS_PRODUCTION=False
SECRET_KEY=some_random_secret
GOOGLE_CLIENT_ID=your_google_client_id
PORT=8080
FLASK_DEBUG=1
```

- Untuk frontend, edit `frontend/.env` atau export variabel berikut:

```env
VITE_API_URL=http://localhost:8080
VITE_MIDTRANS_CLIENT_KEY=your_midtrans_client_key
```

Catatan: `frontend/.env` di repo berisi `VITE_API_URL` yang perlu diperbaiki/diubah bila Anda menjalankan lokal.

**Menjalankan backend (lokal)**
1. Buat virtual environment dan aktifkan (Windows PowerShell contoh):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Pasang dependency:

```powershell
pip install -r backend/requirements.txt
```

3. Siapkan `backend/.env` seperti contoh di atas.

4. Jalankan server:

```powershell
cd backend
python app.py
```

Server akan jalan di `0.0.0.0:8080` (port dapat diubah melalui variabel `PORT`).

Catatan: file database SQLite (`webai.db`) akan dibuat otomatis saat pertama kali server dijalankan.

**Menjalankan frontend (lokal)**
1. Masuk ke folder frontend, pasang dependency dan jalankan dev server:

```bash
cd frontend
npm install
npm run dev
```

2. Buka URL yang diberikan oleh Vite (biasanya `http://localhost:5173`) — pastikan `VITE_API_URL` mengarah ke backend lokal (`http://localhost:8080`).

**Build untuk production (frontend)**

```bash
cd frontend
npm run build
```

Build output akan berada di folder `frontend/dist` (standar Vite).

**Deployment (petunjuk singkat)**
- Railway / Heroku: repo sudah menyertakan `Procfile` (menjalankan `python backend/app.py`) dan `railway.toml` yang meng-invoke `pip install -r backend/requirements.txt`.
- Untuk deployment, pastikan variabel environment (OpenAI, mail, Midtrans, SECRET_KEY, dll.) terpasang di layanan Anda.

**File penting & referensi**
- Backend entry: [SEM 5/RPL/PRAKTIKUM/AkuBantu/backend/app.py](SEM%205/RPL/PRAKTIKUM/AkuBantu/backend/app.py)
- Konfigurasi Python deps: [SEM 5/RPL/PRAKTIKUM/AkuBantu/backend/requirements.txt](SEM%205/RPL/PRAKTIKUM/AkuBantu/backend/requirements.txt)
- Frontend project: [SEM 5/RPL/PRAKTIKUM/AkuBantu/frontend/package.json](SEM%205/RPL/PRAKTIKUM/AkuBantu/frontend/package.json)
- Deploy config: [SEM 5/RPL/PRAKTIKUM/AkuBantu/Procfile](SEM%205/RPL/PRAKTIKUM/AkuBantu/Procfile) and [SEM 5/RPL/PRAKTIKUM/AkuBantu/railway.toml](SEM%205/RPL/PRAKTIKUM/AkuBantu/railway.toml)

**Catatan keamanan & tips**
- Jangan commit kredensial ke Git. Gunakan Secret Manager dari platform hosting atau `.env` yang di-ignore.
- Untuk email via Gmail, gunakan App Password dan set `MAIL_USERNAME` serta `MAIL_PASSWORD_APP`.
- Jika menggunakan Midtrans, pastikan `MIDTRANS_IS_PRODUCTION` sesuai mode.


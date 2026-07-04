<div align="center">
  <h1>🎓 SC-DATA (Smart Campus Data & AI Assistant)</h1>
  <p><b>V16 All Accounts Elite — Infrastruktur Digital Kampus Berbasis Performa Tinggi</b></p>
</div>

<br/>

**SC-DATA** adalah sebuah prototipe *Super App* dan *Command System* terpadu yang dirancang khusus untuk ekosistem universitas. Sistem ini menggabungkan manajemen data akademik (SIAKAD), analitik presensi *real-time*, mesin pencari dokumen akademik berbasis AI (RAG), hingga manajemen karir mahasiswa dalam satu antarmuka UI/UX premium berbasis *glassmorphism*.

## 🚀 Fitur Utama

Sistem ini memiliki **17+ Modul Fungsional**, di antaranya:
- **🗄️ Data Pipeline Builder (ETL)**: Memproses dan memvalidasi otomatis 6 file CSV utama (Mahasiswa, Dosen, MK, KRS, Nilai, Kehadiran).
- **📊 Real-Time Event Monitor**: Dasbor observabilitas untuk melacak trafik kehadiran kampus (Hadir, Izin, Sakit, Alfa) layaknya *monitoring* jaringan IT.
- **🤖 AI Academic Document Search (RAG)**: AI pencarian pedoman kampus berbasis algoritma TF-IDF yang dijamin bebas halusinasi karena selalu mengutip dokumen sumber.
- **🛡️ Role-Based Access Control (RBAC)**: Pemisahan 4 tingkat hak akses mutlak (Mahasiswa, Dosen, Administrator, Pimpinan) lengkap dengan *Immutable Audit Trail*.
- **📄 Paperless Campus**: Autogenerasi Kartu Ujian Digital (PDF) dan Surat Keterangan Mahasiswa Aktif.
- **💼 Ekosistem Mahasiswa**: Modul Manajemen KRS, Pembayaran SPP/UKT, Perpustakaan Digital, Pelacakan PKL/Magang, dan Bursa Beasiswa.

## 🏗️ Arsitektur Sistem (3-Tier)

Kami menggunakan arsitektur yang berorientasi pada kecepatan tanpa mengorbankan fleksibilitas antarmuka pengguna:

1. **Presentation Layer (Frontend)**: `HTML5` + `CSS3` + `Vanilla JS`. Tidak menggunakan Streamlit/Framework Python agar UI sangat cepat, interaktif, dan memungkinkan desain efek *glassmorphism* premium.
2. **Application Layer (Backend)**: `FastAPI (Python)`. Berfungsi sebagai API Gateway yang asinkron, menangani keamanan (RBAC), dan eksekusi logika bisnis.
3. **Data Layer (Storage)**: `DuckDB`. Mesin *in-process analytical database* yang super ringan dan sanggup menghitung jutaan baris data agregasi secara instan tanpa hambatan (*zero-network-overhead*).

## 🛠️ Teknologi yang Digunakan
* **Backend**: Python 3.x, FastAPI, Uvicorn
* **Database**: DuckDB
* **Frontend**: HTML5, CSS3, Vanilla JavaScript
* **Paradigma AI**: Retrieval-Augmented Generation (RAG) dengan TF-IDF

## 💻 Cara Menjalankan Aplikasi Lokal (Local First)

Aplikasi ini didesain 100% luring (tanpa ketergantungan internet eksternal) untuk kemudahan *deployment*.

### 1. Menjalankan Backend (API)
Pastikan Python sudah terinstal di komputer Anda.
```bash
# Buka terminal dan masuk ke folder proyek
cd PROJECT_FINAL_SISTEMBASISDATA

# Install library yang dibutuhkan (opsional: gunakan virtual environment)
pip install fastapi uvicorn duckdb

# Jalankan server FastAPI
cd backend
uvicorn main:app --reload --host 127.0.0.1 --port 8000
```
Server backend akan berjalan di `http://127.0.0.1:8000`.

### 2. Menjalankan Frontend (UI)
Tidak perlu instalasi Node.js atau server *frontend*.
Cukup buka file `frontend/index.html` langsung dari *browser* Anda (Chrome/Firefox/Edge), atau gunakan *extension* Live Server di VSCode.

### 3. Login
Gunakan akun *mockup* berikut di halaman login:
- **Mahasiswa**: `24360007` (Aflin Awaludin)
- **Admin**: `A001`
- **Dosen**: `D001`
- **Pimpinan**: `P001`
*(Password: ketik apa saja)*

---

*Dibangun sebagai Final Project Sistem Basis Data untuk Institut Sains dan Teknologi Nasional (ISTN).*

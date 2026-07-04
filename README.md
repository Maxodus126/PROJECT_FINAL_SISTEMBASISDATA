<div align="center">
  
  # 🎓 SC-DATA (Smart Campus Data & AI Assistant)
  **V16 All Accounts Elite — Infrastruktur Digital Kampus Berbasis Performa Tinggi**

  ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
  ![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
  ![DuckDB](https://img.shields.io/badge/DuckDB-FFF000?style=for-the-badge&logo=duckdb&logoColor=black)
  ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
  ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
  
</div>

<br/>

**SC-DATA** adalah sebuah purwarupa *Super App* dan *Command System* tingkat perusahaan (Enterprise) yang dirancang untuk menjadi tulang punggung digital perguruan tinggi modern. Berbeda dengan Sistem Informasi Akademik (SIAKAD) tradisional yang berjalan lambat dan terfragmentasi, SC-DATA menggabungkan **Mesin ETL**, **Database Analitik In-Memory**, **AI Semantic Search (RAG)**, dan **Layanan Mahasiswa Terpadu** dalam satu arsitektur berkinerja tinggi (*High-Performance Architecture*).

---

## 📑 Daftar Isi
1. [Arsitektur Sistem (3-Tier)](#1-arsitektur-sistem-3-tier)
2. [Ekosistem Fitur & Modul Utama](#2-ekosistem-fitur--modul-utama)
3. [Keamanan & Tata Kelola (RBAC)](#3-keamanan--tata-kelola-rbac)
4. [Mekanisme AI (Retrieval-Augmented Generation)](#4-mekanisme-ai-retrieval-augmented-generation)
5. [Skema Database Utama](#5-skema-database-utama)
6. [Panduan Instalasi & Deployment](#6-panduan-instalasi--deployment)
7. [API Endpoints Reference](#7-api-endpoints-reference)

---

## 🏗️ 1. Arsitektur Sistem (3-Tier)

Sistem ini menghindari penggunaan *framework* SSR (*Server-Side Rendering*) yang berat seperti Streamlit demi mencapai antarmuka yang 100% interaktif (*Zero-Latency UI*). Arsitektur dirancang menjadi tiga lapisan (*tier*) independen:

```mermaid
flowchart TD
    subgraph TIER1 [PRESENTATION LAYER]
        UI["Visual UI (HTML5 + CSS Glassmorphism)"]
        Logic["Client Logic (Vanilla JavaScript)"]
    end

    subgraph TIER2 [APPLICATION LAYER]
        Gateway["FastAPI Gateway"]
        Business["Business Logic & Security (RBAC)"]
    end

    subgraph TIER3 [DATA LAYER]
        Engine[("DuckDB (In-Process OLAP)")]
        Raw["Raw Data (CSV & TXT)"]
    end

    UI <==>|HTTP REST (JSON)| Gateway
    Gateway <==>|SQL Queries| Engine
```

- **Tier 1 (Frontend)**: Dibangun murni dari bawah (*from scratch*) dengan HTML5, CSS3 kustom (efek *Glassmorphism/Aurora*), dan logika *Vanilla JavaScript* agar grafik dan rendering terjadi secara lokal di CPU peramban pengguna.
- **Tier 2 (Backend API)**: Menggunakan **FastAPI (Python)**. Memiliki kemampuan eksekusi asinkron, memvalidasi keamanan lalu lintas, dan menjembatani akses ke basis data.
- **Tier 3 (Database Engine)**: Menggunakan **DuckDB**. Sebuah *Analytical Database (OLAP)* yang beroperasi secara *in-process* (langsung di dalam memori Python), membuang latensi jaringan (network overhead) konvensional untuk mengolah jutaan baris data kehadiran dan nilai.

---

## 🚀 2. Ekosistem Fitur & Modul Utama

SC-DATA merangkum **Siklus Hidup Mahasiswa 360 Derajat**, dibagi ke dalam 5 pilar fungsional:

### A. Rekayasa Data & Infrastruktur (Data Engineering)
- **Data Pipeline Builder (ETL)**: Mengekstraksi, mentransformasi, dan memuat 6 set CSV (Data Mahasiswa, Dosen, MK, KRS, Nilai, Presensi) dengan proteksi *Auto-Quarantine* jika mendeteksi anomali (misal: duplikasi *Primary Key* atau nilai tidak valid).
- **Real-Time Event Monitor**: Endpoint ingestion simulasi *streaming* untuk mencatat log absensi. Tersedia agregasi langsung (Hadir, Izin, Sakit, Alfa) untuk observabilitas operasi rektorat.
- **Self-Validation System**: API bawaan (`/api/validation/final`) yang mengaudit kesehatan database, kesiapan struktur tabel, dan integritas *pipeline* tanpa koneksi internet.

### B. Eksekusi Akademik
- **Dasbor KRS & Jadwal Mingguan**: Menghitung beban SKS aktif dan merender jadwal kuliah dalam format *time-block* layaknya *Google Calendar*.
- **Auto-Generasi Dokumen (Paperless)**: Merender **Kartu Ujian Digital** (lengkap dengan foto, list mata ujian, ruang, dan stempel digital) serta **Surat Keterangan Mahasiswa Aktif** langsung ke PDF siap cetak.

### C. Manajemen Finansial & Fasilitas
- **Modul SPP/UKT**: Pencatatan riwayat tagihan, metode pembayaran terintegrasi, dan metrik indikator Lunas vs Tunggakan.
- **Perpustakaan Digital**: Katalog pencarian stok fisik perpustakaan, tracking buku yang sedang dipinjam, hingga integrasi akses E-Book eksternal.

### D. Akselerator Karir Mahasiswa
- **Pusat PKL/Magang & Skripsi**: *Tracking* komprehensif mulai dari tempat magang mahasiswa (contoh: perusahaan tech), dosen pendamping magang, hingga status 3 fase tahapan bimbingan skripsi.
- **Bursa Beasiswa & Tracer Study**: Daftar kuota KIP/Beasiswa eksternal beserta prasyarat IPK. Modul pencatatan karir (Tracer Study) untuk alumni fakultas.

### E. Ekosistem Sosial & Komunikasi
- **Forum Diskusi Akademik**: Wadah tanya jawab ala StackOverflow untuk memecahkan *error* kuliah atau membahas teori, per-mata kuliah.
- **Helpdesk Ticketing**: Pusat pelaporan insiden IT atau akademik (misal: "sistem *down*") yang dilacak mulai dari 'Menunggu', 'Proses', hingga 'Selesai'.

---

## 🛡️ 3. Keamanan & Tata Kelola (RBAC)

Aplikasi ini menggunakan metode **Role-Based Access Control (RBAC)** secara tegas baik di *frontend* maupun di *backend*:
- **4 Role Absolut**: `Mahasiswa`, `Dosen`, `Administrator`, `Pimpinan`.
- **Data Masking (UI)**: Menu samping (*sidebar*) otomatis bersembunyi untuk fitur yang bukan wewenang rolenya.
- **Backend Guard**: Endpoint kritis seperti `/api/events/reset` atau `/api/pipeline/run` dikunci menggunakan *dependency injection* `require_admin`. Upaya meretas sistem melalui Postman akan ditolak dengan `403 Forbidden`.
- **Immutable Audit Trail (`audit_log`)**: Setiap transaksi kritis di sistem (Login, Akses RAG, Eksekusi ETL) dicatat secara presisi (Siapa pelakunya, Modul apa, Jam berapa) untuk kebutuhan forensik dan kepatuhan (Compliance).

---

## 🧠 4. Mekanisme AI (Retrieval-Augmented Generation)

Sistem ini tidak memanggil LLM buta, melainkan membangun kecerdasannya secara internal menggunakan metode *Retrieval-Augmented Generation (RAG)*.
1. **Document Ingestion**: File Pedoman Akademik (berformat `.txt` di `docs/rag`) akan dipecah (*chunking*) per 90 kata maksimum.
2. **Indexing**: Data disimpan dalam tabel `document_chunks`.
3. **Semantic Querying**: Saat *User* bertanya via RAG Search, algoritma murni Python (TF-IDF basik) menghitung persilangan kata (Intersection) antara kueri dan *chunks*.
4. **Anti-Hallucination**: Sistem akan mengembalikan jawaban dengan mengutip secara eksplisit **Nama Dokumen Rujukan**, menjamin kebenaran mutlak tanpa halusinasi AI generatif.

---

## 📊 5. Skema Database Utama

Sistem basis data dimuat otomatis oleh `init_db.py` ke dalam `sc_data.duckdb`. Beberapa entitas relasional (*Relational Entities*) meliputi:
* `mahasiswa`, `dosen`, `mata_kuliah` (Master Data)
* `krs`, `nilai`, `kehadiran` (Transactional Data)
* `event_log` (Streaming Log Data Presensi)
* `pipeline_issue_log` (Karantina Data ETL)
* `audit_log` (Security Tracking)
* `document_chunks` (Vektor AI/RAG Data)

---

## 💻 6. Panduan Instalasi & Deployment

Proyek ini menggunakan pendekatan **Local-First / Edge Compute**, artinya Anda bisa menjalankan arsitektur masif ini cukup dari laptop pribadi tanpa *cloud dependency*.

### Prasyarat
- Python 3.9 atau lebih baru.
- Web Browser modern (Chrome/Edge/Firefox).

### Langkah Menjalankan Aplikasi
1. **Kloning Repositori**
   ```bash
   git clone https://github.com/Maxodus126/PROJECT_FINAL_SISTEMBASISDATA.git
   cd PROJECT_FINAL_SISTEMBASISDATA
   ```

2. **Instalasi Dependencies (Backend)**
   Sangat disarankan menggunakan *virtual environment*.
   ```bash
   pip install fastapi uvicorn duckdb
   ```

3. **Menyalakan Server Backend (API)**
   ```bash
   cd backend
   uvicorn main:app --reload --host 127.0.0.1 --port 8000
   ```
   *(Backend akan mulai mendengar di `http://localhost:8000`)*

4. **Menyalakan Frontend (UI)**
   Cukup klik dua kali (buka) file `frontend/index.html` menggunakan browser Anda.
   *(Opsional: Gunakan ekstensi Live Server di VSCode untuk pengalaman lebih mulus).*

### Menggunakan Akun Sandbox (Mockup)
Di halaman portal login (*V16 All Accounts Elite*), gunakan otentikasi berikut (*Password bebas*):
* **Mahasiswa**: `24360007`
* **Admin**: `A001`
* **Dosen**: `D001`
* **Pimpinan**: `P001`

---

## 🔌 7. API Endpoints Reference

Apabila Anda ingin menguji integrasi sistem eksternal, berikut adalah rute *Command Center* yang disediakan FastAPI (Akses dokumentasi Swagger lengkap di `http://127.0.0.1:8000/docs`):

| HTTP Method | Endpoint | Fungsi | Role Butuh |
|-------------|----------|--------|------------|
| `GET`       | `/api/health` | Cek status server (*heartbeat*) | - |
| `POST`      | `/api/events/load` | Menyimulasikan aliran batch absen terbaru | Admin |
| `GET`       | `/api/events/latest` | Menarik 10 antrean event log terakhir | - |
| `POST`      | `/api/pipeline/run` | Menjalankan mesin ETL memproses 6 CSV | Admin |
| `POST`      | `/api/rag/build` | Memecah `.txt` dokumen menjadi indeks RAG | Admin |
| `GET`       | `/api/rag/search?q=...` | AI Semantic Search dokumen akademik | - |
| `GET`       | `/api/audit/log` | Menarik rekaman *Immutable Audit Trail* | Admin |
| `GET`       | `/api/validation/final` | Memeriksa integritas sistem 100% | - |

---
*Dikembangkan dengan penuh ketelitian oleh Aflin Awaludin sebagai Final Project Sistem Basis Data - Institut Sains dan Teknologi Nasional (ISTN).*

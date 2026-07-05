<div align="center">
  
  # 🎓 SC-DATA (Smart Campus Data & AI Assistant)
  **V16 All Accounts Elite — Infrastruktur Digital Kampus Berbasis Performa Tinggi**

  ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
  ![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
  ![DuckDB](https://img.shields.io/badge/DuckDB-FFF000?style=for-the-badge&logo=duckdb&logoColor=black)
  ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
  ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
  
</div>

<div align="center">
  <h3>🔴 <a href="https://maxodus126.github.io/PROJECT_FINAL_SISTEMBASISDATA/frontend/index.html">LIVE DEMO UI (GITHUB PAGES) KLIK DI SINI</a> 🔴</h3>
  <p><i>Catatan: Karena GitHub Pages bersifat statis, fungsi login/backend tidak berjalan di versi demo ini.</i></p>
</div>

<br/>

**SC-DATA** adalah sebuah purwarupa *Super App* dan *Command System* tingkat perusahaan (Enterprise) yang dirancang untuk menjadi tulang punggung digital perguruan tinggi modern. Berbeda dengan Sistem Informasi Akademik (SIAKAD) tradisional yang berjalan lambat dan terfragmentasi, SC-DATA menggabungkan **Mesin ETL**, **Database Analitik In-Memory**, **AI Semantic Search (RAG)**, dan **Layanan Mahasiswa Terpadu** dalam satu arsitektur berkinerja tinggi (*High-Performance Architecture*).

---

## 📸 Cuplikan Layar (Screenshots)

*(Catatan: Buat folder `docs/images/` dan unggah file gambar Anda ke sana agar gambar di bawah ini muncul)*

<div align="center">
  <img src="docs/images/login.png" width="45%" alt="Halaman Login V16 Elite">
  <img src="docs/images/dashboard.png" width="45%" alt="Dasbor Utama Mahasiswa">
</div>
<br/>
<div align="center">
  <img src="docs/images/event_monitor.png" width="45%" alt="Event Monitor Real-Time">
  <img src="docs/images/kartu_ujian.png" width="45%" alt="Auto-Generate Kartu Ujian PDF">
</div>

---

## 📑 Daftar Isi
1. [Arsitektur Sistem (3-Tier)](#1-arsitektur-sistem-3-tier)
2. [Visualisasi Data Analytics](#2-visualisasi-data-analytics)
3. [Ekosistem Fitur & Modul Utama](#3-ekosistem-fitur--modul-utama)
4. [Skema Database Utama (ER Diagram)](#4-skema-database-utama-er-diagram)
5. [Keamanan & Tata Kelola (RBAC)](#5-keamanan--tata-kelola-rbac)
6. [Panduan Instalasi & Deployment](#6-panduan-instalasi--deployment)
7. [API Endpoints Reference](#7-api-endpoints-reference)

---

## 🏗️ 1. Arsitektur Sistem (3-Tier)

Sistem ini menghindari penggunaan *framework* SSR (*Server-Side Rendering*) yang berat seperti Streamlit demi mencapai antarmuka yang 100% interaktif (*Zero-Latency UI*). Arsitektur dirancang menjadi tiga lapisan (*tier*) independen:

```mermaid
flowchart TD
    %% Styling
    classDef layer1 fill:#1e1e2e,stroke:#89b4fa,stroke-width:2px,color:#cdd6f4
    classDef layer2 fill:#11111b,stroke:#a6e3a1,stroke-width:2px,color:#cdd6f4
    classDef layer3 fill:#181825,stroke:#f9e2af,stroke-width:2px,color:#cdd6f4

    subgraph TIER1 [1. TIER PRESENTASI / FRONTEND LAYER]
        direction TB
        UI["Visual UI (HTML5 + CSS)"]:::layer1
        Logic["Client Logic (Vanilla JavaScript)"]:::layer1
    end

    subgraph TIER2 [2. TIER APLIKASI / LOGIC LAYER]
        direction TB
        Gateway["API Gateway (FastAPI)"]:::layer2
        Business["Business Logic & AI (Pipeline, RAG)"]:::layer2
    end

    subgraph TIER3 [3. TIER DATA / STORAGE LAYER]
        direction TB
        Engine[("Database (DuckDB)")]:::layer3
        Raw["Raw Data (CSV)"]:::layer3
    end

    %% Hubungan antar Layer
    TIER1 -->|HTTP REST JSON| TIER2
    TIER2 -->|SQL Queries| TIER3

    %% Penjelasan batas
    style TIER1 fill:none,stroke:#89b4fa,stroke-width:2px,stroke-dasharray: 5 5
    style TIER2 fill:none,stroke:#a6e3a1,stroke-width:2px,stroke-dasharray: 5 5
    style TIER3 fill:none,stroke:#f9e2af,stroke-width:2px,stroke-dasharray: 5 5
```

---

## 📊 2. Visualisasi Data Analytics

Sistem secara otomatis mengubah jutaan baris log absensi dan integritas data menjadi grafik analitik untuk pimpinan kampus.

### Distribusi Kehadiran (*Real-Time Event Monitor*)
Grafik ini mewakili pemantauan trafik *event_log* yang masuk ke dalam DuckDB secara seketika.

```mermaid
pie title Agregasi Kehadiran Mahasiswa Harian
    "Hadir (85%)" : 850
    "Izin (10%)" : 100
    "Sakit (3%)" : 30
    "Alfa (2%)" : 20
```

### Karantina Data ETL (*Data Quality Issues*)
Grafik ini memetakan jenis error yang paling sering terdeteksi oleh mesin ETL dan ditolak (*quarantined*) ke `pipeline_issue_log`.

```mermaid
pie title Distribusi Isu Data Mentah (ETL Rejects)
    "Nilai Tidak Valid (>100)" : 45
    "NIM Mahasiswa Ganda (Duplikasi PK)" : 25
    "Kolom Kosong (Missing Values)" : 20
    "Format Tanggal Rusak" : 10
```

---

## 🚀 3. Ekosistem Fitur & Modul Utama

### Peta Ekosistem Fitur (Mindmap)

```mermaid
mindmap
  root((SC-DATA V16))
    (1. Infrastruktur Data & AI)
      Data Pipeline ETL
      AI RAG Search Engine
      Real-Time Event Monitor
      Audit Trail & Security RBAC
      Self-Validation System
    (2. Layanan Akademik)
      Dasbor KRS & SKS
      Jadwal Kuliah Time-Block
      Jadwal & Pengawas Ujian
      Auto-Gen Kartu Ujian PDF
      Auto-Gen Surat Keterangan
    (3. Finansial & Fasilitas)
      Tagihan SPP / UKT
      Metode Pembayaran
      E-Library & Jurnal
      Stok Buku Fisik
    (4. Akselerasi Karir)
      Manajemen PKL / Magang
      Tracking Skripsi
      Bursa Beasiswa
      Tracer Study Alumni
    (5. Ekosistem Sosial)
      Forum Diskusi Kuliah
      Helpdesk & Ticketing
      Pusat Notifikasi
      Profil UKM & Organisasi
```

SC-DATA merangkum **Siklus Hidup Mahasiswa 360 Derajat**, dibagi ke dalam 5 pilar fungsional:

### A. Rekayasa Data & Infrastruktur (Data Engineering)
- **Data Pipeline Builder (ETL)**: Memproses 6 set CSV dengan proteksi *Auto-Quarantine* jika mendeteksi anomali.
- **Real-Time Event Monitor**: Endpoint ingestion simulasi *streaming* absensi. 
- **Self-Validation System**: API bawaan yang mengaudit kesehatan database tanpa internet.

### B. Eksekusi Akademik
- **Dasbor KRS & Jadwal Mingguan**: Matriks visual jadwal kuliah dalam format *time-block*.
- **Auto-Generasi Dokumen (Paperless)**: Merender **Kartu Ujian Digital** dan **Surat Keterangan Aktif** ke format PDF siap cetak.

### C. Manajemen Finansial & Fasilitas
- **Modul SPP/UKT**: Pencatatan riwayat tagihan, metode pembayaran, dan metrik Lunas vs Tunggakan.
- **Perpustakaan Digital**: Katalog fisik perpustakaan dan akses E-Book eksternal.

### D. Akselerator Karir Mahasiswa
- **Pusat PKL/Magang & Skripsi**: *Tracking* 3 fase bimbingan skripsi dan lokasi magang perusahaan.
- **Bursa Beasiswa & Tracer Study**: Daftar kuota KIP/Beasiswa dan pelacakan karir alumni.

### E. Ekosistem Sosial & Komunikasi
- **Forum Diskusi Akademik**: Wadah tanya jawab ala StackOverflow.
- **Helpdesk Ticketing**: Pusat pelaporan insiden IT/Akademik.

---

## 🗄️ 4. Skema Database Utama (ER Diagram)

Sistem basis data dimuat otomatis oleh `init_db.py` ke dalam `sc_data.duckdb`. Berikut adalah relasi antar tabel utamanya:

```mermaid
erDiagram
    MAHASISWA ||--o{ KRS : "mengambil"
    MAHASISWA ||--o{ KEHADIRAN : "mencatat"
    MAHASISWA ||--o{ NILAI : "memperoleh"
    
    DOSEN ||--o{ MATA_KULIAH : "mengampu"
    MATA_KULIAH ||--o{ KRS : "terdaftar_di"
    MATA_KULIAH ||--o{ NILAI : "diujikan"
    
    MAHASISWA {
        string nim PK
        string nama
        string prodi
        int angkatan
    }
    
    DOSEN {
        string nip PK
        string nama
        string departemen
    }
    
    MATA_KULIAH {
        string kode_mk PK
        string nip_dosen FK
        string nama_mk
        int sks
    }
    
    KEHADIRAN {
        string id_kehadiran PK
        string nim FK
        string kode_mk FK
        date tanggal
        string status "Hadir/Izin/Alfa"
    }
```

*Catatan: Tersedia juga tabel non-relasional untuk logging seperti `event_log`, `pipeline_issue_log`, `audit_log`, dan `document_chunks` (Untuk vektor teks AI).*

---

## 🛡️ 5. Keamanan & Tata Kelola (RBAC)

Aplikasi ini menggunakan metode **Role-Based Access Control (RBAC)** secara tegas:
- **4 Role Absolut**: `Mahasiswa`, `Dosen`, `Administrator`, `Pimpinan`.
- **Backend Guard**: Endpoint kritis dikunci menggunakan *dependency injection* `require_admin`. Upaya meretas sistem via API tanpa token Admin ditolak dengan `403 Forbidden`.
- **Immutable Audit Trail (`audit_log`)**: Setiap transaksi (Login, Eksekusi ETL, RAG) dicatat presisi (Siapa pelakunya, Modul, Jam) untuk forensik.

---

## 💻 6. Panduan Instalasi & Deployment

Proyek ini menggunakan pendekatan **Local-First / Edge Compute**.

### Langkah Menjalankan Aplikasi
1. **Kloning Repositori**
   ```bash
   git clone https://github.com/Maxodus126/PROJECT_FINAL_SISTEMBASISDATA.git
   cd PROJECT_FINAL_SISTEMBASISDATA
   ```

2. **Instalasi Dependencies (Backend)**
   ```bash
   pip install fastapi uvicorn duckdb
   ```

3. **Menyalakan Server Backend (API)**
   ```bash
   cd backend
   uvicorn main:app --reload --host 127.0.0.1 --port 8000
   ```
   *(Backend berjalan di `http://localhost:8000`)*

4. **Menyalakan Frontend (UI)**
   Buka file `frontend/index.html` menggunakan browser Anda.

### Menggunakan Akun Sandbox (Mockup)
- **Mahasiswa**: `24360007` | **Admin**: `A001` | **Dosen**: `D001` | **Pimpinan**: `P001` *(Password bebas)*

---

## 🔌 7. API Endpoints Reference

| HTTP Method | Endpoint | Fungsi | Role |
|-------------|----------|--------|------------|
| `POST`      | `/api/events/load` | Menyimulasikan aliran batch absen terbaru | Admin |
| `POST`      | `/api/pipeline/run` | Menjalankan mesin ETL memproses 6 CSV | Admin |
| `GET`       | `/api/rag/search?q=...` | AI Semantic Search dokumen akademik | - |
| `GET`       | `/api/validation/final` | Memeriksa integritas sistem 100% | - |

---
*Dikembangkan dengan penuh ketelitian oleh Aflin Awaludin sebagai Final Project Sistem Basis Data - Institut Sains dan Teknologi Nasional (ISTN).*


---

# Arsitektur & Alur Kerja Lengkap Sistem SC-DATA

Dokumen ini memuat paparan komprehensif mengenai **Arsitektur Tingkat Tinggi**, **Alur Kerja (Flows)**, **Logika Bisnis**, serta **Skema Data** dari sistem perguruan tinggi terintegrasi SC-DATA.

---

## 🏗️ 1. Arsitektur Komponen Utama (3-Tier Terperinci)

Sistem dibangun menggunakan filosofi *Edge/Local-First* di mana seluruh antarmuka, API, dan database dapat berjalan luring tanpa latensi jaringan eksternal (Internet). Tujuannya adalah menghadirkan sistem "Zero-Latency UI".

```mermaid
flowchart TD

    subgraph CLIENT [Layer Presentasi - Frontend Klien]
        direction TB
        Browser["Web Browser (Chrome, Firefox)"]:::client
        HTML["Struktur Tampilan (HTML5 + Vanilla CSS)"]:::client
        JS["Client Logic (Vanilla JS) - Router & State"]:::client
        Browser --> HTML
        Browser --> JS
    end

    subgraph BACKEND [Layer Aplikasi - Backend Server]
        direction TB
        FastAPI["API Gateway (FastAPI Python)"]:::api
        Auth["Middleware Autentikasi (Base64)"]:::api
        RBAC["RBAC Guard (Dependency Injection)"]:::api
        Controllers["Controllers & Logika Bisnis"]:::api
        
        FastAPI --> Auth
        Auth --> RBAC
        RBAC --> Controllers
    end

    subgraph STORAGE [Layer Penyimpanan Data]
        direction TB
        DuckDB[("DuckDB (In-Memory/File)")]:::db
        RawCSV["Berkas CSV Mentah"]:::db
        DocsTXT["Kumpulan Dokumen TXT"]:::db
    end

    %% Relasi
    JS -->|HTTP REST / JSON Data| FastAPI
    FastAPI -->|JSON Response| JS
    Controllers -->|Read / Write| RawCSV
    Controllers -->|SQL Queries / Ingestion| DuckDB
    Controllers -->|Ekstrak Teks| DocsTXT

    %% Styling Layer
    classDef client fill:#1e1e2e,stroke:#89b4fa,stroke-width:2px,color:#cdd6f4
    classDef api fill:#11111b,stroke:#a6e3a1,stroke-width:2px,color:#cdd6f4
    classDef db fill:#181825,stroke:#f9e2af,stroke-width:2px,color:#cdd6f4
```

### Penjelasan Lapisan Teknologi:
1. **Frontend Layer**: Sepenuhnya dibangun dengan statis (`index.html` dan Javascript lokal) agar antarmuka instan terbuka. Tidak ada server-side rendering (SSR). Semua navigasi menu diatur lewat DOM manipulation menggunakan Javascript *vanilla*.
2. **API Layer**: Dibangun di atas **FastAPI**, sebuah kerangka kerja berbasis *Asynchronous Python*. Semua permintaan HTTP dari klien masuk ke sini. Tersedia middleware CORS dan autentikasi token (Base64 `Role:Username`).
3. **Data Layer**: Alih-alih MySQL/PostgreSQL biasa, arsitektur ini menggunakan **DuckDB** yang dikenal kencang untuk pemrosesan kolom logikal (OLAP). File tersimpan dalam bentuk file `.duckdb` yang bisa di-backup secara instan.

---

## 🔄 2. Alur Interaksi Klien-Server (Request Flow)

Bagaimana sebuah interaksi pengguna dari klik tombol hingga data kembali? Di bawah adalah urutan (*sequence*) sistematisnya.

```mermaid
sequenceDiagram
    autonumber
    actor User
    participant Frontend as Frontend (JS)
    participant API as FastAPI Gateway
    participant Guard as RBAC & Auth Guard
    participant DB as DuckDB

    User->>Frontend: Membuka Menu Dashboard
    Frontend->>API: HTTP GET/POST Request (Bearer Token)
    API->>Guard: Verifikasi Token & Hak Akses
    
    alt Token Tidak Valid / Role Ditolak
        Guard-->>API: 401 Unauthorized / 403 Forbidden
        API-->>Frontend: Error Response
        Frontend-->>User: Muncul Notifikasi Error
    else Token Valid
        Guard->>API: Akses Diizinkan
        API->>DB: Eksekusi Query SQL
        DB-->>API: Hasil Query
        API->>DB: Rekam Aktivitas ke audit_log
        API-->>Frontend: HTTP 200 OK (JSON Payload)
        Frontend->>Frontend: Render Ulang Komponen DOM
        Frontend-->>User: Menampilkan Tampilan Baru
    end
```

---

## 🛠️ 3. Alur Rekayasa Data / ETL Pipeline (Data Engineering Flow)

Fitur unggulan di backend adalah **Data Pipeline** (ETL) otomatis. Berbeda dengan sekadar memasukkan data, SC-DATA memvalidasi baris data terlebih dulu, dan **menolak** data yang cacat tanpa membuat aplikasinya hancur.

```mermaid
flowchart TD

    Start(["Admin Klik Run Pipeline"]) --> ReadCSV
    
    subgraph EXTRACTION
        ReadCSV["Membaca 6 Berkas CSV"]:::process
    end

    subgraph TRANSFORMATION_VALIDATION
        ReadCSV --> CekKolom{"Cek Kolom Wajib"}:::decision
        CekKolom -->|Kurang| BatalDataset["Batalkan Seluruh Dataset"]:::process
        CekKolom -->|Lengkap| Normalisasi["Normalisasi String & Tipe Data"]:::process
        
        Normalisasi --> Validasi["Validasi Per Baris (PK, Kosong)"]:::process
    end

    subgraph LOADING_QUARANTINE
        Validasi --> SplitData{"Pemisahan Baris"}:::decision
        
        SplitData -->|Baris Cacat/Error| LogIssue["Catat ke pipeline_issue_log"]:::process
        SplitData -->|Baris Valid| ReplaceTable["Timpa Data Lama di Tabel"]:::process
    end

    LogIssue --> CatatSummary
    ReplaceTable --> CatatSummary
    BatalDataset --> CatatSummary
    
    CatatSummary["Catat Metrik Keseluruhan"]:::storage
    CatatSummary --> Finish(["Selesai"])

    %% Styling
    classDef process fill:#f9e2af,stroke:#f2cdcd,stroke-width:2px,color:#181825
    classDef storage fill:#89dceb,stroke:#89b4fa,stroke-width:2px,color:#181825
    classDef decision fill:#f38ba8,stroke:#fab387,stroke-width:2px,color:#181825
```

**Alur Detail Pipeline:**
1. **Extraction (E)**: Sistem mengimpor file `mahasiswa.csv`, `dosen.csv`, dan kawan-kawan dari folder `data/csv`.
2. **Transformation (T)**: Membuang spasi kosong yang tidak perlu, menyamakan kapitalisasi (lowercase), lalu mengevaluasi formula (seperti mengalkulasi Nilai Akhir dari persentase Tugas + UTS + UAS otomatis).
3. **Validation & Karantina**: Jika ada NIM ganda, atau nilai kosong, baris tersebut ditolak dan di-*log* penyebabnya ke `pipeline_issue_log`. Baris lainnya yang sehat tetap lolos.
4. **Load (L)**: Baris sehat di-*insert* massal (Batch Insert) ke tabel DuckDB.

---

## 🧠 4. Alur Mesin Pencari Semantik / AI RAG (Retrieval-Augmented Generation)

Aplikasi memiliki asisten *Smart Search* tanpa API internet seperti OpenAI. Menggunakan algoritma **TF-IDF** (Term Frequency - Inverse Document Frequency) yang ditulis manual secara asali (native).

```mermaid
flowchart LR
    subgraph BUILD [Tahap Pembangunan Indeks]
        Docs["Dokumen Teks"] --> Chunker["Chunker (Potong per 90 kata)"]
        Chunker --> DBChunk[("Tabel document_chunks")]
    end

    subgraph SEARCH [Tahap Pencarian]
        User["Pencarian User"] --> Clean["Pembersihan Kata Kunci"]
        Clean --> Math["Kalkulasi TF-IDF Dinamis"]
        DBChunk --> Math
        Math --> Rank["Urutkan Relevansi (Top 5)"]
        Rank --> Output["Gabung Hasil (Answer)"]
    end
```

**Bagaimana ini bekerja:**
- Saat pencarian dilakukan, backend membagi kata kunci (query). 
- Ia menghitung seberapa sering setiap kata muncul dalam suatu *chunk* (Term Frequency), dan mengimbanginya dengan *Inverse Document Frequency* (mendiskon bobot kata-kata umum seperti "dan", "yang").
- *Chunk* dengan skor matematis tertinggi akan dikembalikan ke pengguna sebagai informasi paling relevan.

---

## 🗄️ 5. Skema Relasi Database Terperinci (Detailed ERD)

Skema database dipecah menjadi dua bagian utama agar lebih mudah dipahami: **Skema Akademik** (Tabel Master & Transaksi) dan **Skema Operasional** (Pencatatan Pipeline & Audit).

### A. Skema Akademik Inti
Menyimpan entitas master (Mahasiswa, Dosen, Mata Kuliah) serta interaksi akademiknya seperti Nilai, Kehadiran, dan KRS.

```mermaid
erDiagram
    %% Tabel Master
    MAHASISWA {
        string nim PK
        string nama
        string prodi
        int semester
        string status
    }
    
    DOSEN {
        string nidn PK
        string nama
        string prodi
        string email
        string status
    }
    
    MATA_KULIAH {
        string kode_mk PK
        string nama_mk
        int sks
        string prodi
        int semester
    }
    
    %% Tabel Transaksi
    KEHADIRAN {
        string hadir_id PK
        string nim FK
        string kode_mk FK
        date tanggal
        string status_hadir
    }
    
    NILAI {
        string nilai_id PK
        string nim FK
        string kode_mk FK
        float tugas
        float uts
        float uas
        float nilai_akhir
        string grade
    }
    
    KRS {
        string krs_id PK
        string nim FK
        string kode_mk FK
        string tahun_ajaran
        string semester_akademik
    }
    
    %% Relasi Logika
    MAHASISWA ||--o{ KRS : "mengambil"
    MAHASISWA ||--o{ KEHADIRAN : "mencatat"
    MAHASISWA ||--o{ NILAI : "memperoleh"
    
    DOSEN ||--o{ MATA_KULIAH : "mengampu"
    MATA_KULIAH ||--o{ KRS : "terdaftar_di"
    MATA_KULIAH ||--o{ NILAI : "diujikan"
    MATA_KULIAH ||--o{ KEHADIRAN : "digelar"
```

### B. Skema Operasional & Pipeline Log (Black-Box System)
Tabel-tabel ini tidak memiliki relasi langsung dengan tabel akademik karena berfungsi sebagai **Audit Trail** dan **Karantina ETL** berkinerja tinggi.

```mermaid
erDiagram
    PIPELINE_LOG {
        string pipeline_id PK
        string dataset_name
        int total_rows
        int invalid_rows
        string status
    }
    
    PIPELINE_ISSUE_LOG {
        string issue_id PK
        string pipeline_id FK
        int row_number
        string issue_type
    }
    
    EVENT_LOG {
        string log_id PK
        string event_id
        string nim
        timestamp waktu_event
        string status_hadir 
    }
    
    AUDIT_LOG {
        string audit_id PK
        timestamp created_at
        string role
        string action
        string detail
        string status
    }
    
    %% Relasi Operasional
    PIPELINE_LOG ||--o{ PIPELINE_ISSUE_LOG : "mencatat_anomali"
```

> [!NOTE]
> Pemisahan skema operasional dan akademik ini sangat disengaja. Jika data akademik di-reset (*Truncate*), data pada Audit Log dan Event Log tetap dipertahankan untuk kebutuhan forensik dan keamanan sistem (Standard Enterprise).

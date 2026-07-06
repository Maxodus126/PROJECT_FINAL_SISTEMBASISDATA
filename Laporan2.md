# Laporan Teknis Lengkap & Ekstensif Proyek SC-DATA (Smart Campus Data & AI Assistant)
**Versi: V16 All Accounts Elite — Infrastruktur Digital Kampus Berbasis Performa Tinggi**

---

## 1. Pendahuluan & Visi Proyek
Proyek **SC-DATA V16 Elite** dikembangkan untuk mendobrak batasan Sistem Informasi Akademik (SIAKAD) tradisional yang seringkali lambat, sulit dikustomisasi, dan terpecah-pecah. Dengan pendekatan arsitektur **Super App** dan **Command System**, proyek ini menyatukan administrasi akademik, *Learning Management System* (LMS), kecerdasan buatan (AI), analitik eksekutif, serta tata kelola data ke dalam satu ekosistem tunggal yang *seamless*.

Filosofi utama dari sistem ini adalah **Edge/Local-First** dan **Zero-Latency**. Dengan merancang ulang bagaimana aplikasi berinteraksi dengan basis data melalui pemrosesan *In-Memory*, aplikasi mampu merender grafik, memuat puluhan ribu baris log, dan melakukan pencarian AI tanpa hambatan *loading* (*lag*) yang biasa terjadi pada sistem berbasis web terpusat.

---

## 2. Arsitektur Komponen (3-Tier Decoupled Architecture)
Sistem ini memisahkan secara ketat (Decoupled) antara logika tampilan, pemrosesan bisnis, dan penyimpanan data, menjadikannya sistem yang modular dan tahan banting (*fault-tolerant*).

### 2.1. Tier Presentasi (Frontend Klien)
- **Teknologi**: Dibangun **tanpa menggunakan framework berat** (seperti React, Vue, atau Angular). Sistem murni mengandalkan HTML5, CSS Vanilla, dan JavaScript Vanilla tingkat lanjut. 
- **Keunggulan**: Memastikan aplikasi memiliki *footprint* memori yang sangat kecil, dieksekusi secepat kedipan mata oleh *browser*, dan memberi kebebasan penuh dalam mengatur animasi di tingkat DOM (*Document Object Model*).
- **Komunikasi**: Menggunakan `fetch` API untuk mengirim instruksi asinkronous (AJAX) ke Backend berbasis JSON.

### 2.2. Tier Aplikasi (Backend Gateway)
- **Teknologi**: Menggunakan **FastAPI (Python)**.
- **Peran**: Bertindak sebagai *API Gateway*, *RBAC Guard* (Middleware Keamanan), Mesin *Data Pipeline* (ETL), pemroses logika bisnis, dan *Engine* Pencarian AI.

### 2.3. Tier Penyimpanan Data (Database Layer)
- **Teknologi**: Menggunakan **DuckDB**, *In-Process Analytical Database*.
- **Peran**: Menyimpan seluruh data Master, Transaksi, dan Log dalam format relasional berorientasi kolom (*columnar*), sehingga kueri agregasi (seperti menghitung rata-rata kehadiran seluruh kampus) bisa berjalan dalam waktu milidetik.

---

## 3. Detail Implementasi Frontend: Super App Akademik

### 3.1. UI/UX Premium (Desain Eksekutif)
- **Visual**: Sistem dibalut dengan bahasa desain *Premium* seperti efek **Glassmorphism** (panel transparan dengan blur latar), *Aurora Background*, dan *Particle Canvas* dinamis di halaman depan.
- **Responsivitas**: Terdapat mode *Dark/Light Mode* otomatis, *Compact Mode* (untuk menampilkan lebih banyak tabel di satu layar), serta animasi transisi yang mulus.

### 3.2. Struktur JavaScript Modular
Semua modul dipecah secara sistematis:
- `app.js`: Otak dari sistem SPA (*Single Page Application*). Mengelola *state*, *router* virtual (pergantian menu tanpa pemuatan ulang halaman), dan rendering komponen.
- `api.js`: Jembatan penghubung (layar jaringan) antara interaksi UI dengan server FastAPI.
- `seeds.js`: Sistem pangkalan data lokal (*Mock Data*) untuk memastikan sistem tetap bisa diakses (Demo Offline) meskipun server belum siap.
- `features.js`: Modul ekstensi (*Feature Extension*) yang menyuntikkan **17 fitur super tambahan** ke dalam *router* tanpa merusak modul utama.

### 3.3. Command Center (Pusat Komando Cepat)
Terinspirasi dari Spotlight macOS, pengguna dapat menekan **Ctrl+K** kapan saja untuk memunculkan bilah perintah universal. Dari sini, mereka bisa mencari nama mahasiswa, melompat ke halaman nilai, atau bertanya pada AI secara instan.

### 3.4. 17+ Modul Fitur Akademik Lanjutan
Selain fitur inti seperti KRS dan Jadwal, sistem diperkaya dengan modul berskala penuh:
1. **Papan Pengumuman**: Berita kampus berdasarkan prioritas (Tinggi/Sedang).
2. **Jadwal Ujian**: Penjadwalan UTS/UAS beserta lokasi dan pengawas.
3. **Kartu Ujian Digital**: Dibuat dinamis dari HTML/CSS murni untuk langsung dicetak (Print Ready).
4. **Surat Keterangan Aktif**: Surat otomatis (*auto-generated*) lengkap dengan nomor seri dan format resmi.
5. **Manajemen SPP/UKT**: Status pembayaran, total tunggakan, riwayat transaksi.
6. **Perpustakaan Digital**: Katalog buku, status ketersediaan, e-book, dan integrasi reservasi.
7. **PKL & Magang**: Pendaftaran, persetujuan pembimbing, *upload* laporan PKL.
8. **Skripsi / Tugas Akhir**: Alur pengajuan judul hingga persetujuan sidang.
9. **Informasi Beasiswa**: Katalog pendaftaran beasiswa dan persyaratannya.
10. **Forum Diskusi Akademik**: Wadah tanya jawab interaktif per mata kuliah.
11. **Helpdesk & Ticketing**: Sistem pelaporan masalah mahasiswa ke teknisi/admin.
12. **Organisasi & UKM**: Manajemen unit kegiatan mahasiswa.
13. **Data Alumni**: *Tracer study*, IPK kelulusan, dan status pekerjaan.
14. **Sistem Notifikasi**: Lonceng pemberitahuan global (Tugas, Pesan, Pengumuman).
15. **QR Code Attendance**: Pembuatan identitas QR KTM elektronik di dalam profil.

---

## 4. Sistem Keamanan & Tata Kelola (RBAC Guard)
Aplikasi mematuhi standar *Enterprise Governance* dengan **Role-Based Access Control (RBAC)** empat tingkat yang dikunci mutlak dari *Frontend* hingga *Backend*:

1. **Mahasiswa**: Hak akses *Read-Only* ke data pribadi, mengisi presensi mandiri, mengumpulkan tugas, mengecek nilai, dan mencari info via AI.
2. **Dosen**: Hak akses memodifikasi kelas yang diampu, memberi instruksi tugas, menginput nilai secara *batch*, dan menyetujui PKL bimbingan.
3. **Administrator**: Pengendali sistem. Berhak menekan eksekusi sinkronisasi ETL, mengubah data Master Mahasiswa/Dosen secara CRUD, dan mengelola keamanan akun.
4. **Pimpinan**: Pengguna dasbor level-C (*Executive Summary*). Melihat analitik tren kehadiran, diagram distribusi nilai, dan memantau Peta Risiko Mahasiswa secara *real-time*.

*Middleware* FastAPI mengenkripsi identitas di dalam Token Base64, dan fungsi dependensi `require_admin` memastikan aksi sensitif tidak bisa ditembus oleh manipulasi akses *Client*.

---

## 5. Mesin Backend & Rekayasa Data (Data Engineering)

### 5.1. Data Pipeline Engine (Sistem ETL Otonom)
Inovasi paling mutakhir dari SC-DATA adalah pemrosesan ETL yang diotomatiskan. Ketika Admin menjalankan pipeline, server Python akan:
- **E (Extract)**: Menyerap puluhan ribu baris data mentah dari 6 sumber (*dataset*) berkas `.csv`.
- **T (Transform & Validate)**: Sistem secara paksa menormalisasi teks (menghapus spasi lebih, meratakan huruf besar), mengecek format *Primary Key* ganda, dan menghitung total SKS serta formula rasio Nilai secara *on-the-fly*.
- **Karantina Data**: Fitur **Anti-Crash**. Jika ada baris CSV yang cacat (misal huruf dimasukkan ke kolom angka), aplikasi **TIDAK EROR**. Baris tersebut dibuang ke tabel spesifik `PIPELINE_ISSUE_LOG` untuk ditinjau admin, sementara sisa data yang benar tetap diproses.
- **L (Load)**: Menyuntikkan data bersih (Tervalidasi) ke tabel DuckDB dalam sekian milidetik menggunakan metode *batch insertion*.

### 5.2. AI Semantic Search (RAG - Retrieval Augmented Generation)
Tidak menggunakan sambungan internet atau API berbayar seperti ChatGPT. Sistem memiliki mesin RAG lokal.
- Algoritma **TF-IDF (Term Frequency-Inverse Document Frequency)** dibuat manual menggunakan pustaka `math` dan `re` bawaan Python.
- *Chunking*: Peraturan dan prosedur akademik (berkas `.txt`) dicacah menjadi potongan teks berukuran 90 kata, lalu diindeks ke dalam memori.
- Ketika mahasiswa bertanya ("Bagaimana cara ujian?"), Python menghitung perkalian *Cosign Similarity* untuk mencari *chunk* paling relevan, lalu mencetaknya langsung tanpa latensi jaringan eksternal.

### 5.3. Real-Time Event Monitor
Menghapus batas antara perangkat keras dan basis data. Aplikasi memiliki modul `Event Ingestion` untuk menangkap data dari gerbang sensor/QR Code absensi. Data tersebut mengalir masuk ke tabel `event_log` secara asinkron tanpa menahan (*blocking*) kinerja aplikasi, lalu diagregasi otomatis ke Dasbor Pimpinan dalam format *Live Metrics*.

### 5.4. Immutable Audit Trail (Black-Box Forensik)
Laporan keamanan tidak pernah direkayasa ulang. Setiap masuk, pemanggilan API, penambahan nilai, maupun modifikasi struktur, otomatis dicatat melalui `log_audit()` ke tabel rahasia `AUDIT_LOG`. Tabel ini dirancang antipengubahan (*immutable*) agar jejak digital dapat diaudit selamanya, memenuhi kaidah kepatuhan operasional (*Compliance*).

---

## 6. Skema Relasi Database Terpusat (DuckDB)
Tabel dalam DuckDB dipisahkan secara strategis:

**A. Skema Transaksional & Akademik Inti**
Menyimpan relasi langsung SIAKAD:
- `MAHASISWA` (Master Data Mahasiswa).
- `DOSEN` (Master Data Pengajar).
- `MATA_KULIAH` (Master Data Kelas).
- `KRS` (Tabel pivot relasi Mahasiswa - Matkul - Semester).
- `NILAI` (Simpanan nilai teragregasi Tugas, UTS, UAS, Akhir).
- `KEHADIRAN` (Absensi terstruktur per matkul).

**B. Skema Operasional (Data Black-Box)**
Tabel-tabel berkinerja tinggi yang aman dari risiko *Truncate* (reset tabel master):
- `EVENT_LOG`: Riwayat raw-data absensi/klik per detik.
- `PIPELINE_LOG`: Meta-data riwayat sinkronisasi ETL.
- `PIPELINE_ISSUE_LOG`: Kotak karantina data CSV yang rusak.
- `AUDIT_LOG`: Buku besar riwayat keamanan.
- `DOCUMENT_CHUNKS`: Indeks teks khusus AI RAG TF-IDF.

---

## 7. Struktur Direktori Proyek
Mengikuti prinsip modularitas dan *Separation of Concerns*, repositori dipisah menjadi beberapa lingkungan kerja terstruktur:

```text
ISTN_One_Portal_SC_DATA_API.../
├── backend/                  # Layer Aplikasi (Backend Gateway)
│   ├── db.py                 # Konfigurasi koneksi DuckDB
│   ├── init_db.py            # Script pembuat tabel (DDL) DuckDB 
│   ├── main.py               # Otak utama FastAPI (API, ETL, RAG, RBAC)
│   ├── one_click_demo.py     # Script bootstrap untuk menjalankan server
│   ├── seed_data.py          # Script inisialisasi data mentah ke DuckDB
│   └── sc_data.duckdb        # Berkas database fisik DuckDB berkinerja tinggi
├── data/                     # Area Penyimpanan File Data
│   ├── csv/                  # Folder karantina dataset mentah (ETL source)
│   └── json/                 # Ekspor snapshot dan arsip riwayat
├── docs/                     # Repositori file ".txt" (SOP Kampus) untuk RAG AI
├── frontend/                 # Layer Presentasi (Client-Side SPA)
│   ├── index.html            # Kerangka dasar UI (Particle Canvas, Layout)
│   ├── css/                  # Styling Vanilla (Glassmorphism, Dark Mode)
│   └── js/                   
│       ├── core/app.js       # Sistem state-management & router tanpa-reload
│       ├── data/seeds.js     # Fallback data luring (Mock Data)
│       ├── features/features.js # Ekstensi sistem: injeksi 17 fitur baru
│       ├── services/api.js   # Modul Fetch AJAX untuk pemanggilan backend
│       └── utils/helpers.js  # Pemroses micro-task (format tanggal, angka)
├── scripts/                  # Kumpulan shell script pembantu pengembangan
└── README.md                 # Dokumentasi panduan cara menghidupkan proyek
```

---

## 8. Kesimpulan & Rekomendasi
Proyek **SC-DATA V16 Elite** bukan sekadar antarmuka web statis. Ini adalah sebuah mahakarya purwarupa sistem terpadu (*Integrated Ecosystem*) yang membuktikan kelayakan arsitektur *Edge-Computing* pada manajemen kampus. 

Dengan menggabungkan **17 modul fitur tingkat lanjut**, **Mesin ETL mandiri yang tahan eror**, **Database In-Process (*DuckDB*)**, dan **Algoritma AI RAG asli Python**, proyek ini mencapai apa yang disebut dengan keandalan Enterprise. 

Sebagai rekomendasi *Deployment*:
- **Fase Prototipe Aksi (Sekarang)**: Sangat sempurna dipresentasikan secara lokal (*Local-First*) dengan `main.py` (FastAPI) dan indeks `html` statis.
- **Fase Produksi**: *Frontend* siap untuk diunggah ke *Static Hosting* (Netlify / Vercel), sementara backend FastAPI dan basis data DuckDB dapat di-wadah-kan (*Containerized* via Docker) menuju infrastruktur peladen kampus (VPS/AWS) secara asimetris, menjanjikan kecepatan super dengan skalabilitas tak terbatas.

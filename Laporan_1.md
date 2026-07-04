# Draf Presentasi Proyek SC-DATA (Smart Campus Data & AI Assistant)

## Slide 1: Judul Presentasi
- **Judul Slide**: SC-DATA: Fondasi Infrastruktur Digital & AI Asisten Kampus Pintar
- **Penjelasan Fitur & Poin Utama**:
  - Pengenalan SC-DATA sebagai *core system block* untuk ekosistem akademik universitas (V16 All Accounts Elite).
  - Mengintegrasikan manajemen akademik (KRS, Jadwal, Nilai) dengan *data pipeline* otomatis dan AI Assistant.
  - Berfokus pada performa tinggi, desain UI premium (glassmorphism), dan keamanan operasional.
- **Rekomendasi Visual/Artefak**: Tampilkan layar *Login Portal* dengan logo ISTN, menyoroti teks "V16 ALL ACCOUNTS ELITE".
- **Narasi Presentasi (Speaker Notes)**: 
  "Selamat pagi Bapak/Ibu sekalian. Hari ini saya mempresentasikan purwarupa SC-DATA (Smart Campus Data). Sistem ini dirancang bukan sekadar sebagai SIAKAD biasa, melainkan sebagai fondasi digital atau *Command System* terpadu. Mulai dari manajemen data master, otomatisasi ETL, hingga integrasi kecerdasan buatan, semuanya dibalut dalam satu antarmuka premium berkinerja tinggi. Mari kita lihat arsitektur dan fitur fungsional yang sudah sepenuhnya diimplementasikan."

## Slide 2: Arsitektur Utama (FastAPI + DuckDB)
- **Judul Slide**: Arsitektur Berbasis Performa & Kinerja Tinggi
- **Penjelasan Fitur & Poin Utama**:
  - Arsitektur sistem murni menggunakan **HTML/Vanilla JS -> FastAPI -> DuckDB** (Bukan Streamlit).
  - Backend menggunakan **FastAPI** (Python) untuk *throughput* tinggi dan respons instan.
  - Database menggunakan **DuckDB** sebagai *in-process analytical database* tanpa perlu *setup server* rumit.
  - Frontend dibangun dari nol dengan Vanilla JS modular dan CSS custom (glassmorphism), memberikan fleksibilitas penuh tanpa batasan framework.
- **Diagram Arsitektur (Mermaid)**:
  ```mermaid
  graph TD
      subgraph Frontend ["Presentation Layer (Browser)"]
          UI["HTML5 + CSS3 (Glassmorphism)"]
          JS["Vanilla JS (app.js, features.js)"]
          UI --- JS
      end

      subgraph Backend ["Application Layer (Python)"]
          API["FastAPI App"]
          Auth["RBAC & Security"]
          Routes["API Endpoints (/api/*)"]
          API --- Auth
          API --- Routes
      end

      subgraph DataLayer ["Data Layer (Local)"]
          DuckDB[("DuckDB (In-Process)")]
          Files["CSV Data & TXT Docs"]
      end

      JS -- "HTTP REST (JSON/Fetch API)" --> API
      Routes -- "SQL Queries (duckdb.py)" --> DuckDB
      DuckDB -. "Load Data" .-> Files
  ```
- **Rekomendasi Visual/Artefak**: Tangkapan layar endpoint `/api/health` atau halaman "System Pulse" di *sidebar*, disandingkan dengan diagram arsitektur di atas.
- **Narasi Presentasi (Speaker Notes)**: 
  "Dari sisi arsitektur data, keputusan teknis kami sangat pragmatis. Kami **tidak menggunakan Streamlit**, melainkan membangun *frontend* kustom murni dengan HTML dan Vanilla JavaScript. Kenapa? Agar kita memiliki kontrol 100% terhadap UI/UX berdesain *premium* ini tanpa *lag* yang sering terjadi di *framework* Python berbasis web. *Frontend* ini berkomunikasi langsung dengan backend FastAPI yang sangat cepat. Di lapisan data, FastAPI mengeksekusi kueri ke DuckDB—sebuah *in-process analytical database*. Pilihan ini memungkinkan kita mengolah jutaan baris data kehadiran dan nilai dalam hitungan milidetik secara lokal."

## Slide 3: Modul 9 - Event Monitor Dashboard
- **Judul Slide**: Event Monitor: Observabilitas Data Presensi
- **Penjelasan Fitur & Poin Utama**:
  - Pemantauan metrik kehadiran kampus secara langsung (hadir, izin, sakit, alfa).
  - Dasbor diagregasi dari tabel `event_log` secara *real-time*.
  - Menampilkan daftar 10 event presensi terbaru yang diurutkan berdasarkan waktu.
- **Rekomendasi Visual/Artefak**: Screenshot UI "Event Monitor", fokus pada 4 kartu metrik kehadiran di bagian atas dan tabel daftar event.
- **Narasi Presentasi (Speaker Notes)**: 
  "Masuk ke Modul 9, kita memiliki Event Monitor Dashboard. Pimpinan kini tidak perlu lagi menunggu laporan akhir semester. Dasbor ini langsung membaca metrik agregat dari tabel `event_log` di DuckDB. Distribusi status Hadir, Izin, Sakit, atau Alfa dapat langsung terpantau, memberikan visibilitas operasional yang transparan hari itu juga."

## Slide 4: Modul 9 - Mekanisme Load Event Baru
- **Judul Slide**: Ingestion Aliran Data (Streaming Mockup)
- **Penjelasan Fitur & Poin Utama**:
  - Tombol **"Load Event Baru"** memicu endpoint API (`/api/events/load`) untuk memuat data *batch* baru.
  - Pengecekan duplikasi *event_id* secara otomatis di database.
  - Pembaruan UI seketika tanpa perlu *reload* halaman berkat interaksi asinkron JS.
- **Rekomendasi Visual/Artefak**: Tangkapan layar *toast notification* "Berhasil dimuat" atau log saat tombol "Load Event Baru" ditekan.
- **Narasi Presentasi (Speaker Notes)**: 
  "Untuk mendemonstrasikan aliran datanya, modul ini memiliki mekanisme *Load Event*. Saat tombol ditekan, backend mensimulasikan *ingestion* data dari sensor QR atau aplikasi mobile mahasiswa. API memvalidasi data dan memastikan tidak ada duplikasi ID sebelum memasukkannya ke DuckDB. Antarmuka langsung memperbarui tabel 10 event terbaru secara instan. Ini membuktikan ketangguhan *pipeline* data kita."

## Slide 5: Modul 10 - Data Pipeline Builder
- **Judul Slide**: Data Pipeline Builder: Mesin ETL Terpadu
- **Penjelasan Fitur & Poin Utama**:
  - Proses **ETL** otomatis yang mengolah 6 entitas CSV utama: Mahasiswa, Dosen, Mata Kuliah, KRS, Nilai, Kehadiran.
  - Mentransformasi *raw data* menjadi tabel terstruktur yang siap dipakai (*AI-Ready*).
  - Memastikan konsistensi seluruh entitas akademik dalam satu kali klik ("Run Pipeline").
- **Rekomendasi Visual/Artefak**: Screenshot layar "Data Pipeline" yang menunjukkan 6 kotak entitas CSV dengan status keberhasilan masing-masing.
- **Narasi Presentasi (Speaker Notes)**: 
  "Infrastruktur modern bergantung pada kualitas data. Modul 10, Data Pipeline Builder, adalah pabrik data kita. Alih-alih mengeksekusi skrip manual, pengguna cukup menjalankan satu *pipeline* otomatis. Sistem memproses 6 file CSV utama—dari data Mahasiswa hingga Nilai akhir—lalu membersihkan dan menstrukturnya di dalam database. Dalam hitungan detik, data mentah berubah menjadi pangkalan data yang siap disajikan untuk RAG dan analitik."

## Slide 6: Modul 10 - Data Quality & Validasi Otomatis
- **Judul Slide**: Karantina Data & Pencatatan Anomali
- **Penjelasan Fitur & Poin Utama**:
  - Validasi ketat terhadap anomali (kolom kosong, *Primary Key* ganda, atau nilai ujian > 100).
  - Mekanisme perlindungan database: Baris cacat dikarantina dan dicatat ke `pipeline_issue_log` (maks 200 issue per dataset).
  - Baris data yang valid tetap berhasil dimuat (Toleransi Kesalahan / *Fault Tolerance*).
- **Rekomendasi Visual/Artefak**: Screenshot bagian log *issues* di tabel Data Pipeline (menampilkan tipe *error* seperti DUPLICATE_PK atau INVALID_SCORE).
- **Narasi Presentasi (Speaker Notes)**: 
  "Kecerdasan *pipeline* ini terletak pada validasinya. Jika ada dosen yang keliru menginput nilai ujian 110, atau terjadi duplikasi NIM mahasiswa, sistem tidak akan mogok (*crash*). Baris anomali tersebut otomatis dicegat, dikarantina, dan dicatat di tabel isu log. Sementara itu, baris yang valid tetap diloloskan ke database. Ini memastikan integritas data terjamin 100% tanpa mengorbankan produktivitas."

## Slide 7: Modul 11 - Academic Document Search (RAG)
- **Judul Slide**: Integrasi AI: Pencarian Kognitif Dokumen Akademik
- **Penjelasan Fitur & Poin Utama**:
  - Fitur **Build RAG Index** yang memecah file dokumen teks (*chunking*) ke tabel `document_chunks`.
  - Algoritma pencarian berbasis TF-IDF untuk menelusuri relevansi semantik dokumen pedoman/SOP.
  - AI menyertakan **Sumber Dokumen** untuk mencegah halusinasi *Generative AI*.
- **Rekomendasi Visual/Artefak**: Screenshot antarmuka pencarian RAG (Academic Document Search) yang menampilkan jawaban dari sistem beserta kutipan sumber dokumen aslinya.
- **Narasi Presentasi (Speaker Notes)**: 
  "Selanjutnya Modul 11, tempat AI mulai beraksi secara praktis. Mahasiswa atau dosen sering kesulitan mencari detail pedoman akademik. Melalui arsitektur *Retrieval-Augmented Generation* atau RAG, dokumen panjang dipecah (*chunking*) dan diindeks. Saat pengguna bertanya, mesin tidak menebak, melainkan mengekstrak kutipan spesifik dari dokumen pedoman. Dengan selalu menyertakan sumber referensi, kita menghilangkan risiko AI berhalusinasi."

## Slide 8: Modul 12 - Security & Governance (RBAC)
- **Judul Slide**: Tata Kelola & Role-Based Access Control
- **Penjelasan Fitur & Poin Utama**:
  - Autentikasi ketat berbasis 4 Role (Mahasiswa, Dosen, Administrator, Pimpinan).
  - **Data Masking di UI**: Menu dinamis; Mahasiswa tidak akan melihat fitur kelola sistem Admin.
  - **Proteksi di Backend**: Fungsi `require_admin` memblokir mutlak akses ilegal ke endpoint kritikal (`/api/pipeline/run`, `/api/events/reset`).
- **Rekomendasi Visual/Artefak**: Dua tangkapan layar disandingkan: *Sidebar* Mahasiswa (menu spesifik akademik) vs *Sidebar* Administrator (menu penuh).
- **Narasi Presentasi (Speaker Notes)**: 
  "Sistem yang hebat tidak ada artinya tanpa keamanan. Di Modul 12, kami menerapkan Role-Based Access Control (RBAC). Di antarmuka, *sidebar* otomatis menyesuaikan menu berdasarkan peran login. Namun yang terpenting ada di belakang layar; backend API kami memiliki fungsi khusus yang memblokir akses ke fungsi berbahaya (seperti me-*reset* database) apabila peran pengguna di dalam token bukanlah Administrator. Akses data dijamin berada di tangan yang tepat."

## Slide 9: Modul 12 - Audit Trail & Immutable Logging
- **Judul Slide**: Jejak Audit: Transparansi Mutlak
- **Penjelasan Fitur & Poin Utama**:
  - Tabel `audit_log` melacak seluruh aksi sistem, siapa pelakunya (*Role*), dan status (Success/Failed).
  - Rekam jejak untuk *login error*, eksekusi *pipeline*, pemuatan *event*, hingga pembuatan RAG index.
  - Bisa diekspor (*Export Riwayat*) menjadi file CSV untuk pelaporan IT dan kepatuhan.
- **Rekomendasi Visual/Artefak**: Screenshot tabel "Audit Log" atau terminal command yang menunjukkan isi file ekspor CSV dari Audit Log.
- **Narasi Presentasi (Speaker Notes)**: 
  "Untuk melengkapi tata kelola, semua operasi kritikal dicatat secara permanen di Audit Log. Kapan sebuah *pipeline* dijalankan? Siapa yang melakukan *reset event*? Semua tercatat lengkap dengan stempel waktu dan identitas pelakunya. Jejak audit ini *immutable* atau tidak bisa diubah dari antarmuka, menjadi bukti kuat jika diperlukan investigasi teknis, *troubleshooting*, atau audit standar kepatuhan IT dari pihak eksternal."

## Slide 10: Modul 13 - Deployment Decision Canvas
- **Judul Slide**: Strategi Skalabilitas & Arsitektur
- **Penjelasan Fitur & Poin Utama**:
  - Layar interaktif yang menyajikan dokumentasi Architecture Decision Record (ADR).
  - Perbandingan opsi implementasi: Local (sekarang), On-Premise, Cloud, atau Hybrid.
  - Menentukan kelayakan migrasi sistem di masa mendatang tanpa vendor *lock-in*.
- **Rekomendasi Visual/Artefak**: Screenshot modul "Deployment Decision Canvas" di dalam website SC-DATA.
- **Narasi Presentasi (Speaker Notes)**: 
  "Sebagai arsitek sistem, saya membekali aplikasi ini dengan Modul 13: Deployment Decision Canvas. Ini adalah kanvas interaktif di dalam portal yang membandingkan matriks biaya dan keamanan antara implementasi di *server* lokal, *on-premise*, atau *cloud*. Meskipun purwarupa ini berjalan di mesin *sandbox* menggunakan DuckDB, *blueprint* aplikasinya siap dinaikkan ke arsitektur *cloud-native* kapan saja, memberi universitas kebebasan penuh dari *vendor lock-in*."

## Slide 11: Ekstensi Fungsional - KRS & Jadwal Terpadu
- **Judul Slide**: Eksekusi Akademik: Dasbor KRS & Jadwal
- **Penjelasan Fitur & Poin Utama**:
  - Menampilkan ringkasan (SKS, total MK, status DPA) melalui *Metric Cards*.
  - Visualisasi "Jadwal Mingguan" yang rapi ala kalender *compact* (senin s.d. sabtu).
  - Status lulus/tidak per mata kuliah beserta indikator warna performa mahasiswa.
- **Rekomendasi Visual/Artefak**: Tangkapan layar fitur "KRS & Jadwal" (dari UI *snapshot* atau implementasi web).
- **Narasi Presentasi (Speaker Notes)**: 
  "Lalu, mari kita lihat ekstensi fungsional mahasiswa. Sistem SC-DATA sudah mengimplementasikan halaman Dasbor KRS dan Jadwal secara penuh. Mahasiswa bisa melihat sisa batas SKS maksimal, konfirmasi Dosen Wali, serta jadwal mingguan yang disusun rapi secara visual (Time-Block). Semua disajikan di atas antarmuka UI/UX yang *smooth* sehingga meminimalkan keluhan ke bagian administrasi."

## Slide 12: Ekstensi Fungsional - Dokumen & Kartu Digital
- **Judul Slide**: Autogenerasi Dokumen: Paperless Campus
- **Penjelasan Fitur & Poin Utama**:
  - Fitur "Kartu Ujian Digital" yang *auto-generated* lengkap dengan daftar MK dan validasi paraf.
  - Pembuatan "Surat Keterangan Aktif" otomatis berdasarkan perhitungan *hash* validasi *real-time*.
  - Tombol *Cetak Native* yang merender elemen ke layout PDF siap cetak.
- **Rekomendasi Visual/Artefak**: Screenshot dari *render* Kartu Ujian Digital atau tata letak form Surat Keterangan Aktif di UI.
- **Narasi Presentasi (Speaker Notes)**: 
  "Mewujudkan kampus *paperless* adalah komitmen kami. SC-DATA memiliki generator dokumen internal. Mahasiswa tidak perlu lagi mengantre ke loket untuk meminta Kartu Ujian atau Surat Keterangan Aktif. Sistem secara instan me-*render* dokumen resmi—lengkap dengan stempel digital, ID *hash* mahasiswa, dan format siap cetak (*print native*). Ini memangkas birokrasi ratusan jam setiap semesternya."

## Slide 13: Ekstensi Fungsional - Manajemen Finansial
- **Judul Slide**: Transparansi Finansial: Modul SPP/UKT
- **Penjelasan Fitur & Poin Utama**:
  - Pencatatan riwayat penagihan per semester beserta status (Lunas / Belum Lunas).
  - Tampilan ringkasan metrik: Total Tagihan, Lunas, dan Tunggakan berjalan.
  - Integrasi tata cara pembayaran multi-platform.
- **Rekomendasi Visual/Artefak**: Screenshot halaman "Pembayaran SPP / UKT" yang menunjukkan tabel tagihan dan metrik keuangan.
- **Narasi Presentasi (Speaker Notes)**: 
  "Di luar ranah akademik murni, portal ini juga mengonsolidasikan fungsi finansial. Melalui halaman Pembayaran SPP/UKT, mahasiswa dan administrator dapat melihat status penagihan dalam satu layar. Metrik secara tegas membedakan mana yang sudah lunas dan mana yang masuk kategori tunggakan. Sistem tidak mentransfer dana secara langsung, melainkan menjadi *ledger* atau buku besar status finansial yang sinkron dengan biro keuangan kampus."

## Slide 14: Ekstensi Fungsional - Akselerasi Karir Mahasiswa
- **Judul Slide**: Penunjang Karir: PKL, Skripsi, & Beasiswa
- **Penjelasan Fitur & Poin Utama**:
  - Sub-modul **PKL/Magang**: Pencatatan lokasi *internship* dan dosen pembimbing mahasiswa.
  - Sub-modul **Skripsi**: Status progres dari pengajuan judul hingga siap sidang (Tahap 1 s.d. 3).
  - Sub-modul **Beasiswa**: Informasi ketersediaan dana bantuan dan syarat IPK secara tersentralisasi.
- **Rekomendasi Visual/Artefak**: Tangkapan layar salah satu halaman karir (contohnya tabel daftar Beasiswa atau daftar mahasiswa PKL).
- **Narasi Presentasi (Speaker Notes)**: 
  "Bukan cuma masalah nilai, SC-DATA didesain untuk menjembatani mahasiswa ke dunia profesional. Kami menanamkan modul pelacakan Praktik Kerja Lapangan (PKL), pemantauan tahapan penulisan Skripsi, serta *hub* daftar Beasiswa yang tersedia. Sistem sentral ini memastikan pimpinan fakultas tahu persis berapa persen mahasiswa tingkat akhir yang sudah berstatus magang atau siap melangkah ke sidang kelulusan."

## Slide 15: Penutup & Validasi Sistem Akhir
- **Judul Slide**: Kesiapan Teknis & Rencana Tahap Selanjutnya
- **Penjelasan Fitur & Poin Utama**:
  - Mekanisme mandiri **Final Validation** (`/api/validation/final`) memastikan semua elemen (DB, Pipeline, API) berstatus *PASS*.
  - Tidak ada dependensi eksternal (100% jalan secara luring/*Local First*).
  - Ringkasan 17 fitur terintegrasi yang telah rampung dan berjalan sempurna.
- **Rekomendasi Visual/Artefak**: Screenshot hasil JSON dari endpoint `/api/validation/final` yang menunjukkan indikator "PASS" di semua kriteria.
- **Narasi Presentasi (Speaker Notes)**: 
  "Untuk menutup presentasi ini, hal terbaik dari SC-DATA adalah kapabilitas *Self-Validation* nya. Melalui API Final Validation, sistem mengaudit sendiri kesiapan infrastruktur database-nya dan memberi laporan hijau (PASS) yang mengonfirmasi bahwa 17 fitur masif ini berdiri kokoh tanpa butuh internet eksternal (*Local First*). Saat ini kode sudah matang dan arsitektur siap di bawa ke tahap UAT (User Acceptance Testing) fakultas. Terima kasih atas waktunya, saya buka sesi untuk tanya jawab teknis."

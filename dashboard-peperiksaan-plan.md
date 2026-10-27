# Dashboard Pengurusan Peperiksaan — Jabatan Kejuruteraan Elektrik, POLISAS

## Gambaran Keseluruhan

Membina sebuah **dashboard web** berpusat untuk pengurusan peperiksaan peringkat jabatan di Jabatan Kejuruteraan Elektrik, POLISAS. Sistem ini boleh diakses oleh tiga peranan utama: **KPPJ** (Ketua Pegawai Peperiksaan Jabatan), **Pensyarah**, dan **Pelajar**. Setiap peranan mempunyai akses modul yang berbeza berdasarkan tanggungjawab masing-masing.

**Stack Teknologi Cadangan:**
- Frontend: React.js + Tailwind CSS
- Backend: Node.js + Express.js
- Database: MySQL / PostgreSQL
- Auth: JWT (JSON Web Token)
- PDF: html2pdf.js / pdfmake (untuk jana/download dokumen)

---

## Senibina Sistem

**Peranan & Kawalan Akses:**

| Modul | KPPJ | Pensyarah | Pelajar |
|---|:---:|:---:|:---:|
| Rayuan Peperiksaan | ✅ Urus + Update Status | ✅ Semak | ✅ Semak Status + Download Borang |
| CTCE | ✅ Urus + Luluskan | ✅ Semak | ✅ Mohon + Semak Status |
| Proses Mastersheet | ✅ Penuh | ✅ Input/Semak | ❌ |
| Penggubalan Item Peperiksaan | ✅ Penuh | ✅ Input/Semak | ❌ |
| Jadual Waktu Peperiksaan | ✅ Urus | ✅ Semak | ✅ Semak |
| Laporan Pertengahan Semester | ✅ Penuh | ✅ Input | ❌ |
| Bengkel Pengesahan Item PA | ✅ Penuh | ✅ Semak/Sertai | ❌ |
| List Tahan Peperiksaan Akhir | ✅ Urus | ✅ Semak | ✅ Semak Status |
| Peperiksaan Akhir Khas | ✅ Penuh | ✅ Semak | ✅ Mohon |
| Peperiksaan Akhir | ✅ Penuh | ✅ Semak/Mohon Ganti | ❌ |

---

## Sub-Tugas

---

### Sub-Tugas 1 — Persediaan Projek & Sistem Pengesahan (Auth)

**Intent:**
Menyediakan asas projek (project scaffold) dan sistem log masuk dengan kawalan akses berdasarkan peranan (Role-Based Access Control).

**Expected Outcomes:**
- Struktur folder projek frontend dan backend diwujudkan.
- Halaman log masuk berfungsi untuk ketiga-tiga peranan.
- JWT digunakan untuk sesi pengguna.
- Selepas log masuk, pengguna diarahkan ke dashboard mengikut peranan masing-masing.
- Halaman utama (home dashboard) berbeza untuk KPPJ, Pensyarah, dan Pelajar.

**Todo List:**
- [ ] Scaffold projek React.js (frontend) dan Node.js/Express (backend)
- [ ] Bina halaman log masuk dengan borang (Nombor Staf / Nombor Matrik + Kata Laluan)
- [ ] Laksanakan JWT auth di backend
- [ ] Bina middleware kawalan akses berdasarkan peranan (KPPJ / Pensyarah / Pelajar)
- [ ] Bina halaman dashboard utama untuk setiap peranan dengan senarai modul yang boleh diakses
- [ ] Bina komponen navigasi (sidebar/navbar) yang paparkan modul mengikut peranan

**Relevant Context:**
- Pelajar log masuk menggunakan Nombor Matrik
- Pensyarah dan KPPJ log masuk menggunakan Nombor Staf
- Peranan ditentukan semasa pendaftaran / oleh admin (KPPJ)

**Status:** `[ ] pending`

---

### Sub-Tugas 2 — Modul Rayuan Peperiksaan

**Intent:**
Membolehkan pelajar mengetahui tatacara rayuan, memuat turun borang, dan menyemak status rayuan mereka. KPPJ mengemaskini status rayuan secara manual.

**Expected Outcomes:**
- Halaman tatacara rayuan dengan dua jenis rayuan dipaparkan dengan jelas.
- Pelajar boleh muat turun borang PDF (Lampiran 1 & 2).
- Pautan ke website POLISAS untuk proses pembayaran/penghantaran rasmi.
- Pelajar boleh semak status rayuan mereka (dikemaskini oleh KPPJ).
- Pelajar boleh muat turun surat kelulusan apabila status = Lulus.
- KPPJ boleh lihat senarai semua rayuan dan kemaskini status.

**Todo List:**
- [ ] Bina halaman "Rayuan Peperiksaan" dengan dua seksyen: Rayuan Semak Semula Skrip dan Rayuan Keputusan
- [ ] Paparkan tatacara permohonan bagi setiap jenis rayuan (langkah demi langkah)
- [ ] Paparkan kadar bayaran: RM25.00 (Semak Semula Skrip) dan RM50.00 (Rayuan Keputusan)
- [ ] Sediakan butang muat turun borang PDF (Lampiran 1 & Lampiran 2)
- [ ] Letak pautan terus ke website POLISAS untuk proses pembayaran
- [ ] Bina borang input ringkas untuk pelajar daftar rayuan (Nama, No. Matrik, Kursus, Jenis Rayuan, Tarikh Hantar)
- [ ] Paparkan arahan penghantaran: "Borang yang telah lengkap diisi perlu diserahkan terus ke Unit Peperiksaan POLISAS"
- [ ] Bina halaman semak status rayuan untuk pelajar (tunjuk: Sedang Diproses / Lulus / Tidak Lulus)
- [ ] Apabila status = Lulus, aktifkan butang muat turun surat kelulusan (PDF)
- [ ] Bina panel KPPJ untuk senarai semua rayuan masuk dan kemaskini status
- [ ] Pensyarah boleh semak senarai rayuan yang berkaitan dengan kursus mereka

**Relevant Context:**
- Pelajar isi borang secara manual (PDF) dan hantar terus ke Unit Peperiksaan POLISAS secara fizikal
- Dashboard hanya untuk tatacara, download borang, daftar rekod, dan semak status
- Surat kelulusan dijana oleh sistem sebagai PDF

**Status:** `[ ] pending`

---

### Sub-Tugas 3 — Modul CTCE (Credit Transfer and Course Exemption)

**Intent:**
Membolehkan pelajar membuat permohonan CTCE (Pindahan Kredit dan Pengecualian Kursus) melalui dashboard, dan KPPJ meluluskan atau menolak permohonan tersebut.

**Expected Outcomes:**
- Pelajar boleh isi dan hantar borang permohonan CTCE dalam talian.
- Permohonan disimpan dalam pangkalan data dengan status awal "Sedang Diproses".
- KPPJ boleh semak, luluskan, atau tolak setiap permohonan.
- Pelajar menerima notifikasi status terkini dalam dashboard mereka.
- Pelajar boleh muat turun surat kelulusan CTCE apabila diluluskan.

**Todo List:**
- [ ] Bina halaman CTCE dengan penerangan ringkas tentang CTCE
- [ ] Bina borang permohonan CTCE dalam talian (Nama, No. Matrik, Program, Kursus Asal, Kursus yang Dimohon, Justifikasi, lampiran dokumen sokongan)
- [ ] Fungsi hantar borang dan simpan ke pangkalan data
- [ ] Bina panel KPPJ untuk semak semua permohonan CTCE (senarai dengan status)
- [ ] KPPJ boleh luluskan atau tolak dengan nota/ulasan
- [ ] Kemaskini status permohonan secara automatik apabila KPPJ bertindak
- [ ] Paparkan status terkini kepada pelajar dalam halaman "Permohonan Saya"
- [ ] Jana surat kelulusan PDF apabila status = Lulus
- [ ] Pensyarah boleh semak senarai permohonan CTCE yang berkaitan dengan kursus mereka

**Relevant Context:**
- CTCE = Credit Transfer and Course Exemption (Pindahan Kredit dan Pengecualian Kursus)
- Aliran: Pelajar mohon → KPPJ semak → Lulus/Tolak → Pelajar dapat notifikasi

**Status:** `[ ] pending`

---

### Sub-Tugas 4 — Modul Proses Mastersheet

**Intent:**
Menyediakan platform berpusat untuk KPPJ dan Pensyarah mengurus dan memuat naik mastersheet markah pelajar.

**Expected Outcomes:**
- Pensyarah boleh muat naik mastersheet (fail Excel/CSV) mengikut kursus dan semester.
- KPPJ boleh semak, luluskan, dan simpan semua mastersheet.
- Status mastersheet setiap kursus dipaparkan (Belum Hantar / Telah Hantar / Disahkan).

**Todo List:**
- [ ] Bina halaman Proses Mastersheet untuk KPPJ dan Pensyarah
- [ ] Senarai kursus mengikut semester dengan status mastersheet
- [ ] Fungsi muat naik fail (Excel/CSV/PDF) oleh Pensyarah
- [ ] KPPJ boleh semak fail yang dimuat naik dan kemaskini status (Disahkan / Perlu Semak Semula)
- [ ] Paparan ringkasan status keseluruhan mastersheet jabatan

**Relevant Context:**
- Hanya KPPJ dan Pensyarah yang mempunyai akses modul ini

**Status:** `[ ] pending`

---

### Sub-Tugas 5 — Modul Penggubalan Item Peperiksaan

**Intent:**
Menyediakan platform pengurusan bank soalan digital dari fasa penggubalan hingga pengesahan.

**Expected Outcomes:**
- Pensyarah boleh masukkan item soalan baru dengan status "Draf".
- Aliran semakan: Draf → Semak → Lulus.
- KPPJ boleh semak dan luluskan item soalan.
- Item soalan boleh ditapis mengikut kursus, semester, atau status.

**Todo List:**
- [ ] Bina halaman Penggubalan Item Peperiksaan
- [ ] Borang tambah item soalan baru (kursus, tahap kesukaran, soalan, skema jawapan, pensyarah)
- [ ] Aliran status item: Draf → Sedang Disemak → Lulus / Perlu Pindaan
- [ ] Pensyarah boleh semak item yang mereka cipta dan status semasa
- [ ] KPPJ boleh semak, beri ulasan, dan luluskan atau kembalikan item
- [ ] Fungsi tapis dan cari mengikut kursus, status, dan semester

**Relevant Context:**
- Hanya KPPJ dan Pensyarah yang mempunyai akses modul ini

**Status:** `[ ] pending`

---

### Sub-Tugas 6 — Modul Jadual Waktu Peperiksaan

**Intent:**
Memaparkan jadual waktu peperiksaan dalam format yang mudah dibaca untuk semua pengguna.

**Expected Outcomes:**
- KPPJ boleh tambah, kemaskini, dan padam jadual peperiksaan.
- Pensyarah dan pelajar boleh semak jadual mengikut program atau semester.
- Jadual boleh dimuat turun sebagai PDF.

**Todo List:**
- [ ] Bina halaman Jadual Waktu Peperiksaan
- [ ] Paparan jadual dalam format jadual (table) atau kalendar
- [ ] Fungsi tapis mengikut program, semester, dan tarikh
- [ ] KPPJ boleh tambah/edit/padam entri jadual
- [ ] Fungsi muat turun jadual sebagai PDF

**Relevant Context:**
- Boleh diakses oleh KPPJ, Pensyarah, dan Pelajar

**Status:** `[ ] pending`

---

### Sub-Tugas 7 — Modul Laporan Pertengahan Semester

**Intent:**
Memudahkan pensyarah mengisi laporan pertengahan semester dan KPPJ menyemak semua laporan jabatan.

**Expected Outcomes:**
- Pensyarah boleh isi borang laporan pertengahan semester untuk setiap kursus.
- KPPJ boleh semak semua laporan dan papar ringkasan status.
- Status laporan dipaparkan: Belum Hantar / Telah Hantar / Disahkan.

**Todo List:**
- [ ] Bina halaman Laporan Pertengahan Semester
- [ ] Borang digital laporan pertengahan semester (markah ujian, kehadiran, ulasan)
- [ ] Pensyarah hantar laporan mengikut kursus yang diajar
- [ ] KPPJ semak senarai laporan semua pensyarah dengan status
- [ ] Fungsi muat turun laporan sebagai PDF

**Relevant Context:**
- Hanya KPPJ dan Pensyarah yang mempunyai akses modul ini

**Status:** `[ ] pending`

---

### Sub-Tugas 8 — Modul Bengkel Pengesahan Item PA

**Intent:**
Menyediakan maklumat dan pengurusan bengkel pengesahan item Penilaian Alternatif (PA) untuk KPPJ dan Pensyarah.

**Expected Outcomes:**
- KPPJ boleh tambah maklumat bengkel (tarikh, masa, tempat, agenda).
- Senarai peserta boleh diurus oleh KPPJ.
- Pensyarah boleh semak maklumat bengkel dan muat turun dokumen berkaitan.
- Status pengesahan item PA dipaparkan selepas bengkel.

**Todo List:**
- [ ] Bina halaman Bengkel Pengesahan Item PA
- [ ] KPPJ boleh tambah/edit/padam maklumat bengkel
- [ ] Senarai peserta (pensyarah) boleh diurus oleh KPPJ
- [ ] Fungsi muat naik dan muat turun dokumen bengkel (minit mesyuarat, item yang disahkan)
- [ ] Status item PA dipaparkan: Belum Disahkan / Telah Disahkan

**Relevant Context:**
- Hanya KPPJ dan Pensyarah yang mempunyai akses modul ini

**Status:** `[ ] pending`

---

### Sub-Tugas 9 — Modul List Tahan Peperiksaan Akhir

**Intent:**
Membolehkan pelajar menyemak status tahan peperiksaan mereka, dan KPPJ menguruskan senarai pelajar yang ditahan.

**Expected Outcomes:**
- KPPJ boleh tambah/kemaskini senarai pelajar yang ditahan daripada menduduki peperiksaan akhir.
- Pensyarah boleh semak senarai tahan mengikut kursus yang diajar.
- Pelajar boleh semak status tahan mereka menggunakan nombor matrik.
- Sebab tahan dan arahan seterusnya dipaparkan kepada pelajar.

**Todo List:**
- [ ] Bina halaman List Tahan Peperiksaan Akhir
- [ ] KPPJ boleh tambah pelajar ke senarai tahan (Nama, No. Matrik, Kursus, Sebab Tahan)
- [ ] Pensyarah boleh semak senarai tahan bagi kursus mereka
- [ ] Pelajar boleh cari status tahan menggunakan nombor matrik
- [ ] Paparan sebab tahan dan tindakan yang perlu diambil oleh pelajar

**Relevant Context:**
- Pelajar hanya boleh semak status — tiada fungsi mohon/edit

**Status:** `[ ] pending`

---

### Sub-Tugas 10 — Modul Peperiksaan Akhir Khas

**Intent:**
Membolehkan pelajar memohon peperiksaan akhir khas atas sebab-sebab tertentu, dengan aliran kelulusan bertingkat.

**Expected Outcomes:**
- Pelajar boleh hantar permohonan peperiksaan akhir khas.
- KPPJ semak dan luluskan/tolak permohonan.
- Pelajar dapat notifikasi status dalam dashboard.
- Jadual peperiksaan khas dipaparkan selepas kelulusan.

**Todo List:**
- [ ] Bina halaman Peperiksaan Akhir Khas
- [ ] Borang permohonan (Nama, No. Matrik, Kursus, Sebab Permohonan, Dokumen Sokongan)
- [ ] Aliran permohonan: Pelajar mohon → KPPJ semak → Lulus/Tolak
- [ ] Pelajar boleh semak status permohonan mereka
- [ ] KPPJ boleh tetapkan tarikh dan masa peperiksaan khas selepas meluluskan
- [ ] Papar jadual peperiksaan khas kepada pelajar yang diluluskan

**Relevant Context:**
- Boleh diakses oleh KPPJ, Pensyarah (semak sahaja), dan Pelajar (mohon + semak status)

**Status:** `[ ] pending`

---

### Sub-Tugas 11 — Modul Peperiksaan Akhir

**Intent:**
Menguruskan tugas-tugas berkaitan pengawasan peperiksaan akhir, termasuk pengurusan jadual pengawas dan proses gantian pengawas.

**Expected Outcomes:**
- KPPJ boleh cipta dan urus jadual pengawas peperiksaan.
- KPPJ boleh cipta dan urus jadual pengawas kedua.
- Pensyarah boleh semak jadual pengawasan mereka.
- Pensyarah boleh memohon gantian pengawas melalui borang dalam dashboard.
- KPPJ boleh semak dan luluskan permohonan gantian pengawas.

**Todo List:**
- [ ] Bina halaman Peperiksaan Akhir dengan tiga sub-seksyen
- [ ] Sub-seksyen 1: Jadual Pengawas Peperiksaan — KPPJ cipta/edit jadual, Pensyarah semak jadual diri sendiri
- [ ] Sub-seksyen 2: Jadual Pengawas Kedua — sama seperti di atas untuk pengawas kedua
- [ ] Sub-seksyen 3: Borang Gantian Pengawas — Pensyarah isi borang gantian (Nama, Sesi, Tarikh, Sebab, Nama Pengganti)
- [ ] KPPJ boleh semak permohonan gantian dan luluskan/tolak
- [ ] Paparan status gantian kepada pensyarah pemohon

**Relevant Context:**
- Hanya KPPJ dan Pensyarah yang mempunyai akses modul ini
- Pensyarah hanya boleh semak jadual diri mereka sendiri, bukan keseluruhan jadual

**Status:** `[ ] pending`

---

### Sub-Tugas 12 — Halaman Profil & Pengaturan Admin

**Intent:**
Menyediakan fungsi pengurusan akaun pengguna dan pengaturan asas sistem.

**Expected Outcomes:**
- KPPJ boleh tambah, kemaskini, dan nyahaktif akaun pengguna (pensyarah & pelajar).
- Semua pengguna boleh kemaskini maklumat profil dan kata laluan mereka.

**Todo List:**
- [ ] Bina halaman profil pengguna (kemaskini nama, email, kata laluan)
- [ ] Bina panel pengurusan pengguna untuk KPPJ (tambah/edit/nyahaktif akaun)
- [ ] KPPJ boleh assign peranan kepada pengguna baru (KPPJ / Pensyarah / Pelajar)

**Relevant Context:**
- KPPJ adalah pentadbir sistem

**Status:** `[ ] pending`

---

## Susunan Pembangunan (Dicadangkan)

1. Sub-Tugas 1 — Auth & Scaffold (asas sistem)
2. Sub-Tugas 2 — Rayuan Peperiksaan
3. Sub-Tugas 3 — CTCE
4. Sub-Tugas 6 — Jadual Waktu Peperiksaan
5. Sub-Tugas 9 — List Tahan Peperiksaan Akhir
6. Sub-Tugas 10 — Peperiksaan Akhir Khas
7. Sub-Tugas 11 — Peperiksaan Akhir
8. Sub-Tugas 4 — Proses Mastersheet
9. Sub-Tugas 5 — Penggubalan Item Peperiksaan
10. Sub-Tugas 7 — Laporan Pertengahan Semester
11. Sub-Tugas 8 — Bengkel Pengesahan Item PA
12. Sub-Tugas 12 — Profil & Admin

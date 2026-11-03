ASSETbyNu v1 — PETUNJUK INSTALASI
================================

ISI PAKET
- index.html: login
- dashboard.html: monitoring
- master.html: master gardu + rotasi + histori
- pengukuran.html: pengukuran siang/malam + WO + export
- peta.html: peta Leaflet/OpenStreetMap
- app.js, style.css, config.js
- database.sql: struktur database + RLS + rotasi atomik
- master_gardu_import.csv: 346 gardu dari GARDU SPN(1).xlsx

LANGKAH 1 — SUPABASE SQL
1. Masuk https://supabase.com/dashboard, pilih project ekoeueflvarnjlfgympv.
2. SQL Editor > New Query > paste seluruh database.sql > Run.
3. Authentication > Users > Add user: admin@asset.spn dan inspeksi@asset.spn, tentukan password masing-masing. Aktifkan email confirmed bila membuat secara manual. Jangan membagikan password.
4. SQL sudah membuat profiles otomatis dari email di atas. Jika user sudah dibuat sebelum SQL dijalankan, SQL juga mengisi profiles.
5. Table Editor > gardu > Import data from CSV > pilih master_gardu_import.csv. Jangan menghapus data lain jika project dipakai bersama.
6. Pastikan jumlah gardu 346.

LANGKAH 2 — GITHUB PAGES
1. Buat repo, upload seluruh file .html, .js, .css ke root repo.
2. Settings > Pages > Deploy from a branch > main / root > Save.
3. Buka URL Pages, login username 'admin' atau 'inspeksi' beserta password masing-masing.

CATATAN PENTING
- Published key di config.js memang publik; keamanan akses bergantung pada Supabase RLS. Jangan memasukkan service_role/secret key ke web.
- Jika Supabase Auth menolak domain .spn saat membuat user, gunakan email valid yang benar dan ubah mapping config.js serta alamat email pada SQL trigger sebelum menjalankan SQL. Email .spn bukan domain publik untuk pengiriman email.
- Akun inspeksi hanya dapat membaca gardu yang masuk WO miliknya, dan hanya dapat input pengukuran untuk gardu tersebut.
- Semester baru otomatis tampil BELUM UKUR tanpa menghapus hasil semester lalu.
- Reset progres dilakukan dengan memilih semester baru; data historis tidak dihapus.
- Master gardu Excel memiliki 113 baris dengan kapasitas aset berbeda dari kapasitas trafo. Dua kolom dipertahankan terpisah untuk validasi.
- Status sumber kosong atau tidak dikenali ditandai PERLU_VERIFIKASI, tidak otomatis diasumsikan aktif.
- Rotasi menukar identitas trafo secara atomik di SQL. Penggantian trafo satu gardu dilakukan melalui Edit dan terekam di riwayat.
- Aplikasi ini belum terhubung ke project Supabase secara live pada saat file dibuat; setelah SQL, import dan user dibuat, uji login dan operasi di project kamu.
- Field pengukuran mengikuti singkatan pada Excel: tegangan VRN/VSN/VTN/VRS/VST/VTR, arus utama IUN/IUR/IUS/IUT dan jurusan A–D.
- CDN internet diperlukan untuk Supabase JS, Leaflet, XLSX, dan font.

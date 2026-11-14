# Dashboard BMS Hormon-Oktober — Penyimpanan JSON di GitHub

Website: https://smartlab738-max.github.io/Hormon-Oktober/  
Repository: https://github.com/smartlab738-max/Hormon-Oktober

## Isi paket

```text
Hormon-Oktober/
├── index.html
└── bms-data/
    ├── 2026-09.json
    └── 2026-10.json
```

`index.html` tidak lagi menanam angka meter dari PDF. Data awal 13 panel berasal dari 13 PDF BMS yang dilampirkan (30 September – 31 Oktober 2026). 
JSON dibagi per bulan: setiap `panels.<kode_DPM>.<timestamp>` menyimpan `[Vavg, Iavg, Ptot, Edel, Freq, PF]`.

## Cara mengunggah

1. **Backup terlebih dahulu** `index.html` dan semua isi `bms-data/` yang telah ada di GitHub. JANGAN timpa file JSON online yang sudah berisi hasil impor baru dengan versi contoh ini.
2. Di repository `smartlab738-max/Hormon-Oktober` branch `main`, ganti `index.html` dengan file dari paket ini.
3. Jika folder `bms-data` **belum ada**, upload `bms-data/2026-09.json` dan `bms-data/2026-10.json` (buat folder lewat menu Add file → Create new file, nama `bms-data/2026-09.json`, atau upload folder via drag-drop).
4. Jika folder sudah ada, cek file bulan yang telah tersedia. Pertahankan data aktual dan hanya upload bulan yang belum ada; jangan overwrite tanpa menggabungkan data.
5. Commit perubahan, buka situs dan tekan Ctrl+Shift+R. Grafik Harian akan membaca JSON bulan terpilih, Grafik Bulanan membaca file tahun terpilih.

## Menambah PDF bulan depan

- Pilih PDF (satu atau banyak file). Dashboard mendeteksi panel, tanggal, bulan, dan tahun dari timestamp PDF, bukan header bulan.
- Data yang diimpor langsung diperlihatkan dan sementara dicadangkan di browser (IndexedDB).
- Tekan **Simpan ke GitHub** agar JSON bulan tersebut dibuat/diperbarui di repository, misalnya `bms-data/2026-11.json` atau `bms-data/2027-01.json`.
- Simpan ke GitHub memerlukan fine-grained PAT khusus repository `Hormon-Oktober`, **Contents: Read and write**. Token dimasukkan di halaman admin untuk sesi saat ini; jangan pernah masukkan token di HTML, JSON, commit, atau chat.
- GitHub Pages tidak menyediakan database server atau tulis otomatis tanpa autentikasi. File JSON di repo adalah sumber data, bukan database SQL. Isi JSON bersifat publik jika repo publik.

## Rumus & kelengkapan

Pemakaian harian = Edel jam terakhir − Edel jam pertama **pada tanggal yang sama**. Hari lengkap perlu data Edel 00:00 dan 23:00 serta 24 jam valid, tanpa delta negatif. Grafik Bulanan menjumlah hari lengkap. Jika bulan belum penuh, grafik dapat menampilkan *subtotal sementara*, dan tabel menandainya sebagai belum lengkap; data kosong bukan nol.

## Pengujian lokal

Karena browser memblokir `fetch()` file lokal via `file://`, lihat hasilnya dari GitHub Pages atau jalankan server statis di folder paket: `python -m http.server 8000`, kemudian buka `http://localhost:8000/`. Pada localhost dashboard dapat membaca JSON, tetapi tombol Simpan ke GitHub tetap memerlukan token.

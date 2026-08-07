# Dashboard Supervisi BOSP Kinerja Terbaik 2026

Dashboard satu halaman (Output 2) — link pengisian per lokus, status progres,
dan ringkasan analisis. Statis (HTML/CSS/JS polos, tanpa framework/build
step), memanggil data dari Web App API yang sudah dibuat di project Apps
Script terpisah (`web-app-api.js` di repo `bosp-instrumen-satdik`).

## Struktur

```
index.html   -> seluruh dashboard: markup, style, dan logic dalam satu file
```

## Sebelum deploy: pastikan API_URL benar

Di `index.html`, cari baris ini (dekat akhir file, dalam tag `<script>`):

```js
const API_URL = 'https://script.google.com/macros/s/AKfycbwH.../exec';
```

Ganti dengan Web App URL yang sebenarnya (dari Deploy > Manage deployments
di project Apps Script). Kalau URL itu berubah karena redeploy dengan opsi
yang menghasilkan URL baru, update baris ini juga.

## Setup GitHub (sekali saja)

```
cd bosp-dashboard
git init
git add .
git commit -m "Setup awal dashboard"
git branch -M main
git remote add origin https://github.com/<username>/<nama-repo>.git
git push -u origin main
```

## Deploy ke Vercel (sekali saja)

1. Buka vercel.com, login pakai akun yang sama dengan GitHub.
2. Klik "Add New" > "Project".
3. Pilih repo GitHub yang baru dibuat di atas (`bosp-dashboard` atau apapun
   namanya). Kalau repo belum muncul di daftar, klik "Adjust GitHub App
   Permissions" dan izinkan akses ke repo itu.
4. Framework Preset: biarkan default/"Other" — tidak perlu build command,
   karena ini cuma HTML statis. Root Directory: biarkan default (folder
   repo itu sendiri).
5. Klik Deploy. Beberapa detik selesai, muncul URL (bentuknya seperti
   `nama-project.vercel.app`). Itu link dashboard yang dibagikan ke semua
   pihak.

## Kalau ada revisi tampilan nanti

Edit `index.html`, commit, push ke GitHub — Vercel otomatis redeploy setiap
ada push ke branch `main`, tidak perlu langkah manual tambahan di Vercel.

## Catatan CORS

Dashboard ini fetch data dari domain berbeda (script.google.com dipanggil
dari domain vercel.app). Google Apps Script Web App biasanya mengizinkan
ini untuk request GET sederhana, tapi kalau saat dites ternyata data tidak
termuat dan console browser (F12) menunjukkan error CORS, itu tandanya
perlu penyesuaian di sisi `web-app-api.js` — beri tahu saya kalau ini
terjadi, ada cara mengatasinya.

# Dashboard Success Rate & RTS Rate

Dashboard interaktif (satu file `index.html`) yang membaca **CSV tracking order mentah langsung di browser**. Tidak ada data olahan di repo — hanya file CSV di folder `data/`.

## Aturan perhitungan
- Dihitung: **Delivered**, **Processing** (termasuk *Undelivered*), dan **RTS** (kolom `REMARK`).
- **Cancel** dan **Resi Menyusul** tidak ikut dihitung.
- Success Rate = Delivered ÷ (Delivered + Processing + RTS); RTS Rate = RTS ÷ total yang sama.
- Pengiklan dibaca dari kode di akhir nama produk (mis. `B-S-NFZ` → Albar, Sandy). Toko selain NFZ mengikuti nama toko. Pemetaan ada di `index.html` (konstanta `LEAD`, `SUB`, `TOKO`).

## Struktur
```
index.html   # dashboard (parsing CSV + grafik)
data/        # CSV tracking order per bulan
.nojekyll
```

## Menjalankan
**GitHub Pages:** Settings → Pages → Deploy from branch → `main` / root. Buka `https://<user>.github.io/<repo>/`.

**Lokal:** browser memblokir `fetch` dari `file://`, jadi jalankan server sederhana:
```
python3 -m http.server 8000   # lalu buka http://localhost:8000
```
Atau buka `index.html` langsung dan pakai tombol **Tambah / ganti data** untuk memilih CSV secara manual.

## Menambah bulan baru
1. Taruh CSV baru di `data/` dengan nama berakhiran kode bulan 3 huruf, mis. `..._-_OKT.csv`.
2. Tambahkan path file tersebut ke array `FILES` di `index.html`.
3. Commit & push.

Kolom yang wajib ada di header CSV: `TOKO`, `PRODUCT`, `REMARK` (yang dipakai adalah kolom pertama dengan nama tersebut).

> Catatan: CSV berisi nama dan nomor HP penerima. Pastikan repo **private**, atau hapus kolom tersebut dari CSV sebelum dipublikasikan.

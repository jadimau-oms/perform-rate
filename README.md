# Perform Rate — Dashboard Success Rate & RTS Rate

Dashboard statis (HTML + Chart.js + PapaParse) untuk memantau **Success Rate**, **RTS Rate**, konversi CS × pengiklan, dan produk konversi tinggi.

🔗 **Live:** https://jadimau-oms.github.io/perform-rate/

## Cara pakai
1. Buka link live di atas.
2. Unggah file CSV lewat tombol **Tambah / ganti data** (bisa banyak file sekaligus):
   - CSV **tracking** (`TRACKING_PAID_*`: kolom `ORDER ID`, `Tracking ID`, `DASHBOARD`, `ITEM`, `TANGGAL ORDER`, `GRANULAR STATUS`, `SETTLEMENT`). Format lama (`TOKO`, `PRODUCT`, `REMARK`) masih terbaca.
   - CSV **orderonline** (kolom `order_id`, `handled_by`, `status`, `payment_method`, `created_at`, ...)
3. Status tracking dibaca dari `GRANULAR STATUS`: DELIVERED, RTS, PROCESSING dihitung; IN PROGRESS (BAD SCORE / BLACKLIST COD), CANCEL, TIDAK COVER, dan RESI MENYUSUL dikeluarkan. `SETTLEMENT` ditampilkan di dialog selisih.
4. Order ID yang sama akan ditimpa, data lama tidak dihapus.

## Penyimpanan data
Di GitHub Pages, data yang diunggah disimpan di **IndexedDB browser** masing-masing pengguna (tidak dikirim ke server mana pun). Artinya data hanya ada di browser/perangkat yang dipakai mengunggah; buka dari perangkat lain harus unggah ulang.

> ⚠️ Jangan commit file CSV ke repo ini (sudah diblokir lewat `.gitignore`): isinya data order pelanggan dan repo/Pages bersifat publik.

## Struktur
```
index.html   # seluruh aplikasi (satu file)
.nojekyll    # matikan proses Jekyll di GitHub Pages
.gitignore
data/        # folder lokal untuk CSV (tidak di-commit)
```

## Deploy (GitHub Pages)
Settings → Pages → Source: **Deploy from a branch** → Branch: `main` / `(root)`.

## Pengembangan lokal
```bash
python3 -m http.server 8000   # lalu buka http://localhost:8000
```

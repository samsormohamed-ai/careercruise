# CareerCruise PWA (Pembalut GitHub Pages)

Pembalut ini membolehkan **CareerCruise: Jelajah Kota Kerjaya** dipasang sebagai ikon aplikasi di skrin telefon / tablet / Chromebook murid. Permainan sebenar tetap berjalan di Google Apps Script, jadi rekod murid kekal masuk ke Google Sheet yang sama.

## Isi kandungan

| Fail | Fungsi |
|---|---|
| `index.html` | Skrin pembuka + paparan penuh aplikasi Apps Script |
| `manifest.json` | Nama, warna dan ikon aplikasi |
| `sw.js` | Service worker (syarat untuk boleh dipasang) |
| `icons/` | Ikon aplikasi (biasa, maskable, Apple) |

## Langkah 1 — Pastikan Apps Script benarkan iframe

Dalam fail `Code.gs` CareerCruise, fungsi `doGet()` mesti ada baris `setXFrameOptionsMode` seperti ini:

```javascript
function doGet(e) {
  return HtmlService.createHtmlOutputFromFile('Index')   // atau createTemplateFromFile(...).evaluate()
    .setTitle('CareerCruise')
    .addMetaTag('viewport', 'width=device-width, initial-scale=1, viewport-fit=cover')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
}
```

Jika baris itu tiada, skrin akan kekal kosong dalam PWA. Selepas menambahnya: **Deploy → Manage deployments → Edit (ikon pensel) → Version: New version → Deploy**. Cara ini mengekalkan URL `/exec` yang sama.

## Langkah 2 — Muat naik ke GitHub

1. Buat repo baharu, contohnya `CAREERCRUISE` (Public).
2. **Add file → Upload files** → seret semua fail **dan folder `icons`** (ekstrak zip dahulu).
3. **Commit changes**.

## Langkah 3 — Hidupkan GitHub Pages

1. **Settings → Pages**.
2. Source: **Deploy from a branch** → Branch: **main** → folder **/ (root)** → **Save**.
3. Tunggu 1–2 minit. Pautan akan jadi:
   `https://<nama-pengguna>.github.io/CAREERCRUISE/`

## Langkah 4 — Pasang di peranti

- **Android (Chrome):** buka pautan → menu ⋮ → **Pasang aplikasi / Tambah ke skrin utama**.
- **iPhone / iPad (Safari):** buka pautan → butang Kongsi → **Add to Home Screen**.
- **Chromebook / komputer (Chrome/Edge):** ikon pasang di hujung kanan bar alamat.

## Nota

- Internet tetap diperlukan semasa bermain (rekod disimpan ke Google Sheet).
- Jika URL `/exec` berubah (deployment baharu, bukan "new version"), kemas kini `APP_URL` dalam `index.html`.
- Jika ikon lama masih muncul selepas kemas kini, tukar `careercruise-v1` kepada `careercruise-v2` dalam `sw.js`.
- Butang **Buka terus** pada skrin pembuka membuka permainan terus di Google jika paparan dalam PWA bermasalah.

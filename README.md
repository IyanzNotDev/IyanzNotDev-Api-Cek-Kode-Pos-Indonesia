# 📮 IyanzNotDev API Kode Pos

REST API simpel buat cari data kode pos Indonesia. Bisa cari pakai **nama wilayah** atau **kode pos 5 digit**.

**Base URL:** `https://iyanzinotdev.vercel.app`

---

## 📌 Endpoint

### 1. Cari berdasarkan nama

```
GET /api/kodepos?q=<nama>
```

| Parameter | Tipe   | Wajib | Keterangan                                   |
|-----------|--------|-------|----------------------------------------------|
| `q`       | string | ✅    | Nama wilayah (kelurahan/kecamatan/kota, dll) |

**Contoh:**

```
https://iyanzinotdev.vercel.app/api/kodepos?q=menteng
```

### 2. Cari berdasarkan kode pos

```
GET /api/kodepos?kodepos=<5 digit>
```

| Parameter  | Tipe   | Wajib | Keterangan             |
|------------|--------|-------|------------------------|
| `kodepos`  | string | ✅    | Kode pos (5 digit)     |

**Contoh:**

```
https://iyanzinotdev.vercel.app/api/kodepos?kodepos=10310
```

> Pakai salah satu aja: `q` **atau** `kodepos`.

---

## 🚀 Contoh Pemakaian

### cURL

```bash
curl "https://iyanzinotdev.vercel.app/api/kodepos?q=menteng"
curl "https://iyanzinotdev.vercel.app/api/kodepos?kodepos=10310"
```

### Node.js (fetch, tanpa dependency)

```js
const BASE = "https://iyanzinotdev.vercel.app/api/kodepos";

async function cariKodePos(nama) {
  const res = await fetch(`${BASE}?q=${encodeURIComponent(nama)}`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}

async function cekKodePos(kode) {
  const res = await fetch(`${BASE}?kodepos=${kode}`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}

cariKodePos("menteng").then(console.log).catch(console.error);
```

> Node.js 18+ udah bawaan `fetch`, jadi aman jalan di Termux tanpa install apa-apa.

---

## 📦 Contoh Response

> Bentuk field bisa beda tergantung data, ini cuma ilustrasi.

```json
{
  "status": true,
  "result": [
    {
      "kelurahan": "Menteng",
      "kecamatan": "Menteng",
      "kota": "Jakarta Pusat",
      "provinsi": "DKI Jakarta",
      "kodepos": "10310"
    }
  ]
}
```

---

## ⚠️ Catatan

- Kalau `q` / `kodepos` nggak diisi, request bakal gagal / hasil kosong.
- Kode pos harus **5 digit angka**.
- Pakai `encodeURIComponent` kalau nama wilayah ada spasi atau karakter khusus.

---

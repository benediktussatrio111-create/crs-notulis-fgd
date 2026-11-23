---
name: template-notulis-fgd
description: Membuat template atau slide notulensi FGD 16:9 bergaya CRS Ecosystem, berformat Heading, Sub-heading, Poin dengan cek diksi negatif. Gunakan saat pengguna meminta "template notulis", "template notulensi FGD", "slide notulensi", "rapikan notulen FGD", atau "buat lembar notulis untuk FGD" untuk acara CRS Ecosystem.
---

# Template Notulis FGD (CRS Ecosystem)

Membuat dek 16:9 (1920×1080) berisi satu slide notulensi per kelompok FGD, dengan gaya dan warna yang sama seperti deck informasi umum CRS Ecosystem.

Tampilan slide: eyebrow biru `FGD 01 · NOTULENSI`, judul `Hasil FGD <Bidang>` dengan nama bidang berwarna biru, tiga kartu (Lokasi · PJ · Notulis), lalu kotak **Catatan**. Footer: `Notulensi FGD · <Nama Acara> CRS Ecosystem` dan nomor `01 / 04`.

## Isi skill

- `scripts/build_deck.py` — mengubah data JSON menjadi satu file HTML mandiri (hanya pustaka standar Python).
- `scripts/cek_diksi.py` — menandai diksi berkonotasi negatif beserta opsi penggantinya (tidak mengubah file).
- `references/diksi.json` — daftar diksi negatif → opsi yang lebih positif.
- `references/deck.css`, `references/tokens.json` — gaya dan token sistem desain CRS Ecosystem.
- `examples/notulensi-kosong.json` — template kosongan 4 bidang.
- `examples/notulensi-contoh-isi.json` — contoh catatan yang sudah terisi.

## Data default

| No | id | Bidang | Lokasi default |
|----|----|--------|----------------|
| 01 | produksi | Produksi | Resto Lt. 11 · Indoor |
| 02 | marketing | Marketing | Ruang Progo · Lt. 5 |
| 03 | financial | Financial | Resto Lt. 3 · Indoor |
| 04 | sdm | SDM | Resto Lt. 3 · Outdoor |

- Lokasi berlaku untuk Technical Meetup November 2026. Untuk acara lain, tanyakan lokasi atau isi "…".
- PJ dan Notulis diisi "…" kecuali pengguna menyebut namanya.
- Nama acara default: "Technical Meetup". Selalu tulis "Financial", bukan "Keuangan".

## Struktur data

```json
{
  "acara": { "nama": "Technical Meetup", "organisasi": "CRS Ecosystem", "tanggal": "Selasa, 24 November 2026", "tempat": "Aruss Hotel" },
  "slides": [
    { "type": "notulensi", "nomor": "01", "id": "produksi", "nama": "Produksi",
      "lokasi": "Resto Lt. 11 · Indoor", "pj": "…", "notulis": "…",
      "catatan": [
        { "heading": "Laporan Keuangan Studio",
          "sub": [ { "judul": "Kondisi saat ini", "poin": ["…"] },
                   { "judul": "Kesepakatan", "poin": ["…"] } ] },
        { "heading": "Kelas Marketing", "poin": ["…"] }
      ] }
  ]
}
```

`id` menentukan warna badge nomor heading (produksi pink, marketing oranye, financial kuning tua, sdm hijau). `catatan: []` tampil sebagai satu poin "…" untuk diisi manual.

## Format isi Catatan: Heading → Sub-heading → Poin

- **Heading** = topik besar yang dibahas (2–5 kata, tanpa titik). Diberi nomor otomatis 01, 02, … dalam badge berwarna bidang.
- **Sub-heading** (`sub[].judul`) = aspek dari topik, berwarna biru. Pola yang dianjurkan: *Kondisi saat ini*, *Usulan*, *Kesepakatan*, *Tindak lanjut*, *PIC & tenggat*. Boleh dilewati bila topiknya sederhana (pakai `poin` langsung di bawah heading).
- **Poin** = satu gagasan per poin, kalimat pendek tanpa titik di akhir, maksimal ±15 kata.
- Jangan mengarang isi. Rapikan bahasa dan kelompokkan saja; jika ada bagian yang tidak jelas, tanyakan ke pengguna.
- Isi panjang otomatis dibagi ke 2 kolom, lalu ke slide lanjutan (`FGD 03 · NOTULENSI · LANJUTAN`) tanpa terpotong.

## Langkah

1. **Template kosongan:** salin `examples/notulensi-kosong.json`, sesuaikan nama acara, bidang, lokasi, PJ dan notulis yang disebut pengguna, lalu lanjut ke langkah 4.
2. **Notulen berisi:** susun catatan mentah pengguna ke format Heading → Sub-heading → Poin di atas.
3. **Wajib cek diksi sebelum membuat slide:**
   ```bash
   python3 scripts/cek_diksi.py data.json
   ```
   Baca juga seluruh catatan sendiri: nada negatif bisa muncul tanpa kata yang ada di daftar (menyalahkan orang tertentu, sindiran, kalimat menghakimi).
   **Jangan mengganti diksi secara diam-diam.** Tampilkan setiap temuan ke pengguna:
   > **[1] Financial › Laporan Keuangan › Kondisi saat ini**
   > "Laporan beberapa studio sering *telat* masuk"
   > Opsi: (a) melewati jadwal · (b) belum tepat waktu · (c) perlu penyesuaian jadwal · (d) biarkan apa adanya

   Beri 2–3 opsi yang lebih positif tetapi tetap jujur dan tidak mengubah fakta, plus opsi membiarkan. Bila AskUserQuestion tersedia, pakai pilihan ganda per temuan. Terapkan pilihan pengguna; kata yang dipilih untuk dibiarkan tidak ditanyakan lagi di sesi itu. Tambahkan diksi baru ke `references/diksi.json` bila pengguna memintanya.
4. Bangun slide:
   ```bash
   python3 scripts/build_deck.py data.json notulensi.html
   ```
5. Periksa hasilnya, lalu serahkan: publikasikan sebagai artifact (HTML) bila tersedia, atau kirim file HTML. Untuk PDF: buka di Chrome → Print → Save as PDF (margin None, background graphics aktif).
6. Jika sesi menawarkan tipe Slides dan pengguna ingin mengetik langsung di slide, susun dek dengan tipe Slides memakai `references/tokens.json` dan tata letak yang sama.

## Gaya bahasa

Bahasa Indonesia yang ringkas dan santai-profesional, seperti materi CRS Ecosystem lainnya. Pakai "·" sebagai pemisah info (`Resto Lt. 3 · Indoor`).

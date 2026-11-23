---
name: template-notulis-fgd
description: Membuat template notulis atau notulensi FGD berbentuk slide 16:9 dengan branding CRS Ecosystem. Gunakan saat pengguna meminta "template notulis", "template notulensi FGD", "slide notulensi", atau "buat lembar notulis untuk FGD" untuk acara CRS Ecosystem.
---

# Template Notulis FGD (CRS Ecosystem)

Buat dek slide 16:9 berisi satu slide notulensi kosong per kelompok FGD, dengan gaya yang sama seperti deck informasi umum CRS Ecosystem.

## Data default

Gunakan urutan dan warna bidang ini kecuali pengguna memberi data lain:

| No | id | Bidang | Kelas warna | Lokasi default |
|----|----|--------|-------------|----------------|
| 01 | produksi | Produksi | c-produksi (#be185d) | Resto Lt. 11 · Indoor |
| 02 | marketing | Marketing | c-marketing (#c2410c) | Ruang Progo · Lt. 5 |
| 03 | financial | Financial | c-financial (#b45309) | Resto Lt. 3 · Indoor |
| 04 | sdm | SDM | c-sdm (#047857) | Resto Lt. 3 · Outdoor |

- Lokasi berlaku untuk Technical Meetup November 2026. Untuk acara lain, tanyakan lokasi atau isi "…".
- PJ dan Notulis diisi "…" kecuali pengguna menyebut namanya.
- Nama acara default: "Technical Meetup".
- Selalu tulis "Financial", bukan "Keuangan".

## Langkah

1. Tanyakan hanya yang belum jelas: nama acara, bidang yang ikut, lokasi, PJ dan notulis. Jika pengguna ingin "kosongan", pakai default dan "…".
2. Buat dek dari tipe Slides jika sesi menawarkannya; jika tidak, buat file HTML atau PPTX dengan tampilan yang sama.
3. Pakai `references/deck.css` sebagai CSS bersama dek, dan `references/tokens.json` sebagai token sistem desain CRS Ecosystem.
4. Untuk setiap bidang, isi `references/slide-template.html`: ganti `{{id}}`, `{{nomor}}`, `{{bidang}}`, `{{lokasi}}`, `{{pj}}`, `{{notulis}}`, `{{nama_acara}}`, `{{no_halaman}}` (dua digit, misalnya 01) dan `{{total_halaman}}`.
5. Pertahankan kotak Catatan tetap kosong (satu poin "…") agar notulis bisa mengetik langsung. Jangan menambah topik, tabel kesepakatan, jumlah hadir, tidak hadir, atau tanda tangan kecuali diminta.
6. Font: Inter (Google Fonts, `family=Inter:opsz,wght@14..32,400..900`).
7. Beri tahu pengguna bahwa slide bisa diduplikat jika catatan lebih dari satu halaman.

## Gaya bahasa

Tulis dalam Bahasa Indonesia yang ringkas dan santai-profesional, seperti materi CRS Ecosystem lainnya.

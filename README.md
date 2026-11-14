# DEVTRACE AI — Deck Presentasi Web

Deck hackathon Tim **Noer Maha Oke** dalam satu file: `index.html`.
Tanpa build step, tanpa server, tanpa dependency — cukup dibuka di browser.

- Format: satu slide memenuhi **seluruh layar** (fluid, tanpa letterbox 16:9) — aman di 16:9, 16:10, dan 21:9
- Theme: glassy iOS, font monospace (JetBrains Mono)
- Animasi: transisi slide, stagger reveal, typewriter, count-up, gradient orbs
- Navigasi: keyboard + swipe. **Tanpa HUD**: brand, dots, counter, dan tombol fullscreen disembunyikan

## Cara presentasi

1. Buka `index.html` di Chrome (double-click atau drag ke browser).
2. Tekan **F** untuk fullscreen. Kursor sembunyi otomatis setelah 2 detik idle.
3. Navigasi:

| Aksi | Kontrol |
|---|---|
| Slide berikutnya | `→` · `Space` · `PageDown` · swipe kiri |
| Slide sebelumnya | `←` · `PageUp` · swipe kanan |
| Slide pertama / terakhir | `Home` / `End` |
| Fullscreen | `F` |
| Lompat ke slide tertentu | buka `index.html#8` |

Semua chrome di layar sudah disembunyikan supaya tampilan bersih saat presentasi.
Kalau nanti mau dots/counter/tombol fullscreen muncul lagi, hapus baris ini di `<style>`:

```css
#hud,#progress,.zone{display:none !important}
```

## Mengganti nama anggota tim

Buka `index.html`, cari placeholder ini dan ganti teksnya:

```
[Nama 1]   [Peran 1]
[Nama 2]   [Peran 2]
[Nama 3]   [Peran 3]
[Nama 4]   [Peran 4]
```

Semua ada di slide 2 (`data-title="Tim"`). Kalau jumlah anggota bukan 4, hapus/duplikasi satu blok `<article class="member glass reveal">…</article>`.

## Struktur slide

| # | Slide | Isi |
|---|---|---|
| 1 | Cover | Judul, tagline, mock terminal error → diagnosis |
| 2 | Tim | Nama tim + kartu anggota |
| 3 | Problem | 5 pain point + inti masalah |
| 4 | Current Process | 7 langkah manual + keterbatasan |
| 5 | Solution | 5 pilar solusi |
| 6 | Arsitektur | 4 tahap alur monitoring → aksi developer |
| 7 | AI Diagnosis | Contoh diagnosis + rekomendasi kode |
| 8 | Impact | Before/After, 79,2%, tabel target |
| 9 | Governance | 8 aspek + 5 prinsip |
| 10 | Security | 9 ancaman → mitigasi + acuan OWASP/PDP |
| 11 | KODE | Kolaboratif · Otomatisasi · Data-Driven · Efisien & Etis |
| 12 | Pembeda | 3 proposisi inovasi |
| 13 | Recap | Problem → Solution → Impact |
| 14 | Thanks | "Thanks for your attention." + ajakan demo |
| 15 | Q&A | "Apakah ada pertanyaan?" |

## Catatan teknis

- **Font**: JetBrains Mono dimuat dari Google Fonts. Tanpa internet, otomatis jatuh ke monospace sistem (Menlo/Consolas) — layout tetap aman.
- **Fluid layout**: ukuran teks, padding, dan tinggi kartu memakai `clamp()` berbasis viewport, jadi deck mengisi layar berapa pun rasionya tanpa scroll.
- **Deep link** (`#8`) bekerja saat disajikan lewat HTTP; di `file://` sebagian browser memblokir update hash, tapi navigasi tetap normal.
- **Reduced motion**: jika OS mengaktifkan "reduce motion", semua animasi dimatikan otomatis.
- **Kustomisasi warna**: semua warna ada di blok `:root` (`--blue`, `--mint`, `--purple`, dst.) di bagian atas `<style>`.
- **Bawa ke venue**: cukup bawa folder ini (atau `index.html` saja). Tidak ada proses install.

## Validasi yang sudah dilakukan

- 15 slide terdaftar, struktur HTML tanpa tag menggantung, `node --check` untuk JS inline lolos.
- Screenshot headless Chrome pada 1280×800, 1440×900, 1600×900, dan 2560×1080 — tanpa overflow/teks terpotong.


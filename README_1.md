# GSAP Text Interactions — 20 Animasi Premium

Satu file `index.html` berisi 20 animasi teks siap production. Hanya memakai **GSAP 3 + SplitText + ScrollTrigger + TextPlugin** (semua gratis sejak GSAP diakuisisi Webflow). Semua gerak lewat `transform` + `opacity` untuk 60fps.

## Cara pakai global

Semua parameter diatur langsung di objek `ANIMATIONS` dalam `<script>`. Pola umum tiap tween:

```js
gsap.from(target, {
  duration: 0.9,        // ← DURASI (detik)
  delay:    0,          // ← DELAY sebelum mulai
  ease:     "power3.out", // ← EASE
  stagger:  0.05        // ← jeda antar huruf/kata
});
```

- **Ubah durasi** → ganti `duration`.
- **Ubah ease** → `power2.out`, `power4.out`, `back.out(1.7)`, `elastic.out(1,0.4)`, `sine.inOut`.
- **Ubah stagger** → besar = lebih lambat berurutan; `from:"center"|"random"|"edges"`.
- **Ubah teks** → ganti properti `text` pada animasi terkait.
- **Ubah warna** → CSS variabel `--accent` di `:root`, atau `color` pada `.headline`.

Default proyek: `gsap.defaults({ ease:"power3.out", duration:0.9 })`.

## Referensi per animasi (Durasi · Warna · Teks)

| # | Nama | Ubah Durasi | Ubah Warna | Ubah Teks |
|---|------|-------------|------------|-----------|
| 01 | Fade In per Huruf | `duration` / `stagger` di tween | `--accent` atau `.headline{color}` | properti `text` |
| 02 | Fade In per Kata | `duration` / `stagger` | `.headline{color}` | `text` |
| 03 | Typewriter | `full.length * 0.045` (naikkan faktor) | `--accent` (caret) | ubah `const full` |
| 04 | Scramble Text | `duration:1.4` | `.headline{color}` | `const final` |
| 05 | Split Text Reveal | `duration` / `stagger` | `.headline{color}` | `text` |
| 06 | Slide Up Characters | `duration` / `ease:"back.out(n)"` | `.headline{color}` | `text` |
| 07 | Slide Down Words | `duration` / blur `filter` | `.headline{color}` | `text` |
| 08 | Rotate Characters | `duration` / `rotationX` | `.headline{color}` | `text` |
| 09 | Wave Text | `each` di stagger / `duration` | `.headline{color}` | `text` |
| 10 | Elastic Bounce | `ease:"elastic.out(amp,period)"` | `.headline{color}` | `text` |
| 11 | Glitch Reveal | `repeat` & `duration` getar | `.glitch::before/after` (RGB) | `text` |
| 12 | Neon Flicker | durasi tiap step timeline | `--accent`, `--accent-2` (glow) | `text` |
| 13 | Blur to Sharp | `duration` / `blur(px)` | `.headline{color}` | `text` |
| 14 | Zoom In Characters | `duration` / `scale` awal | `.headline{color}` | `text` |
| 15 | Flip Text Reveal | `duration` / `stagger` | `.headline{color}` | `text` |
| 16 | Mask Reveal | `duration` / `ease` | `.headline{color}` | `text` |
| 17 | Infinite Floating | `duration` loop / `y` jarak | `.headline{color}` | `text` |
| 18 | Scroll Trigger Reveal | `duration`, `start:"top 88%"` | `.headline{color}` | `text` |
| 19 | Hover Letter Explosion | `duration` explode/reset | `.headline{color}` | `text` |
| 20 | Mouse Follow Distortion | `quickTo(...,{duration})` | `.headline{color}` | `text` |

## Replay & auto-play

Setiap kartu punya tombol **Replay** yang membangun ulang teks dari state bersih lalu memanggil `anim.play()`. Animasi masuk berjalan otomatis saat halaman dibuka; animasi hover/mouse (19, 20) mengikat listener dan menunggu interaksi.

## Aksesibilitas

Menghormati `prefers-reduced-motion`: jika aktif, teks langsung tampil tanpa animasi.

## Pindah ke React / Vue / Next.js

Kode sudah modular — setiap animasi adalah fungsi `play({ headline, stage })`.

- **React**: pasang di `useGSAP(() => { ... }, { scope: ref })`; taruh `SplitText`/registrasi plugin di top-level.
- **Vue**: jalankan di `onMounted`, cleanup di `onUnmounted` via `gsap.context()` atau `ScrollTrigger.kill()`.
- Ganti `document.querySelector` dengan `ref`, sisanya identik.

## Ganti font

Edit `--font-display` / `--font-body` di `:root` dan link Google Fonts di `<head>`.

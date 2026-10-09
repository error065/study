# 📘 Materi CSS Lengkap

Materi ini disusun berurutan dari dasar sampai lanjutan. Setiap contoh kode disertai **contoh output** (gambaran tampilan di browser dalam bentuk teks/diagram, karena file `.md` tidak bisa menjalankan CSS).

## 📑 Daftar Isi

1. [Apa itu CSS](#1-apa-itu-css)
2. [Macam-macam Selector CSS](#2-macam-macam-selector-css)
3. [Macam-macam Property CSS beserta Value-nya — Part 1](#3-property-css-part-1-satuan-warna-background-font--teks)
4. [Macam-macam Property CSS beserta Value-nya — Part 2](#4-property-css-part-2-box-model-display-position--layout-dasar)
5. [Macam-macam Property CSS beserta Value-nya — Part 3](#5-property-css-part-3-flexbox-grid-animasi-responsive--lanjutan)

---

# 1. Apa itu CSS

## 1.1 Pengertian

**CSS** adalah singkatan dari **Cascading Style Sheets**. CSS adalah bahasa *style sheet* yang dipakai untuk mengatur **tampilan** dokumen HTML: warna, ukuran, jarak, posisi, font, animasi, dan tata letak (layout).

Analogi sederhana:

| Teknologi | Peran | Analogi pada rumah |
|-----------|-------|--------------------|
| HTML | Struktur / isi halaman | Tembok, pintu, jendela |
| **CSS** | Tampilan / gaya | Cat, dekorasi, tata ruang |
| JavaScript | Perilaku / interaksi | Listrik, lampu, pintu otomatis |

Arti kata **Cascading**: ketika ada beberapa aturan CSS yang mengenai elemen yang sama, browser memakai aturan berurutan (cascade) untuk menentukan aturan mana yang menang (berdasarkan asal, *specificity*, dan urutan penulisan).

**Contoh: HTML tanpa CSS vs dengan CSS**

```html
<h1>Halo Dunia</h1>
<p>Ini paragraf.</p>
```

**Output (tanpa CSS):**

```text
Halo Dunia          ← hitam, tebal, besar (gaya bawaan browser)
Ini paragraf.       ← hitam, ukuran normal
```

```html
<style>
  h1 { color: white; background: royalblue; padding: 10px; }
  p  { color: gray; font-style: italic; }
</style>
<h1>Halo Dunia</h1>
<p>Ini paragraf.</p>
```

**Output (dengan CSS):**

```text
┌────────────────────────────┐
│ Halo Dunia                 │  ← teks putih, latar biru, ada jarak dalam
└────────────────────────────┘
Ini paragraf.                   ← teks abu-abu, miring
```

## 1.2 Sintaks Dasar CSS

```text
selector {
  property: value;
  property: value;
}
```

| Bagian | Fungsi | Contoh |
|--------|--------|--------|
| **Selector** | Memilih elemen HTML yang ingin diberi gaya | `h1` |
| **Declaration block** | Kurung kurawal `{ }` berisi deklarasi | `{ ... }` |
| **Property** | Sifat yang diubah | `color` |
| **Value** | Nilai dari sifat tersebut | `red` |
| **Declaration** | Pasangan `property: value;` | `color: red;` |

```css
p {
  color: red;
  font-size: 20px;
}
```

**Output:**

```text
Semua <p> tampil dengan teks MERAH berukuran 20px.
```

## 1.3 Tiga Cara Menulis CSS

### a) Inline CSS
Ditulis langsung di atribut `style` pada elemen.

```html
<p style="color: green; font-size: 18px;">Teks hijau inline</p>
```

**Output:**

```text
Teks hijau inline      ← hijau, 18px (hanya berlaku untuk elemen ini)
```

### b) Internal CSS
Ditulis di dalam tag `<style>` pada `<head>`.

```html
<head>
  <style>
    p { color: purple; }
  </style>
</head>
<body>
  <p>Paragraf 1</p>
  <p>Paragraf 2</p>
</body>
```

**Output:**

```text
Paragraf 1      ← ungu
Paragraf 2      ← ungu
```

### c) External CSS (paling direkomendasikan)
Ditulis di file terpisah (`style.css`) lalu dihubungkan dengan `<link>`.

```html
<!-- index.html -->
<head>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <p>Teks dari file eksternal</p>
</body>
```

```css
/* style.css */
p { color: orange; }
```

**Output:**

```text
Teks dari file eksternal      ← oranye
```

**Perbandingan:**

| Cara | Kelebihan | Kekurangan |
|------|-----------|------------|
| Inline | Cepat untuk uji coba | Sulit dirawat, tidak bisa dipakai ulang |
| Internal | Cocok untuk 1 halaman | Tidak bisa dipakai di halaman lain |
| External | Rapi, dipakai banyak halaman, di-*cache* browser | Perlu file tambahan |

### d) `@import`
Mengimpor CSS lain dari dalam file CSS (harus di baris paling atas).

```css
@import url("reset.css");
body { margin: 0; }
```

**Output:**

```text
Aturan di reset.css ikut dimuat, lalu body tanpa margin.
```

## 1.4 Komentar di CSS

```css
/* Ini komentar satu baris */
p {
  color: blue; /* komentar di samping kode */
  /*
    Komentar
    banyak baris
  */
}
```

**Output:**

```text
Komentar tidak tampil di halaman. Paragraf tetap berwarna biru.
```

## 1.5 Cascade, Specificity, dan Inheritance

### a) Urutan penulisan (cascade)
Jika specificity sama, aturan yang **ditulis terakhir** yang menang.

```css
p { color: red; }
p { color: blue; }
```

**Output:**

```text
Teks <p> berwarna BIRU (aturan terakhir menang).
```

### b) Specificity (tingkat kekhususan)
Semakin spesifik selector, semakin tinggi prioritasnya.

| Jenis | Bobot | Contoh |
|-------|-------|--------|
| Inline style | 1000 | `style="..."` |
| ID | 100 | `#judul` |
| Class, atribut, pseudo-class | 10 | `.kotak`, `[type]`, `:hover` |
| Tag, pseudo-element | 1 | `p`, `::before` |
| Universal | 0 | `*` |

```html
<p id="a" class="b">Teks</p>
<style>
  p      { color: red; }     /* bobot 1   */
  .b     { color: green; }   /* bobot 10  */
  #a     { color: blue; }    /* bobot 100 */
</style>
```

**Output:**

```text
Teks      ← BIRU (ID punya bobot tertinggi)
```

### c) `!important`
Memaksa sebuah deklarasi menang (gunakan seperlunya).

```css
p { color: red !important; }
#a { color: blue; }
```

**Output:**

```text
Teks      ← MERAH (karena !important mengalahkan ID)
```

### d) Inheritance (pewarisan)
Beberapa property (misalnya `color`, `font-family`, `line-height`) otomatis diwariskan ke elemen anak. Property lain (misalnya `border`, `margin`, `padding`) **tidak** diwariskan.

```html
<div style="color: crimson; border: 2px solid black;">
  Teks div
  <p>Teks di dalam p</p>
</div>
```

**Output:**

```text
┌──────────────────────────┐
│ Teks div          (merah)│
│ Teks di dalam p   (merah)│  ← warna diwariskan, tapi border TIDAK
└──────────────────────────┘
```

### e) Nilai khusus pewarisan

| Value | Arti |
|-------|------|
| `inherit` | Ambil nilai dari elemen induk |
| `initial` | Kembali ke nilai awal bawaan spesifikasi CSS |
| `unset` | `inherit` jika property bisa diwariskan, jika tidak jadi `initial` |
| `revert` | Kembali ke gaya bawaan browser |

```css
.induk { border: 2px solid red; }
.anak  { border: inherit; }
```

**Output:**

```text
Elemen .anak memakai border 2px solid red seperti induknya.
```

## 1.6 Gambaran Box Model

Setiap elemen HTML dianggap sebagai **kotak** yang terdiri dari 4 lapisan:

```text
┌───────────────────────────────┐
│            MARGIN             │  ← jarak luar
│  ┌─────────────────────────┐  │
│  │         BORDER          │  │  ← garis tepi
│  │  ┌───────────────────┐  │  │
│  │  │      PADDING      │  │  │  ← jarak dalam
│  │  │  ┌─────────────┐  │  │  │
│  │  │  │   CONTENT   │  │  │  │  ← isi (teks/gambar)
│  │  │  └─────────────┘  │  │  │
│  │  └───────────────────┘  │  │
│  └─────────────────────────┘  │
└───────────────────────────────┘
```

(Dibahas detail di Bagian 4.)

---

# 2. Macam-macam Selector CSS

**Selector** adalah bagian CSS yang menentukan **elemen mana** yang akan diberi gaya.

Kita pakai HTML contoh ini untuk beberapa pembahasan:

```html
<div class="kotak" id="utama">
  <h2>Judul</h2>
  <p class="intro">Paragraf pertama</p>
  <p>Paragraf kedua</p>
  <a href="#">Tautan</a>
</div>
```

## 2.1 Selector Dasar

### a) Universal selector `*`
Memilih **semua** elemen.

```css
* { margin: 0; padding: 0; box-sizing: border-box; }
```

**Output:**

```text
Semua elemen kehilangan margin & padding bawaan browser,
sehingga teks dan kotak menempel rapat ke tepi.
```

### b) Type / Element selector
Memilih berdasarkan nama tag.

```css
p { color: teal; }
```

**Output:**

```text
Paragraf pertama      ← teal
Paragraf kedua        ← teal
```

### c) Class selector `.nama`
Memilih elemen dengan atribut `class`. Boleh dipakai banyak elemen.

```css
.intro { font-weight: bold; color: crimson; }
```

**Output:**

```text
Paragraf pertama      ← MERAH & TEBAL
Paragraf kedua        ← normal
```

### d) ID selector `#nama`
Memilih satu elemen dengan atribut `id` (ID harus unik).

```css
#utama { background: lightyellow; padding: 10px; }
```

**Output:**

```text
┌─────────────────────────────┐
│ (latar kuning muda)         │
│ Judul                       │
│ Paragraf pertama            │
│ Paragraf kedua              │
│ Tautan                      │
└─────────────────────────────┘
```

### e) Grouping selector `,`
Memberi gaya yang sama ke beberapa selector.

```css
h2, .intro, a { color: royalblue; }
```

**Output:**

```text
Judul                 ← biru
Paragraf pertama      ← biru
Tautan                ← biru
Paragraf kedua        ← warna normal
```

### f) Selector gabungan tag + class
```css
p.intro { text-decoration: underline; }
```

**Output:**

```text
Paragraf pertama      ← bergaris bawah (hanya <p> yang punya class intro)
```

### g) Beberapa class sekaligus
```html
<p class="a b">Teks</p>
```
```css
.a.b { color: red; }   /* harus punya class a DAN b */
```

**Output:**

```text
Teks      ← merah
```

## 2.2 Selector Kombinator (Hubungan Antar Elemen)

### a) Descendant (spasi) — semua keturunan
```css
.kotak p { color: green; }
```

**Output:**

```text
Semua <p> di dalam .kotak (di kedalaman mana pun) → hijau
```

### b) Child `>` — anak langsung saja
```css
.kotak > p { border-left: 4px solid red; padding-left: 8px; }
```

**Output:**

```text
┃ Paragraf pertama      ← ada garis merah di kiri
┃ Paragraf kedua        ← ada garis merah di kiri
(cucu elemen tidak terkena)
```

### c) Adjacent sibling `+` — saudara tepat sesudahnya
```css
h2 + p { color: red; }
```

**Output:**

```text
Judul
Paragraf pertama      ← MERAH (tepat setelah h2)
Paragraf kedua        ← normal
```

### d) General sibling `~` — semua saudara sesudahnya
```css
h2 ~ p { color: red; }
```

**Output:**

```text
Judul
Paragraf pertama      ← MERAH
Paragraf kedua        ← MERAH
```

## 2.3 Attribute Selector

| Selector | Arti |
|----------|------|
| `[attr]` | Punya atribut `attr` |
| `[attr="x"]` | Nilai atribut sama persis `x` |
| `[attr~="x"]` | Salah satu kata (dipisah spasi) sama dengan `x` |
| `[attr\|="x"]` | Sama dengan `x` atau diawali `x-` |
| `[attr^="x"]` | Diawali `x` |
| `[attr$="x"]` | Diakhiri `x` |
| `[attr*="x"]` | Mengandung `x` |
| `[attr="x" i]` | Tidak membedakan huruf besar/kecil |

```html
<a href="https://google.com">Google</a>
<a href="/halaman.pdf">File PDF</a>
<a href="mailto:a@b.com">Email</a>
<input type="text">
<input type="password">
```

```css
a[href^="https"] { color: green; }       /* diawali https */
a[href$=".pdf"]  { color: red; }         /* diakhiri .pdf */
a[href*="mailto"]{ color: purple; }      /* mengandung mailto */
input[type="text"] { border: 2px solid blue; }
```

**Output:**

```text
Google      ← hijau
File PDF    ← merah
Email       ← ungu
[__________]  ← input teks, border biru
[**********]  ← input password, border normal
```

## 2.4 Pseudo-class (keadaan elemen) — diawali `:`

### a) Pseudo-class tautan & interaksi

| Pseudo-class | Aktif saat |
|--------------|-----------|
| `:link` | Tautan belum pernah dikunjungi |
| `:visited` | Tautan sudah dikunjungi |
| `:hover` | Kursor di atas elemen |
| `:active` | Elemen sedang diklik/ditekan |
| `:focus` | Elemen sedang fokus (misal input diklik) |
| `:focus-visible` | Fokus yang tampil via keyboard |
| `:focus-within` | Elemen/anaknya sedang fokus |

```css
a:link    { color: blue; }
a:visited { color: purple; }
a:hover   { color: red; text-decoration: underline; }
a:active  { color: orange; }
input:focus { outline: 3px solid dodgerblue; }
```

**Output:**

```text
Tautan baru          → biru
Tautan dikunjungi    → ungu
Kursor di atasnya    → merah + garis bawah
Saat ditekan         → oranye
Input diklik         → muncul garis tepi biru tebal
```

### b) Pseudo-class struktural

| Pseudo-class | Fungsi |
|--------------|--------|
| `:first-child` | Anak pertama |
| `:last-child` | Anak terakhir |
| `:only-child` | Satu-satunya anak |
| `:nth-child(n)` | Anak ke-n |
| `:nth-last-child(n)` | Anak ke-n dari belakang |
| `:first-of-type` / `:last-of-type` | Pertama/terakhir dari tipe tag yang sama |
| `:nth-of-type(n)` | Ke-n dari tipe tag yang sama |
| `:only-of-type` | Satu-satunya dari tipe tag itu |
| `:empty` | Elemen tanpa isi |
| `:root` | Elemen akar (`<html>`) |

```html
<ul>
  <li>Satu</li>
  <li>Dua</li>
  <li>Tiga</li>
  <li>Empat</li>
  <li>Lima</li>
</ul>
```

```css
li:first-child     { color: red; }
li:last-child      { color: blue; }
li:nth-child(2)    { font-weight: bold; }
li:nth-child(odd)  { background: #eee; }
li:nth-child(3n)   { text-decoration: underline; }
```

**Output:**

```text
• Satu      ← merah, latar abu (ganjil)
• Dua       ← tebal
• Tiga      ← latar abu (ganjil), bergaris bawah (kelipatan 3)
• Empat
• Lima      ← biru, latar abu (ganjil)
```

Rumus `nth-child`:

| Ekspresi | Hasil |
|----------|-------|
| `2` | Hanya ke-2 |
| `odd` | 1, 3, 5, … |
| `even` | 2, 4, 6, … |
| `3n` | 3, 6, 9, … |
| `2n+1` | 1, 3, 5, … |
| `n+3` | Ke-3 dan seterusnya |
| `-n+3` | 3 pertama |

### c) Pseudo-class logika

| Pseudo-class | Fungsi |
|--------------|--------|
| `:not(x)` | Elemen yang BUKAN `x` |
| `:is(a, b)` | Salah satu dari daftar (menyingkat penulisan) |
| `:where(a, b)` | Sama seperti `:is` tapi specificity 0 |
| `:has(x)` | Elemen yang **memiliki** keturunan `x` (parent selector) |

```css
li:not(:last-child) { border-bottom: 1px solid gray; }
:is(h1, h2, h3) { color: navy; }
div:has(img) { border: 2px solid green; }
```

**Output:**

```text
Semua <li> kecuali yang terakhir punya garis pemisah di bawah.
h1, h2, h3 berwarna navy.
<div> yang berisi <img> diberi border hijau.
```

### d) Pseudo-class form

| Pseudo-class | Fungsi |
|--------------|--------|
| `:checked` | Checkbox/radio terpilih |
| `:disabled` / `:enabled` | Input nonaktif / aktif |
| `:required` / `:optional` | Input wajib / opsional |
| `:valid` / `:invalid` | Isi valid / tidak valid |
| `:read-only` / `:read-write` | Hanya baca / bisa diedit |
| `:placeholder-shown` | Placeholder sedang tampil |
| `:in-range` / `:out-of-range` | Dalam / luar rentang min–max |

```html
<input type="email" required placeholder="Email">
<input type="checkbox" id="c"><label for="c">Setuju</label>
```

```css
input:invalid { border: 2px solid red; }
input:valid   { border: 2px solid green; }
input:checked + label { color: green; font-weight: bold; }
```

**Output:**

```text
[ Email kosong/salah ]   ← border merah
[ a@b.com            ]   ← border hijau
☑ Setuju                 ← label hijau tebal saat dicentang
```

### e) Pseudo-class lain
| Pseudo-class | Fungsi |
|--------------|--------|
| `:target` | Elemen yang ID-nya sedang ditunjuk oleh URL `#id` |
| `:lang(id)` | Elemen dengan bahasa tertentu |
| `:fullscreen` | Elemen dalam mode layar penuh |

```css
section:target { background: yellow; }
```

**Output:**

```text
Saat URL berakhiran #bagian1, <section id="bagian1"> berlatar kuning.
```

## 2.5 Pseudo-element — diawali `::`

| Pseudo-element | Fungsi |
|----------------|--------|
| `::before` | Menyisipkan konten sebelum isi elemen |
| `::after` | Menyisipkan konten sesudah isi elemen |
| `::first-letter` | Huruf pertama |
| `::first-line` | Baris pertama |
| `::selection` | Teks yang diblok/seleksi |
| `::placeholder` | Teks placeholder input |
| `::marker` | Penanda list (bullet/angka) |
| `::backdrop` | Latar belakang dialog/fullscreen |

```html
<p class="catatan">Ini teks penting.</p>
<p class="cerita">Pada suatu hari ada seekor kancil yang cerdik.</p>
<input placeholder="Ketik nama">
```

```css
.catatan::before { content: "⚠ "; color: orange; }
.catatan::after  { content: " (wajib)"; color: red; }
.cerita::first-letter { font-size: 2em; color: crimson; }
.cerita::first-line { font-weight: bold; }
::selection { background: gold; color: black; }
input::placeholder { color: lightgray; font-style: italic; }
li::marker { color: red; }
```

**Output:**

```text
⚠ Ini teks penting. (wajib)      ← ikon oranye di depan, "(wajib)" merah di belakang
Pada suatu hari ada ...          ← huruf "P" besar & merah, baris pertama tebal
[ Ketik nama ]                   ← placeholder abu-abu muda & miring
(Teks yang diblok mouse berlatar emas)
```

## 2.6 CSS Nesting (selector bersarang)

CSS modern mendukung penulisan selector di dalam selector lain.

```css
.kartu {
  padding: 10px;
  background: white;

  h3 { color: navy; }
  &:hover { background: #f0f0f0; }
  .tombol { color: white; background: blue; }
}
```

**Output:**

```text
Setara dengan:
.kartu {...}
.kartu h3 {...}
.kartu:hover {...}
.kartu .tombol {...}
```

## 2.7 Ringkasan Selector

| Selector | Contoh | Memilih |
|----------|--------|---------|
| Universal | `*` | Semua elemen |
| Tag | `p` | Semua `<p>` |
| Class | `.a` | Elemen `class="a"` |
| ID | `#a` | Elemen `id="a"` |
| Grup | `h1, p` | h1 dan p |
| Descendant | `div p` | p di dalam div |
| Child | `div > p` | p anak langsung div |
| Adjacent | `h1 + p` | p tepat setelah h1 |
| Sibling | `h1 ~ p` | Semua p setelah h1 |
| Atribut | `[type="text"]` | Elemen berdasarkan atribut |
| Pseudo-class | `a:hover` | Elemen dalam keadaan tertentu |
| Pseudo-element | `p::first-line` | Bagian tertentu dari elemen |

---

# 3. Property CSS Part 1: Satuan, Warna, Background, Font & Teks

## 3.1 Satuan (Unit) di CSS

### a) Satuan absolut

| Satuan | Arti |
|--------|------|
| `px` | Pixel (paling umum) |
| `cm`, `mm`, `in` | Sentimeter, milimeter, inci |
| `pt`, `pc` | Point (1/72 in), pica (12pt) |

### b) Satuan relatif

| Satuan | Relatif terhadap |
|--------|------------------|
| `%` | Persen dari elemen induk |
| `em` | Ukuran font elemen itu sendiri/induk |
| `rem` | Ukuran font elemen `<html>` (root) |
| `vw` | 1% lebar viewport (layar) |
| `vh` | 1% tinggi viewport |
| `vmin` / `vmax` | 1% sisi viewport terkecil / terbesar |
| `ch` | Lebar karakter "0" |
| `dvh`, `svh`, `lvh` | Tinggi viewport dinamis/kecil/besar (berguna di mobile) |
| `fr` | Pecahan ruang di CSS Grid |

```html
<div class="a">Kotak A</div>
<div class="b">Kotak B</div>
<div class="c">Kotak C</div>
```

```css
html { font-size: 16px; }
.a { width: 200px;  background: lightblue; }
.b { width: 50%;    background: lightgreen; }   /* 50% dari lebar induk */
.c { width: 10rem;  background: pink; }         /* 10 x 16px = 160px */
```

**Output (induk lebar 600px):**

```text
┌────────────────────┐
│ Kotak A            │  200px (biru)
└────────────────────┘
┌──────────────────────────────┐
│ Kotak B                      │  300px (hijau)
└──────────────────────────────┘
┌──────────────────┐
│ Kotak C          │  160px (merah muda)
└──────────────────┘
```

## 3.2 Warna

### a) Cara menulis warna

| Format | Contoh |
|--------|--------|
| Nama warna | `red`, `tomato`, `skyblue` |
| HEX | `#ff0000`, `#f00`, `#ff000080` (dengan alpha) |
| RGB | `rgb(255, 0, 0)` |
| RGBA | `rgba(255, 0, 0, 0.5)` |
| HSL | `hsl(0, 100%, 50%)` |
| HSLA | `hsla(0, 100%, 50%, 0.5)` |
| Modern | `rgb(255 0 0 / 50%)`, `oklch()`, `lab()`, `color-mix()` |
| Khusus | `transparent`, `currentColor` |

```html
<p class="w1">Merah nama</p>
<p class="w2">Merah HEX</p>
<p class="w3">Merah RGB</p>
<p class="w4">Merah HSL</p>
<p class="w5">Merah transparan 50%</p>
```

```css
.w1 { color: red; }
.w2 { color: #ff0000; }
.w3 { color: rgb(255, 0, 0); }
.w4 { color: hsl(0, 100%, 50%); }
.w5 { color: rgba(255, 0, 0, 0.5); }
```

**Output:**

```text
Merah nama              ← merah
Merah HEX               ← merah (sama)
Merah RGB               ← merah (sama)
Merah HSL               ← merah (sama)
Merah transparan 50%    ← merah pudar (setengah transparan)
```

### b) Property `color`
Mengatur warna teks.

```css
h1 { color: darkgreen; }
```

**Output:**

```text
Judul      ← teks hijau tua
```

### c) Property `opacity`
Tingkat transparansi seluruh elemen (0 = transparan, 1 = solid).

```css
.pudar { opacity: 0.4; }
```

**Output:**

```text
Kotak biasa     ← jelas
Kotak pudar     ← samar (40% terlihat), termasuk teks & isinya
```

## 3.3 Background

| Property | Fungsi | Contoh value |
|----------|--------|--------------|
| `background-color` | Warna latar | `red`, `#eee`, `transparent` |
| `background-image` | Gambar latar | `url("a.jpg")`, `linear-gradient(...)` |
| `background-repeat` | Pengulangan gambar | `repeat`, `no-repeat`, `repeat-x`, `repeat-y`, `space`, `round` |
| `background-position` | Posisi gambar | `center`, `top left`, `50% 20%`, `10px 20px` |
| `background-size` | Ukuran gambar | `auto`, `cover`, `contain`, `100px 50px`, `50%` |
| `background-attachment` | Perilaku saat scroll | `scroll`, `fixed`, `local` |
| `background-origin` | Area awal posisi gambar | `padding-box`, `border-box`, `content-box` |
| `background-clip` | Area yang tertutup latar | `border-box`, `padding-box`, `content-box`, `text` |
| `background-blend-mode` | Pencampuran layer latar | `multiply`, `screen`, `overlay` |
| `background` | Shorthand semuanya | `red url(a.jpg) no-repeat center/cover` |

### a) background-color
```css
.kotak { background-color: lightcoral; padding: 20px; }
```

**Output:**

```text
┌──────────────────────┐
│ Teks                 │  ← latar merah muda kecoklatan
└──────────────────────┘
```

### b) Gradient

```css
.linear  { background: linear-gradient(to right, red, yellow); }
.sudut   { background: linear-gradient(45deg, blue, pink); }
.radial  { background: radial-gradient(circle, white, navy); }
.conic   { background: conic-gradient(red, yellow, green, blue, red); }
.ulang   { background: repeating-linear-gradient(45deg, #eee 0 10px, #ccc 10px 20px); }
```

**Output:**

```text
.linear  : [merah ▓▓▒▒░░ kuning]            gradasi kiri ke kanan
.sudut   : gradasi miring 45°, biru → pink
.radial  : pusat putih memudar ke biru tua di tepi (lingkaran)
.conic   : gradasi melingkar seperti roda warna
.ulang   : garis-garis miring abu-abu bergantian
```

### c) background-image, repeat, position, size

```css
.hero {
  height: 200px;
  background-image: url("pantai.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
```

**Output:**

```text
┌──────────────────────────────────┐
│  [foto pantai memenuhi kotak,    │
│   dipotong agar pas, di tengah]  │
└──────────────────────────────────┘
```

Perbandingan `background-size`:

| Value | Perilaku |
|-------|----------|
| `cover` | Gambar menutupi seluruh area (bisa terpotong) |
| `contain` | Gambar tampil utuh (bisa ada ruang kosong) |
| `100% 100%` | Ditarik memenuhi area (bisa gepeng) |
| `auto` | Ukuran asli gambar |

### d) Multiple background & shorthand

```css
.banner {
  background:
    linear-gradient(rgba(0,0,0,.5), rgba(0,0,0,.5)),
    url("kota.jpg") center / cover no-repeat;
}
```

**Output:**

```text
Foto kota dengan lapisan hitam transparan 50% di atasnya
(sehingga teks putih di atasnya lebih mudah dibaca).
```

### e) background-clip: text (teks bergradasi)

```css
.judul {
  font-size: 40px;
  font-weight: bold;
  background: linear-gradient(to right, red, blue);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
```

**Output:**

```text
HALO DUNIA   ← huruf-hurufnya berwarna gradasi merah → biru
```

## 3.4 Font

| Property | Fungsi | Contoh value |
|----------|--------|--------------|
| `font-family` | Jenis font | `Arial, sans-serif` |
| `font-size` | Ukuran font | `16px`, `1.2rem`, `larger`, `x-large` |
| `font-weight` | Ketebalan | `normal`, `bold`, `100`–`900`, `lighter`, `bolder` |
| `font-style` | Gaya | `normal`, `italic`, `oblique` |
| `font-variant` | Varian | `normal`, `small-caps` |
| `font-stretch` | Kelebaran font | `condensed`, `expanded`, `75%`–`125%` |
| `line-height` | Tinggi baris | `1.5`, `24px`, `150%` |
| `font` | Shorthand | `italic bold 16px/1.5 Arial, sans-serif` |

### a) font-family
Selalu beri *fallback* (font cadangan) dan diakhiri *generic family*: `serif`, `sans-serif`, `monospace`, `cursive`, `fantasy`, `system-ui`.

```css
.a { font-family: "Times New Roman", serif; }
.b { font-family: Arial, Helvetica, sans-serif; }
.c { font-family: "Courier New", monospace; }
```

**Output:**

```text
Teks A  ← huruf berkait (serif) seperti koran
Teks B  ← huruf tanpa kait (sans-serif), modern
Teks C  ← huruf lebar sama (monospace) seperti kode
```

### b) font-size, font-weight, font-style

```css
.kecil  { font-size: 12px; }
.besar  { font-size: 2rem; }
.tebal  { font-weight: 700; }
.tipis  { font-weight: 300; }
.miring { font-style: italic; }
.kapital{ font-variant: small-caps; }
```

**Output:**

```text
teks kecil            ← 12px
TEKS BESAR            ← 32px (2 x 16px)
**teks tebal**        ← bold
teks tipis            ← light
*teks miring*         ← italic
Teks Kapital          ← huruf kecil tampil sebagai kapital mini
```

### c) line-height

```css
p { line-height: 1.8; }
```

**Output:**

```text
Baris pertama paragraf

Baris kedua paragraf       ← jarak antar baris lebih lega (1.8 x ukuran font)
```

### d) font shorthand

```css
p { font: italic bold 18px/1.5 Georgia, serif; }
```

**Output:**

```text
Teks miring, tebal, 18px, tinggi baris 1.5, font Georgia.
```

### e) @font-face (font sendiri) & Google Fonts

```css
@font-face {
  font-family: "FontKu";
  src: url("fontku.woff2") format("woff2");
  font-weight: normal;
  font-display: swap;
}
body { font-family: "FontKu", sans-serif; }
```

Atau lewat Google Fonts:

```html
<link href="https://fonts.googleapis.com/css2?family=Poppins&display=swap" rel="stylesheet">
<style> body { font-family: "Poppins", sans-serif; } </style>
```

**Output:**

```text
Seluruh teks halaman tampil dengan font kustom (FontKu / Poppins).
Jika gagal dimuat, memakai sans-serif.
```

## 3.5 Teks (Text)

| Property | Fungsi | Contoh value |
|----------|--------|--------------|
| `text-align` | Perataan horizontal | `left`, `right`, `center`, `justify` |
| `text-align-last` | Perataan baris terakhir | `left`, `center`, `justify` |
| `text-decoration` | Dekorasi | `none`, `underline`, `overline`, `line-through` |
| `text-decoration-color/style/thickness` | Detail dekorasi | `red`, `wavy`, `3px` |
| `text-underline-offset` | Jarak garis bawah | `5px` |
| `text-transform` | Huruf besar/kecil | `uppercase`, `lowercase`, `capitalize` |
| `text-indent` | Indentasi baris pertama | `30px`, `2em` |
| `text-shadow` | Bayangan teks | `2px 2px 4px gray` |
| `letter-spacing` | Jarak antar huruf | `2px`, `0.1em` |
| `word-spacing` | Jarak antar kata | `10px` |
| `white-space` | Penanganan spasi/baris baru | `normal`, `nowrap`, `pre`, `pre-wrap`, `pre-line` |
| `word-break` | Pemotongan kata | `normal`, `break-all`, `keep-all` |
| `overflow-wrap` | Patahkan kata panjang | `normal`, `break-word`, `anywhere` |
| `text-overflow` | Teks yang meluber | `clip`, `ellipsis` |
| `direction` | Arah teks | `ltr`, `rtl` |
| `writing-mode` | Arah penulisan | `horizontal-tb`, `vertical-rl` |
| `vertical-align` | Perataan vertikal inline | `baseline`, `top`, `middle`, `bottom`, `sub`, `super` |
| `text-wrap` | Pembungkusan teks | `wrap`, `nowrap`, `balance`, `pretty` |
| `hyphens` | Tanda hubung otomatis | `none`, `manual`, `auto` |
| `tab-size` | Lebar tab | `4` |

### a) text-align

```css
.kiri   { text-align: left; }
.tengah { text-align: center; }
.kanan  { text-align: right; }
.rata   { text-align: justify; }
```

**Output:**

```text
Teks kiri
        Teks tengah
                          Teks kanan
Teks rata kiri-kanan sehingga kedua tepi lurus rapi
```

### b) text-decoration

```css
.u { text-decoration: underline; }
.l { text-decoration: line-through; }
.w { text-decoration: underline wavy red 2px; }
a  { text-decoration: none; }
```

**Output:**

```text
Teks u    ← bergaris bawah
Teks l    ← dicoret
Teks w    ← garis bawah bergelombang merah
Tautan    ← tanpa garis bawah
```

### c) text-transform

```css
.a { text-transform: uppercase; }
.b { text-transform: lowercase; }
.c { text-transform: capitalize; }
```
```html
<p class="a">belajar css</p>
<p class="b">BELAJAR CSS</p>
<p class="c">belajar css</p>
```

**Output:**

```text
BELAJAR CSS
belajar css
Belajar Css
```

### d) text-indent, letter-spacing, word-spacing

```css
.p1 { text-indent: 40px; }
.p2 { letter-spacing: 5px; }
.p3 { word-spacing: 20px; }
```

**Output:**

```text
    Baris pertama menjorok ke dalam 40px.
B e l a j a r  C S S    ← huruf berjarak 5px
Belajar        CSS      ← jarak antar kata 20px
```

### e) text-shadow

```css
h1 { text-shadow: 3px 3px 5px gray; }
.neon { color: white; text-shadow: 0 0 5px cyan, 0 0 15px cyan; }
```

Format: `offset-x offset-y blur warna`.

**Output:**

```text
JUDUL   ← ada bayangan abu-abu di kanan-bawah huruf
NEON    ← teks putih dengan cahaya cyan di sekelilingnya
```

### f) white-space, text-overflow (teks terpotong titik tiga)

```css
.potong {
  width: 150px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```
```html
<p class="potong">Ini adalah kalimat yang sangat panjang sekali</p>
```

**Output:**

```text
┌────────────────┐
│Ini adalah kal… │   ← terpotong dan diakhiri titik tiga
└────────────────┘
```

### g) Memotong teks setelah N baris (line clamp)

```css
.clamp {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

**Output:**

```text
Baris pertama teks panjang yang
baris kedua juga masih tampil ...   ← sisanya disembunyikan, ditutup "…"
```

### h) word-break & overflow-wrap

```css
.kotak { width: 120px; border: 1px solid; }
.a { overflow-wrap: break-word; }
.b { word-break: break-all; }
```
```html
<p class="kotak a">Supercalifragilisticexpialidocious</p>
```

**Output:**

```text
┌────────────┐
│Supercalifra│
│gilisticexpi│   ← kata panjang dipatahkan agar tidak keluar kotak
│alidocious  │
└────────────┘
```

### i) vertical-align (untuk elemen inline / sel tabel)

```css
img { vertical-align: middle; }
.atas { vertical-align: super; }
```

**Output:**

```text
[gambar] teks sejajar tengah gambar
x² ← teks "2" tampil naik seperti pangkat
```

### j) writing-mode

```css
.tegak { writing-mode: vertical-rl; }
```

**Output:**

```text
H
a
l
o
(teks tampil vertikal dari atas ke bawah)
```

## 3.6 List (Daftar)

| Property | Fungsi | Contoh value |
|----------|--------|--------------|
| `list-style-type` | Jenis penanda | `disc`, `circle`, `square`, `decimal`, `lower-alpha`, `upper-roman`, `none` |
| `list-style-position` | Posisi penanda | `inside`, `outside` |
| `list-style-image` | Penanda berupa gambar | `url("icon.png")` |
| `list-style` | Shorthand | `square inside` |

```css
.a { list-style-type: square; }
.b { list-style-type: upper-roman; }
.c { list-style: none; padding: 0; }
```
```html
<ul class="a"><li>Apel</li><li>Jeruk</li></ul>
<ol class="b"><li>Satu</li><li>Dua</li></ol>
<ul class="c"><li>Tanpa bullet</li></ul>
```

**Output:**

```text
■ Apel
■ Jeruk

I. Satu
II. Dua

Tanpa bullet
```

## 3.7 Link/Tautan & Cursor

### a) Gaya tautan

```css
a { color: royalblue; text-decoration: none; }
a:hover { color: crimson; text-decoration: underline; }
```

**Output:**

```text
Tautan       ← biru tanpa garis bawah
Tautan(hover)← merah bergaris bawah
```

### b) cursor

| Value | Bentuk kursor |
|-------|---------------|
| `default` | Panah |
| `pointer` | Tangan (untuk tautan/tombol) |
| `text` | Tanda I (teks) |
| `move` | Panah empat arah |
| `not-allowed` | Dilarang (lingkaran dicoret) |
| `wait` | Jam pasir/loading |
| `grab` / `grabbing` | Tangan menggenggam |
| `crosshair` | Tanda plus |
| `zoom-in` / `zoom-out` | Kaca pembesar |
| `help` | Tanda tanya |

```css
button { cursor: pointer; }
button:disabled { cursor: not-allowed; }
```

**Output:**

```text
Kursor di atas tombol aktif     → 👆 tangan
Kursor di atas tombol nonaktif  → 🚫 dilarang
```

## 3.8 Contoh Gabungan Part 1

```html
<div class="kartu">
  <h2>Belajar CSS</h2>
  <p>CSS membuat web menjadi indah dan menarik.</p>
  <a href="#">Baca selengkapnya</a>
</div>
```

```css
.kartu {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  font-family: Arial, sans-serif;
  padding: 20px;
  width: 300px;
}
.kartu h2 {
  text-transform: uppercase;
  letter-spacing: 2px;
  text-shadow: 2px 2px 4px rgba(0,0,0,.4);
}
.kartu p { line-height: 1.6; }
.kartu a { color: gold; text-decoration: none; }
.kartu a:hover { text-decoration: underline; }
```

**Output:**

```text
┌──────────────────────────────────┐
│ B E L A J A R  C S S             │  ← putih, huruf kapital, berbayang
│                                  │
│ CSS membuat web menjadi indah    │
│ dan menarik.                     │
│                                  │
│ Baca selengkapnya                │  ← emas
└──────────────────────────────────┘
   (latar gradasi biru → ungu)
```

---

# 4. Property CSS Part 2: Box Model, Display, Position & Layout Dasar

## 4.1 Box Model

Setiap elemen terdiri dari **content → padding → border → margin** (lihat diagram di bagian 1.6).

### a) width & height

| Property | Fungsi | Contoh value |
|----------|--------|--------------|
| `width` / `height` | Lebar / tinggi | `200px`, `50%`, `auto`, `100vw`, `fit-content`, `max-content`, `min-content` |
| `min-width` / `min-height` | Ukuran minimum | `100px` |
| `max-width` / `max-height` | Ukuran maksimum | `600px`, `100%`, `none` |

```css
.kotak {
  width: 200px;
  height: 100px;
  background: lightblue;
}
.fleksibel {
  width: 100%;
  max-width: 400px;   /* tidak akan lebih lebar dari 400px */
  background: lightgreen;
}
```

**Output:**

```text
┌─────────────────┐
│                 │  200 x 100 px (biru muda)
└─────────────────┘
┌───────────────────────────────┐
│ lebar penuh, tapi maks 400px  │  (hijau muda)
└───────────────────────────────┘
```

### b) padding (jarak dalam)

| Property | Fungsi |
|----------|--------|
| `padding` | Semua sisi |
| `padding-top/right/bottom/left` | Sisi tertentu |
| `padding-inline` / `padding-block` | Arah horizontal / vertikal (logical) |

Aturan shorthand:

| Penulisan | Arti |
|-----------|------|
| `padding: 10px` | Semua sisi 10px |
| `padding: 10px 20px` | Atas-bawah 10px, kiri-kanan 20px |
| `padding: 10px 20px 30px` | Atas 10, kiri-kanan 20, bawah 30 |
| `padding: 10px 20px 30px 40px` | Atas, kanan, bawah, kiri (searah jarum jam) |

```css
.kotak { padding: 20px 40px; background: gold; }
```

**Output:**

```text
┌──────────────────────────────┐
│          (20px)              │
│ (40px) Teks di sini  (40px)  │
│          (20px)              │
└──────────────────────────────┘
```

### c) margin (jarak luar)

| Property | Fungsi |
|----------|--------|
| `margin` | Semua sisi (aturan shorthand sama dengan padding) |
| `margin-top/right/bottom/left` | Sisi tertentu |
| `margin: 0 auto` | Elemen block berlebar tertentu jadi **rata tengah** horizontal |
| `margin` negatif | Menarik elemen ke arah sebaliknya |

```css
.kotak {
  width: 200px;
  background: salmon;
  margin: 30px auto;
}
```

**Output:**

```text
        (jarak 30px dari atas)
          ┌──────────────┐
          │    Kotak     │   ← berada di TENGAH halaman
          └──────────────┘
        (jarak 30px dari bawah)
```

**Margin collapsing:** margin vertikal dua elemen block yang bertemu **menyatu** (diambil yang terbesar).

```css
.a { margin-bottom: 40px; }
.b { margin-top: 20px; }
```

**Output:**

```text
[ A ]
        ← jarak 40px (bukan 60px)
[ B ]
```

### d) border

| Property | Fungsi | Contoh value |
|----------|--------|--------------|
| `border-width` | Ketebalan | `1px`, `thin`, `medium`, `thick` |
| `border-style` | Gaya garis | `solid`, `dashed`, `dotted`, `double`, `groove`, `ridge`, `inset`, `outset`, `none`, `hidden` |
| `border-color` | Warna | `red`, `#333` |
| `border` | Shorthand | `2px solid red` |
| `border-top/right/bottom/left` | Sisi tertentu | `border-bottom: 3px solid blue` |
| `border-radius` | Sudut membulat | `10px`, `50%`, `10px 20px`, `20px / 50px` |
| `border-image` | Border dari gambar/gradasi | `linear-gradient(red, blue) 1` |
| `border-collapse` | Gabung border tabel | `collapse`, `separate` |
| `border-spacing` | Jarak antar sel tabel | `5px` |

```css
.s { border: 3px solid black; }
.d { border: 3px dashed red; }
.t { border: 3px dotted green; }
.g { border: 6px double blue; }
.b { border-bottom: 4px solid orange; }
```

**Output:**

```text
┌─────────────┐  solid  (garis hitam utuh)
┌ ─ ─ ─ ─ ─ ─ ┐  dashed (garis putus-putus merah)
· · · · · · · ·  dotted (titik-titik hijau)
╔═════════════╗  double (garis ganda biru)
_______________  hanya border bawah (oranye)
```

**border-radius:**

```css
.a { border-radius: 10px; }
.b { border-radius: 50%; width: 100px; height: 100px; }
.c { border-radius: 20px 0 20px 0; }
.d { border-radius: 999px; padding: 10px 30px; }   /* tombol pil */
```

**Output:**

```text
.a  : persegi dengan sudut sedikit membulat   ╭────╮
.b  : LINGKARAN sempurna (karena lebar = tinggi)   ( ● )
.c  : sudut kiri-atas & kanan-bawah bulat, lainnya tajam
.d  : tombol berbentuk kapsul (ujung setengah lingkaran)  (  Tombol  )
```

### e) outline
Mirip border tapi **tidak memengaruhi ukuran** elemen.

| Property | Contoh |
|----------|--------|
| `outline` | `2px solid red` |
| `outline-offset` | `5px` (jarak outline dari tepi elemen) |
| `outline-style/color/width` | Detail |

```css
button:focus { outline: 3px solid dodgerblue; outline-offset: 4px; }
```

**Output:**

```text
   ┌────────────────┐
   │ ┌────────────┐ │   ← garis biru terpisah 4px di luar tombol
   │ │   Tombol   │ │
   │ └────────────┘ │
   └────────────────┘
```

### f) box-sizing

| Value | Perhitungan lebar total |
|-------|-------------------------|
| `content-box` (default) | width + padding + border |
| `border-box` | width **sudah termasuk** padding + border |

```css
.a { width: 200px; padding: 20px; border: 5px solid; box-sizing: content-box; }
.b { width: 200px; padding: 20px; border: 5px solid; box-sizing: border-box; }
```

**Output:**

```text
.a : lebar total = 200 + 40 + 10 = 250px
.b : lebar total = 200px (padding & border masuk ke dalam 200px)
```

Praktik umum:

```css
*, *::before, *::after { box-sizing: border-box; }
```

### g) box-shadow

Format: `offset-x offset-y blur spread warna [inset]`

```css
.a { box-shadow: 5px 5px 10px gray; }
.b { box-shadow: 0 4px 12px rgba(0,0,0,.2); }
.c { box-shadow: inset 0 0 10px black; }
.d { box-shadow: 0 0 0 4px red; }                     /* seperti border luar */
.e { box-shadow: 0 2px 4px #000, 0 8px 16px #555; }   /* berlapis */
```

**Output:**

```text
.a : kotak dengan bayangan abu-abu di kanan-bawah
.b : bayangan lembut halus di bawah (gaya kartu modern)
.c : bayangan di DALAM kotak (tampak cekung)
.d : cincin merah 4px mengelilingi kotak
.e : dua lapis bayangan sekaligus
```

## 4.2 Overflow (Isi yang Meluber)

| Value | Perilaku |
|-------|----------|
| `visible` (default) | Isi tetap tampil keluar kotak |
| `hidden` | Isi yang keluar dipotong |
| `scroll` | Selalu ada scrollbar |
| `auto` | Scrollbar hanya jika perlu |
| `clip` | Seperti hidden tanpa bisa di-scroll |

Property: `overflow`, `overflow-x`, `overflow-y`.

```css
.kotak { width: 150px; height: 60px; border: 1px solid; }
.h { overflow: hidden; }
.a { overflow: auto; }
```

**Output:**

```text
.h:                       .a:
┌────────────────┐        ┌────────────────┐▲
│Teks panjang    │        │Teks panjang    │█
│sekali yang ... │        │sekali yang ... │▼
└────────────────┘        └────────────────┘
(sisa teks terpotong)     (ada scrollbar untuk melihat sisanya)
```

## 4.3 Display

| Value | Perilaku |
|-------|----------|
| `block` | Mengambil satu baris penuh, bisa diatur width/height |
| `inline` | Sebaris dengan teks, width/height diabaikan |
| `inline-block` | Sebaris, tetapi width/height berlaku |
| `none` | Elemen **hilang** dan tidak memakan ruang |
| `flex` / `inline-flex` | Flexbox (Bagian 5) |
| `grid` / `inline-grid` | Grid (Bagian 5) |
| `table`, `table-cell`, `table-row` | Perilaku tabel |
| `contents` | Elemen "dilebur", anaknya naik ke induk |
| `list-item` | Berperilaku seperti `<li>` |
| `flow-root` | Membuat konteks block baru |

```html
<span class="i">A</span><span class="i">B</span><span class="i">C</span>
<div class="b">D</div><div class="b">E</div>
<span class="ib">F</span><span class="ib">G</span>
```

```css
.i  { display: inline;       background: pink; width: 100px; }       /* width diabaikan */
.b  { display: block;        background: lightblue; }
.ib { display: inline-block; background: lightgreen; width: 100px; padding: 10px; }
```

**Output:**

```text
ABC                                 ← sebaris, lebar sesuai isi
┌──────────────────────────────┐
│ D                            │   ← block: memenuhi lebar
└──────────────────────────────┘
┌──────────────────────────────┐
│ E                            │
└──────────────────────────────┘
┌────────┐┌────────┐
│   F    ││   G    │              ← inline-block: sebaris tapi bisa diatur ukuran
└────────┘└────────┘
```

### display: none vs visibility: hidden

```css
.a { display: none; }
.b { visibility: hidden; }
```
```html
<p>Satu</p><p class="a">Dua</p><p>Tiga</p>
<p>Empat</p><p class="b">Lima</p><p>Enam</p>
```

**Output:**

```text
Satu
Tiga           ← "Dua" hilang dan tempatnya ikut hilang

Empat
               ← "Lima" tak terlihat tapi tempatnya TETAP ada (kosong)
Enam
```

`visibility` : `visible`, `hidden`, `collapse`.

## 4.4 Position

| Value | Perilaku |
|-------|----------|
| `static` (default) | Posisi normal, `top/left/...` diabaikan |
| `relative` | Digeser relatif dari posisi normalnya (ruang asli tetap) |
| `absolute` | Dikeluarkan dari alur, posisi relatif ke induk terdekat yang `position`-nya bukan static |
| `fixed` | Menempel ke layar (viewport), tidak ikut scroll |
| `sticky` | Normal dulu, lalu "menempel" saat di-scroll sampai batas tertentu |

Property pendukung: `top`, `right`, `bottom`, `left`, `inset` (shorthand 4 sisi), `z-index`.

### a) relative

```css
.kotak { position: relative; top: 20px; left: 30px; background: orange; }
```

**Output:**

```text
Posisi normal:      Hasil:
[ kotak ]                 (bergeser 20px turun, 30px ke kanan)
                       [ kotak ]
```

### b) absolute

```html
<div class="induk">
  <div class="anak">Anak</div>
</div>
```
```css
.induk { position: relative; width: 300px; height: 150px; background: #ddd; }
.anak  { position: absolute; top: 10px; right: 10px; background: crimson; color: white; padding: 5px; }
```

**Output:**

```text
┌──────────────────────────────┐
│                   ┌────────┐ │
│                   │  Anak  │ │  ← menempel 10px dari kanan-atas induk
│                   └────────┘ │
│                              │
└──────────────────────────────┘
```

Menengahkan dengan absolute:

```css
.tengah { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); }
/* atau: position:absolute; inset:0; margin:auto; (dengan width/height) */
```

**Output:**

```text
┌──────────────────────────────┐
│                              │
│          ┌────────┐          │
│          │ Tengah │          │  ← tepat di tengah induk
│          └────────┘          │
│                              │
└──────────────────────────────┘
```

### c) fixed

```css
.tombol-atas { position: fixed; bottom: 20px; right: 20px; }
```

**Output:**

```text
(Saat halaman di-scroll)
                                   ┌────┐
                                   │ ↑  │  ← tetap di pojok kanan-bawah layar
                                   └────┘
```

### d) sticky

```css
header { position: sticky; top: 0; background: white; }
```

**Output:**

```text
Saat di-scroll ke bawah, <header> ikut naik
lalu "menempel" di bagian paling atas layar dan tidak hilang.
```

### e) z-index (urutan tumpukan)
Hanya bekerja pada elemen yang `position`-nya bukan `static` (atau item flex/grid). Nilai lebih besar = di depan.

```css
.a { position: absolute; top: 0;    left: 0;    z-index: 1; background: red; }
.b { position: absolute; top: 20px; left: 20px; z-index: 2; background: blue; }
```

**Output:**

```text
┌──────────┐
│ A (merah)│
│   ┌──────────┐
│   │ B (biru) │  ← B menutupi sebagian A karena z-index lebih besar
└───│          │
    └──────────┘
```

## 4.5 Float & Clear

| Property | Value | Fungsi |
|----------|-------|--------|
| `float` | `left`, `right`, `none` | Mengambang ke kiri/kanan, teks mengalir di sampingnya |
| `clear` | `left`, `right`, `both`, `none` | Mencegah elemen berada di samping float |

```css
img { float: left; width: 80px; margin: 0 10px 10px 0; }
```

**Output:**

```text
┌──────┐ Teks paragraf mengalir di sisi
│ GBR  │ kanan gambar sampai teks lebih
└──────┘ panjang dari gambar, lalu teks
kembali memenuhi lebar penuh di bawahnya.
```

Membersihkan float (clearfix):

```css
.clearfix::after { content: ""; display: block; clear: both; }
```

**Output:**

```text
Induk kembali membungkus anak-anaknya yang float (tinggi tidak "runtuh").
```

> Untuk layout, sekarang lebih dianjurkan memakai **Flexbox** dan **Grid** (Bagian 5).

## 4.6 Gambar & Media

| Property | Value | Fungsi |
|----------|-------|--------|
| `object-fit` | `fill`, `contain`, `cover`, `none`, `scale-down` | Cara gambar/video mengisi kotaknya |
| `object-position` | `center`, `top`, `20% 80%` | Posisi isi gambar |
| `aspect-ratio` | `16 / 9`, `1 / 1`, `4 / 3` | Rasio lebar : tinggi |

```css
img {
  width: 200px;
  height: 200px;
  object-fit: cover;
}
.video { width: 100%; aspect-ratio: 16 / 9; }
```

**Output:**

```text
┌────────────┐
│ foto       │  ← foto memenuhi kotak 200x200, bagian lebih dipotong (tidak gepeng)
│ terpotong  │
└────────────┘
Kotak video selalu berbanding 16:9, berapa pun lebarnya.
```

Gambar responsif:

```css
img { max-width: 100%; height: auto; display: block; }
```

**Output:**

```text
Gambar mengecil mengikuti lebar induk, tidak pernah keluar kotak.
```

## 4.7 Tabel

| Property | Value | Fungsi |
|----------|-------|--------|
| `border-collapse` | `collapse`, `separate` | Gabung/pisah border sel |
| `border-spacing` | `0`, `5px` | Jarak antar sel (jika separate) |
| `caption-side` | `top`, `bottom` | Posisi judul tabel |
| `empty-cells` | `show`, `hide` | Tampilkan sel kosong |
| `table-layout` | `auto`, `fixed` | Algoritma lebar kolom |

```html
<table>
  <tr><th>Nama</th><th>Nilai</th></tr>
  <tr><td>Budi</td><td>90</td></tr>
  <tr><td>Ani</td><td>85</td></tr>
</table>
```
```css
table { border-collapse: collapse; width: 100%; }
th, td { border: 1px solid #999; padding: 8px; text-align: left; }
th { background: #333; color: white; }
tr:nth-child(even) { background: #f2f2f2; }
```

**Output:**

```text
┌──────────┬──────────┐
│ Nama     │ Nilai    │  ← header gelap, teks putih
├──────────┼──────────┤
│ Budi     │ 90       │
├──────────┼──────────┤
│ Ani      │ 85       │  ← baris genap abu-abu muda
└──────────┴──────────┘
```

## 4.8 Interaksi Pengguna

| Property | Value | Fungsi |
|----------|-------|--------|
| `pointer-events` | `auto`, `none` | `none`: elemen tidak bisa diklik/hover |
| `user-select` | `auto`, `none`, `text`, `all` | Mengatur apakah teks bisa diblok |
| `resize` | `none`, `both`, `horizontal`, `vertical` | Mengubah ukuran (textarea) |
| `appearance` | `none`, `auto` | Menghapus tampilan bawaan form |
| `caret-color` | warna | Warna kursor ketik |
| `accent-color` | warna | Warna checkbox/radio/range |
| `scroll-behavior` | `auto`, `smooth` | Scroll halus |

```css
.tak-bisa-diklik { pointer-events: none; opacity: .5; }
.tak-bisa-diblok { user-select: none; }
textarea { resize: vertical; }
input[type="checkbox"] { accent-color: tomato; }
input { caret-color: red; }
html { scroll-behavior: smooth; }
```

**Output:**

```text
Tombol dengan pointer-events:none → pudar & klik tidak bereaksi
Teks user-select:none             → tidak bisa diblok mouse
Textarea                          → hanya bisa di-resize ke atas-bawah
☑ (centang berwarna tomat)
Klik link anchor → halaman bergulir mulus, tidak melompat
```

## 4.9 Content & Counter

`content` dipakai bersama `::before` / `::after`.

```css
a[href^="http"]::after { content: " ↗"; }
blockquote::before { content: "“"; font-size: 2em; }
```

**Output:**

```text
Google ↗         ← panah otomatis ditambahkan di belakang tautan
“ Kutipan ...    ← tanda kutip besar di depan blockquote
```

Counter (penomoran otomatis):

```css
body { counter-reset: bab; }
h2::before { counter-increment: bab; content: "Bab " counter(bab) ". "; }
```
```html
<h2>Pendahuluan</h2><h2>Isi</h2><h2>Penutup</h2>
```

**Output:**

```text
Bab 1. Pendahuluan
Bab 2. Isi
Bab 3. Penutup
```

## 4.10 Contoh Gabungan Part 2: Kartu Profil

```html
<div class="kartu">
  <img class="foto" src="foto.jpg" alt="Foto">
  <h3>Roy</h3>
  <p>Student Developer</p>
  <button>Follow</button>
</div>
```

```css
.kartu {
  width: 220px;
  margin: 40px auto;
  padding: 20px;
  text-align: center;
  background: white;
  border: 1px solid #ddd;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0,0,0,.15);
}
.foto {
  width: 90px; height: 90px;
  border-radius: 50%;
  object-fit: cover;
}
button {
  padding: 8px 24px;
  border: none;
  border-radius: 999px;
  background: royalblue;
  color: white;
  cursor: pointer;
}
button:hover { background: navy; }
```

**Output:**

```text
        ╭────────────────────────╮
        │         ( ● )          │   ← foto bulat
        │          Roy           │
        │   Student Developer    │
        │      (  Follow  )      │   ← tombol kapsul biru
        ╰────────────────────────╯
          (bayangan lembut di bawah, kartu berada di tengah halaman)
```

---

# 5. Property CSS Part 3: Flexbox, Grid, Animasi, Responsive & Lanjutan

## 5.1 Flexbox

Flexbox mengatur tata letak **satu dimensi** (baris atau kolom). Aktifkan dengan `display: flex` pada **container**; anak langsungnya menjadi **flex item**.

### a) Property pada container

| Property | Fungsi | Value |
|----------|--------|-------|
| `display` | Mengaktifkan flex | `flex`, `inline-flex` |
| `flex-direction` | Arah sumbu utama | `row`, `row-reverse`, `column`, `column-reverse` |
| `flex-wrap` | Boleh turun baris | `nowrap`, `wrap`, `wrap-reverse` |
| `flex-flow` | Shorthand direction + wrap | `row wrap` |
| `justify-content` | Perataan di **sumbu utama** | `flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `space-evenly` |
| `align-items` | Perataan di **sumbu silang** | `stretch`, `flex-start`, `flex-end`, `center`, `baseline` |
| `align-content` | Perataan antar baris (saat wrap) | sama seperti justify-content, plus `stretch` |
| `gap`, `row-gap`, `column-gap` | Jarak antar item | `10px` |

```html
<div class="wadah">
  <div>1</div><div>2</div><div>3</div>
</div>
```

```css
.wadah { display: flex; gap: 10px; background: #eee; padding: 10px; }
.wadah div { background: royalblue; color: white; padding: 20px; }
```

**Output:**

```text
┌──────────────────────────────────┐
│ ┌────┐ ┌────┐ ┌────┐             │  ← item berjajar horizontal
│ │ 1  │ │ 2  │ │ 3  │             │
│ └────┘ └────┘ └────┘             │
└──────────────────────────────────┘
```

**flex-direction:**

```css
.wadah { flex-direction: column; }
```

**Output:**

```text
┌────────┐
│   1    │
├────────┤   ← item tersusun ke bawah
│   2    │
├────────┤
│   3    │
└────────┘
```

**justify-content:**

```css
.a { justify-content: flex-start; }
.b { justify-content: center; }
.c { justify-content: flex-end; }
.d { justify-content: space-between; }
.e { justify-content: space-around; }
.f { justify-content: space-evenly; }
```

**Output:**

```text
a: [1][2][3]·····················
b: ·········[1][2][3]·············
c: ·····················[1][2][3]
d: [1]··········[2]··········[3]
e: ··[1]····[2]····[3]··
f: ···[1]···[2]···[3]···
```

**align-items (container tinggi 100px):**

```css
.wadah { height: 100px; align-items: center; }
```

**Output:**

```text
┌──────────────────────────┐
│                          │
│  [1] [2] [3]             │  ← item di tengah secara vertikal
│                          │
└──────────────────────────┘
```

Menengahkan elemen di tengah halaman (horizontal + vertikal):

```css
.tengah { display: flex; justify-content: center; align-items: center; height: 100vh; }
```

**Output:**

```text
┌──────────────────────────┐
│                          │
│         [ Kotak ]        │  ← tepat di tengah layar
│                          │
└──────────────────────────┘
```

**flex-wrap:**

```css
.wadah { display: flex; flex-wrap: wrap; width: 250px; }
.wadah div { width: 100px; }
```

**Output:**

```text
[ 1 ][ 2 ]
[ 3 ]         ← item ke-3 turun ke baris baru karena tidak muat
```

### b) Property pada item

| Property | Fungsi | Value |
|----------|--------|-------|
| `flex-grow` | Kemampuan memanjang mengisi sisa ruang | `0`, `1`, `2` |
| `flex-shrink` | Kemampuan menyusut | `1`, `0` |
| `flex-basis` | Ukuran awal | `auto`, `200px`, `30%` |
| `flex` | Shorthand grow shrink basis | `1`, `1 1 0`, `0 0 200px` |
| `align-self` | Perataan sumbu silang khusus item | `auto`, `center`, `flex-end`, `stretch` |
| `order` | Urutan tampil | `-1`, `0`, `2` |

```css
.wadah { display: flex; }
.satu { flex: 1; }
.dua  { flex: 2; }
.tiga { width: 100px; }   /* tetap 100px */
```

**Output:**

```text
┌────────┬────────────────┬──────┐
│ satu   │      dua       │ tiga │
│ (1/3)  │     (2/3)      │ 100px│  ← sisa ruang dibagi 1 : 2
└────────┴────────────────┴──────┘
```

**order dan align-self:**

```css
.a { order: 2; }
.b { order: 1; align-self: flex-end; }
.c { order: 0; }
```

**Output:**

```text
Urutan HTML : A B C
Urutan tampil: C B A       ← berdasarkan nilai order
B juga menempel ke bagian bawah container (align-self: flex-end)
```

## 5.2 CSS Grid

Grid mengatur tata letak **dua dimensi** (baris dan kolom sekaligus).

### a) Property pada container

| Property | Fungsi | Contoh value |
|----------|--------|--------------|
| `display` | Mengaktifkan grid | `grid`, `inline-grid` |
| `grid-template-columns` | Definisi kolom | `200px 1fr 1fr`, `repeat(3, 1fr)`, `repeat(auto-fit, minmax(150px, 1fr))` |
| `grid-template-rows` | Definisi baris | `100px auto` |
| `grid-template-areas` | Pemetaan area bernama | `"header header" "side main"` |
| `gap` / `row-gap` / `column-gap` | Jarak antar sel | `10px` |
| `grid-auto-rows` / `grid-auto-columns` | Ukuran baris/kolom otomatis | `100px` |
| `grid-auto-flow` | Arah pengisian otomatis | `row`, `column`, `dense` |
| `justify-items` / `align-items` | Perataan isi sel | `start`, `center`, `end`, `stretch` |
| `justify-content` / `align-content` | Perataan seluruh grid | `start`, `center`, `space-between` |
| `place-items` / `place-content` | Shorthand align + justify | `center` |

```html
<div class="grid">
  <div>1</div><div>2</div><div>3</div>
  <div>4</div><div>5</div><div>6</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
.grid div { background: tomato; color: white; padding: 20px; text-align: center; }
```

**Output:**

```text
┌────────┐ ┌────────┐ ┌────────┐
│   1    │ │   2    │ │   3    │
└────────┘ └────────┘ └────────┘
┌────────┐ ┌────────┐ ┌────────┐
│   4    │ │   5    │ │   6    │
└────────┘ └────────┘ └────────┘
(3 kolom sama lebar)
```

**Kolom campuran:**

```css
.grid { grid-template-columns: 200px 1fr 2fr; }
```

**Output:**

```text
┌───────┬──────────┬──────────────────┐
│ 200px │   1fr    │       2fr        │
└───────┴──────────┴──────────────────┘
```

**Grid responsif tanpa media query:**

```css
.grid { display: grid; gap: 16px; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); }
```

**Output:**

```text
Layar lebar : [ 1 ][ 2 ][ 3 ][ 4 ]
Layar sedang: [ 1 ][ 2 ][ 3 ]
              [ 4 ]
Layar sempit: [ 1 ][ 2 ]
              [ 3 ][ 4 ]       ← jumlah kolom menyesuaikan otomatis
```

### b) Property pada item

| Property | Fungsi | Contoh |
|----------|--------|--------|
| `grid-column` | Rentang kolom | `1 / 3`, `span 2` |
| `grid-row` | Rentang baris | `1 / 3`, `span 2` |
| `grid-area` | Nama area / shorthand | `header`, `1 / 1 / 2 / 3` |
| `justify-self` / `align-self` | Perataan satu item | `center` |
| `place-self` | Shorthand | `center` |

```css
.grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }
.lebar { grid-column: span 2; }
```
```html
<div class="grid"><div class="lebar">A</div><div>B</div><div>C</div><div>D</div><div>E</div></div>
```

**Output:**

```text
┌───────────────────┐ ┌────────┐
│         A         │ │   B    │   ← A memakai 2 kolom
└───────────────────┘ └────────┘
┌────────┐ ┌────────┐ ┌────────┐
│   C    │ │   D    │ │   E    │
└────────┘ └────────┘ └────────┘
```

### c) grid-template-areas (layout halaman)

```html
<div class="halaman">
  <header>Header</header>
  <nav>Menu</nav>
  <main>Konten</main>
  <footer>Footer</footer>
</div>
```

```css
.halaman {
  display: grid;
  grid-template-columns: 150px 1fr;
  grid-template-areas:
    "header header"
    "menu   konten"
    "footer footer";
  gap: 8px;
}
header { grid-area: header; }
nav    { grid-area: menu; }
main   { grid-area: konten; }
footer { grid-area: footer; }
```

**Output:**

```text
┌────────────────────────────────┐
│             Header             │
├─────────┬──────────────────────┤
│  Menu   │       Konten         │
├─────────┴──────────────────────┤
│             Footer             │
└────────────────────────────────┘
```

### Flexbox vs Grid

| | Flexbox | Grid |
|-|---------|------|
| Dimensi | 1 dimensi (baris/kolom) | 2 dimensi (baris + kolom) |
| Cocok untuk | Navbar, tombol berjajar, perataan | Layout halaman, galeri, dashboard |

## 5.3 Transform

| Fungsi | Efek |
|--------|------|
| `translate(x, y)` / `translateX()` / `translateY()` | Menggeser |
| `rotate(45deg)` | Memutar |
| `scale(1.5)` / `scaleX()` / `scaleY()` | Memperbesar/memperkecil |
| `skew(20deg)` | Memiringkan |
| `matrix(...)` | Gabungan |
| `translate3d`, `rotateX/Y/Z`, `perspective()` | Efek 3D |

Property terkait: `transform`, `transform-origin` (titik pusat), `transform-style`, `perspective`, `backface-visibility`, serta properti individual `translate`, `rotate`, `scale`.

```css
.a { transform: rotate(15deg); }
.b { transform: scale(1.5); }
.c { transform: translate(50px, 20px); }
.d { transform: skew(20deg); }
.e { transform: rotate(45deg) scale(1.2); }   /* digabung */
```

**Output:**

```text
.a : kotak miring berputar 15° searah jarum jam
.b : kotak membesar 1,5x dari ukuran semula
.c : kotak bergeser 50px ke kanan, 20px ke bawah
.d : kotak menjadi jajar genjang  ╱▔▔▔╱
.e : kotak berputar 45° (menjadi berbentuk belah ketupat) dan 1,2x lebih besar
```

Efek 3D:

```css
.kartu { transform: perspective(500px) rotateY(30deg); }
```

**Output:**

```text
Kartu tampak berputar menghadap samping dengan efek kedalaman 3D
(sisi dekat lebih besar daripada sisi jauh).
```

## 5.4 Transition

Membuat perubahan nilai property terjadi **halus** (bukan mendadak).

| Property | Fungsi | Value |
|----------|--------|-------|
| `transition-property` | Property yang dianimasikan | `all`, `background`, `transform` |
| `transition-duration` | Lama | `0.3s`, `300ms` |
| `transition-timing-function` | Kurva kecepatan | `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`, `cubic-bezier(...)`, `steps(4)` |
| `transition-delay` | Jeda sebelum mulai | `0.2s` |
| `transition` | Shorthand | `all 0.3s ease` |

```css
.tombol {
  background: royalblue;
  color: white;
  padding: 10px 20px;
  transition: background 0.3s ease, transform 0.3s ease;
}
.tombol:hover {
  background: crimson;
  transform: translateY(-4px);
}
```

**Output:**

```text
Normal  : [ Tombol ]   ← biru
Hover   : [ Tombol ]   ← perlahan (0,3 detik) berubah merah dan naik 4px
Dilepas : kembali biru perlahan dan turun ke posisi semula
```

## 5.5 Animation & @keyframes

| Property | Fungsi | Value |
|----------|--------|-------|
| `animation-name` | Nama keyframes | `gerak` |
| `animation-duration` | Lama satu siklus | `2s` |
| `animation-timing-function` | Kurva kecepatan | `ease`, `linear`, ... |
| `animation-delay` | Jeda mulai | `1s` |
| `animation-iteration-count` | Jumlah ulang | `1`, `3`, `infinite` |
| `animation-direction` | Arah | `normal`, `reverse`, `alternate`, `alternate-reverse` |
| `animation-fill-mode` | Keadaan sebelum/sesudah | `none`, `forwards`, `backwards`, `both` |
| `animation-play-state` | Jalan/jeda | `running`, `paused` |
| `animation` | Shorthand | `gerak 2s ease infinite alternate` |

### a) Animasi bergerak (bouncing)

```css
@keyframes lompat {
  0%   { transform: translateY(0); }
  50%  { transform: translateY(-40px); }
  100% { transform: translateY(0); }
}
.bola {
  width: 50px; height: 50px;
  background: tomato;
  border-radius: 50%;
  animation: lompat 1s ease-in-out infinite;
}
```

**Output:**

```text
Frame 0%     Frame 50%    Frame 100%
                ( ● )
                                     ← bola naik-turun terus menerus
   ( ● )                    ( ● )
```

### b) Animasi muncul (fade in)

```css
@keyframes muncul {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
.kartu { animation: muncul 0.6s ease-out both; }
```

**Output:**

```text
Saat halaman dimuat: kartu awalnya transparan & agak di bawah,
lalu perlahan terlihat jelas dan naik ke posisi sebenarnya.
```

### c) Animasi berputar (loading spinner)

```css
@keyframes putar { to { transform: rotate(360deg); } }
.spinner {
  width: 40px; height: 40px;
  border: 5px solid #ddd;
  border-top-color: royalblue;
  border-radius: 50%;
  animation: putar 1s linear infinite;
}
```

**Output:**

```text
   ◜          ◝          ◞          ◟
  (lingkaran abu-abu dengan satu busur biru yang terus berputar)
```

## 5.6 Filter & Efek Visual

| Property | Fungsi |
|----------|--------|
| `filter` | Efek pada elemen: `blur()`, `brightness()`, `contrast()`, `grayscale()`, `sepia()`, `saturate()`, `hue-rotate()`, `invert()`, `opacity()`, `drop-shadow()` |
| `backdrop-filter` | Efek pada **latar di belakang** elemen (efek kaca/glassmorphism) |
| `mix-blend-mode` | Pencampuran warna elemen dengan latarnya |
| `clip-path` | Memotong bentuk elemen |
| `mask-image` | Menyamarkan bagian elemen |

```css
.a { filter: blur(4px); }
.b { filter: grayscale(100%); }
.c { filter: brightness(1.3) contrast(1.2); }
.d { filter: drop-shadow(4px 4px 6px black); }
.kaca { background: rgba(255,255,255,.2); backdrop-filter: blur(10px); }
```

**Output:**

```text
.a : gambar tampak buram
.b : gambar menjadi hitam-putih
.c : gambar lebih terang dan kontras
.d : bayangan mengikuti bentuk asli gambar (cocok untuk PNG transparan)
.kaca : panel semi transparan yang mengaburkan latar di belakangnya
```

**clip-path:**

```css
.segitiga { clip-path: polygon(50% 0, 0 100%, 100% 100%); background: orange; width: 100px; height: 100px; }
.lingkaran { clip-path: circle(50%); }
```

**Output:**

```text
.segitiga :     ▲
               ▲▲▲
              ▲▲▲▲▲      ← kotak dipotong berbentuk segitiga oranye
.lingkaran : kotak/gambar tampil berbentuk lingkaran
```

## 5.7 Variabel CSS (Custom Properties) & Fungsi

### a) Variabel CSS

Dibuat dengan awalan `--` dan dipakai dengan `var()`.

```css
:root {
  --warna-utama: royalblue;
  --jarak: 16px;
}
.tombol {
  background: var(--warna-utama);
  padding: var(--jarak);
  border: 2px solid var(--warna-border, black);   /* nilai cadangan */
}
```

**Output:**

```text
Tombol berlatar biru (royalblue), padding 16px, border hitam (nilai cadangan).
Mengubah --warna-utama di satu tempat → semua elemen yang memakainya ikut berubah.
```

Tema gelap dengan variabel:

```css
:root { --bg: white; --teks: black; }
[data-tema="gelap"] { --bg: #111; --teks: white; }
body { background: var(--bg); color: var(--teks); }
```

**Output:**

```text
Tema terang : latar putih, teks hitam
Tema gelap  : latar hitam pekat, teks putih (cukup ganti atribut data-tema)
```

### b) Fungsi matematika & lainnya

| Fungsi | Kegunaan | Contoh |
|--------|----------|--------|
| `calc()` | Hitungan | `calc(100% - 40px)` |
| `min()` | Nilai terkecil | `min(90%, 600px)` |
| `max()` | Nilai terbesar | `max(50%, 300px)` |
| `clamp(min, ideal, max)` | Dibatasi rentang | `clamp(1rem, 4vw, 2rem)` |
| `var()` | Memakai variabel | `var(--x)` |
| `attr()` | Mengambil nilai atribut HTML | `attr(data-label)` |
| `url()` | Alamat file | `url("a.png")` |
| `color-mix()` | Mencampur warna | `color-mix(in srgb, red, blue)` |

```css
.a { width: calc(100% - 40px); }
.b { width: min(90%, 600px); }
h1 { font-size: clamp(1.5rem, 5vw, 3rem); }
```

**Output:**

```text
.a : lebar = lebar induk dikurangi 40px
.b : 90% lebar induk, tapi tidak pernah lebih dari 600px
h1 : ukuran font menyesuaikan lebar layar, minimal 24px dan maksimal 48px
```

## 5.8 Responsive Design: Media Query

Media query menerapkan CSS **hanya jika kondisi terpenuhi**.

```css
@media (kondisi) {
  /* aturan CSS */
}
```

### a) Fitur media yang umum

| Fitur | Contoh |
|-------|--------|
| `min-width` / `max-width` | `(max-width: 768px)` |
| `orientation` | `(orientation: landscape)` |
| `prefers-color-scheme` | `(prefers-color-scheme: dark)` |
| `prefers-reduced-motion` | `(prefers-reduced-motion: reduce)` |
| `hover` | `(hover: hover)` |
| Tipe media | `print`, `screen` |
| Operator | `and`, `,` (atau), `not` |

### b) Meta viewport (wajib untuk responsive)

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### c) Contoh breakpoint umum

| Perangkat | Lebar |
|-----------|-------|
| Ponsel | ≤ 600px |
| Tablet | 601px – 992px |
| Laptop | 993px – 1200px |
| Desktop besar | > 1200px |

```css
.container { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }

@media (max-width: 992px) {
  .container { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 600px) {
  .container { grid-template-columns: 1fr; }
}
```

**Output:**

```text
Lebar > 992px :  [ 1 ][ 2 ][ 3 ]
                 [ 4 ][ 5 ][ 6 ]

Lebar ≤ 992px :  [ 1 ][ 2 ]
                 [ 3 ][ 4 ]
                 [ 5 ][ 6 ]

Lebar ≤ 600px :  [ 1 ]
                 [ 2 ]
                 [ 3 ] ... (satu kolom)
```

### d) Mobile-first (disarankan)
Tulis gaya dasar untuk ponsel, lalu tambahkan untuk layar yang lebih besar.

```css
.menu { display: none; }                       /* ponsel: disembunyikan */
@media (min-width: 768px) {
  .menu { display: flex; gap: 20px; }          /* layar besar: tampil */
}
```

**Output:**

```text
Ponsel     : menu tidak terlihat
≥ 768px    : [ Beranda ] [ Tentang ] [ Kontak ]
```

### e) Dark mode, reduced motion, print

```css
@media (prefers-color-scheme: dark) {
  body { background: #121212; color: #eee; }
}
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !important; }
}
@media print {
  nav, footer { display: none; }
}
```

**Output:**

```text
Perangkat mode gelap     → halaman otomatis berlatar gelap
Pengguna kurangi animasi → semua animasi dimatikan
Dicetak (print)          → menu dan footer tidak ikut tercetak
```

## 5.9 At-rule Lainnya

| At-rule | Fungsi |
|---------|--------|
| `@import` | Mengimpor CSS lain |
| `@font-face` | Mendefinisikan font kustom |
| `@keyframes` | Mendefinisikan animasi |
| `@media` | Media query |
| `@supports` | Memeriksa dukungan fitur browser |
| `@container` | Container query |
| `@layer` | Mengatur lapisan cascade |
| `@property` | Mendaftarkan custom property bertipe |
| `@charset` | Encoding file CSS |

### a) @supports

```css
.galeri { display: flex; flex-wrap: wrap; }
@supports (display: grid) {
  .galeri { display: grid; grid-template-columns: repeat(3, 1fr); }
}
```

**Output:**

```text
Browser mendukung grid → galeri memakai grid 3 kolom.
Browser lama           → tetap memakai flex-wrap.
```

### b) Container Query
Responsive berdasarkan ukuran **container**, bukan ukuran layar.

```css
.sisi { container-type: inline-size; }
@container (min-width: 400px) {
  .kartu { display: flex; }
}
```

**Output:**

```text
Container sempit (< 400px) : kartu bertumpuk vertikal
Container lebar (≥ 400px)  : kartu berubah menjadi susunan horizontal
(berlaku walau layar sama, tergantung lebar wadahnya)
```

### c) @layer

```css
@layer reset, dasar, komponen;

@layer reset    { a { color: black; } }
@layer komponen { a { color: red; } }
```

**Output:**

```text
Tautan berwarna MERAH, karena layer "komponen" dideklarasikan
setelah "reset" sehingga prioritasnya lebih tinggi
(terlepas dari specificity).
```

## 5.10 Scroll & Snap

| Property | Fungsi | Value |
|----------|--------|-------|
| `scroll-behavior` | Scroll halus | `smooth` |
| `scroll-snap-type` | Aktifkan snap di container | `x mandatory`, `y proximity` |
| `scroll-snap-align` | Titik snap tiap item | `start`, `center`, `end` |
| `scroll-margin` / `scroll-padding` | Offset snap/anchor | `80px` |
| `overscroll-behavior` | Perilaku di ujung scroll | `contain`, `none` |
| `position: sticky` | Menempel saat scroll | — |

```css
.slider { display: flex; overflow-x: auto; scroll-snap-type: x mandatory; }
.slider img { flex: 0 0 100%; scroll-snap-align: center; }
```

**Output:**

```text
Geser kiri-kanan → gambar "berhenti" pas di tengah satu per satu
seperti carousel.   [ img1 ] → [ img2 ] → [ img3 ]
```

## 5.11 Property Lain yang Sering Dipakai

| Property | Fungsi | Contoh |
|----------|--------|--------|
| `all` | Reset semua property | `all: unset` |
| `isolation` | Konteks tumpukan baru | `isolate` |
| `will-change` | Petunjuk optimasi | `transform` |
| `contain` | Isolasi render | `layout paint` |
| `content-visibility` | Tunda render yang tak terlihat | `auto` |
| `columns` / `column-count` / `column-gap` / `column-rule` | Teks berkolom | `3` |
| `shape-outside` | Teks mengalir mengikuti bentuk float | `circle(50%)` |
| `text-orientation` | Orientasi huruf vertikal | `upright` |
| `quotes` | Gaya tanda kutip | `"«" "»"` |
| `inset` | Shorthand top/right/bottom/left | `0` |
| `place-items` | Shorthand perataan grid | `center` |
| `scrollbar-width` / `scrollbar-color` | Gaya scrollbar | `thin` |
| `aspect-ratio` | Rasio ukuran | `1 / 1` |
| `object-fit` | Penyesuaian gambar | `cover` |

### Teks berkolom (multi-column)

```css
.artikel { column-count: 3; column-gap: 30px; column-rule: 1px solid #ccc; }
```

**Output:**

```text
Lorem ipsum dolor │ consectetur adip │ sed do eiusmod
sit amet, ...     │ iscing elit, ... │ tempor ...
```

### Scrollbar kustom

```css
.kotak { overflow: auto; scrollbar-width: thin; scrollbar-color: royalblue #eee; }
```

**Output:**

```text
Scrollbar menjadi tipis dengan "jempol" biru dan jalur abu-abu muda.
```

## 5.12 Contoh Gabungan Part 3: Landing Page Mini

```html
<header class="nav">
  <h1 class="logo">Roy.dev</h1>
  <nav class="menu">
    <a href="#">Beranda</a><a href="#">Proyek</a><a href="#">Kontak</a>
  </nav>
</header>
<section class="grid">
  <article class="kartu">Proyek 1</article>
  <article class="kartu">Proyek 2</article>
  <article class="kartu">Proyek 3</article>
</section>
```

```css
:root { --utama: royalblue; --gelap: #111; }
* { box-sizing: border-box; margin: 0; }
body { font-family: system-ui, sans-serif; }

.nav {
  display: flex; justify-content: space-between; align-items: center;
  padding: 16px 24px; background: var(--gelap); color: white;
  position: sticky; top: 0;
}
.menu { display: flex; gap: 20px; }
.menu a { color: white; text-decoration: none; transition: color .3s; }
.menu a:hover { color: var(--utama); }

.grid {
  display: grid; gap: 16px; padding: 24px;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
}
.kartu {
  padding: 40px 20px; text-align: center;
  background: white; border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,.15);
  transition: transform .3s;
}
.kartu:hover { transform: translateY(-6px); }

@media (max-width: 500px) {
  .nav { flex-direction: column; gap: 10px; }
}
```

**Output (layar lebar):**

```text
┌──────────────────────────────────────────────┐
│ Roy.dev            Beranda  Proyek  Kontak   │  ← navbar gelap, menempel di atas
└──────────────────────────────────────────────┘
  ╭──────────╮  ╭──────────╮  ╭──────────╮
  │ Proyek 1 │  │ Proyek 2 │  │ Proyek 3 │       ← kartu putih bersudut bulat
  ╰──────────╯  ╰──────────╯  ╰──────────╯          (naik 6px saat di-hover)
```

**Output (layar ≤ 500px):**

```text
┌──────────────────┐
│     Roy.dev      │
│ Beranda Proyek   │  ← logo dan menu bertumpuk
│      Kontak      │
└──────────────────┘
  ╭──────────────╮
  │   Proyek 1   │
  ╰──────────────╯
  ╭──────────────╮
  │   Proyek 2   │   ← kartu otomatis menjadi 1 kolom
  ╰──────────────╯
```

---

# 🎯 Penutup & Tips Belajar CSS

**Urutan belajar yang disarankan:**

1. Pahami **Box Model** dan **Selector** terlebih dahulu.
2. Kuasai **Display**, **Position**, lalu **Flexbox** dan **Grid**.
3. Pelajari **Responsive Design** (media query, satuan relatif).
4. Tambahkan **Transition**, **Animation**, dan **Variabel CSS**.
5. Latihan membuat ulang tampilan website nyata (navbar, kartu, form, landing page).

**Kebiasaan baik:**

- Pakai `box-sizing: border-box` untuk semua elemen.
- Gunakan class, hindari terlalu banyak ID dan `!important`.
- Beri nama class yang jelas (misalnya metode BEM: `.kartu__judul--besar`).
- Gunakan satuan relatif (`rem`, `%`, `fr`) agar responsif.
- Gunakan DevTools browser (klik kanan → Inspect) untuk melihat dan menguji CSS langsung.

**Referensi:** [MDN Web Docs – CSS](https://developer.mozilla.org/id/docs/Web/CSS) · [CSS-Tricks](https://css-tricks.com) · [Can I use](https://caniuse.com)

*Selamat belajar! 🚀*


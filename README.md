# OSCR Works — Kantor Digital 3D

Kantor digital 1 lantai dalam 1 file HTML. Buka file-nya, kantornya langsung hidup:
karyawan jalan, ngobrol, ke pantry, ke halaman, main sama kucing, cuaca berubah,
jam dan cahaya ikut jam perangkat yang buka halaman.

Demo-nya adalah kantor OSCR Works (Bedah Keuangan, Jejak Kuasa, Rancang Undangan,
BaruTauAda). Silakan fork dan ganti jadi kantor kamu sendiri.

## Fitur

- View 3D paling atas, tombol di bawah view, musik di bawah tombol, kotak info paling bawah
- Header clean dan minimal
- 14 karakter: Director + Manager + 12 karyawan, masing-masing punya meja, label
  3 baris (nama panggilan / role / segmen), dan profil lengkap saat diklik
- Tombol Ganti Orang: siklus 1 klik ke semua karyawan, kamera ikut orangnya kalau dia jalan
- Tombol arah 360 derajat: putar kiri/kanan 15 derajat per tap, kamera naik/turun,
  drag di layar juga bisa putar, plus Putar 360 Otomatis yang pelan (1 putaran 30 detik)
- Cuaca berubah otomatis (cerah / mendung / hujan) + tombol ganti manual
- Jam dan cahaya ikut jam perangkat: pagi, siang, sore, senja, malam
- Musik via widget SoundCloud (stream, bukan file ditempel) + suara kantor:
  ketikan, obrolan Indonesia tipis (TTS id-ID), murmur, dengung, printer sesekali
- Layout lega ala desainer interior: sirkulasi tengah bebas, zona kerja utara,
  lounge meeting timur berkarpet + TV dinding, meja perimeter selatan

## Cara pakai (paling gampang)

1. Download / clone repo ini
2. Buka `index.html` di browser (Chrome / Edge)
3. Butuh internet sekali saat dibuka: library 3D Three.js di-load dari CDN,
   dan musik di-stream dari SoundCloud. Setelah itu tidak ada instalasi apa-apa.

## Tangga pindah sayap kiri + dinding lt 2 ditutup (v24, masih versi HP embedded)

- Tangga pindah dari tengah selatan (yang menghalangi pintu masuk dan
  view Keseluruhan) ke sayap kiri dekat Arsip: berjalan utara–selatan
  di x=-10 (lebar 2), dasar z=6, atas z=2, 12 anak tangga, bordes
  (-10,3.52,1.25), railing x=-11.05/-8.95. Plat lantai 2 dibagi ulang,
  lubang baru x -11.5..-8.5, z 2..6 (lubang lama tengah dihapus).
  Rute karakter lewat koridor z=6.5 di timur tangga (bukan lewat meja
  Made di (-10,7.5)), masuk lantai 2 lewat (-10,1,3.6). View Tangga
  baru kamera (-5,7,11) target (-10,1.8,4). Lantai 1 lain tidak digeser.
- Dinding depan lantai 2 yang jebol ditutup: akar masalahnya celah
  pintu x -1..1 di dinding depan eksterior kebawa sampai atap
  (0..7.2), padahal pintu cuma 0..2.6. Perbaikan: segmen dinding
  eksterior (0,5.4,9) 2×3.6 menutup celah lantai 2 saja (pintu tetap
  terbuka di bawahnya) + jendela pusat lantai 2 di (0,5.4) sehingga
  fasad depan lantai 2 jadi 7 jendela; segmen dinding depan rendah
  interior lantai 2 (0,3.9,9) 2×0.6 juga ditutup. Pintu, kanopi,
  papan nama tetap di bawah segmen baru.
  Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep + review diff), garis lurus waypoint masih bisa
  menyenggol sudut furnitur, pengecualian briefing dari lantai 2
  masih turun bertahap bukan lewat tangga.

## Lantai 2 kosong + tangga (v23, masih versi HP embedded)

- Lantai 1 tidak digeser sama sekali. Lantai 2: plat atas y=3.6
  dengan lubang tangga x −1.5..1.5, z 4..9, dinding meniru lantai 1,
  partisi rendah membagi 3 ruang kosong — Ekspansi 1 (barat), Ekspansi
  2 (tengah), Ekspansi 3 (timur), hanya karpet + label "Kosong, siap
  diisi segmen baru", tanpa meja kerja dan tanpa tim permanen.
- Tangga dalam di sirkulasi tengah selatan (x −1..1, z 4..8), 12 anak
  tangga naik 0.3/anak, railing + bordes, rute karakter lewat waypoint
  tangga dengan y bertahap (bukan teleport), masuk lantai 2 lewat sisi
  utara lubang. Waypoint lantai 1 yang dulu lewat x=0 digeser ke x=−2.5
  supaya tidak menembus tangga.
- Toggle: grup "Lantai:" (Lantai 1/2) + grup "Lantai 2:" (Ekspansi
  1/2/3, Tangga); ruangan lantai 1 / Ganti Orang / Keseluruhan otomatis
  lantai 1, tombol lantai 2 otomatis lantai 2. Eksterior Gedung Utuh
  jadi 2 lantai: dinding depan sampai 7.2, atap pyramidRoof baseY 7.2,
  jendela lantai 2 di y=5.4. Aktivitas lantai 2 probabilitas kecil
  (Oemar 3%, umum 4%), label "Di Lantai 2 (ekspansi)".
  Keterbatasan yang dicatat: belum diuji di browser (hanya node --check
  + grep), garis lurus antar waypoint masih bisa menyenggol sudut
  tangga, dan saat briefing karakter dari lantai 2 turun bertahap ke
  lantai 1 bukan lewat tangga.

## Kotak Segmen sendiri + label tombol maks 2 kata (v22, masih versi HP embedded)

- Tombol segmen (Bedah Keuangan, Jejak Kuasa, Rancang Undangan,
  BaruTauAda) dipindah keluar dari Tour Ruangan ke kotak sendiri
  "📂 Segmen:" di antara Tour dan Setting — jadi kalau segmen nambah
  (mis. lantai 2 / ekspansi), tinggal tambah tombol di kotak Segmen,
  tidak mencampur tombol ruangan lagi. Fungsi goView tiap segmen tidak
  berubah.
- Label tombol kontrol dipangkas maks 2 kata biar hemat space:
  Gedung Utuh (Luar) → Gedung Utuh, Refresh Status Sekarang →
  Refresh Status, Ganti Cuaca Manual → Ganti Cuaca, Coba Briefing
  Pagi/Penutup → Briefing Pagi/Penutup (fungsi tetap tombol tes
  briefing 60 detik), Test Suara Cowo/Cewe → Suara Cowo/Cewe.
  Teks chatbot ikut disesuaikan ke label baru. Label tab dan pertanyaan
  cepat chatbot tidak diubah (itu judul/pertanyaan, bukan tombol kontrol).

## Chatbot kantor tanpa AI, tanpa Muse (v20, masih versi HP embedded)

- Tombol 💬 Chat Kantor melayang di kanan bawah (dinaikkan, v21:
  tombol 88px + safe-area dari bawah, panel 160px + safe-area, supaya
  tidak nyempil ketutup bar bawah HP), panel chat 360px / 480px
  (HP: selebar layar minus margin), header Bot Kantor OSCR Works,
  tombol cepat: Apa itu OSCR Works? / Jam briefing? / Siapa timnya? /
  Cara pakai kantor? / Di mana toilet?
- Bot jawaban jadi (rule-based keyword, tanpa API, tanpa biaya, tanpa
  key): segmen BK/JK/RU/BTA, tim 14 orang, briefing 08:00/17:00, toilet
  timur pantry, pantry, tamu/sofa, parkir/driveway, bunga, sampah pilah,
  kotak surat, tetangga, stranger, musik/suara, gedung utuh, cara pakai,
  tab Dashboard/Report/Personel/KPI, jam/cuaca perangkat. Kalau di luar
  topik, bot jujur bilang cuma bisa jawab topik itu, tidak mengarang.
- Identitas jelas: bot ini resepsionis, bukan Lux dan bukan Muse,
  karyawan fiktif simulasi ditegaskan di jawaban tim dan di catatan panel.
  Script chatbot terpisah dari script 3D, jadi chat tetap jalan walau 3D
  gagal dimuat.

## Toilet vs pantry + karyawan ke toilet / sofa tamu (v19, masih versi HP embedded)

- Toilet nabrak meja pantry diperbaiki: penyebabnya meja bundar pantry
  lama di (10,-5) radius 1,2 menyentuh sudut toilet (10,5,-4,5). Meja
  digeser ke barat jadi (9,-5), stool jadi (9,-3,6), (7,8,-5), (9,-6,5)
  — jarak ke dinding toilet sekarang 0,3 ke atas, tidak nabrak lagi.
  View Toilet juga diperbaiki: kamera lama (7,4,1) melihat lewat dinding
  barat toilet, jadi yang kelihatan cuma kayu. Kamera baru (7,2,5,-2,8)
  melihat lurus lewat celah pintu barat toilet, jadi interior toilet
  kelihatan.
- Karyawan bisa dipantau masuk toilet dan duduk di sofa tamu: state baru
  toilet (durasi pendek 6–10 detik, masuk lewat celah pintu barat,
  keluar lewat pintu yang sama, titik di dalam toilet per orang) dan
  tamu (duduk di sofa Ruang Tamu (4,5/-5,5,-6,8), masuk lewat selatan
  tamu, menghadap meja kopi). Aktivitasnya kelihatan kalau klik karakter
  / Ganti Orang: "Ke toilet (timur pantry)" / "Duduk di sofa Ruang Tamu".
  Jalur keluar dari toilet/tamu juga lewat pintu, tidak nabrak dinding.

## Versi HP (v18) — Three.js embedded, tanpa CDN

- Penyebab gagal buka di HP: file lama ngandelin Three.js dari CDN di
  head + SoundCloud API di head — kalau dibuka lewat preview aplikasi
  (bukan browser beneran) atau jaringan HP lemot, script itu ke-block /
  kelamaan, halaman stuck / hijau doang.
- v18: Three.js 0.160.0 ditempel di dalam file (748 KB total, dari 94 KB),
  jadi 3D jalan tanpa CDN, bahkan tanpa internet. SoundCloud API tidak
  lagi di head, tapi di-load malas (lazy) pas tombol ▶ ditekan saja.
- Sentuhan HP: canvas 3D pakai touch-action:none (drag di area 3D jadi
  putar kamera, bukan scroll halaman), pixel ratio HP dibatasi 1,5
  supaya tidak berat.
- Cara buka di HP yang benar: jangan dari preview aplikasi — download
  file dulu, lalu buka dari Files dengan Chrome (Android) / Safari
  (iPhone). Musik SoundCloud tetap butuh internet, 3D-nya tidak.

## Atap presisi, jendela besar, pintu bagus, stranger (v17)

- Atap diperbaiki presisi: penyebab atap v16 aneh adalah kerucut 4 sisi
  yang di-scale x/z lalu di-rotasi 45° — hasilnya belah ketupat miring
  yang meluber jauh dari footprint. Sekarang atap pakai piramida
  custom: alas persegi tepat 26x18 untuk kantor (puncak tengah, tinggi
  5 dari y 3,6) dan 8x10 untuk tetangga — tidak meluber, tidak miring.
- Jendela besar sekeliling gedung (mode eksterior saja, supaya interior
  tetap transparan): depan 6 jendela (2,5x1,8, bingkai putih, kaca biru),
  belakang 4, samping kiri-kanan masing-masing 3 — besar dan berjarak,
  tidak sumpek. Pintu utama baru: kusen putih, pintu ganda kayu + kaca,
  gagang emas, anak tangga, kanopi merah + tiang, papan nama
  "OSCR Works" di atas pintu. Pintu lama disembunyikan di mode eksterior
  supaya tidak dobel.
- Stranger: 2 pejalan kaki di trotoar (timur di jalur utara trotoar,
  barat di jalur selatan, lewat terus loop), 1 orang naik sepeda di
  jalan (jalur utara jalan, arah timur, loop), 1 orang jalan sama anjing
  (anjing ikut di samping, ekor goyang). Stranger tanpa label dan tanpa
  detail klik, jadi tidak kecampur sama karyawan.

## 1 bunga dihapus, jalan keluar kendaraan, toilet pindah, gedung utuh (v16)

- Bed bunga tinggal 1 (16,8.5). Bed timur (21,8.5) dihapus, tempatnya
  jadi paving transisi / jalan keluar kendaraan: slab paving 3 lebar
  dari parkir aspal (z 6,5) sampai tepi jalan (z 13), di x 19,5–22,5,
  nyebrang trotoar (slab di atas trotoar, jadi seperti driveway).
  Kupu-kupu semua pindah ke bed yang tersisa.
- Toilet pindah dari depan dekat Meeting 2 (selatan-timur, x 10–13,
  z 6–9) ke timur pantry (x 10,5–13, z -4,5 s.d. -1,5), pintu barat
  menghadap pantry — jadi dari meja pantry ada jalan tembus ke toilet.
  Filing dan rak yang bentrok pindah ke dinding timur area bekas toilet
  lama (filing 12,4,7, rak 12,8), tanaman di dalam toilet baru dihapus.
  Area Meeting 2 selatan jadi jauh lebih luas, tidak ada lagi yang
  kerja dekat toilet. View Toilet dan detailnya ikut pindah.
- Gedung utuh vs interior: tombol baru "🏢 Gedung Utuh (Luar)" di Tour.
  Ditekan, dinding depan rendah disembunyikan, dinding depan penuh +
  dinding samping sampai 3,6 + atap piramida muncul, kamera zoom out ke
  (0,32,42) — kantor kelihatan utuh seperti gedung tetangga, dari luar.
  Tombol ruangan lain / "🏠 Keseluruhan" / Ganti Orang otomatis balik
  ke mode interior transparan seperti sekarang (atap hilang, dinding
  depan rendah balik).

## Paving dihapus, bunga pindah, kotak surat (v15)

- Paving masuk DIHAPUS — offside, karena jalan + trotoar sudah ada.
  Zebra di jalan tetap ada, yang dihapus cuma ubin paving dari pintu
  sampai selatan jalan.
- Bunga pindah ke rumput selatan parkiran: 2 bed di (16,8.5) dan
  (21,8.5), di antara parkir aspal (sampai z 6,5) dan trotoar (mulai
  z 10,4) — jadi tidak kena trotoar, tidak kena aspal parkir.
  Kupu-kupu ikut pindah ke bed baru.
- Kotak surat di dekat trotoar pintu masuk: barat pintu (-2,5,10,2),
  utara trotoar (jadi dekat trotoar tapi tidak di atasnya), badan biru,
  tutup merah, bendera merah, label "Surat".
- Bonus kerapian: titik jalan karakter di halaman pindah dari jalan /
  trotoar (z 12–14) ke rumput depan kantor (z 9,5–9,8), jadi tidak ada
  karakter yang berdiri di jalan.

## Briefing, suara cowo/cewe, luar kantor, Next/Prev musik (v14)

- Briefing: 08:00 briefing pagi oleh Oemar, 17:00 briefing penutup oleh Lux
  (17:00 = jam 5 sore, dikonfirmasi Oemar — bukan 05:00 pagi). Saat jam itu
  tiba (jam perangkat yang buka halaman), semua berkumpul di Meeting 2
  lounge timur, pemimpin di depan (9,2.6), yang lain menghadap ke depan,
  banner briefing muncul di atas tab, dan pemimpin berbicara via TTS
  (dijelaskan di banner: bukan suara asli Oemar). Briefing 15 menit
  (08:00–08:15, 17:00–17:15), setelah itu semua balik ke meja. Tombol
  "Coba Briefing Pagi / Penutup" di Setting untuk tes 60 detik tanpa
  nunggu jamnya.
- Suara ngobrol: obrolan sekarang bergantian cowo/cewe — pitch cowo rendah
  (0,7–0,85), cewe tinggi (1,25–1,45), plus pilihan voice Indonesia kalau
  perangkat punya voice berlabel gender; kalau perangkat cuma punya satu
  voice Indonesia, pembedanya tetap pitch. Ditambah frasa becanda
  ("haha", "wkwk") dan ketawa audio berkala (~20–45 detik) saat Suara
  Kantor nyala. Tombol "Test Suara Cowo / Cewe" di panel musik untuk cek
  langsung.
- Luar kantor: trotoar di depan kantor + jalan aspal dengan garis putus
  dan zebra cross, parkir lantainya aspal (bukan paving kotak lagi) dengan
  garis parkir putih, 3 tong sampah pilah di trotoar timur pintu masuk
  (Organik hijau, Plastik kuning, Kertas biru, pakai label), 3 sepeda
  motor + 3 sepeda (2 di parkir, 1 sepeda di trotoar), tetangga kiri
  (krem, atap merah) dan kanan (biru muda, atap abu, di timur parkir)
  berupa bangunan utuh: dinding, jendela 2 lantai, pintu, sampai atap
  piramida — bisa, bukan cuma fasad.
- Musik Next/Prev: tombol ⏮ Prev dan Next ⏭ di panel musik, pakai
  SoundCloud Widget API. Tekan ▶ dulu, baru Prev/Next jalan; judul lagu
  yang sedang main tampil di status musik. Pause sekarang pakai
  widget.pause (playlist tidak ke-reset, player tetap tampil).
- Area kosong: TIDAK diisi lagi (koreksi Oemar 16:40) — area itu memang
  tempat player SoundCloud muncul saat musik di-play, jadi saat di-play
  dia full sendiri.

## Filter personel/KPI + musik di kolom kiri (v13)

- Tab Personel dan tab KPI punya filter: Semua, Management, Bedah Keuangan,
  Jejak Kuasa, Rancang Undangan, BaruTauAda. Daftar nama berubah sesuai filter.
- KPI dibuat per orang dulu, per role, bukan generik: misalnya Nadia pakai
  naskah + hook, Rizky pakai posting + komen dibalas, Yusuf pakai order +
  chat dibalas cepat, Lina pakai posting 5 platform, dan seterusnya.
  Angka KPI di demo ini CONTOH, target resmi belum ditetapkan.
- Panel Musik / Suara Kantor pindah ke kolom kiri, di bawah Setting Kondisi,
  supaya tidak ada area kosong di antara tombol dan musik. Kolom kiri
  (Tour + Setting + Musik) dan kolom Kamera kanan sekarang tingginya
  hampir sama, tidak ada space besar yang menganggur.

## Tab bawah + kolom kamera (v12)

- Tombol arah (kiri, kanan, naik, turun, 360 otomatis, zoom in/out) ada di
  kolom Kamera tersendiri di kanan tombol, tidak nyampur dengan tombol tour.
- Kolom paling bawah sekarang pakai tab, bukan 1 panel panjang:
  - **Dashboard:** pilih segmen + filter socmed (Semua, Instagram, TikTok,
    Threads, X, Facebook), angka dashboard berubah sesuai pilihan, plus
    Ongoing Task per segmen. Angka dashboard di demo ini CONTOH / ILUSTRASI,
    belum tersambung API socmed — ganti angka di `dashboardData` dengan data asli.
  - **Report:** filter Harian / Mingguan / Bulanan, isi report berubah sesuai periode.
  - **Personel & Aktivitas:** daftar 14 orang, klik nama atau karakter di kantor
    untuk lihat profil + aktivitasnya saat itu.
  - **KPI Personel:** pilih orang, lihat target, selesai, progress, dan tepat waktu.
    Angka KPI di demo ini CONTOH, target belum ditetapkan — ganti di `kpiData`.

## Status live via fetch (v9, tanpa reload, tanpa token)

Status 4 segmen (BK, JK, RU, BTA) tidak lagi nempel mati di `index.html` —
statusnya ada di `status.json`. Halaman nge-fetch file itu tiap 5 menit
(`cache: no-store`, ditambah timestamp biar tidak kena cache browser lama),
lalu panel segmen di-update di tempat, tanpa reload halaman, tanpa reset
scene 3D, tanpa token AI, tanpa token auth (file JSON-nya publik, sama
kayak HTML-nya).

- Update status = edit `status.json` saja (ganti `updatedAt` + `body` segmen
  yang berubah), commit, push, Vercel auto-deploy
- Pengunjung yang sudah buka dari tadi akan ke-update sendiri dalam
  maksimal 5 menit, tanpa tekan F5
- Tombol "Refresh Status Sekarang" di halaman = fetch manual sekarang juga
- Kalau dibuka sebagai file lokal (bukan lewat server/Vercel), fetch akan
  gagal karena aturan file lokal — halaman otomatis pakai data bawaan
  di dalam `index.html`, jadi tetap jalan, cuma tidak live sampai di-deploy

## Cara custom jadi kantor kamu

Semua ada di dalam `index.html`, cari bagian ini:

- `SOUNDCLOUD_URL` — ganti dengan link playlist SoundCloud kamu sendiri
- Daftar `persons` dan pemanggilan `chibi(...)` — ganti nama, panggilan, role,
  segmen, warna outfit, gaya rambut, dan posisi meja karyawan kamu
- Objek `data` — ganti profil dan status tiap segmen / ruangan
- `monitorDesk(x, z)` — pindah / tambah meja, koordinatnya x (kiri-kanan) dan
  z (utara-selatan, makin besar makin ke selatan / depan)

Tidak perlu build tool, tidak perlu server. File ini statis.

## Deploy ke Vercel (gratis, Hobby)

1. Push repo ini ke GitHub (public kalau mau open source)
2. Di Vercel: New Project → Import repo ini → Framework: Other / Static
3. Tidak perlu build command, tidak perlu output directory khusus
4. Deploy, dapat link demo yang bisa dibagikan

Setiap update kantor = edit `index.html`, commit, Vercel auto-deploy.

## Catatan penting (baca sebelum fork)

- 12 karyawan di demo ini adalah **karakter fiktif simulasi**, bukan karyawan
  beneran. Nama, umur, tempat/tanggal lahir, asal, suku, dan agama mereka
  dibuat sebagai contoh unity in diversity. Ganti dengan tim kamu sendiri.
- Playlist SoundCloud di demo adalah contoh publik. Ganti dengan playlist kamu.
- Status segmen di demo (misalnya reel yang sudah tayang) adalah status kantor
  OSCR Works saat file ini dibuat. Ganti dengan status usaha kamu sendiri.

## Lisensi

MIT — bebas pakai, ubah, dan bagikan, dengan tetap mencantumkan lisensi ini.
Lihat `LICENSE`.

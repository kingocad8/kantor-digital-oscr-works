# OSCR Works — Kantor Digital 3D

## Kustomisasi jadi kantor kamu (v37 — cara baru, cukup edit 1 file)

Mau pakai kantor ini untuk usaha kamu sendiri, tanpa minta ke Oemar/Lux?
**Baca `README-CUSTOMIZE.md`** — caranya: fork repo ini → edit `config.json`
langsung di web GitHub (nama kantor, album SoundCloud, deskripsi segmen,
angka Dashboard, daftar karyawan, jawaban chatbot) → commit → deploy fork
kamu ke Vercel (Hobby gratis, tanpa build command, tanpa env). Repo Oemar
tidak terganggu; link kamu sendiri yang berubah. Kalau `config.json` tidak
ada / rusak, situs tetap jalan dengan default OSCR (fallback) — tidak blank.

Isi v37 singkat (file `index.html` + `config.json` di repo ini sudah v37):

- `config.json` berisi default OSCR yang sama persis dengan data v36, jadi
  situs dengan config ini tampil identik dengan v36 — kecuali satu
  perubahan di bawah. Semua field config-driven: `officeName`,
  `soundcloudUrl`, segmen (nama/kode/emoji/deskripsi), Dashboard,
  karyawan (karakter 3D + profil klik + KPI + filter + chatbot tim), dan
  jawaban bisnis chatbot. Yang tetap hardcoded: bentuk gedung, posisi
  perabot/ruang, layout tombol, cuaca/suara/kendaraan, logika 3D.
- **Koreksi atas bagian v36 di bawah:** span keterangan baris audio
  "Obrolan bergantian cowo/cewe + ketawa" kini **DIHAPUS TOTAL di v37**
  (perintah Oemar 30 Okt 2026 12:58 WIB). Yang tetap di baris audio:
  tombol Musik (Prev/Musik/Next), tombol Suara Kantor, slider volume,
  label Mati/Nyala. Logika obrolan ambience (bergantian cowo/cewe +
  ketawa) tetap jalan di balik layar, hanya teks keterangannya yang
  tidak lagi tampil. Chatbot boleh tetap menyebut obrolan bergantian
  (itu fakta perilaku, bukan tombol).
- Keterbatasan yang dicatat: belum diuji di browser sungguhan (hanya
  node --check + grep + smoke test logika di Node); config hanya terbukti
  saat di-deploy (Vercel) atau dibuka sebagai folder lengkap
  (`index.html` + `config.json` berdampingan) — dibuka sebagai lampiran
  file tunggal di penampil Muse, config tidak ikut terlayani sehingga
  tampil default OSCR (keterbatasan penampil, bukan bug config).

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

## v40 — BaruTauAda pindah lantai 2, lantai 1 dilonggarkan, klik TV di POV muter musik (mencakup v39)

- v39: matahari sisi timur lebih tinggi, pathfinding (tidak tembus tembok/perabot/TV), jalan melangkah, zoom-out + scroll mouse setelah klik-zoom, rapat grup lintas segmen + aktivitas pakai semua fitur, pintu toilet, TV lantai 2 dijauhkan dari sofa (2,8 m), kucing lantai 2 sebelahan + bisa jalan pindah lantai, rak buku lantai 2, mode POV (WASD/panah, plafon + lampu + kipas + AC, dinding/atap tidak tembus pandang).
- v40: segmen BaruTauAda (Intan, Yohan, Lina) pindah ke lantai 2 ruang timur (bekas Ekspansi 3); lantai 2 kini penuh: Ludo barat, Oki tengah, BaruTauAda timur. Meja lantai 1 diatur ulang per segmen jadi senggang (jarak antar meja minimal 1,4 m, koridor utama bersih, meja Lux geser ke tengah-timur) supaya mode POV bisa lewat dan Oemar tidak terjebak di depan ruang direktur. Klik TV di mode POV memutar/menjeda musik SoundCloud (album yang sama); klik TV di mode normal tetap seperti v39.
- Penting saat deploy v40: config.json HARUS ikut diperbarui bersama index.html, karena live site memuat config.json — bila hanya index.html yang naik, BaruTauAda akan balik ke lantai 1.

## Cuaca auto mati + suara tap-pertama + klik zoom + hover karyawan v38 (masih versi HP embedded — mencakup v28–v37)

- Laporan live v37 Oemar 30 Okt 13:20–13:23 WIB: karakter
  TETAP gerak dan kamera BISA digerakin (scene TIDAK freeze);
  yang bermasalah hanya kotak HUD di atas kanvas yang
  tulisannya ganti-ganti sendiri tanpa klik (13:23 Cuaca Salju
  lalu Hujan). Akar: weatherTimer di animate() mengganti cuaca
  acak tiap 45–65 detik (auto-random v31). Perbaikan: blok
  weatherTimer di animate() DIHAPUS TOTAL — cuaca sekarang
  hanya berubah lewat tombol Cuaca manual (urutan 7 jenis);
  applyTimeWeather via setInterval 30 detik tetap untuk periode
  waktu + jam; cuaca awal tetap cerah; label Fokus tetap hanya
  berubah lewat tombol (bukan lewat drag — drag yang tidak
  mengubah label itu normal, bukan freeze).
- Suara kantor auto-nyala di tap/klik pertama (listener once
  pointerdown + keydown, memanggil toggleAmbience bila ambOn
  mati, kecuali tap pertama di tombol Suara Kantor sendiri
  supaya tidak nyala-lalu-mati; tidak preventDefault, tidak
  blokir klik/drag). Bukan auto pas load (diblokir browser);
  musik SoundCloud tetap manual (tap ▶ Musik).
- Matahari/bulan/bintang masuk frame Keseluruhan desktop
  (perhitungan geometri, FOV 42°): matahari (8,6,-12) scale
  1,7 (Senja (10,5,-12) oranye scale 1,9, Panas Terik scale
  2,0), bulan Malam (-8,6,-12) scale 1,7, bintang Malam 150
  titik di strip langit utara x -18..18 / y 5,5..7,5 /
  z -15..-12 ukuran 0,35. Visibilitas tetap: matahari bila
  period ≠ Malam, bulan/bintang hanya Malam. Trade-off: di
  view Gedung Utuh (eksterior dari selatan) posisi utara
  rendah ini bisa tertutup gedung.
- Klik objek → auto zoom-in: karakter seperti nextPerson
  (focusPerson, orbitRadius 5,5); non-karakter ber-detail:
  orbitCenter = titik klik + 1,0 y, orbitRadius 7, focusLabel
  = title objek tanpa HTML; klik tanah kosong / tanpa detail:
  kamera diam; guard suppressClick drag > 5 px dipertahankan;
  Keseluruhan tetap reset view lebar.
- Judul baris Tour: gaya caption-top seperti Segmen/Setting,
  label "🗺️ Tour Kantor:" di atas tombol Tour (isi/urutan
  tombol tidak berubah).
- Hover lama karyawan: elemen #hoverTip (fixed,
  pointer-events none), tahan kursor ~700 ms di karyawan yang
  sama → popup nama + role + segmen + "Aktivitas saat ini:
  <stateLabel>" + "Jobdesk hari ini: <role> di <segment>"
  (dari role + segmen, TIDAK mengarang daftar tugas harian)
  + 2 metrik KPI; hilang saat kursor geser menjauh / pindah
  karyawan / mulai drag / pointerleave / pointerdown;
  raycast hover throttle 100 ms di pointermove, hanya mouse
  desktop (layar sentuh tetap dapat aktivitas dari panel
  detail setelah tap).
- TIDAK diubah: kecepatan jalan karakter (1,8 * dt), durasi
  aktivitas, drag/putar/zoom manual, orbitAuto, cuaca manual,
  periode waktu, layout HP + freeze, visibilitas lt, tombol
  v36, loader + fallback config.json v37.
- Keterbatasan yang dicatat: belum diuji di browser sungguhan
  (hanya node --check + grep + perhitungan geometri);
  suara tetap butuh satu tap pertama; matahari/bulan/bintang
  baru terbukti geometri untuk view Keseluruhan desktop.

## Hapus tombol dobel v36 (masih versi HP embedded — mencakup v28–v35)

- Tombol contoh Suara Cowo/Cewe DIHAPUS dari baris audio
  (beserta emoji 👨 👩 di depannya) — interpretasi atas chat
  Oemar "dibilangin" = "dihilangin", sesuai konteks
  penghapusan tombol. Yang tetap: tombol Musik (Prev/Musik/
  Next), tombol Suara Kantor, slider volume, label Mati/Nyala,
  dan span keterangan "Obrolan bergantian cowo/cewe + ketawa"
  (obrolan ambience tetap bergantian + ketawa); fungsi
  testVoice() dibiarkan sebagai dead code (tidak dirujuk HTML);
  jawaban chatbot tentang tombol Suara Cowo/Cewe diperbarui
  (kalimat "Ada tombol Suara Cowo / Cewe buat cek langsung."
  dihapus).
- Tombol ruangan segmen baru di baris Tour DIHAPUS, biar tidak
  dobel dengan Segmen: hanya 🟦1 (Ludo) dan 🟩2 (Oki) yang
  dihapus dari Tour (Tour kini 15 tombol, dari 17). Yang tetap:
  semua tombol Tour lain + 🟧3 Ekspansi 3 (bukan segmen) +
  🪜 Tangga; tombol Segmen 🎲 LB dan 🤖 Oki tetap sebagai
  jalan masuk ke ruangan Ludo/Oki; views, goView, label
  ruangan, dan isi ruangan tidak diubah.
- SoundCloud TIDAK diubah (tetap album Hindia) — pertanyaan
  ganti album dijawab terpisah, bukan di build ini.
- Keterbatasan yang dicatat: belum diuji di browser sungguhan
  (hanya node --check + grep); ruangan Ludo/Oki tetap dibuka
  lewat tombol Segmen.

## Orang lt2 hilang saat pilih lt1 + freeze PC/browser v35 (masih versi HP embedded — mencakup v28–v34)

- Akar melayang: setFloorVisibility() hanya mengatur
  floor2Group.visible, sedangkan karakter dibuat scene.add(g)
  (anak scene langsung, y=0 lt1 / 3.6 lt2) — saat lt1 dipilih,
  plat lt2 hilang tapi 5 karakter lt2 tetap di y=3.6 melayang.
  Perbaikan: fungsi baru updateCharacterFloorVisibility()
  berdasarkan POSISI Y SAAT INI (bukan rumah): eksterior
  (Gedung Utuh) = semua karakter terlihat; bukan eksterior +
  activeFloor 1 = terlihat hanya bila y <= 1.8; activeFloor 2 =
  terlihat hanya bila y > 1.8; pengecualian focusPerson selalu
  terlihat; dipanggil di setFloorVisibility, setInterior,
  viewExterior, dan SETIAP FRAME animate(); karakter tetap
  scene.add, tidak dipindah ke floor2Group; posisi/rute/
  aktivitas tidak diubah; label kepala ikut tersembunyi karena
  label anak grup karakter.
- Freeze PC/browser: aturan dasar #scene diubah dari
  position:relative menjadi position:sticky top:0 z-index:50
  height:540px (desktop, kanvas tetap di bawah header saat
  pertama dibuka, menempel di atas saat scroll); mobile
  <=768px TETAP v34 (fixed top:0 left:8px right:8px +
  #sceneSpacer display:block tinggi sama, desktop spacer
  display:none); tinggi desktop tetap 540px, chatBtn/chatPanel
  tetap fixed z-index 999, canvas tetap touch-action:none.
- Keterbatasan yang dicatat: belum diuji di browser sungguhan
  (hanya node --check + grep); karakter di tengah tangga (y
  sekitar 1.8) bisa muncul/hilang sesaat saat lantai diganti di
  tengah pendakian (efek ambang, bukan melayang); freeze desktop
  memakai sticky — di browser PC sungguhan harusnya jalan, tapi
  di penampil file yang scroll-nya di container luar, sticky
  desktop bisa tetap tidak terpicu seperti kasus HP kemarin.

## Perbaikan freeze kanvas v34 atas laporan tes Oemar (masih versi HP embedded — mencakup v28–v33)

- Penyebab v33 tidak ke-freeze: aturan sticky v33 ADA dan
  bentuknya benar (position:sticky top:0 height:52vh di media
  768px, html,body overflow-x:clip) — kemungkinan sticky tidak
  terpicu di penampil file HP Oemar (scroll jalan di container
  luar penampil, bukan dokumen HTML) dan/atau sticky iOS Safari
  yang tidak konsisten. v34 tidak mengulang sticky.
- Di media 768px, #scene diganti position:fixed top:0 left:8px
  right:8px width:auto z-index:50 height:52vh min-height:320px
  max-height:480px (left/right 8px mengikuti padding .wrap
  mobile, supaya kanvas sejajar konten); desktop tetap
  position:relative.
- Spacer: div kosong <div id="sceneSpacer"></div> tepat setelah
  penutup #scene, di dalam .wrap, sebelum .btns — display:none
  di desktop, display:block + tinggi SAMA PERSIS dengan kanvas
  di media 768px, transparan tanpa border/background, tidak
  mengganggu klik; spacer menempati ruang asli kanvas saat
  pertama dibuka (tombol/tab/detail mulai di bawah kanvas,
  bukan tertutup), lalu ikut terscroll ke atas saat scroll,
  sedangkan kanvas fixed tetap menempel di atas layar.
- Tetap: layout HP wrap v33, kamera awal HP (radius 42, phi
  0.65), #sceneHud absolute di dalam #scene, chatBtn/chatPanel
  fixed z-index 999, canvas touch-action:none (drag = putar
  kamera, scroll lewat area bawah canvas), tidak ada listener
  resize baru.
- Keterbatasan yang dicatat: belum diuji di browser sungguhan
  (hanya node --check + grep); fixed + spacer lebih kuat dari
  sticky, tapi tetap perlu dinilai visual di HP Oemar — apakah
  kanvas benar-benar menempel saat scroll di penampil yang dia
  pakai, dan apakah tinggi 52vh terasa pas.

## Layout HP v33 atas screenshot tes Oemar (masih versi HP embedded — mencakup v28–v32)

- HP satu layar penuh, ke bawah, tanpa geser kanan: akar
  masalah `.btn-group.icon-row{flex-wrap:nowrap;overflow-x:auto}`
  (Tour 17 ikon memaksa geser horizontal) — media baru
  max-width:768px di akhir <style> (media 640px lama tetap):
  html,body overflow-x:clip (clip, bukan hidden, supaya sticky
  tetap jalan); .wrap max-width:100% padding:8px; icon-row +
  btn-group + tab-buttons flex-wrap:wrap + overflow-x:visible
  (Tour jadi 2–3 baris ke bawah); .btns/.btns-main column +
  stretch juga untuk HP besar 641–768px; .camera-col
  width:100% D-pad di tengah; #detail/.tab-content
  max-width:100% + wrap kata.
- Kanvas di-freeze (sticky) di atas saat scroll — mobile saja,
  desktop tidak berubah: #scene position:sticky top:0
  z-index:50 height:52vh min-height:320px max-height:480px;
  .wrap tidak diberi overflow:hidden; canvas tetap
  touch-action:none (drag di canvas = putar kamera, scroll
  halaman lewat area di bawah canvas); chatBtn/chatPanel tetap
  fixed (z-index 999, di atas canvas sticky).
- Kamera smartphone dinaikkan — hanya kamera awal, hanya layar
  sempit (innerWidth <= 768 saat load, sebelum animate()
  pertama, pakai mekanisme orbit yang sudah ada): orbitCenter
  (0,1.2,2), orbitRadius 42 (dari 30), orbitPhi 0.65 (dari 0.9,
  lebih tegak dari atas), orbitTheta 0 (dari depan/selatan),
  focusPerson=null, focusLabel 'Fokus: Keseluruhan', camPos/
  camLook disalin dari target supaya frame pertama sudah
  kamera HP; views.all desktop tetap [[0,24,28],[0,0,2]];
  tombol Tour tetap posisi kameranya masing-masing.
- Keterbatasan yang dicatat: belum diuji di browser sungguhan
  (hanya node --check + grep); tinggi sticky 52vh perlu dinilai
  di HP Oemar (terlalu banyak / terlalu pendek); drag canvas
  tetap putar kamera, scroll lewat area bawah canvas.

## Koreksi v32 atas screenshot + 3 pesan Oemar (masih versi HP embedded — mencakup v28–v31)

- Label kepala SATU BARIS: `label3` 3 baris diganti `label1`,
  format "Panggilan | JobSingkat | KodeSegmen" (contoh "Lux |
  Manager | OSCR", "Nadia | Content | BK"), canvas 256×48,
  font bold 20px auto-shrink sampai 14px bila teks lebih lebar
  dari 236 px (tidak terpotong), sprite 2.0×0.38, y=2.0.
  Job singkat hanya untuk label kepala (profil klik tetap peran
  lengkap). Kode: BK/JK/RU/BTA/LB/OKI, Oemar/Lux = OSCR.
- Kaki kursi TEBAL GELAP BERPALANG: kaki v31 (0,07, tekstur
  kayu, nyaris tak terlihat di HP) diganti 0,12×0,43×0,12 warna
  cokelat tua 0x5d3a1a di ±0,25 + palang penghubung y≈0,15
  (sisi 0,08×0,08×0,5 + depan/belakang 0,5×0,08×0,08), di
  `chair()` dan `f2chair()`; posisi/rotasi kursi tidak diubah.
- Meja meeting lt 2 berjejer di samping lounge: lama (0,3,0)
  dihapus → baru (4,0,7,0) timur lounge (karpet 0,7,0; sofa
  0,7,8; TV 0,6,2), satu baris z=7,0, 4 stool (timur 5,3;
  barat 2,7; selatan 4,0,8,3; utara 4,0,5,7); area tengah
  selatan (0,3,0) kembali kosong; target hangout lt 2
  diperbarui ke [[4,0,7,0],[0,7,0]] (meja + lounge baru).
- Kendaraan lewat di jalan raya: aspal x -40..40, trotoar
  z=11,5 tidak dilalui; 2 mobil + 2 motor bergerak looping
  (mobil hijau z=14 timur kec.7, mobil oranye z=16 barat
  kec.6, motor ungu z=14 timur kec.10, motor teal z=16 barat
  kec.9), badan diputar 90° memanjang ke arah x, wrap ±40,
  tanpa label/klik; mobil/motor parkir tetap diam.
- Suara cuaca + luar otomatis (Web Audio sintesis, tanpa file
  luar/CDN/lagu komersial): hujan noise lowpass 0,22; petir
  hujan 0,25 + angin 0,10 + guruh (sine 60→30 Hz) tepat saat
  kilat; badai hujan 0,30 + angin bandpass 0,28 LFO 0,5 Hz;
  salju desis 0,03; mendung angin 0,02; cerah/panas terik 0.
  Luar: burung chirp 2400–3300 Hz hanya Pagi/Siang/Sore +
  cerah/mendung/panas terik (bukan hujan/badai/salju/malam);
  dengung lalu lintas siang 0,10 / senja 0,06 / malam 0,03.
  Diperbarui dari applyTimeWeather() + toggle Suara Kantor
  (tanpa tombol baru); hanya terdengar setelah Suara Kantor
  diketuk (autoplay browser).
- Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep); kursi tetap sebagian tertutup karakter yang
  berdiri di depannya (posisi karakter, bukan kaki hilang);
  roda kendaraan tidak berputar; karakter tetap berdiri bukan
  duduk sempurna.

## Koreksi v31 atas screenshot tes Oemar (masih versi HP embedded — mencakup v28–v30)

- Kursi tidak lagi cacat: `chair()` (lt 1) + `f2chair()` (lt 2)
  dulu hanya dudukan + sandaran tanpa kaki — kini 4 kaki per
  kursi (0,07×0,43, y lokal 0–0,43) menapak ke lantai, semua
  kursi kerja + direktur; stool tidak diubah (sudah bertiang).
- Lounge lt 2 pindah dari tengah jalan (sofa -6, TV -3,4,
  karpet -4,75, semua z=2,5 — dihapus total) ke dekat dinding
  DEPAN selatan, di depan ruang Oki (tengah): karpet (0,7,0)
  3,5×3, sofa teal (0,7,8) menghadap utara, TV (0,6,2) layar
  menghadap selatan ke sofa, konsol generik + kontroler ikut
  pindah (konsol di meja TV, kontroler di karpet).
- Aquarium lt 2 nempel dinding timur, tidak melintang: dari
  (11,2,0) tengah open space → x=12,4, z=2,0, diputar 90°
  (sisi panjang sejajar dinding, kaca x 12,0–12,8), ikan
  berenang sepanjang z (z 1,3–2,7), tidak menembus dinding.
  Aquarium lt 1 (-4,7,5) tidak diubah.
- Meja meeting lt 2 diketengahkan: dari (8,2,0) depan ruang
  timur → (0,3,0) tengah open space selatan, stool timur/
  barat/selatan (tanpa stool utara, koridor z≈1 tetap lewat).
- Cuaca 7 jenis (tombol Ganti Cuaca + auto-random): Cerah →
  Mendung → Hujan → Salju ❄️ (partikel salju jatuh pelan) →
  Petir ⛈️ (awan gelap + hujan + kilat berkala terlihat) →
  Badai 🌪️ (awan 3× lebih cepat + hujan deras/miring) →
  Panas Terik 🔥 (tanpa awan, cahaya 1,4×, matahari lebih
  terang/besar) → kembali ke Cerah.
- Benda langit TERLIHAT mengikuti waktu perangkat: Matahari
  (bola kuning; senja rendah/oranye) di Pagi/Siang/Sore/Senja,
  Bulan (bola pucat) + Bintang (150 titik) di Malam, Matahari
  sembunyi di Malam.
- Karpet open space lt 1: pusat (0,4,8), 9×3,5, y=0,05, warna
  hangat — tidak menutupi aquarium/kucing/pintu masuk.
- Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep); karakter tetap berdiri, bukan duduk sempurna;
  efek salju/petir/badai + benda langit perlu dinilai visual.

## Anggota + perabot segmen baru + label diperkecil + chatbot bisnis (v30, masih versi HP embedded — mencakup v28/v29)

- Anggota baru fiktif simulasi (nama/biodata/KPI disiapkan Lux atas
  konfirmasi Oemar, ditegaskan fiktif di profil + chatbot): Ludo
  (barat lt 2) — Bima Aryo Nugroho (Produk, 27, Semarang), Alya
  Putri Maharani (Marketing, 25, Jakarta), Tari Wulandari (Admin,
  26, Malang); Oki (tengah lt 2) — Raka Aditya Saputra (Riset &
  Konten, 26, Surabaya), Nisa Rahmawati (Socmed, 24, Cirebon).
  Total personel 19 (Oemar + Lux + 12 lama + 5 baru), masuk
  Personel, Ganti Orang, profil klik, KPI sampel, filter
  Ludo/Oki, chatbot. Basis lantai 2 (y=3.6), naik/turun via
  tangga x=-10 y bertahap, briefing lewat tangga, Ganti Orang
  mengatur lantai sesuai rumah karakter, titik briefing 19.
- Perabot lantai 2 (dasar y=3.6): workstation 5× (meja + PC
  monitor + keyboard + kursi kerja) di (-11/-8.5/-6,-5.2) Ludo
  dan (-1.5/1.5,-5.2) Oki, kursi di belakang karakter z=-3.35;
  meja meeting bundar (8,2.0) + 4 stool; arsip 2 lemari hijau
  (-12.4,-8.2) dan (-12.4,-6.8); lounge karpet (-4.75,2.5),
  sofa teal (-6,2.5), TV (-3.4,2.5) + konsol generik tanpa
  merek + kontroler di karpet; aquarium (11,2.0) 3 ikan;
  2 kucing baru (abu-abu (-8,3.2), putih (3,3.2), ekor
  bergoyang) di samping kucing oranye lantai 1 yang tetap.
  Ruang timur lt 2 (Ekspansi 3) tetap kosong.
- Lantai 1: keyboard kecil di semua monitorDesk (utara, selatan,
  Lux; bukan meja meeting/pantry/tamu); kursi kerja 13× —
  utara + Lux tepat di belakang karakter, selatan di sisi
  timur karakter (karena belakangnya sudah dinding depan).
  Meja/karakter/furnitur lantai 1 lain tidak digeser.
- Head label diperkecil (semua karakter): canvas 256×144 →
  200×110 px, font nama 30→26, peran/segmen 20→17, skala sprite
  2.6×1.45 → 1.9×1.05, tinggi di atas kepala y=2.35→2.1; isi
  3 baris: panggilan, job position, KODE segmen saja (BK/JK/
  RU/BTA/LB/OKI, Oemar/Lux = OSCR). Profil klik tetap lengkap.
- Chatbot knowledge bisnis (tetap canned, bukan AI): topik
  payung 6 segmen + per segmen (model bisnis, produk/layanan,
  tim) dari fakta file/MEMORY saja; yang belum dikunci (harga,
  kontak, link, angka follower/penjualan, status Lynk) dijawab
  jujur belum tersedia, tidak dikarang; fallback tetap jujur.
- Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep); karakter berdiri di depan kursi/meja, bukan
  duduk sempurna (keterbatasan model); garis lurus waypoint
  masih bisa menyenggol sudut furnitur; label baru ~27% lebih
  kecil — perlu dinilai keterbacaannya di HP saat tes.

## 2 segmen baru di lantai 2 (v29, masih versi HP embedded — mencakup v28)

- v28 (di dalam v29): Baris 1 Tour+Lantai+Lantai 2 gabungan
  (17 ikon, pemisah tipis, label 🏢/⬆️); Baris 2 Segmen+Setting
  berdampingan, masing-masing berketerangan di atas tombolnya
  (caption-top); Baris 3 Musik; kamera D-pad kanan align-start.
- v29: Segmen menjadi 6 — BK, JK, RU, BTA, lalu 🎲 LB (Ludo
  Berdua, goView('ludo')) dan 🤖 Oki (Oki | AI Sehari-hari,
  goView('okisadma')), 40 px, urutan itu di grup Segmen.
- Kantor segmen baru di lantai 2: barat (dulu Ekspansi 1) →
  Ludo Berdua, tengah (dulu Ekspansi 2) → Oki | AI Sehari-hari,
  timur (Ekspansi 3) tetap kosong. Kamera ludo = kamera ruang
  barat lantai 2, okisadma = ruang tengah; goView keduanya
  otomatis setFloor(2). Tombol ruang di baris Tour 🟦₁/🟩₂
  diubah judul/onclick-nya jadi Ludo/Oki (bukan Ekspansi 1/2
  lagi), 🟧₃ tetap Ekspansi 3 — tanpa duplikasi. Ruangan tetap
  karpet + label saja, tanpa meja/karyawan baru.
- Tim (chatbot saja, tanpa nama karangan, tanpa karakter baru):
  Ludo = Produk, Marketing, Admin saja; Oki = Riset & Konten,
  Socmed saja. Chatbot OSCR menyebut 6 segmen; lantai 2
  dijelaskan terisi 2 dari 3 ruang.
- Tidak berubah: layout v28, 3D lain, data/status lama, angka
  dashboard (tidak ada angka baru untuk segmen baru).
  Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep + diff). Catatan paket: opensource sebelumnya
  masih v27 (v28 sengaja tidak meng-update-nya), kini langsung
  diselaraskan ke v29 yang sudah mencakup v28.

## Setting ikon saja + tombol seragam + Setting naik sebaris Segmen (v27, masih versi HP embedded)

- Grup "Setting Kondisi" → "⚙️ Setting:" saja; keempat tombol jadi
  ikon saja tanpa kata (title/aria-label lengkap): 🔄 Refresh
  Status, 🌤️ Ganti Cuaca, ▶☀️ Briefing Pagi (play + matahari),
  ▶🌙 Briefing Penutup (play + bulan). Label grup tetap sebagai
  keterangan singkat.
- Tombol Segmen diseragamkan 40 px (class .short-btn, height:40px,
  isi terpusat) menyamai tombol ikon Tour; Lantai/Lantai 2 sudah
  40×40 px sejak v25; tombol briefing dua emoji pakai .icon-btn-2
  (56 px lebar, 40 px tinggi).
- Susunan naik: Tour (1 baris penuh) | Segmen → Lantai → Lantai 2
  → Setting (satu baris gabungan; Setting menyusut dari ~670 px
  jadi ~300 px setelah jadi ikon, sehingga tidak lagi jatuh ke
  baris sendiri) | Musik (baris penuh). Area tombol 4 baris → 3
  baris, Dashboard naik lagi. Kamera tetap align-start, tidak
  melar. Catatan jujur: baris gabungan ~950–1000 px, jadi di
  desktop lebar muat sebaris, di desktop lebih sempit / HP bisa
  membungkus — tes visual wajib sebelum deploy.
- Tidak berubah: isi/fungsi tombol lain, 3D, chatbot, data/status.
  Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep + diff).

## Layout tombol dirapatkan, ruang kosong dihilangkan (v26, masih versi HP embedded)

- Akar masalah v25: `.btns` pakai `align-items:stretch` sehingga
  kolom kamera melar setinggi kolom utama (kotak putih kosong di
  bawah Zoom), dan `.btns-main` kolom memaksa tiap grup satu baris
  penuh padahal grupnya sudah pendek.
- Perbaikan: `.btns` → `align-items:flex-start`, `.camera-col` →
  `align-self:flex-start;height:auto` (kotak berakhir tepat di bawah
  Zoom); `.btns-main` → baris membungkus (`flex-direction:row`,
  `flex-wrap:wrap`, `align-items:flex-start`); grup Segmen/Lantai/
  Lantai 2/Setting `flex:0 1 auto` (berdampingan bila muat); Tour
  `flex-basis:100%` (tetap 1 baris penuh); Musik `flex:1 1 100%`
  (baris penuh sendiri — terlalu lebar untuk berbagi baris dengan
  Setting tanpa terpotong). Susunan desktop: Tour | Segmen+Lantai+
  Lantai 2 | Setting | Musik = 4 baris (dari 6), Dashboard naik ke
  atas. Mobile tetap menumpuk vertikal, D-pad terpusat.
- Tidak berubah: isi/fungsi semua tombol, 3D, chatbot, data/status.
  Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep + diff CSS); penghematan persis tergantung lebar
  layar, tes visual desktop + HP wajib sebelum deploy.

## Rapikan tombol (v25, masih versi HP embedded)

- Tour Ruangan jadi ikon saja, satu baris (flex nowrap, scroll
  horizontal di layar sempit): 🏠 🏢 👑 🤝₁ 🤝₂ 🛋️ ☕ 🚻 🗄️ 🌳 👤,
  masing-masing title/aria-label nama lengkap; label grup 🗺️ saja;
  tombol ikon seragam 40×40 px. Meeting 1/2 pakai angka kecil karena
  emojinya sama.
- Kamera jadi remot D-pad 3×3: atas ▲ Naik, tengah ◀ Kiri – tombol
  360 di tengah – ▶ Kanan, bawah ▼ Turun; di luar salib, di bawahnya,
  Zoom 🔍 + / 🔎 − gaya volume plus-minus. orbitBtn jadi ikon saja
  (🔄 mati, ⏸ jalan) — semua penulisan teks panjang orbitBtn di JS
  sudah diubah jadi ikon + title, jadi tidak balik jadi teks panjang
  saat pindah ruangan/ganti lantai. Label grup 🎥 saja, lebar kolom
  170 px → 132 px.
- Lantai jadi ikon saja: ⬇️ Lantai 1, ⬆️ Lantai 2; Lantai 2 jadi
  🟦₁ 🟩₂ 🟧₃ 🪜 (title/aria-label lengkap). Label grup 🏢 / ⬆️ saja.
- Segmen dipersingkat: 💰 BK, 🌍 JK, 💌 RU, 🛒 BTA (title/aria-label
  nama lengkap, onclick asli). Setting Kondisi tetap ikon + label
  pendek (Refresh Status, Ganti Cuaca, Briefing Pagi, Briefing
  Penutup), tidak jadi ikon saja.
- Tidak berubah: musik/Suara Kantor, tab, jam/cuaca/fokus/status,
  seluruh scene 3D, chatbot, data/status.
  Keterbatasan yang dicatat: belum diuji di browser (hanya node
  --check + grep + review diff).

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

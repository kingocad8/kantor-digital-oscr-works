# Kustomisasi Kantor Digital — cukup edit `config.json`

Mulai v37, kamu **tidak perlu mengutak-atik kode 3D** untuk menjadikan kantor
ini kantor kamu sendiri. Cukup edit **satu file: `config.json`** (di folder yang
sama dengan `index.html`), lalu deploy fork kamu sendiri. Repo OSCR Works tidak
terganggu sama sekali — kamu kerja di fork kamu, bukan di repo Oemar.

> Berlaku untuk v37 ke atas. Cara lama (edit `index.html` langsung: ganti
> `SOUNDCLOUD_URL`, daftar `persons`, pemanggilan `chibi(...)`, objek `data`)
> tetap bisa, tapi tidak disarankan lagi — `config.json` lebih aman karena
> salah ketik di sana tidak merusak halaman (ada fallback, lihat bawah).

## Langkah-langkah (tanpa install apa-apa)

1. **Fork repo Oemar di GitHub.** Buka repo kantor digital OSCR Works di
   GitHub → tombol **Fork** (kanan atas) → **Create fork**. Sekarang kamu
   punya salinan repo di akun GitHub kamu sendiri. Repo Oemar tidak berubah.
2. **Edit `config.json` langsung di web GitHub.** Di fork kamu, klik file
   `config.json` → tombol pensil (**Edit this file**) → ubah nilainya sesuai
   tabel di bawah → **Commit changes** (tulis pesan commit, mis. "Ganti jadi
   kantor saya"). Tidak perlu install git, editor, atau apa pun.
3. **Deploy fork kamu ke Vercel (gratis).** Buka vercel.com → **Add New →
   Project** → **Import** fork kamu → Framework: **Other / Static** →
   **tidak perlu build command, tidak perlu output directory, tidak perlu
   env var** → **Deploy**. Selesai — kamu dapat link kantor digital sendiri
   dengan isi versi kamu. Link Oemar tidak berubah dan tidak terganggu.
4. **Ulangi langkah 2 kapan pun** mau mengubah lagi — tiap commit, Vercel
   auto-deploy ulang. Tidak perlu minta ke Oemar/Lux, tidak perlu antre.

## Yang bisa diubah lewat `config.json`

| Field | Yang diubah | Contoh nilai | Kalau dikosongkan / dihapus |
|---|---|---|---|
| `officeName` | Judul header + judul tab browser | `"Kantor Saya - Digital Office"` | Kembali ke `"OSCR Works - Digital Office"` |
| `soundcloudUrl` | Album/playlist musik kantor (tombol ▶ Musik, Prev/Next memutar track di album itu) | `"https://soundcloud.com/namakamu/sets/playlist-kamu"` | Kembali ke album Hindia default OSCR |
| `segments[]` → `code` | Kode pendek di tombol Segmen (mis. BK) | `"BK"` | Tombol pakai kode default OSCR |
| `segments[]` → `emoji` | Emoji tombol Segmen + judul detail segmen | `"💰"` | Emoji default OSCR |
| `segments[]` → `name` | Nama segmen (tombol Segmen, judul detail, opsi Dashboard) | `"Bedah Keuangan"` | Nama default OSCR |
| `segments[]` → `description` | Deskripsi segmen, tampil di atas detail segmen | `"Edukasi keuangan ..."` | Deskripsi default OSCR |
| `segments[]` → `viewKey` | **JANGAN DIUBAH.** Ini kabel ke tombol/kamera (`bk`, `jk`, `ru`, `bta`, `ludo`, `okisadma`). Mengubahnya memutus tombol segmen itu. | — | — |
| `dashboard.note` | Kalimat keterangan di atas Dashboard (setelah "Dashboard Segmen —") | `"angka di bawah ini data asli ..."` | Kalimat default OSCR |
| `dashboard.segments` | Angka Dashboard per segmen per platform: `views`, `likes`, `comments`, `shares`, `followers`, `posts`, `weeks` (array 4 angka, 4 minggu terakhir) | `{"bk": {"instagram": {"views": 12500, ...}}}` | Angka default OSCR. Catatan: hanya `bk`, `jk`, `ru`, `bta` yang punya kartu Dashboard di v37 — menambah segmen lain di sini diabaikan. |
| `employees[]` → `nick` | Nama panggilan (label kepala + tombol Personel/KPI) | `"Nadia"` | Karyawan itu dilewati (tidak dibuat) |
| `employees[]` → `full` | Nama lengkap (profil klik) | `"Nadia Ayu Lestari"` | Diisi sama dengan `nick` |
| `employees[]` → `role` | Jabatan (label kepala + profil klik) | `"Content & Script"` | Karyawan itu dilewati (tidak dibuat) |
| `employees[]` → `segment` | Nama segmen karyawan (profil klik) | `"Bedah Keuangan"` | Karyawan itu dilewati (tidak dibuat) |
| `employees[]` → `segmentCode` | Kode segmen di label kepala (mis. BK) | `"BK"` | Kosong (label jadi `Nick \| Role \| `) |
| `employees[]` → `filter` | Filter Personel/KPI: `management`, `bk`, `jk`, `ru`, `bta`, `ludo`, `oki`, atau `all` | `"bk"` | Ditebak dari `segment`; kalau segmen tidak dikenal → `all` (hanya muncul di filter Semua) |
| `employees[]` → `gender` | `Cowo` / `Cewe` (profil klik + suara obrolan) | `"Cewe"` | `"-"` |
| `employees[]` → `age`, `born`, `origin`, `suku`, `agama`, `karakter` | Biodata profil klik (umur, lahir, asal, suku, agama, karakter) | `"27"`, `"Yogyakarta, 14 Feb 1999"` | `"-"` |
| `employees[]` → `shirt`, `hair`, `skin` | Warna baju / rambut / kulit karakter, format hex string | `"#16a085"` | Abu-abu `#888888` |
| `employees[]` → `hairStyle` | Gaya rambut: `pendek`, `panjang`, `bun`, `ponytail`, `cepak`, `keriting` | `"panjang"` | `"pendek"` |
| `employees[]` → `floor` | Lantai rumah karakter: `1` atau `2` | `2` | `1` |
| `employees[]` → `pos` | Posisi karakter `[x, z]` — **posisi karakter, bukan meja** (meja ada di dekatnya). Default OSCR: lantai 1 baris utara z=1.6 / selatan z=8.5, lantai 2 z=-4.1. Alias lama: `desk`. | `[-11, 1.6]` | `[0, 0]` (tengah kantor — isi yang benar, jangan dikosongkan) |
| `employees[]` → `ry` | Arah hadap karakter: `"PI"` (menghadap selatan, default semua) atau angka radian | `"PI"` | `"PI"` |
| `employees[]` → `isOemar` | `true` hanya untuk karakter Director (pemimpin briefing pagi). Jangan `true` untuk orang lain. | `false` | `false` |
| `employees[]` → `profileBody` | Opsional. Isi profil klik kustom (HTML) — dipakai default hanya untuk Director & Manager. Kosongkan untuk profil biodata standar. | — | Profil biodata standar dari field di atas |
| `employees[]` → `kpi` | KPI sampel: `{"tepat": 85, "metrics": [{"name": "Naskah selesai", "target": 10, "actual": 7}]}`. Alias: `label` untuk `name`, `value` untuk `actual`. | Lihat default di file | `{"tepat": 0, "metrics": []}` |
| `chatbotBusiness.oscr` | Jawaban bot soal payung/grup kantor | `"OSCR Works adalah grup ..."` | Jawaban canned default OSCR |
| `chatbotBusiness.bisnis` | Jawaban bot soal bisnis/usaha/produk/layanan | `"Bisnis OSCR Works itu ..."` | Jawaban canned default OSCR |
| `chatbotBusiness.bk` / `.jk` / `.ru` / `.bta` / `.ludo` / `.oki` | Jawaban bot soal masing-masing segmen | Lihat default di file | Jawaban canned default OSCR |
| `employees[]` → `key` | ID internal karyawan (huruf kecil tanpa spasi). Kalau tidak diisi, dibuat dari `nick`. Jangan pakai `key` yang sama untuk dua orang. | `"nadia"` | Dari `nick` |

## Yang TIDAK bisa diubah lewat `config.json` (tetap hardcoded)

- Bentuk gedung, denah ruangan, posisi perabot/meja/kursi/sofa/TV/aquarium
- Layout dan susunan tombol, kamera, dan tampilan
- Cuaca, suara, kendaraan lewat, dan seluruh logika 3D
- Kalau mau mengubah itu, jalurnya edit `index.html` langsung (cara lama).

## Peringatan privasi — baca sebelum isi

- **JANGAN** isi `config.json` dengan password, alamat lengkap, nomor HP,
  atau data bank — hanya info bisnis publik + data karyawan simulasi.
- Angka Dashboard yang bukan data nyata **harus tetap dilabeli
  CONTOH/ILUSTRASI** (lihat `dashboard.note`). Jangan mengklaim angka contoh
  sebagai data asli.
- Karyawan di default OSCR adalah **karakter fiktif simulasi**, bukan orang
  nyata. Kalau kamu isi dengan tim beneran, pastikan mereka setuju datanya
  tampil di halaman publik fork kamu.

## Jujur soal keterbatasan (bukan bug)

1. **Kustomisasi config hanya terbukti saat situs di-deploy (Vercel) atau
   dibuka sebagai folder lengkap** (`index.html` + `config.json`
   berdampingan di browser). Saat dibuka sebagai **lampiran file tunggal**
   di penampil Muse, `config.json` tidak ikut terlayani (fetch gagal),
   sehingga situs menampilkan **default OSCR (fallback)**, bukan config
   kamu. Ini keterbatasan penampil, bukan bug config — di Vercel, config
   kamu yang tampil.
2. **Tanpa `config.json` pun situs tetap jalan 100%** dengan data default
   OSCR yang sudah ada di dalam kode. Halaman tidak akan blank/error hanya
   karena config hilang atau JSON-nya rusak — tapi kalau JSON rusak,
   yang tampil adalah default OSCR, bukan config kamu. Periksa JSON kamu
   (kurung/koma) kalau perubahan tidak muncul.
3. **`status.json` masih bisa menimpa detail segmen lama.** Untuk segmen
   BK/JK/RU/BTA, isi `status.json` (status + body) akan menimpa detail
   segmen, sedangkan judul + deskripsi dari `config.json` diterapkan ulang
   setelahnya. Kalau kamu mengganti nama segmen, **edit juga `status.json`
   di fork kamu** (atau hapus file itu) supaya teks status OSCR lama tidak
   ikut tampil.
4. **SoundCloud:** kalau tombol Musik sempat ditekan dalam ~100 ms pertama
   sebelum config selesai dimuat, album lama yang terputar sampai halaman
   di-reload. Setelah config dimuat, tekanan Musik berikutnya memakai album
   dari config.
5. **Jumlah karyawan bebas**, tapi posisi (`pos`) harus diisi sendiri untuk
   tiap orang baru — kalau dua orang pakai `pos` yang sama, karakter mereka
   akan bertumpuk. Filter Personel/KPI, profil klik, dan chatbot tim ikut
   daftar karyawan dari config secara otomatis (tidak ada daftar kedua
   yang bisa tidak sinkron).

## Kembali ke default OSCR

Hapus `config.json` dari repo kamu, atau isi ulang dengan default OSCR yang
ada di repo ini (file `config.json` asli). Commit → Vercel auto-deploy →
kantor kembali tampil sebagai OSCR Works.

## Contoh minimal: ganti 3 hal saja

```json
{
  "officeName": "Kantor Saya - Digital Office",
  "soundcloudUrl": "https://soundcloud.com/namakamu/sets/playlist-kamu",
  "segments": [
    {"code": "KU", "emoji": "💰", "name": "Keuangan Saya", "viewKey": "bk",
     "description": "Edukasi keuangan versi saya."}
  ]
}
```

Field lain yang tidak ditulis di contoh ini akan memakai default OSCR —
jadi kamu bisa mengubah sedikit demi sedikit, tidak harus mengisi semuanya
sekaligus. (Catatan: contoh ini hanya mengganti segmen BK; segmen lain,
dashboard, karyawan, dan jawaban bot tetap default OSCR sampai kamu ubah.)

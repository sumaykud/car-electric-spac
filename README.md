# Anatomi Mobil Listrik

Modul 3D interaktif (Three.js) untuk mengenal komponen dan cara kerja powertrain mobil listrik dua motor. Pilih komponen di daftar, klik langsung di model 3D, atau ikuti rantai aliran energi. Setiap komponen punya penjelasan fungsi, langkah cara kerja, spesifikasi tipikal, dan grafik live dari simulasi.

## Menjalankan

Halaman memuat model lewat `fetch()`, jadi harus dibuka lewat server web. Membuka `index.html` langsung dari disk (`file://`) tidak akan memuat model mobil.

```bash
python3 -m http.server 8000
```

Lalu buka <http://localhost:8000>.

Untuk GitHub Pages: **Settings → Pages → Deploy from a branch → `main` / root**.

Three.js r170 dan font dimuat dari CDN (jsDelivr, Google Fonts), jadi perlu koneksi internet.

## Isi

| File | Keterangan |
| --- | --- |
| `index.html` | Seluruh aplikasi: HTML, CSS, dan JavaScript dalam satu file |
| `car.glb` | Model mobil terkompresi (9 MB). Dimuat lebih dulu |
| `car-glb.txt` | Model yang sama dalam base64 (12 MB), cadangan untuk hosting yang tidak melayani file `.glb` |

Untuk membuat ulang file cadangan setelah mengganti model:

```bash
base64 -w0 car.glb > car-glb.txt
```

## Fitur

- 13 komponen: paket baterai (96s46p, 4.416 sel), BMS, kontaktor & sekring, port & OBC, DC-DC & aki 12 V, inverter, motor belakang (magnet permanen), gigi reduksi 9,05:1, diferensial, poros & roda, unit motor depan (induksi), VCU & pedal, sistem termal.
- Simulasi fisika sederhana: pedal gas, rem, setir; skenario parkir, akselerasi, jelajah, regeneratif, pengisian AC dan DC; batas daya dari BMS.
- Partikel aliran energi berwarna menurut jenisnya (DC tegangan tinggi, AC 3-fasa, 12 V, pendingin, sinyal CAN) dan berbalik arah saat regeneratif.
- Bagian bergerak: rotor, roda gigi yang saling mengunci, gigi satelit diferensial saat menikung, urutan pra-isi kontaktor, sel baterai yang bisa diwarnai menurut tegangan atau suhu.
- Mode bodi Solid, Kaca (x-ray), Tanpa, dan Urai (exploded).
- Tautan langsung per komponen, misalnya `#baterai` atau `#inverter`.
- Tema terang dan gelap, tata letak ponsel.

## Catatan akurasi

Model mobil hanya berisi bodi, interior, roda, dan suspensi. Semua komponen powertrain dibangun secara prosedural sebagai ilustrasi edukatif, bukan replika komponen pabrikan mana pun. Angka spesifikasi dan hasil simulasi bersifat representatif untuk sedan listrik kelas menengah dan tidak boleh dianggap data resmi.

## Kredit dan lisensi

- Model mobil 3D: [“Tesla 2018 Model 3”](https://sketchfab.com/3d-models/tesla-2018-model-3-5ef9b845aaf44203b6d04e2c677e444f) oleh Ameer Studio, lisensi [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Diubah: dikompresi dengan glTF-Transform (dedup, weld, simplify, quantize) dari 21,6 MB menjadi 9 MB.
- Tesla dan Model 3 adalah merek dagang Tesla, Inc. Proyek ini tidak berafiliasi dengan Tesla. Tekstur model masih memuat logo Tesla; pertimbangkan hal ini sebelum penggunaan komersial.
- [Three.js](https://threejs.org/) (MIT), dimuat dari CDN.
- Font Barlow, Barlow Condensed, dan IBM Plex Mono (SIL Open Font License) dari Google Fonts.

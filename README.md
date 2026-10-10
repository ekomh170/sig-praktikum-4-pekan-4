# sig-praktikum-4-pekan-4 – Layer Polygon pada Aplikasi Google Map

Repository tugas praktikum 4 **Sistem Informasi Geografis** pekan 4, materi _Aplikasi Google Map 3_: membuat layer area polygon di Google My Maps lalu mengekspor setiap layer ke format **KML** dan **CSV**.

|                   |                                              |
| ----------------- | -------------------------------------------- |
| Nama              | Eko Muchamad Haryono                         |
| NIM               | 0110223079                                   |
| Program Studi     | Teknik Informatika – STT Terpadu Nurul Fikri |
| Mata Kuliah       | Sistem Informasi Geografis                   |
| Dosen Pengampu    | Dr. Sirojul Munir S.Si., M.Kom               |
| Asisten           | Agam                                         |
| Tanggal Praktikum | 7 Oktober 2026                               |

**Tautan peta Google My Maps:**

- Taman Kota Jakarta: _(tempel link share My Maps di sini)_
- Praktikum Mandiri 1: _(tempel link share My Maps di sini)_

## Struktur Repository

```
.
└── data/
    ├── taman_kota_jakarta/          # Peta "Taman Kota Jakarta" – 5 layer
    │   ├── taman_monas.kml / .csv
    │   ├── gelora_bung_karno.kml / .csv
    │   ├── kebun_binatang_ragunan.kml / .csv
    │   ├── taman_mini_indonesia_indah.kml / .csv
    │   └── tebet_eco_park.kml / .csv
    └── praktikum_mandiri_1/         # Peta "Praktikum Mandiri 1" – 3 layer
        ├── dki_jakarta.kml / .csv
        ├── diy_yogyakarta.kml / .csv
        └── kota_depok.kml / .csv
```

## Daftar Layer

|  No | Layer                      | Peta                | Lokasi                               |           Jumlah polygon |
| --: | -------------------------- | ------------------- | ------------------------------------ | -----------------------: |
|   1 | Taman Monas                | Taman Kota Jakarta  | Kec. Gambir, Jakarta Pusat           |                        1 |
|   2 | Gelora Bung Karno          | Taman Kota Jakarta  | Kec. Tanah Abang, Jakarta Pusat      |                        1 |
|   3 | Kebun Binatang Ragunan     | Taman Kota Jakarta  | Kec. Pasar Minggu, Jakarta Selatan   |                        1 |
|   4 | Taman Mini Indonesia Indah | Taman Kota Jakarta  | Kec. Cipayung, Jakarta Timur         |                        1 |
|   5 | Tebet Eco Park             | Taman Kota Jakarta  | Kec. Tebet, Jakarta Selatan          | 2 (sisi utara & selatan) |
|   6 | DKI Jakarta                | Praktikum Mandiri 1 | Provinsi DKI Jakarta (daratan utama) |                        1 |
|   7 | DIY Yogyakarta             | Praktikum Mandiri 1 | Daerah Istimewa Yogyakarta           |                        1 |
|   8 | Kota Depok                 | Praktikum Mandiri 1 | Kota Depok, Jawa Barat               |                        1 |

Catatan:

- **Tebet Eco Park** digambar sebagai dua polygon dalam satu layer agar badan jalan di antara sisi utara dan selatan tidak ikut terhitung sebagai luas taman.
- **DKI Jakarta** hanya mencakup daratan utama; Kabupaten Administrasi Kepulauan Seribu tidak termasuk.

## Format Data

Setiap layer disimpan dalam dua format dengan struktur yang sama seperti hasil _Export data_ Google My Maps:

- **KML** – `<Document>` (nama peta) → `<Folder>` (nama layer) → `<Placemark>` (nama objek) → `<Polygon>/<outerBoundaryIs>/<LinearRing>/<coordinates>` berisi `bujur,lintang,0`; koordinat pertama sama dengan koordinat terakhir. Gaya garis dan isian disimpan pada `<Style>`/`<StyleMap>`.
- **CSV** – kolom `WKT,name,description`; geometri ditulis sebagai `POLYGON ((bujur lintang, ...))`.

Sistem koordinat: WGS 84 (EPSG:4326).

## Cara Membuka Data

- **Google My Maps:** buka peta → _Add layer_ → _Import_ → pilih file `.kml` atau `.csv` (untuk CSV, pilih kolom `WKT` sebagai posisi dan `name` sebagai judul).
- **Google Earth:** _File → Open_ → pilih file `.kml`.
- **QGIS:** seret file `.kml` ke kanvas, atau _Layer → Add Layer → Add Delimited Text Layer_ untuk CSV dengan _Geometry definition: WKT_.

## Acuan Batas Polygon

Batas polygon pada folder `data/` mengacu pada data berikut:

| Layer                       | Acuan                                                                                                                                       |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Taman Monas                 | OpenStreetMap – [way 628537709](https://www.openstreetmap.org/way/628537709)                                                                |
| Gelora Bung Karno           | OpenStreetMap – [way 653084970](https://www.openstreetmap.org/way/653084970)                                                                |
| Kebun Binatang Ragunan      | OpenStreetMap – [way 29416354](https://www.openstreetmap.org/way/29416354)                                                                  |
| Taman Mini Indonesia Indah  | OpenStreetMap – [way 28834489](https://www.openstreetmap.org/way/28834489)                                                                  |
| Tebet Eco Park              | OpenStreetMap – [way 28259160](https://www.openstreetmap.org/way/28259160) (utara), [way 1268320079](https://www.openstreetmap.org/way/1268320079) (selatan) |
| DKI Jakarta, DIY Yogyakarta | [geoBoundaries](https://www.geoboundaries.org/) – batas provinsi Indonesia (daratan)                                                        |
| Kota Depok                  | OpenStreetMap – [relation 14525364](https://www.openstreetmap.org/relation/14525364)                                                        |

Data acuan © OpenStreetMap contributors, [Open Database License (ODbL) 1.0](https://www.openstreetmap.org/copyright).

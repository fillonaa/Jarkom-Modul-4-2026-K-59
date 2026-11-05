# Jarkom-Modul-4-2026-K-59
# Laporan Resmi Praktikum Komdat-Jarkom Modul 4

Kelompok K-59

- Salsabila Rafa Syafira (5027251059)
- Fiorellin Ilona (5027251082)

## Daftar Isi

- [Informasi Jaringan](#informasi-jaringan)
- [Pembagian Peran Node](#pembagian-peran-node)
- [Pemetaan Node dan Koneksi](#pemetaan-node-dan-koneksi)
- [Pembahasan](#pembahasan)
  - [Perintah Soal](#perintah-soal)
  - [Langkah 1: Perhitungan Subnetting VLSM](#langkah-1-perhitungan-subnetting-vlsm)
  - [Langkah 2: Pembagian IP Interface Router](#langkah-2-pembagian-ip-interface-router)
  - [Langkah 3: Routing](#langkah-3-routing)
  - [Langkah 4: Konfigurasi Router di GNS3](#langkah-4-konfigurasi-router-di-gns3)
  - [Langkah 5: Konfigurasi Host di GNS3](#langkah-5-konfigurasi-host-di-gns3)
  - [Pengujian](#pengujian)

## Informasi Jaringan

- IP Address Host: 10.4.89.250
- Prefix IP: 10.93.x.x
- Platform: GNS3 dan Cisco Packet Tracer
- Image Docker: ardhptr21/alpinet:latest
- Metode di GNS3: VLSM
- Total subnet: 25 (A1 - A25), blok terpakai 10.93.0.0 - 10.93.16.91 tanpa celah antar subnet
- topologi 
<img width="1021" height="642" alt="image" src="https://github.com/user-attachments/assets/1bc914b4-5b2c-4489-a3f8-b8f68678bfe9" />


## Pembagian Peran Node

### Router

| Node | Peran | OS |
|---|---|---|
| Cyberia | Router gateway, satu-satunya yang terhubung ke NAT | Alpine |
| Wired | Router hub pusat (Cyberia, Navi, Tachibana, segmen Switch2) | Alpine |
| Navi | Router cabang Switch6, Switch7, Switch8 | Alpine |
| Tachibana | Router cabang Switch9 dan jalur ke Deus | Alpine |
| Deus | Router cabang Switch10 dan jalur ke Protocol7 | Alpine |
| Protocol7 | Router cabang Switch11 dan jalur ke Knights | Alpine |
| Knights | Router cabang Eiri dan jalur ke Phantoma | Alpine |
| Phantoma | Router cabang Switch12 dan jalur ke Shibuya | Alpine |
| Shibuya | Router ujung cabang Switch13 | Alpine |
| Psyche | Router segmen Switch2, cabang Switch3 | Alpine |
| Copland | Router segmen Switch2, cabang Switch4 dan Juri | Alpine |
| Schumann | Router segmen Switch2, cabang Akashic dan jalur ke Accela | Alpine |
| Accela | Router ujung cabang Switch5 | Alpine |

### Host

| Node | Peran | Jumlah Host | OS |
|---|---|---|---|
| Karl | Server | 700 | Alpine |
| Lin | Server | 180 | Alpine |
| Omnipresence | Klien | 510 | Alpine |
| Denpa | Klien | 3 | Alpine |
| Collective | Server | 260 | Alpine |
| Ghost | Klien | 6 | Alpine |
| Masayuki | Klien | 300 | Alpine |
| Alice | Klien | 208 | Alpine |
| Reika | Klien | 45 | Alpine |
| Yasuo | Klien | 120 | Alpine |
| Miho | Klien | 18 | Alpine |
| Kuma | Server | 4 | Alpine |
| JJ | Klien | 95 | Alpine |
| MyuMyu | Klien | 30 | Alpine |
| Lilith | Klien | 77 | Alpine |
| Specter | Klien | 21 | Alpine |
| Taro | Klien | 57 | Alpine |
| Chisa | Klien | 23 | Alpine |
| Hodgeson | Klien | 9 | Alpine |
| Lain | Klien | 57 | Alpine |
| Mika | Klien | 4 | Alpine |
| Juri | Klien | 31 | Alpine |
| Semi | Klien | 14 | Alpine |
| Eiri | Server | 2 | Alpine |
| Akashic | Server | 3 | Alpine |

## Pemetaan Node dan Koneksi

| No. | Node Asal | Interface Asal | Node Tujuan | Interface Tujuan |
|---|---|---|---|---|
| 1 | NAT1 | nat0 | Cyberia | eth0 |
| 2 | Cyberia | eth1 | Wired | eth1 |
| 3 | Cyberia | eth2 | Switch1 | e0 |
| 4 | Wired | eth0 | Switch2 | e0 |
| 5 | Wired | eth2 | Tachibana | eth2 |
| 6 | Wired | eth3 | Navi | eth0 |
| 7 | Switch2 | e1 | Psyche | eth0 |
| 8 | Switch2 | e2 | Copland | eth0 |
| 9 | Switch2 | e3 | Schumann | eth0 |
| 10 | Psyche | eth1 | Switch3 | e0 |
| 11 | Copland | eth1 | Juri | eth0 |
| 12 | Copland | eth2 | Switch4 | e0 |
| 13 | Schumann | eth1 | Accela | eth0 |
| 14 | Schumann | eth2 | Akashic | eth0 |
| 15 | Accela | eth1 | Switch5 | e0 |
| 16 | Navi | eth1 | Switch6 | e0 |
| 17 | Navi | eth2 | Switch7 | e0 |
| 18 | Navi | eth3 | Switch8 | e0 |
| 19 | Tachibana | eth1 | Deus | eth0 |
| 20 | Tachibana | eth3 | Switch9 | e0 |
| 21 | Deus | eth1 | Protocol7 | eth0 |
| 22 | Deus | eth2 | Switch10 | e0 |
| 23 | Protocol7 | eth1 | Knights | eth0 |
| 24 | Protocol7 | eth2 | Switch11 | e0 |
| 25 | Knights | eth1 | Phantoma | eth0 |
| 26 | Knights | eth2 | Eiri | eth0 |
| 27 | Phantoma | eth1 | Shibuya | eth0 |
| 28 | Phantoma | eth2 | Switch12 | e0 |
| 29 | Shibuya | eth1 | Switch13 | e0 |
| 30 | Switch1 | e1 | JJ | eth1 |
| 31 | Switch1 | e2 | MyuMyu | eth1 |
| 32 | Switch3 | e1 | Karl | eth0 |
| 33 | Switch3 | e2 | Lin | eth0 |
| 34 | Switch4 | e1 | Masayuki | eth0 |
| 35 | Switch5 | e1 | Omnipresence | eth0 |
| 36 | Switch5 | e2 | Denpa | eth0 |
| 37 | Switch6 | e1 | Alice | eth0 |
| 38 | Switch6 | e2 | Reika | eth1 |
| 39 | Switch7 | e1 | Taro | eth1 |
| 40 | Switch8 | e1 | Kuma | eth0 |
| 41 | Switch8 | e2 | Miho | eth0 |
| 42 | Switch8 | e3 | Yasuo | eth0 |
| 43 | Switch9 | e1 | Collective | eth0 |
| 44 | Switch9 | e2 | Ghost | eth0 |
| 45 | Switch10 | e1 | Lilith | eth0 |
| 46 | Switch10 | e2 | Specter | eth0 |
| 47 | Switch11 | e1 | Chisa | eth0 |
| 48 | Switch11 | e2 | Hodgeson | eth0 |
| 49 | Switch12 | e1 | Semi | eth0 |
| 50 | Switch13 | e1 | Lain | eth0 |
| 51 | Switch13 | e2 | Mika | eth0 |

## Pembahasan

### Perintah Soal

- Membagi alamat IP pada topologi The Wired menggunakan prefix `10.93.x.x` dengan metode VLSM.
- Hanya router Cyberia yang terhubung ke NAT (GNS3) / Cloud (CPT).
- Jumlah IP tiap subnet dihitung dari jumlah host ditambah jumlah interface router pada subnet tersebut.
- Pembagian IP dan routing harus seefisien mungkin, tidak ada alamat yang terbuang.
- Seluruh node harus saling terhubung dan dapat melakukan ping satu sama lain.

### Langkah 1: Perhitungan Subnetting VLSM

Cara menghitung:

1. Hitung kebutuhan IP tiap subnet: jumlah host + jumlah interface router di subnet tersebut.
2. Tambahkan 2 alamat untuk Network ID dan Broadcast.
3. Cari prefix terkecil yang muat, yaitu blok 2^n yang masih cukup menampung kebutuhan tadi.
4. Urutkan subnet dari kebutuhan terbesar ke terkecil.
5. Alokasikan berurutan mulai dari `10.93.0.0`. Network ID subnet berikutnya adalah broadcast subnet sebelumnya + 1.

Contoh subnet A1 (Switch3, Karl dan Lin): 700 + 180 host + 1 interface Psyche = 881 IP, ditambah 2 = 883. Blok terkecil yang muat adalah 1024 = 2^10, sehingga prefix `/22` (32 - 10).

Contoh subnet A3 (Switch9, Collective dan Ghost): 260 + 6 host + 1 interface Tachibana = 267 IP, ditambah 2 = 269. Blok terkecil yang muat adalah 512 = 2^9, sehingga prefix `/23`.

Hasil perhitungan:

| Subnet | Rute | Prefix | Netmask | Jumlah IP | Network ID | Broadcast | Range IP |
|---|---|---|---|---|---|---|---|
| A1 | Psyche > Switch3 > Karl, Lin | /22 | 255.255.252.0 | 1022 | 10.93.0.0 | 10.93.3.255 | 10.93.0.1 - 10.93.3.254 |
| A2 | Accela > Switch5 > Denpa, Omnipresence | /22 | 255.255.252.0 | 1022 | 10.93.4.0 | 10.93.7.255 | 10.93.4.1 - 10.93.7.254 |
| A3 | Tachibana > Switch9 > Collective, Ghost | /23 | 255.255.254.0 | 510 | 10.93.8.0 | 10.93.9.255 | 10.93.8.1 - 10.93.9.254 |
| A4 | Copland > Switch4 > Masayuki | /23 | 255.255.254.0 | 510 | 10.93.10.0 | 10.93.11.255 | 10.93.10.1 - 10.93.11.254 |
| A5 | Navi > Switch6 > Alice, Reika | /24 | 255.255.255.0 | 254 | 10.93.12.0 | 10.93.12.255 | 10.93.12.1 - 10.93.12.254 |
| A6 | Navi > Switch8 > Kuma, Miho, Yasuo | /24 | 255.255.255.0 | 254 | 10.93.13.0 | 10.93.13.255 | 10.93.13.1 - 10.93.13.254 |
| A7 | Cyberia > Switch1 > JJ, MyuMyu | /25 | 255.255.255.128 | 126 | 10.93.14.0 | 10.93.14.127 | 10.93.14.1 - 10.93.14.126 |
| A8 | Deus > Switch10 > Lilith, Specter | /25 | 255.255.255.128 | 126 | 10.93.14.128 | 10.93.14.255 | 10.93.14.129 - 10.93.14.254 |
| A9 | Navi > Switch7 > Taro | /26 | 255.255.255.192 | 62 | 10.93.15.0 | 10.93.15.63 | 10.93.15.1 - 10.93.15.62 |
| A10 | Protocol7 > Switch11 > Hodgeson, Chisa | /26 | 255.255.255.192 | 62 | 10.93.15.64 | 10.93.15.127 | 10.93.15.65 - 10.93.15.126 |
| A11 | Shibuya > Switch13 > Mika, Lain | /26 | 255.255.255.192 | 62 | 10.93.15.128 | 10.93.15.191 | 10.93.15.129 - 10.93.15.190 |
| A12 | Copland > Juri | /26 | 255.255.255.192 | 62 | 10.93.15.192 | 10.93.15.255 | 10.93.15.193 - 10.93.15.254 |
| A13 | Phantoma > Switch12 > Semi | /27 | 255.255.255.224 | 30 | 10.93.16.0 | 10.93.16.31 | 10.93.16.1 - 10.93.16.30 |
| A14 | Wired > Switch2 > Schumann, Copland, Psyche | /29 | 255.255.255.248 | 6 | 10.93.16.32 | 10.93.16.39 | 10.93.16.33 - 10.93.16.38 |
| A15 | Knights > Eiri | /29 | 255.255.255.248 | 6 | 10.93.16.40 | 10.93.16.47 | 10.93.16.41 - 10.93.16.46 |
| A16 | Schumann > Akashic | /29 | 255.255.255.248 | 6 | 10.93.16.48 | 10.93.16.55 | 10.93.16.49 - 10.93.16.54 |
| A17 | Cyberia > Wired | /30 | 255.255.255.252 | 2 | 10.93.16.56 | 10.93.16.59 | 10.93.16.57 - 10.93.16.58 |
| A18 | Wired > Navi | /30 | 255.255.255.252 | 2 | 10.93.16.60 | 10.93.16.63 | 10.93.16.61 - 10.93.16.62 |
| A19 | Wired > Tachibana | /30 | 255.255.255.252 | 2 | 10.93.16.64 | 10.93.16.67 | 10.93.16.65 - 10.93.16.66 |
| A20 | Tachibana > Deus | /30 | 255.255.255.252 | 2 | 10.93.16.68 | 10.93.16.71 | 10.93.16.69 - 10.93.16.70 |
| A21 | Deus > Protocol7 | /30 | 255.255.255.252 | 2 | 10.93.16.72 | 10.93.16.75 | 10.93.16.73 - 10.93.16.74 |
| A22 | Protocol7 > Knights | /30 | 255.255.255.252 | 2 | 10.93.16.76 | 10.93.16.79 | 10.93.16.77 - 10.93.16.78 |
| A23 | Knights > Phantoma | /30 | 255.255.255.252 | 2 | 10.93.16.80 | 10.93.16.83 | 10.93.16.81 - 10.93.16.82 |
| A24 | Phantoma > Shibuya | /30 | 255.255.255.252 | 2 | 10.93.16.84 | 10.93.16.87 | 10.93.16.85 - 10.93.16.86 |
| A25 | Schumann > Accela | /30 | 255.255.255.252 | 2 | 10.93.16.88 | 10.93.16.91 | 10.93.16.89 - 10.93.16.90 |
| **Total** | | | | **4138** | | | |

![Tabel subnetting pada spreadsheet](img/subnetting.png)

### Langkah 2: Pembagian IP Interface Router

Tiap subnet LAN memakai alamat pertama (`.1`) sebagai gateway di router. Untuk link antar router (/30), router di sisi atas (arah Cyberia) memakai alamat pertama dan router di sisi bawah memakai alamat kedua. Pada segmen Switch2 (A14), Wired memakai `.33`, Psyche `.34`, Copland `.35`, Schumann `.36`.

| Router | Interface | Terhubung ke | Subnet | IP Address | Prefix |
|---|---|---|---|---|---|
| Cyberia | eth0 | NAT | - | DHCP (192.168.122.x) | /24 |
| Cyberia | eth1 | Wired | A17 | 10.93.16.57 | /30 |
| Cyberia | eth2 | Switch1 | A7 | 10.93.14.1 | /25 |
| Wired | eth0 | Switch2 | A14 | 10.93.16.33 | /29 |
| Wired | eth1 | Cyberia | A17 | 10.93.16.58 | /30 |
| Wired | eth2 | Tachibana | A19 | 10.93.16.65 | /30 |
| Wired | eth3 | Navi | A18 | 10.93.16.61 | /30 |
| Navi | eth0 | Wired | A18 | 10.93.16.62 | /30 |
| Navi | eth1 | Switch6 | A5 | 10.93.12.1 | /24 |
| Navi | eth2 | Switch7 | A9 | 10.93.15.1 | /26 |
| Navi | eth3 | Switch8 | A6 | 10.93.13.1 | /24 |
| Tachibana | eth1 | Deus | A20 | 10.93.16.69 | /30 |
| Tachibana | eth2 | Wired | A19 | 10.93.16.66 | /30 |
| Tachibana | eth3 | Switch9 | A3 | 10.93.8.1 | /23 |
| Deus | eth0 | Tachibana | A20 | 10.93.16.70 | /30 |
| Deus | eth1 | Protocol7 | A21 | 10.93.16.73 | /30 |
| Deus | eth2 | Switch10 | A8 | 10.93.14.129 | /25 |
| Protocol7 | eth0 | Deus | A21 | 10.93.16.74 | /30 |
| Protocol7 | eth1 | Knights | A22 | 10.93.16.77 | /30 |
| Protocol7 | eth2 | Switch11 | A10 | 10.93.15.65 | /26 |
| Knights | eth0 | Protocol7 | A22 | 10.93.16.78 | /30 |
| Knights | eth1 | Phantoma | A23 | 10.93.16.81 | /30 |
| Knights | eth2 | Eiri | A15 | 10.93.16.41 | /29 |
| Phantoma | eth0 | Knights | A23 | 10.93.16.82 | /30 |
| Phantoma | eth1 | Shibuya | A24 | 10.93.16.85 | /30 |
| Phantoma | eth2 | Switch12 | A13 | 10.93.16.1 | /27 |
| Shibuya | eth0 | Phantoma | A24 | 10.93.16.86 | /30 |
| Shibuya | eth1 | Switch13 | A11 | 10.93.15.129 | /26 |
| Psyche | eth0 | Switch2 | A14 | 10.93.16.34 | /29 |
| Psyche | eth1 | Switch3 | A1 | 10.93.0.1 | /22 |
| Copland | eth0 | Switch2 | A14 | 10.93.16.35 | /29 |
| Copland | eth1 | Juri | A12 | 10.93.15.193 | /26 |
| Copland | eth2 | Switch4 | A4 | 10.93.10.1 | /23 |
| Schumann | eth0 | Switch2 | A14 | 10.93.16.36 | /29 |
| Schumann | eth1 | Accela | A25 | 10.93.16.89 | /30 |
| Schumann | eth2 | Akashic | A16 | 10.93.16.49 | /29 |
| Accela | eth0 | Schumann | A25 | 10.93.16.90 | /30 |
| Accela | eth1 | Switch5 | A2 | 10.93.4.1 | /22 |

### Langkah 3: Routing

Routing memakai static route dengan prinsip berikut:

- Router ujung (Navi, Shibuya, Psyche, Copland, Accela) cukup memakai **default route** ke router di atasnya.
- Router tengah memakai **default route** ke atas dan route spesifik ke subnet di bawahnya.
- Route ke subnet di bawah satu cabang digabung (**summarization**) menjadi prefix yang lebih pendek selama blok-nya berurutan dan tidak ada alamat di luar subnet yang ikut tercakup.
- Cyberia memakai default route ke NAT (didapat dari DHCP) dan route ke seluruh jaringan internal lewat Wired.

Contoh summarization:

- A5 (`10.93.12.0/24`) + A6 (`10.93.13.0/24`) menjadi `10.93.12.0/23`.
- A1 (`10.93.0.0/22`) + A2 (`10.93.4.0/22`) menjadi `10.93.0.0/21`.
- A3 (`10.93.8.0/23`) + A4 (`10.93.10.0/23`) menjadi `10.93.8.0/22`.
- A21 (`10.93.16.72/30`) + A22 (`10.93.16.76/30`) menjadi `10.93.16.72/29`.

**Cyberia**

| Tujuan | Next Hop |
|---|---|
| 10.93.0.0/21 | 10.93.16.58 |
| 10.93.8.0/22 | 10.93.16.58 |
| 10.93.12.0/23 | 10.93.16.58 |
| 10.93.14.128/25 | 10.93.16.58 |
| 10.93.15.0/24 | 10.93.16.58 |
| 10.93.16.0/27 | 10.93.16.58 |
| 10.93.16.32/28 | 10.93.16.58 |
| 10.93.16.48/29 | 10.93.16.58 |
| 10.93.16.60/30 | 10.93.16.58 |
| 10.93.16.64/28 | 10.93.16.58 |
| 10.93.16.80/29 | 10.93.16.58 |
| 10.93.16.88/30 | 10.93.16.58 |
| 0.0.0.0/0 (default) | via DHCP NAT (192.168.122.1) |

**Wired**

| Tujuan | Next Hop |
|---|---|
| 10.93.12.0/23 | 10.93.16.62 |
| 10.93.15.0/26 | 10.93.16.62 |
| 10.93.8.0/23 | 10.93.16.66 |
| 10.93.14.128/25 | 10.93.16.66 |
| 10.93.15.64/26 | 10.93.16.66 |
| 10.93.15.128/26 | 10.93.16.66 |
| 10.93.16.0/27 | 10.93.16.66 |
| 10.93.16.40/29 | 10.93.16.66 |
| 10.93.16.68/30 | 10.93.16.66 |
| 10.93.16.72/29 | 10.93.16.66 |
| 10.93.16.80/29 | 10.93.16.66 |
| 10.93.0.0/22 | 10.93.16.34 |
| 10.93.10.0/23 | 10.93.16.35 |
| 10.93.15.192/26 | 10.93.16.35 |
| 10.93.4.0/22 | 10.93.16.36 |
| 10.93.16.48/29 | 10.93.16.36 |
| 10.93.16.88/30 | 10.93.16.36 |
| 0.0.0.0/0 (default) | 10.93.16.57 |

**Tachibana**

| Tujuan | Next Hop |
|---|---|
| 10.93.14.128/25 | 10.93.16.70 |
| 10.93.15.64/26 | 10.93.16.70 |
| 10.93.15.128/26 | 10.93.16.70 |
| 10.93.16.0/27 | 10.93.16.70 |
| 10.93.16.40/29 | 10.93.16.70 |
| 10.93.16.72/29 | 10.93.16.70 |
| 10.93.16.80/29 | 10.93.16.70 |
| 0.0.0.0/0 (default) | 10.93.16.65 |

**Deus**

| Tujuan | Next Hop |
|---|---|
| 10.93.15.64/26 | 10.93.16.74 |
| 10.93.15.128/26 | 10.93.16.74 |
| 10.93.16.0/27 | 10.93.16.74 |
| 10.93.16.40/29 | 10.93.16.74 |
| 10.93.16.76/30 | 10.93.16.74 |
| 10.93.16.80/29 | 10.93.16.74 |
| 0.0.0.0/0 (default) | 10.93.16.69 |

**Protocol7**

| Tujuan | Next Hop |
|---|---|
| 10.93.15.128/26 | 10.93.16.78 |
| 10.93.16.0/27 | 10.93.16.78 |
| 10.93.16.40/29 | 10.93.16.78 |
| 10.93.16.80/29 | 10.93.16.78 |
| 0.0.0.0/0 (default) | 10.93.16.73 |

**Knights**

| Tujuan | Next Hop |
|---|---|
| 10.93.15.128/26 | 10.93.16.82 |
| 10.93.16.0/27 | 10.93.16.82 |
| 10.93.16.84/30 | 10.93.16.82 |
| 0.0.0.0/0 (default) | 10.93.16.77 |

**Phantoma**

| Tujuan | Next Hop |
|---|---|
| 10.93.15.128/26 | 10.93.16.86 |
| 0.0.0.0/0 (default) | 10.93.16.81 |

**Schumann**

| Tujuan | Next Hop |
|---|---|
| 10.93.4.0/22 | 10.93.16.90 |
| 0.0.0.0/0 (default) | 10.93.16.33 |

**Navi, Shibuya, Psyche, Copland, Accela**

| Router | Default Route (Next Hop) |
|---|---|
| Navi | 10.93.16.61 |
| Shibuya | 10.93.16.85 |
| Psyche | 10.93.16.33 |
| Copland | 10.93.16.33 |
| Accela | 10.93.16.89 |

### Langkah 4: Konfigurasi Router di GNS3

Konfigurasi dimasukkan lewat klik kanan node, **Configure**, lalu **Edit network configuration**. Isi bawaan (yang di-comment) dihapus dan diganti dengan konfigurasi di bawah, kemudian node di-stop dan di-start ulang. Baris `up` menjalankan perintah setelah interface aktif, yaitu mengaktifkan IP forwarding dan memasang static route.

<details>
<summary>Cyberia</summary>

```
auto eth0
iface eth0 inet dhcp
    up iptables -t nat -A POSTROUTING -s 10.93.0.0/19 -o eth0 -j MASQUERADE
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.93.16.57
    netmask 255.255.255.252
    up ip route replace 10.93.0.0/21 via 10.93.16.58
    up ip route replace 10.93.8.0/22 via 10.93.16.58
    up ip route replace 10.93.12.0/23 via 10.93.16.58
    up ip route replace 10.93.14.128/25 via 10.93.16.58
    up ip route replace 10.93.15.0/24 via 10.93.16.58
    up ip route replace 10.93.16.0/27 via 10.93.16.58
    up ip route replace 10.93.16.32/28 via 10.93.16.58
    up ip route replace 10.93.16.48/29 via 10.93.16.58
    up ip route replace 10.93.16.60/30 via 10.93.16.58
    up ip route replace 10.93.16.64/28 via 10.93.16.58
    up ip route replace 10.93.16.80/29 via 10.93.16.58
    up ip route replace 10.93.16.88/30 via 10.93.16.58

auto eth2
iface eth2 inet static
    address 10.93.14.1
    netmask 255.255.255.128
```

</details>

<details>
<summary>Wired</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.33
    netmask 255.255.255.248
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace 10.93.0.0/22 via 10.93.16.34
    up ip route replace 10.93.10.0/23 via 10.93.16.35
    up ip route replace 10.93.15.192/26 via 10.93.16.35
    up ip route replace 10.93.4.0/22 via 10.93.16.36
    up ip route replace 10.93.16.48/29 via 10.93.16.36
    up ip route replace 10.93.16.88/30 via 10.93.16.36

auto eth1
iface eth1 inet static
    address 10.93.16.58
    netmask 255.255.255.252
    up ip route replace default via 10.93.16.57

auto eth2
iface eth2 inet static
    address 10.93.16.65
    netmask 255.255.255.252
    up ip route replace 10.93.8.0/23 via 10.93.16.66
    up ip route replace 10.93.14.128/25 via 10.93.16.66
    up ip route replace 10.93.15.64/26 via 10.93.16.66
    up ip route replace 10.93.15.128/26 via 10.93.16.66
    up ip route replace 10.93.16.0/27 via 10.93.16.66
    up ip route replace 10.93.16.40/29 via 10.93.16.66
    up ip route replace 10.93.16.68/30 via 10.93.16.66
    up ip route replace 10.93.16.72/29 via 10.93.16.66
    up ip route replace 10.93.16.80/29 via 10.93.16.66

auto eth3
iface eth3 inet static
    address 10.93.16.61
    netmask 255.255.255.252
    up ip route replace 10.93.12.0/23 via 10.93.16.62
    up ip route replace 10.93.15.0/26 via 10.93.16.62
```

</details>

<details>
<summary>Navi</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.62
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.61

auto eth1
iface eth1 inet static
    address 10.93.12.1
    netmask 255.255.255.0

auto eth2
iface eth2 inet static
    address 10.93.15.1
    netmask 255.255.255.192

auto eth3
iface eth3 inet static
    address 10.93.13.1
    netmask 255.255.255.0
```

</details>

<details>
<summary>Tachibana</summary>

```
auto eth1
iface eth1 inet static
    address 10.93.16.69
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace 10.93.14.128/25 via 10.93.16.70
    up ip route replace 10.93.15.64/26 via 10.93.16.70
    up ip route replace 10.93.15.128/26 via 10.93.16.70
    up ip route replace 10.93.16.0/27 via 10.93.16.70
    up ip route replace 10.93.16.40/29 via 10.93.16.70
    up ip route replace 10.93.16.72/29 via 10.93.16.70
    up ip route replace 10.93.16.80/29 via 10.93.16.70

auto eth2
iface eth2 inet static
    address 10.93.16.66
    netmask 255.255.255.252
    up ip route replace default via 10.93.16.65

auto eth3
iface eth3 inet static
    address 10.93.8.1
    netmask 255.255.254.0
```

</details>

<details>
<summary>Deus</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.70
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.69

auto eth1
iface eth1 inet static
    address 10.93.16.73
    netmask 255.255.255.252
    up ip route replace 10.93.15.64/26 via 10.93.16.74
    up ip route replace 10.93.15.128/26 via 10.93.16.74
    up ip route replace 10.93.16.0/27 via 10.93.16.74
    up ip route replace 10.93.16.40/29 via 10.93.16.74
    up ip route replace 10.93.16.76/30 via 10.93.16.74
    up ip route replace 10.93.16.80/29 via 10.93.16.74

auto eth2
iface eth2 inet static
    address 10.93.14.129
    netmask 255.255.255.128
```

</details>

<details>
<summary>Protocol7</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.74
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.73

auto eth1
iface eth1 inet static
    address 10.93.16.77
    netmask 255.255.255.252
    up ip route replace 10.93.15.128/26 via 10.93.16.78
    up ip route replace 10.93.16.0/27 via 10.93.16.78
    up ip route replace 10.93.16.40/29 via 10.93.16.78
    up ip route replace 10.93.16.80/29 via 10.93.16.78

auto eth2
iface eth2 inet static
    address 10.93.15.65
    netmask 255.255.255.192
```

</details>

<details>
<summary>Knights</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.78
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.77

auto eth1
iface eth1 inet static
    address 10.93.16.81
    netmask 255.255.255.252
    up ip route replace 10.93.15.128/26 via 10.93.16.82
    up ip route replace 10.93.16.0/27 via 10.93.16.82
    up ip route replace 10.93.16.84/30 via 10.93.16.82

auto eth2
iface eth2 inet static
    address 10.93.16.41
    netmask 255.255.255.248
```

</details>

<details>
<summary>Phantoma</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.82
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.81

auto eth1
iface eth1 inet static
    address 10.93.16.85
    netmask 255.255.255.252
    up ip route replace 10.93.15.128/26 via 10.93.16.86

auto eth2
iface eth2 inet static
    address 10.93.16.1
    netmask 255.255.255.224
```

</details>

<details>
<summary>Shibuya</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.86
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.85

auto eth1
iface eth1 inet static
    address 10.93.15.129
    netmask 255.255.255.192
```

</details>

<details>
<summary>Psyche</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.34
    netmask 255.255.255.248
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.33

auto eth1
iface eth1 inet static
    address 10.93.0.1
    netmask 255.255.252.0
```

</details>

<details>
<summary>Copland</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.35
    netmask 255.255.255.248
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.33

auto eth1
iface eth1 inet static
    address 10.93.15.193
    netmask 255.255.255.192

auto eth2
iface eth2 inet static
    address 10.93.10.1
    netmask 255.255.254.0
```

</details>

<details>
<summary>Schumann</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.36
    netmask 255.255.255.248
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.33

auto eth1
iface eth1 inet static
    address 10.93.16.89
    netmask 255.255.255.252
    up ip route replace 10.93.4.0/22 via 10.93.16.90

auto eth2
iface eth2 inet static
    address 10.93.16.49
    netmask 255.255.255.248
```

</details>

<details>
<summary>Accela</summary>

```
auto eth0
iface eth0 inet static
    address 10.93.16.90
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1
    up ip route replace default via 10.93.16.89

auto eth1
iface eth1 inet static
    address 10.93.4.1
    netmask 255.255.252.0
```

</details>

### Langkah 5: Konfigurasi Host di GNS3

Tiap host dikonfigurasi dengan cara yang sama (Edit network configuration). Contoh untuk Karl:

```
auto eth0
iface eth0 inet static
    address 10.93.0.2
    netmask 255.255.252.0
    gateway 10.93.0.1
```

Daftar seluruh host:

| Host | Interface | IP Address | Netmask | Gateway | Subnet |
|---|---|---|---|---|---|
| Karl | eth0 | 10.93.0.2 | 255.255.252.0 | 10.93.0.1 | A1 |
| Lin | eth0 | 10.93.0.3 | 255.255.252.0 | 10.93.0.1 | A1 |
| Omnipresence | eth0 | 10.93.4.2 | 255.255.252.0 | 10.93.4.1 | A2 |
| Denpa | eth0 | 10.93.4.3 | 255.255.252.0 | 10.93.4.1 | A2 |
| Collective | eth0 | 10.93.8.2 | 255.255.254.0 | 10.93.8.1 | A3 |
| Ghost | eth0 | 10.93.8.3 | 255.255.254.0 | 10.93.8.1 | A3 |
| Masayuki | eth0 | 10.93.10.2 | 255.255.254.0 | 10.93.10.1 | A4 |
| Alice | eth0 | 10.93.12.2 | 255.255.255.0 | 10.93.12.1 | A5 |
| Reika | eth1 | 10.93.12.3 | 255.255.255.0 | 10.93.12.1 | A5 |
| Yasuo | eth0 | 10.93.13.2 | 255.255.255.0 | 10.93.13.1 | A6 |
| Miho | eth0 | 10.93.13.3 | 255.255.255.0 | 10.93.13.1 | A6 |
| Kuma | eth0 | 10.93.13.4 | 255.255.255.0 | 10.93.13.1 | A6 |
| JJ | eth1 | 10.93.14.2 | 255.255.255.128 | 10.93.14.1 | A7 |
| MyuMyu | eth1 | 10.93.14.3 | 255.255.255.128 | 10.93.14.1 | A7 |
| Lilith | eth0 | 10.93.14.130 | 255.255.255.128 | 10.93.14.129 | A8 |
| Specter | eth0 | 10.93.14.131 | 255.255.255.128 | 10.93.14.129 | A8 |
| Taro | eth1 | 10.93.15.2 | 255.255.255.192 | 10.93.15.1 | A9 |
| Chisa | eth0 | 10.93.15.66 | 255.255.255.192 | 10.93.15.65 | A10 |
| Hodgeson | eth0 | 10.93.15.67 | 255.255.255.192 | 10.93.15.65 | A10 |
| Lain | eth0 | 10.93.15.130 | 255.255.255.192 | 10.93.15.129 | A11 |
| Mika | eth0 | 10.93.15.131 | 255.255.255.192 | 10.93.15.129 | A11 |
| Juri | eth0 | 10.93.15.194 | 255.255.255.192 | 10.93.15.193 | A12 |
| Semi | eth0 | 10.93.16.2 | 255.255.255.224 | 10.93.16.1 | A13 |
| Eiri | eth0 | 10.93.16.42 | 255.255.255.248 | 10.93.16.41 | A15 |
| Akashic | eth0 | 10.93.16.50 | 255.255.255.248 | 10.93.16.49 | A16 |

### Pengujian

Pengujian dilakukan dengan `ping` ke seluruh IP host dan seluruh IP interface router (62 alamat) dari tiap node. Loop berikut dipaste di console node dan hanya menampilkan alamat yang gagal:

```
f=0; for ip in 10.93.0.2 10.93.0.3 10.93.4.2 10.93.4.3 10.93.8.2 10.93.8.3 10.93.10.2 10.93.12.2 10.93.12.3 10.93.13.2 10.93.13.3 10.93.13.4 10.93.14.2 10.93.14.3 10.93.14.130 10.93.14.131 10.93.15.2 10.93.15.66 10.93.15.67 10.93.15.130 10.93.15.131 10.93.15.194 10.93.16.2 10.93.16.42 10.93.16.50 10.93.0.1 10.93.4.1 10.93.8.1 10.93.10.1 10.93.12.1 10.93.13.1 10.93.14.1 10.93.14.129 10.93.15.1 10.93.15.65 10.93.15.129 10.93.15.193 10.93.16.1 10.93.16.33 10.93.16.34 10.93.16.35 10.93.16.36 10.93.16.41 10.93.16.49 10.93.16.57 10.93.16.58 10.93.16.61 10.93.16.62 10.93.16.65 10.93.16.66 10.93.16.69 10.93.16.70 10.93.16.73 10.93.16.74 10.93.16.77 10.93.16.78 10.93.16.81 10.93.16.82 10.93.16.85 10.93.16.86 10.93.16.89 10.93.16.90; do ping -c 1 -W 2 $ip >/dev/null 2>&1 || { echo "GAGAL: $ip"; f=$((f+1)); }; done; [ $f -eq 0 ] && echo "SEMUA 62 IP OK" || echo "$f IP GAGAL"
```

Hasil ping ke seluruh host:
<img width="1110" height="831" alt="image" src="https://github.com/user-attachments/assets/3446ae61-8c1c-46d5-b8a2-80d2bfcaf1ae" />

## CIDR
<br><img width="1919" height="645" alt="image" src="https://github.com/user-attachments/assets/f2e4b018-719d-4b45-b0e5-ecb41201befd" />
<img width="1919" height="645" alt="image" src="https://github.com/user-attachments/assets/79834ad5-6f24-444a-ad7f-cb1286820092" /><br>

<br><img width="1919" height="915" alt="image" src="https://github.com/user-attachments/assets/482d8a47-088f-4bea-9bda-aa56eea71ad8" />
<img width="1919" height="911" alt="image" src="https://github.com/user-attachments/assets/3260b841-e59f-4163-8c84-7cc92766ddbc" /><br>
  
### Tabel koneksi

| Asal | Interface | Tujuan | Interface |
|---|---|---|---|
| Cloud0 | Fa0 | R-Cyberia | Fa0/0 |
| R-Cyberia | Fa0/1 | Switch1 | Fa0/1 |
| Switch1 | Fa1/1 | JJ | Fa0 |
| Switch1 | Fa2/1 | MyuMyu | Fa0 |
| R-Cyberia | Fa1/0 | R-Wired | Fa0/0 |
| R-Wired | Fa0/1 | R-Navi | Fa0/0 |
| R-Navi | Fa0/1 | Switch6 | Fa0/1 |
| R-Navi | Fa1/0 | Switch7 | Fa0/1 |
| R-Navi | Fa1/1 | Switch8 | Fa0/1 |
| Switch6 | Fa1/1 | Alice | Fa0 |
| Switch6 | Fa2/1 | Reika | Fa0 |
| Switch7 | Fa1/1 | Taro | Fa0 |
| Switch8 | Fa1/1 | ServerKuma | Fa0 |
| Switch8 | Fa2/1 | Miho | Fa0 |
| Switch8 | Fa3/1 | Yasuo | Fa0 |
| R-Wired | Fa1/0 | R-Tachibana | Fa0/0 |
| R-Tachibana | Fa0/1 | R-Deus | Fa0/0 |
| R-Tachibana | Fa1/0 | Switch9 | Fa0/1 |
| Switch9 | Fa1/1 | Ghost | Fa0 |
| Switch9 | Fa2/1 | ServerCollective | Fa0 |
| R-Deus | Fa0/1 | Switch10 | Fa0/1 |
| Switch10 | Fa1/1 | Lilith | Fa0 |
| Switch10 | Fa2/1 | Specter | Fa0 |
| R-Deus | Fa1/0 | R-Protocol7 | Fa0/0 |
| R-Protocol7 | Fa1/0 | Switch11 | Fa0/1 |
| Switch11 | Fa1/1 | Hodgeson | Fa0 |
| Switch11 | Fa2/1 | Chisa | Fa0 |
| R-Protocol7 | Fa0/1 | R-Knights | Fa0/0 |
| R-Knights | Fa0/1 | ServerEri | Fa0 |
| R-Knights | Fa1/0 | R-Phamoma | Fa0/0 |
| R-Phamoma | Fa0/1 | R-Shibuya | Fa0/0 |
| R-Shibuya | Fa0/1 | Switch13 | Fa0/1 |
| Switch13 | Fa1/1 | Mika | Fa0 |
| Switch13 | Fa2/1 | Lain | Fa0 |
| R-Phamoma | Fa1/0 | Switch12 | Fa0/1 |
| Switch12 | Fa1/1 | Semi | Fa0 |
| R-Wired | Fa1/1 | Switch2 | Fa0/1 |
| Switch2 | Fa1/1 | R-Schumann | Fa0/0 |
| R-Schumann | Fa0/1 | R-Accela | Fa0/0 |
| R-Accela | Fa0/1 | ServerAkashic | Fa0 |
| R-Accela | Fa1/0 | Switch5 | Fa0/1 |
| Switch5 | Fa1/1 | Denpa | Fa0 |
| Switch5 | Fa2/1 | Omnipresence | Fa0 |
| Switch2 | Fa2/1 | R-Copland | Fa0/0 |
| R-Copland | Fa0/1 | Switch4 | Fa0/1 |
| Switch4 | Fa1/1 | Masayuki | Fa0 |
| R-Copland | Fa1/0 | Juri | Fa0 |
| Switch2 | Fa3/1 | R-Psyche | Fa0/0 |
| R-Psyche | Fa0/1 | Switch3 | Fa0/1 |
| Switch3 | Fa1/1 | ServerLin | Fa0 |
| Switch3 | Fa2/1 | ServerKarl | Fa0 |

### Konfigurasi

<details>
<summary><strong>R-Cyberia</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Cyberia
interface fastEthernet0/0
 no shutdown
interface fastEthernet0/1
 ip address 10.93.11.1 255.255.255.128
 no shutdown
interface fastEthernet1/0
 ip address 10.93.11.129 255.255.255.252
 no shutdown
ip route 0.0.0.0 0.0.0.0 10.93.11.130
end
write memory
```

</details>

<details>
<summary><strong>R-Wired</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Wired
interface fastEthernet0/0
 ip address 10.93.11.130 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.9.65 255.255.255.252
 no shutdown
interface fastEthernet1/0
 ip address 10.93.9.69 255.255.255.252
 no shutdown
interface fastEthernet1/1
 ip address 10.93.2.65 255.255.255.248
 no shutdown
ip route 10.93.11.0 255.255.255.128 10.93.11.129
ip route 10.93.8.0 255.255.254.0 10.93.9.66
ip route 10.93.10.0 255.255.255.0 10.93.9.66
ip route 10.93.16.0 255.255.252.0 10.93.9.70
ip route 10.93.0.0 255.255.254.0 10.93.2.67
ip route 10.93.2.0 255.255.255.192 10.93.2.67
ip route 10.93.4.0 255.255.252.0 10.93.2.68
ip route 10.93.2.72 255.255.255.252 10.93.2.66
ip route 10.93.2.80 255.255.255.248 10.93.2.66
ip route 10.93.20.0 255.255.252.0 10.93.2.66
end
write memory
```

</details>

<details>
<summary><strong>R-Navi</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Navi
interface fastEthernet0/0
 ip address 10.93.9.66 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.10.1 255.255.255.0
 no shutdown
interface fastEthernet1/0
 ip address 10.93.9.1 255.255.255.192
 no shutdown
interface fastEthernet1/1
 ip address 10.93.8.1 255.255.255.0
 no shutdown
ip route 0.0.0.0 0.0.0.0 10.93.9.65
end
write memory
```

</details>

<details>
<summary><strong>R-Tachibana</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Tachibana
interface fastEthernet0/0
 ip address 10.93.9.70 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.16.65 255.255.255.252
 no shutdown
interface fastEthernet1/0
 ip address 10.93.18.1 255.255.254.0
 no shutdown
ip route 10.93.16.0 255.255.254.0 10.93.16.66
ip route 0.0.0.0 0.0.0.0 10.93.9.69
end
write memory
```

</details>

<details>
<summary><strong>R-Deus</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Deus
interface fastEthernet0/0
 ip address 10.93.16.66 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.16.129 255.255.255.128
 no shutdown
interface fastEthernet1/0
 ip address 10.93.16.69 255.255.255.252
 no shutdown
ip route 10.93.16.0 255.255.255.192 10.93.16.70
ip route 10.93.17.0 255.255.255.0 10.93.16.70
ip route 0.0.0.0 0.0.0.0 10.93.16.65
end
write memory
```

</details>

<details>
<summary><strong>R-Protocol7</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Protocol7
interface fastEthernet0/0
 ip address 10.93.16.70 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.17.137 255.255.255.252
 no shutdown
interface fastEthernet1/0
 ip address 10.93.16.1 255.255.255.192
 no shutdown
ip route 10.93.17.0 255.255.255.0 10.93.17.138
ip route 0.0.0.0 0.0.0.0 10.93.16.69
end
write memory
```

</details>

<details>
<summary><strong>R-Knights</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Knights
interface fastEthernet0/0
 ip address 10.93.17.138 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.17.129 255.255.255.248
 no shutdown
interface fastEthernet1/0
 ip address 10.93.17.141 255.255.255.252
 no shutdown
ip route 10.93.17.0 255.255.255.128 10.93.17.142
ip route 0.0.0.0 0.0.0.0 10.93.17.137
end
write memory
```

</details>

<details>
<summary><strong>R-Phamoma</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Phamoma
interface fastEthernet0/0
 ip address 10.93.17.142 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.17.97 255.255.255.252
 no shutdown
interface fastEthernet1/0
 ip address 10.93.17.65 255.255.255.224
 no shutdown
ip route 10.93.17.0 255.255.255.192 10.93.17.98
ip route 0.0.0.0 0.0.0.0 10.93.17.141
end
write memory
```

</details>

<details>
<summary><strong>R-Shibuya</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Shibuya
interface fastEthernet0/0
 ip address 10.93.17.98 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.17.1 255.255.255.192
 no shutdown
ip route 0.0.0.0 0.0.0.0 10.93.17.97
end
write memory
```

</details>

<details>
<summary><strong>R-Schumann</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Schumann
interface fastEthernet0/0
 ip address 10.93.2.66 255.255.255.248
 no shutdown
interface fastEthernet0/1
 ip address 10.93.2.73 255.255.255.252
 no shutdown
ip route 10.93.20.0 255.255.252.0 10.93.2.74
ip route 10.93.2.80 255.255.255.248 10.93.2.74
ip route 0.0.0.0 0.0.0.0 10.93.2.65
end
write memory
```

</details>

<details>
<summary><strong>R-Accela</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Accela
interface fastEthernet0/0
 ip address 10.93.2.74 255.255.255.252
 no shutdown
interface fastEthernet0/1
 ip address 10.93.2.81 255.255.255.248
 no shutdown
interface fastEthernet1/0
 ip address 10.93.20.1 255.255.252.0
 no shutdown
ip route 0.0.0.0 0.0.0.0 10.93.2.73
end
write memory
```

</details>

<details>
<summary><strong>R-Copland</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Copland
interface fastEthernet0/0
 ip address 10.93.2.67 255.255.255.248
 no shutdown
interface fastEthernet0/1
 ip address 10.93.0.1 255.255.254.0
 no shutdown
interface fastEthernet1/0
 ip address 10.93.2.1 255.255.255.192
 no shutdown
ip route 0.0.0.0 0.0.0.0 10.93.2.65
end
write memory
```

</details>

<details>
<summary><strong>R-Psyche</strong></summary>

<br>

```cisco
enable
configure terminal
hostname R-Psyche
interface fastEthernet0/0
 ip address 10.93.2.68 255.255.255.248
 no shutdown
interface fastEthernet0/1
 ip address 10.93.4.1 255.255.252.0
 no shutdown
ip route 0.0.0.0 0.0.0.0 10.93.2.65
end
write memory
```

</details>


### Tabel host

| Node | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| JJ | 10.93.11.2 | 255.255.255.128 | 10.93.11.1 |
| MyuMyu | 10.93.11.3 | 255.255.255.128 | 10.93.11.1 |
| Alice | 10.93.10.2 | 255.255.255.0 | 10.93.10.1 |
| Reika | 10.93.10.3 | 255.255.255.0 | 10.93.10.1 |
| Taro | 10.93.9.2 | 255.255.255.192 | 10.93.9.1 |
| ServerKuma | 10.93.8.2 | 255.255.255.0 | 10.93.8.1 |
| Miho | 10.93.8.3 | 255.255.255.0 | 10.93.8.1 |
| Yasuo | 10.93.8.4 | 255.255.255.0 | 10.93.8.1 |
| ServerCollective | 10.93.18.2 | 255.255.254.0 | 10.93.18.1 |
| Ghost | 10.93.18.3 | 255.255.254.0 | 10.93.18.1 |
| Lilith | 10.93.16.130 | 255.255.255.128 | 10.93.16.129 |
| Specter | 10.93.16.131 | 255.255.255.128 | 10.93.16.129 |
| Hodgeson | 10.93.16.2 | 255.255.255.192 | 10.93.16.1 |
| Chisa | 10.93.16.3 | 255.255.255.192 | 10.93.16.1 |
| ServerEri | 10.93.17.130 | 255.255.255.248 | 10.93.17.129 |
| Semi | 10.93.17.66 | 255.255.255.224 | 10.93.17.65 |
| Mika | 10.93.17.2 | 255.255.255.192 | 10.93.17.1 |
| Lain | 10.93.17.3 | 255.255.255.192 | 10.93.17.1 |
| ServerAkashic | 10.93.2.82 | 255.255.255.248 | 10.93.2.81 |
| Denpa | 10.93.20.2 | 255.255.252.0 | 10.93.20.1 |
| Omnipresence | 10.93.20.3 | 255.255.252.0 | 10.93.20.1 |
| Masayuki | 10.93.0.2 | 255.255.254.0 | 10.93.0.1 |
| Juri | 10.93.2.2 | 255.255.255.192 | 10.93.2.1 |
| ServerKarl | 10.93.4.2 | 255.255.252.0 | 10.93.4.1 |
| ServerLin | 10.93.4.3 | 255.255.252.0 | 10.93.4.1 |

### Testing 

#### Komunikasi satu subnet
JJ ke MyuMyu
```
ping 10.93.11.3
```
<br><img width="473" height="228" alt="image" src="https://github.com/user-attachments/assets/786b1e5e-9f81-4a90-a635-50fb8778081c" /><br>

#### Komunikasi antarsubnet
JJ ke Alice
```
ping 10.93.10.2
```
<br><img width="479" height="211" alt="image" src="https://github.com/user-attachments/assets/633d170c-4ada-4508-b72e-0af46c2783a7" /><br>

#### Ping antarnode paling jauh
Server Lin ke Mika
```
ping 10.93.17.2
```
<br><img width="497" height="211" alt="image" src="https://github.com/user-attachments/assets/754b1ca2-62cc-4cd3-9f61-e635bdd04be9" /><br>
<br><img width="469" height="236" alt="image" src="https://github.com/user-attachments/assets/779a6b83-92a3-4138-9da3-24e367e678ff" /><br>

**Hasil Traceroute**
  
| Hop | IP Address   | Node        | Keterangan                |
| --- | ------------ | ----------- | ------------------------- |
| 1   | 10.93.4.1    | R-Psyche    | Default gateway ServerLin |
| 2   | 10.93.2.65   | R-Wired     | Router pusat              |
| 3   | 10.93.9.70   | R-Tachibana | Menuju cabang R-Deus      |
| 4   | 10.93.16.66  | R-Deus      | Menuju R-Protocol7        |
| 5   | 10.93.16.70  | R-Protocol7 | Menuju R-Knights          |
| 6   | 10.93.17.138 | R-Knights   | Menuju R-Phamoma          |
| 7   | 10.93.17.142 | R-Phamoma   | Menuju R-Shibuya          |
| 8   | 10.93.17.98  | R-Shibuya   | Gateway jaringan Mika     |
| 9   | 10.93.17.2   | Mika        | Host tujuan               |

#### Hanya Cyberia yang Terhubung ke NAT/Cloud

Untuk memenuhi persyaratan bahwa R-Cyberia merupakan satu-satunya router yang terhubung langsung ke NAT/Cloud, dilakukan penambahan perangkat **Cable Modem** dan **R-ISP** sebagai simulasi jaringan eksternal  
  
Cable Modem berfungsi menghubungkan Cloud0 dengan R-ISP melalui kabel Coaxial dan Copper Straight-Through. Pada Cloud0, ditambahkan modul port Coaxial serta konfigurasi koneksi Cable agar trafik dapat diteruskan antara R-Cyberia dan R-ISP  
  
R-ISP dikonfigurasi menggunakan IP `203.0.113.1/30` pada interface Fa0/0 dan IP `198.51.100.10/32` pada Loopback0 sebagai alamat tujuan pengujian jaringan eksternal. Sementara itu, R-Cyberia menggunakan IP `203.0.113.2/30` pada Fa0/0 serta konfigurasi NAT Overload agar perangkat dalam jaringan internal dapat mengakses jaringan eksternal melalui satu alamat IP keluar  
  
Selain itu, default route pada R-Wired diarahkan menuju R-Cyberia, sedangkan default route R-Cyberia diarahkan menuju R-ISP. Dengan konfigurasi tersebut, seluruh trafik menuju jaringan eksternal diarahkan melalui R-Cyberia sebagai satu-satunya gerbang keluar jaringan internal  
  
**1. Pengujian Koneksi R-Cyberia ke R-ISP**

```bash
! Node R-Cyberia
ping 203.0.113.1
```

<br><img width="585" height="98" alt="image" src="https://github.com/user-attachments/assets/de365c13-f9d5-41d2-8086-9a0504786d5f" /><br>


**Keterangan:** Pengujian menunjukkan bahwa R-Cyberia berhasil melakukan ping ke IP `203.0.113.1` . Ini membuktikan bahwa koneksi antara R-Cyberia dan R-ISP melalui Cloud0 dan Cable Modem telah berfungsi dengan baik

**2. Pengujian Koneksi R-Cyberia ke Jaringan Eksternal**

```bash
! Node R-Cyberia
ping 198.51.100.10
```

<br><img width="582" height="109" alt="image" src="https://github.com/user-attachments/assets/cde439eb-a615-4fbb-b7d6-9dc4ad5f751d" /><br>


**Keterangan:** Pengujian menunjukkan bahwa R-Cyberia berhasil menjangkau IP `198.51.100.10`, yaitu alamat Loopback0 pada R-ISP yang digunakan sebagai simulasi tujuan eksternal. Keberhasilan ping membuktikan bahwa R-Cyberia dapat meneruskan paket menuju jaringan eksternal melalui Cloud0. Pengujian ini juga memastikan bahwa alamat tujuan eksternal dapat dijangkau sebelum dilakukan pengujian dari host internal.

**3. Pengujian Akses Jaringan Eksternal dari ServerLin**

```bash
! Node ServerLin
ping 198.51.100.10
```

<br><img width="463" height="207" alt="image" src="https://github.com/user-attachments/assets/cc4c79ec-f8e1-4b73-99dd-4cf5a45f605f" /><br>


**Keterangan:** Pengujian menunjukkan bahwa ServerLin (`10.93.4.3`) berhasil melakukan ping ke IP eksternal `198.51.100.10`. Paket dari ServerLin diteruskan melalui R-Psyche, R-Wired, dan R-Cyberia sebelum mencapai R-ISP.

Keberhasilan pengujian ini membuktikan bahwa perangkat pada jaringan internal dapat mengakses jaringan eksternal melalui R-Cyberia. Dengan demikian, R-Cyberia berfungsi sebagai gerbang utama menuju Cloud tanpa memerlukan koneksi Cloud langsung pada router internal lainnya.

**Kesimpulan**

Ketiga pengujian menunjukkan bahwa koneksi antara jaringan internal dan jaringan eksternal telah berfungsi. R-Cyberia berhasil terhubung ke R-ISP melalui Cloud0, serta mampu meneruskan komunikasi dari ServerLin menuju jaringan eksternal. Dengan topologi yang hanya menghubungkan R-Cyberia secara langsung ke Cloud0, persyaratan bahwa R-Cyberia menjadi satu-satunya router internal yang terhubung ke NAT/Cloud telah terpenuhi.




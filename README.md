# Tiga Sebaris — Tic-Tac-Toe dalam Bahasa Indonesiaku

Game **Tic-Tac-Toe** di terminal untuk melawan komputer. Seluruh kodenya ditulis
dengan [**Indonesiaku**](https://github.com/teguh02/Indonesiaku-Lang), bahasa
pemrograman berkata kunci Bahasa Indonesia yang semantiknya mengikuti Python dan
bloknya memakai kurung kurawal `{ }`.

```
 X | 2 | O
---+---+---
 4 | X | 6
---+---+---
 7 | 8 | O
```

## Fitur

- **Dua level kesulitan**
  - **Mudah**: komputer memilih kotak secara acak.
  - **Sulit**: komputer memakai algoritma **minimax**, jadi tidak bisa dikalahkan.
    Hasil terbaikmu adalah seri.
- **Papan dengan petunjuk**: kotak yang masih kosong menampilkan nomornya (1–9).
- **Papan skor** (menang, kalah, seri) yang terus dihitung selama sesi.
- **Giliran pertama bergantian** setiap ronde antara kamu dan komputer.
- **Validasi masukan**: masukan yang tidak valid atau kotak yang sudah terisi
  ditolak dengan pesan yang jelas.

## Pemasangan

### 1. Pasang interpreter Indonesiaku

**Windows**

1. Unduh `indk-windows.zip` dari
   [halaman rilis Indonesiaku](https://github.com/teguh02/Indonesiaku-Lang/releases/latest).
2. Ekstrak ke sebuah folder, misalnya `C:\Indonesiaku\`. Folder `pustaka\` harus
   tetap berada di samping `indk.exe`.
3. Tambahkan folder tersebut ke PATH (PowerShell):

   ```powershell
   [Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Indonesiaku", "User")
   ```

4. Buka **terminal baru**, lalu periksa:

   ```powershell
   indk -v
   ```

> Jika SmartScreen atau Defender memblokir `indk.exe`, klik kanan file itu, pilih
> **Properties**, centang **Unblock**, lalu klik **OK**.

**Linux / macOS**

```bash
# Ganti "linux" dengan "macos" untuk macOS
curl -LO https://github.com/teguh02/Indonesiaku-Lang/releases/latest/download/indk-linux.tar.gz
tar -xzf indk-linux.tar.gz
# Pindahkan isi folder hasil ekstrak ke lokasi pilihanmu, lalu tambahkan ke PATH
```

**Docker** (tanpa memasang apa pun):

```bash
docker run --rm -it -v "$PWD:/kode" teguh02/indonesiaku /kode/tictactoe/tiga_sebaris.idk
```

Panduan instalasi lengkap ada di
[02_INSTALASI.md](https://github.com/teguh02/Indonesiaku-Lang/blob/main/website/panduan/02_INSTALASI.md).

### 2. Unduh proyek ini

```bash
git clone <url-repo-ini>
cd <nama-folder-repo>
```

## Cara Menjalankan

```bash
cd tictactoe
indk tiga_sebaris.idk
```

## Cara Bermain

Kamu bermain sebagai **X**, komputer sebagai **O**. Siapa pun yang lebih dulu
membentuk tiga simbol sebaris (mendatar, menurun, atau diagonal) menang.

| Masukan | Aksi |
|---|---|
| `1` / `2` | Pilih level di awal (mudah / sulit) |
| `1`–`9` | Isi kotak sesuai nomor |
| `q` | Keluar saat giliranmu |
| `y` / `n` | Main lagi atau berhenti setelah ronde selesai |

Nomor kotak:

```
 1 | 2 | 3
---+---+---
 4 | 5 | 6
---+---+---
 7 | 8 | 9
```

## Cara Kerja Kode

Semua logika ada di [`tictactoe/tiga_sebaris.idk`](tictactoe/tiga_sebaris.idk).

| Fungsi | Tugas |
|---|---|
| `gambar(papan)` | Mencetak papan 3×3 ke terminal |
| `pemenang(papan)` | Memeriksa 8 garis menang; mengembalikan `"X"`, `"O"`, `"seri"`, atau `""` |
| `kotak_kosong(papan)` | Daftar indeks kotak yang masih kosong |
| `minimax(papan, giliran_o, kedalaman)` | Menilai posisi secara rekursif dari sudut pandang komputer |
| `langkah_komputer(papan, level)` | Memilih langkah acak (mudah) atau langkah dengan skor minimax tertinggi (sulit) |
| `langkah_pemain(papan)` | Membaca dan memvalidasi masukan pemain |
| `main_ronde(level, pemain_duluan)` | Menjalankan satu ronde sampai ada pemenang atau seri |

**Minimax** mencoba setiap kemungkinan langkah sampai permainan berakhir.
Kemenangan komputer bernilai `10 - kedalaman`, kekalahan bernilai
`kedalaman - 10`, dan seri bernilai `0`. Dengan memperhitungkan `kedalaman`,
komputer memilih kemenangan tercepat dan menunda kekalahan selama mungkin.

Papan disimpan sebagai daftar 9 teks:

```indonesiaku
papan = [" ", " ", " ", " ", " ", " ", " ", " ", " "]
papan[4] = "X"     # kotak tengah (nomor 5)
```

## Struktur Proyek

```
.
├── README.md
└── tictactoe/
    └── tiga_sebaris.idk   # kode game
```

## Kontribusi

Ide pengembangan:

- Mode dua pemain (manusia lawan manusia)
- Level "sedang" (campuran langkah acak dan minimax)
- Menyimpan skor ke berkas dengan `tulis_semua()` / `baca_semua()`

Pull request dan issue sangat diterima.

## Tentang Indonesiaku

Indonesiaku adalah proyek bahasa pemrograman independen karya
[teguh02](https://github.com/teguh02/Indonesiaku-Lang). Dokumentasi dan
playground tersedia di [idk-lang.web.id](https://idk-lang.web.id).

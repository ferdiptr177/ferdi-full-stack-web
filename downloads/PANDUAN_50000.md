# NEBULA 50000

File mandiri `dist/NEBULA_50000.lua` memiliki tepat **50.000 baris**.
Salinan `.txt` memiliki isi dan checksum yang sama. ZIP mencakup sumber,
generator, katalog profil, metadata, dan pengujian.

Build ini memiliki 14 tab, 44 toggle runtime, 98 field konfigurasi, dan 451 preset unik. Hitungan 182 kontrol juga mencakup slider, tombol, dan catatan, bukan 182 fitur terpisah.

Jumlah baris mencakup 2.154 baris mesin fitur dan 47.846 baris katalog snapshot profil lengkap. Ini
bukan 50.000 baris logika fitur yang berbeda. Lihat `dist/manifest.json` untuk
rincian jumlah baris inti, baris katalog, jumlah preset, dan SHA-256.
Generator membungkus deskripsi katalog untuk mencapai jumlah tepat; tidak
menambahkan baris kosong, komentar pengisi, atau preset yang identik.

## Cara memakai

1. Buka `dist/NEBULA_50000.txt` menggunakan editor teks.
2. Pilih seluruh isi, salin, kemudian tempel ke editor executor client.
3. Jalankan pada pengalaman yang mengizinkan pengujian perubahan client.
4. Di Roblox Studio milikmu, kode juga dapat ditempatkan di LocalScript pada
   `StarterPlayer > StarterPlayerScripts`, lalu jalankan Play.

Tidak memerlukan library GUI eksternal, `loadstring`, HTTP download script,
atau key system. File tunggal sudah memuat seluruh katalog dan kode.
Skrip, profil, dan bookmark tidak dikirim ke endpoint eksternal.

**RightShift** menampilkan/menyembunyikan panel. Pada mobile, gunakan tombol
minimalkan lalu tombol **N**. Geser judul untuk memindahkan panel. Tab pada
layar sempit dapat digeser mendatar. Tombol **×** unload dan memulihkan
properti yang sebelumnya diubah oleh panel.

## Tab dan fitur

| Tab | Isi |
| --- | --- |
| Move | Walk speed, jump, flight, noclip, infinite jump, freeze, bunny hop, air walk, auto rotate, sit, dash |
| Visual | Fullbright, fog, Atmosphere, night vision, blur, bloom, shadows, time, FOV, zoom, exposure, color grade, local hide self |
| Players | Highlight, nama/jarak, pilihan pemain, spectate, perpindahan lokal ke target |
| Places | Tiga bookmark posisi sesi, kembali, undo perpindahan, koordinat/clipboard |
| Profiles | Snapshot sesi, dua file JSON opsional, validasi tipe/batas nilai, reset |
| Settings | FPS/ping/health/koordinat, skala GUI, tema, minimalkan, informasi server |
| Camera | Freecam, orbit target, rekam kamera sampai 60 detik, playback/loop, tiga view kamera |
| Navigate | Pathfinding menuju bookmark, pembatalan, camera raycast, penanda, panah arah, pemulihan dari void |
| HUD | Kompas, speedometer, health bar, statistik sesi, opacity, posisi HUD, rainbow accent |
| Tools | Countdown, pemeriksaan target, diagnostik sesi, stop otomasi, stop fitur |
| Reticle | Crosshair, dot/ring, celah dinamis, warna/ukuran/opacity, info raycast permukaan |
| Scout | Daftar pemain terdekat, filter tim, metrik gerakan/lompatan/jatuh, jejak gerakan lokal |
| Scene | Brightness/fog/ambient, RGB, custom bloom dan depth of field, letterbox |
| Library | Snapshot konfigurasi unik (jumlah aktual ada pada manifest) yang bisa dipratinjau, diterapkan, dan diekspor sebagai JSON |

Flight: WASD/thumbstick, Space naik, Ctrl turun, atau tombol UP/DOWN.
Freecam: WASD dan Q/E, tahan klik kanan untuk memutar kamera. Pada mobile,
thumbstick dan UP/DOWN menggeser freecam; putaran kamera sentuh khusus belum
diimplementasikan. Keluar dari kendaraan/kursi sebelum flight.

Orbit/spectate memerlukan target yang dipilih di Players. Mode freecam,
orbit, playback, dan spectate saling eksklusif. Rekaman kamera disimpan
dalam memori dan tidak bertahan setelah pindah server atau menjalankan ulang
script. Setiap bookmark juga hanya berlaku selama sesi panel tersebut.

Pathfinding membutuhkan area yang bisa dinavigasi. Jalur yang terhalang,
waypoint yang tidak tercapai dalam delapan detik, kematian, atau pembatalan
akan menghentikan perjalanan. Tidak ada janji bahwa semua peta dapat dilalui.

Library menerapkan snapshot penuh dan menggantikan pengaturan aktif. Preset
tidak menyalakan flight, navigasi, teleport, freecam, atau orbit secara otomatis.
Untuk JSON persisten, executor perlu menyediakan `writefile`/`readfile`.
Tanpa API tersebut, profil sesi tetap tersedia. Clipboard juga opsional.

## Batas dan status validasi

- Semua fitur berjalan dari client. Server dapat menolak perubahan properti,
  perpindahan, atau gerakan. Hide self hanya memengaruhi tampilan lokal.
- Tidak ada god mode server, jaminan kebal damage, bypass anti-cheat, atau jaminan anti-ban. Permintaan bypass belum diimplementasikan: game dan mekanisme pemeriksaannya belum diketahui serta belum dapat diuji.
- Property override menyimpan nilai sebelum fitur aktif. Jika game mengubah
  properti yang sama selama fitur aktif, unload mengembalikan nilai awal.
- Roblox Studio, Roblox live, Delta, dan Arceus X **belum diuji langsung**.
  Nama executor tidak menjamin kompatibilitas API atau perilaku runtime.
- Kompilasi menggunakan Luau melalui `luau-web@1.5.1` berhasil.
- Pengujian memakai model API lokal: reticle, nearby panel, metrik, trail, layering Scene, mutual exclusion bloom/depth, mouse lock freecam, kontrol navigasi, koneksi daftar pemain dan perubahan Head, inisialisasi tab, seluruh preset,
  layering properti, konflik kamera, rekaman/playback, navigasi model,
  respawn, unload, dan menjalankan ulang panel. Model ini tidak mensimulasikan
  renderer, network ownership, anti-cheat, physics, atau pathfinding Roblox asli.

## Build dan pengujian ulang

Python 3 dan Node.js diperlukan untuk generator/pengujian, tidak untuk
menjalankan file `.lua` yang sudah dibangun.

```sh
cd nebula-50000
npm ci --ignore-scripts
python3 build.py
npm test
```

Untuk memakai instalasi `luau-web` yang sudah tersedia di luar direktori ini:

```sh
LUAU_WEB_MODULE=/absolute/path/to/luau-web/src/index.js node tests/check.mjs
```

`src/base.lua` adalah snapshot kode dasar. `src/upgrade.lua` menambahkan fitur. `src/expanded.lua` memasang tab dan fitur perluasan; schema scalar berada di `src/expanded-defaults.json` dan `src/expanded-bounds.json`.
`build.py` menggabungkan keduanya dengan katalog profil. Edit sumber tersebut
lalu build ulang; perubahan langsung pada file `dist` akan ditimpa generator.

## Perubahan tambahan pada versi 50000

- Kontrak modul dan schema konfigurasi untuk kontrol perluasan.
- Kontrol PlayerModule default ditangguhkan hanya selama navigasi, kemudian
  dipulihkan sesuai status sebelumnya; PlayerModule yang tidak dikenali
  menghentikan permintaan navigasi agar tidak merebut kontrol secara sembarang.
- Freecam memegang mouse lock saat klik kanan dan memulihkannya saat fokus
  hilang, tombol dilepas, mode dinonaktifkan, atau panel di-unload.
- Rebuild daftar pemain melepas event baris lama. Nameplate dibangun ulang
  ketika Head berubah walaupun model karakter tidak berubah.
- Versi 15000 tetap tersimpan terpisah dan tidak diubah.

Hitungan 50.000 baris mencakup kode inti dan tabel snapshot preset. Jumlah baris
bukan jumlah fitur; rincian keduanya disimpan dalam manifest build.

Loader HTTPS hanya memuat file mandiri yang sama. HTTP dan `loadstring` memerlukan dukungan executor; loader maupun fitur belum diuji pada executor atau Roblox live.

# Eksperimen Performa: WebAssembly (WASM) vs JavaScript

Repository ini berisi kode sumber untuk eksperimen yang membandingkan kecepatan eksekusi antara **WebAssembly** dan **JavaScript murni**. Eksperimen ini ditujukan untuk memenuhi Tugas UTS mata kuliah Pemrograman Web.

Eksperimen dilakukan dengan menjalankan fungsi rekursif yang cukup berat, yaitu menghitung deret Fibonacci ke-40.

## Hasil Eksperimen

Berdasarkan pengujian yang dilakukan di *local environment*, berikut adalah perbandingan waktu eksekusinya (hasil dapat dilihat pada tab Console di browser):

* **Hasil Perhitungan (Fibonacci ke-40):** 102334155
* **Waktu Eksekusi WebAssembly:** `~365.28 ms`
* **Waktu Eksekusi JavaScript:** `~1303.58 ms`


Bukti hasil gambar:
![foto](https://github.com/Elisabethbanjarnahor/ekspriment-wasm-vs-javascript/blob/0ba9935ebe73209b8afc22eecdddc234ed54e24e/Screenshot%202026-04-30%20030452.png)

**Kesimpulan:** WebAssembly terbukti berjalan sekitar **3,5 kali lebih cepat** dibandingkan JavaScript untuk komputasi matematis yang berat.

## Analisis: Mengapa WASM Lebih Cepat?

Perbedaan performa yang signifikan ini disebabkan oleh cara *engine* browser memproses kedua jenis kode tersebut:

1. **Format Biner vs Parsing Teks:** JavaScript dikirim ke browser dalam bentuk teks. Browser harus melakukan *parsing*, memahaminya, dan mengonversinya ke *bytecode* sebelum dieksekusi (*Just-In-Time Compilation*). Sebaliknya, WebAssembly sudah dikirim dalam format biner tingkat rendah sejak awal. Browser tidak perlu lagi membuang waktu untuk *parsing* teks dan langsung mengeksekusi instruksi tersebut.

2. **Pengecekan Tipe Data (Static vs Dynamic):**
   JavaScript adalah bahasa *dynamically typed*. Saat menjalankan perulangan rekursif secara masif, mesin JS terus-menerus membuang waktu untuk mengecek apakah variabel yang sedang dihitung adalah angka, teks, atau objek. Sedangkan WebAssembly (yang dalam kasus ini dikompilasi menggunakan format struktur bahasa tingkat rendah) bersifat *statically typed*. Mesin sudah tahu 100% bahwa data yang diolah adalah *integer*, sehingga tidak ada performa komputasi yang terbuang untuk proses pengecekan tipe data.

## Cara Menjalankan Kode

Jika Anda ingin menjalankan eksperimen ini di komputer Anda:

1. Pastikan Anda memiliki Text Editor seperti **Visual Studio Code (VS Code)**.
2. *Clone* atau *download* repository ini, lalu buka foldernya di VS Code.
3. Install ekstensi **Live Server** di VS Code (jika belum ada). Hal ini wajib dilakukan agar file `.wasm` dapat di-*fetch* tanpa terkena *error CORS*.
4. Klik kanan pada file `index.html` dan pilih **"Open with Live Server"**.
5. Setelah browser terbuka, klik kanan pada halaman web -> pilih **Inspect** (atau Inspect Element).
6. Buka tab **Console** dan tunggu beberapa saat. Hasil komparasi waktu akan muncul di sana.

---
*Dibuat untuk keperluan eksperimen performa web.*

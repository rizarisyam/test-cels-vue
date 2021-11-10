# cels-vue

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

# Tugas Anda
### Harap menginstall dependensi sesuai kebutuhan, wajib menggunakan Vue minimal versi 3 (`vue@next`).

1. Ambil data menu dari konstan pada file `kitchen.js` dan ganti tampilan yang statik dengan data tersebut.
2. Isi filter "Food Groups" dengan semua kemungkinan grup dari data menu (poin 1).
3. Filter "Food Groups" diisi dengan elemen yang *capitalized*, sementara label grup ditampilkan dengan *lowercase*.
4. Apabila dimasukkan teks di isian pencarian, filter menu berdasarkan `title`.
5. Apabila pengguna memilih filter "Food Groups", filter data menu berdasarkan label grup.
6. Apabila pengguna menekan tanda tambah, masukkan menu tersebut ke dalam cart (apabila belum termasuk dalam cart), atau tambahkan quantity menu tersebut dalam cart. Juga tambahkan tombol bertanda kurang.
7. Apabila pengguna menekan tanda kurang, kurangi quantity dari menu tersebut dalam cart, atau hapus menu tersebut dari cart (apabila quantity 0). Juga hilangkan tombol ini apabila menu tersebut tidak di dalam cart.
8. Pastikan angka pada tombol `Place Order [x] (y)` sesuai dengan **jenis** dan **total jumlah** menu yang terdapat dalam cart, `x` & `y` merepresentasikan salah satu dengan urutan bebas.

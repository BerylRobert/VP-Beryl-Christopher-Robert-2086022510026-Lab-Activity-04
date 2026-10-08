1. StoreHeader (nama toko)
- Error: overflow 219 px di kanan pada 320 dp
- Rule broken: Row memberi Column lebar tak terbatas, dan tidak ada yang menyuruh teks mengalah
- Fix: Bungkus Column dengan Expanded, tambah maxLines + TextOverflow.ellipsis

2. StoreHeader (rating)
- Error: teks "4.8 · 1,2 rb ulasan" ikut mendorong Row keluar layar
- Rule broken: Text di dalam Row tidak bisa mengecil
- Fix: Flexible + naxLines: 1 + ellipsis

3. CategoryBar
- Error: overflow 321 px di kanan
- Rule broken: 6 chip dalam Row lebih lebar dari layar, dan Row tidak bisa digeser
- Fix: Bungkus Row dengan SingleChildScrollView(scrollDirection: Axis.horizontal)

4. PromoCard / PromoStrip
- Error: overflow 128 px di kanan
- Rule broken: width: 200 hard-coded mengabaikan constraint dari parent (2 × 200 + jarak > 320 dp)
- Fix: Hapus width, bungkus tiap kartu dengan Expanded di dalam Row

5. PromoCard
- Error: nama promo 200 karakter merusak kartu (tinggi terbatas)
- Rule broken: teks tanpa batas di ruang yang terbatas
- Fix: maxLines: 2 untuk nama, maxLines:  1 untuk label dan harga, semua dengan ellipsis

6. MenuTile
- Error: overflow 22 px di kanan
- Rule broken: Column di dalam Row tanpa Expanded, ditambah Spacer
- Fix: Expanded di Column, nama maxLines: 2 + ellipsis, hapus Spacer, harga maxLines: 1

7. CartBar
- Error: overflow 96 px di kanan
- Rule broken: SizedBox(width: 160) dan height: 72 hard-coded, Text panjang tanpa batas dalam Row
- Fix: Hapus height dan width, Expanded + maxLines: 2 + ellipsis di teks pesanan

8. CartBar
- Error: tombol pesan bisa tertutup gesture bar
- Rule broken: tidak ada yang menjauhkan konten dari inset sistem
- Fix: SafeArea(top: false) di dalam Container berwarna, supaya warna bar tetap sampai ke tepi

9. MenuScreen
- Error: overflow bawah (190 dan 80 px) di landscape; 138 dan 306 px saat keyboard terbuka
- Rule broken: Column berisi header + search + chip + promo + Expanded list: sisa tinggi untuk list menjadi negatif di layar pendek
- Fix: Satu CostumScrollView, semua bagian jadi silver dan ikut menggulir bersama list

10. MenuScreen
- Error: tablet hanya melebar, tidak berubah struktur
- Rule broken: MediaQuery dengan > 600 mengukur layar, bukan ruang yang diberikan parent, dan batas 600 tidak ikut
- Fix: LayoutBuilder dengan constraints.maxWidth >= 600, di atas itu pakai grid

11. MenuScreen
- Error: 500 item dibangun sekaligus
- Rule broken: ListView(children:) membangun semua anak di muka, list yang panjangnya tidak dikontrol harus lazy
- Fix: SliverList.builder untuk list

12. MenuScreen (grid)
- Error: grid fix 4 kolom dan children: eager
- Rule broken: jumlah kolom hard-coded tidak menyesuaikan lebar, children: tidak lazy
- Fix: SliverGrid.builder dengan SliverGridDelegateWithMaxCrossAxisExtent (kolom menyesuaikan lebar)

13. MenuCard
- Error: overflow bawah 98 / 118 / 138 px di sel grid (tinggi sel 140)
- Rule broken: Container(height: 110) + teks tanpa batas di dalam sel yang tingginya sudah ditentukan parent
- Fix: Gambar dibuat Expanded (gambar yang mengalah), nama maxLines: 2, harga dan tombol maxLines: 1

14. PromoStrip
- Error: RangeError saat data kosong
- Rule broken: kode mengasumsikan selalu ada dua promo (promos[0], promos[1])
- Fix: PromoStrip menerima daftar, ambil .take(2), sembunyikan strip kalau tidak ada promo

15. MenuScreen
- Error: data kosong menampilkan layar kosong
- Rule broken: kode mengasumsikan data selalu ada
-  Fix: EmptyState (ikon, pesan, tombol "Reset filter") dengan key: const Key('empty-state')
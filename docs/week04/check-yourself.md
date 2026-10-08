1. A Text inside a Row overflows. Which part of "constraints go down, sizes go up, parent sets position" was violated, and by which widget?
> Bagian yang dilanggar itu "constraints go down", oleh widget Row. Karena Row tidak memberi batas lebar yang jelas ke Text, jadi Text melebar sepanjang tulisannya sampai keluar layar. Solusinya pakai Expanded supaya Text cuma boleh memakai sisa ruang yang ada/

2. Why is adding width: 150 to the text the wrong fix, even if the stripes disappear?
> Karena angka 150 itu cuma pas di layar yang sedang aku pakai. Kalau layarnya lebih kecil atau tulisannya diperbesar, garis kuningnya muncul lagi. Jadi masalahnya cuma pindah tempat, bukan selesai.

Ibaratnya: kalau kita bilang "duduk di kursi nomor 5", itu gagal kalau ruangannya ganti. Kalau kita bilang "duduk di tempat yang kosong", itu selalu cocok.

3. You fixed the landscape overflow by wrapping everything in a SingleChildScrollView and setting shrinkWrap: true on the list. Which test fails, and why does it matter once the data comes from an API?
> Tes 7 (500 items) yang gagal. shrinkWrap: true membuat Flutter menggambar semua item sekaligus, padahal layar cuma muat beberapa. Kalau datanya dari API, jumlahnya bisa ribuan dan kita tidak bisa menebaknya, jadi aplikasi jadi lambat dan berat. Dengan .builder, Flutter hanya menggambar item yang kelihatan di layar.

4. Why does the tablet layout use LayoutBuilder rather than MediaQuery.sizeOf(context)?
> MediaQuery menjawab "seberapa besar layar HP-nya?", sedangkan LayoutBuilder menjawab "seberapa besar ruang yang diberikan ke widget ini?". Kedua ukuran itu tidak selalu sama, misalnya waktu layar dibagi dua (split-screen) atau widget ditaruh di panel kecil. LayoutBuilder memilih tampilan berdasarkan ruang yang benar-benar tersedia, jadi lebih akurat.

5. The empty-data crash was not a layout error. ?> Why does it belong in a layout lab anyway?
Karena layar yang crash itu sama rusaknya dengan layar yang overflow, dimana pengguna sama-sama tidak bisa memakainya. Penyebabnya juga mirip, yaitu kode kita mengira datanya selalu ada. Layout yang bagus harus tetap tampil rapi walaupun datanya kosong, kepanjangan, atau sangat banyak.
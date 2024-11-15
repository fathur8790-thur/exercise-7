# Exercise 7 - Demonstrasikan Dampak Kontensi Sumber Daya pada Performa Sistem

## Tujuan Percobaan
Exercise 7 bertujuan untuk menunjukkan bagaimana penggunaan sumber daya bersama dalam sistem multitasking dapat menyebabkan penurunan kinerja sistem. Pada percobaan ini, kita akan menggunakan tiga tugas yang berbagi satu sumber daya bersama, dan kita akan mengamati bagaimana akses simultan terhadap sumber daya ini mengganggu performa sistem.

## Langkah-langkah Percobaan

### 1. Persiapan Awal
- Pastikan sistem sudah siap dengan tiga tugas (tasks) yang berfungsi untuk menyalakan LED. Setiap tugas akan memiliki waktu eksekusi yang berbeda untuk menghasilkan pola nyala dan padam LED yang berbeda.
  - **Tugas Green LED**: Nyala selama 200 ms, lalu mati selama 200 ms.
  - **Tugas Red LED**: Nyala selama 550 ms, lalu mati selama 550 ms.
  - **Tugas Orange LED**: Nyala dan padam setiap 50 ms (frekuensi 10 Hz), dengan prioritas lebih tinggi dari tugas lainnya.

### 2. Langkah Pertama - Menjalankan Setiap Tugas Secara Individual
**Tujuan**: Menjalankan setiap tugas secara terpisah untuk memastikan waktu eksekusi sesuai dengan yang diinginkan tanpa gangguan dari tugas lainnya.

**Langkah-langkah**:
- Komentari atau nonaktifkan dua tugas lainnya, kemudian jalankan hanya satu tugas.
- Amati pola nyala dan padam LED untuk memastikan LED menyala sesuai dengan waktu yang diharapkan. Misalnya, Green LED harus menyala selama 200 ms dan mati selama 200 ms.
- Ulangi langkah ini untuk setiap tugas, memastikan bahwa waktu eksekusi sesuai spesifikasi saat tugas berjalan sendiri.

### 3. Langkah Kedua - Menjalankan Semua Tugas Bersamaan Tanpa *Mutual Exclusion*
**Tujuan**: Mengamati dampak dari kontensi pada sumber daya bersama ketika semua tugas aktif bersamaan tanpa mekanisme *mutual exclusion*.

**Langkah-langkah**:
- Aktifkan semua tugas dalam kode (hapus komentar atau aktifkan kembali).
- Jalankan sistem dengan ketiga tugas aktif secara bersamaan, tetapi tanpa mekanisme *mutual exclusion*.
- Amati pola nyala dan padam LED. Karena ketiga tugas berusaha mengakses sumber daya bersama (misalnya, variabel atau perangkat keras), kontensi akan terjadi, dan pola LED akan menjadi tidak konsisten dan berbeda dari spesifikasi yang diharapkan.
- Catat perbedaan pola LED yang terjadi sebagai tanda adanya penurunan performa akibat kontensi.

### 4. Langkah Ketiga - Mengaktifkan *Mutual Exclusion* untuk Mencegah Kontensi
**Tujuan**: Menggunakan *mutual exclusion* untuk mencegah kontensi, sehingga hanya satu tugas yang dapat mengakses sumber daya pada satu waktu.

**Langkah-langkah**:
- Implementasikan mekanisme *mutual exclusion* di kode akses sumber daya bersama. Gunakan fungsi `taskENTER_CRITICAL()` dan `taskEXIT_CRITICAL()` untuk menangguhkan *scheduler* sementara akses berlangsung.
  
- Jalankan sistem dengan ketiga tugas aktif. Pastikan untuk mengamati pola nyala LED yang lebih stabil dan sesuai dengan waktu eksekusi yang diharapkan.
### 5. Analisis Hasil Percobaan
- Tanpa Mutual Exclusion: Pada percobaan kedua, Anda akan melihat bahwa LED berkedip secara tidak konsisten, menunjukkan adanya gangguan waktu eksekusi akibat kontensi.
- Dengan Mutual Exclusion: Pada percobaan ketiga, LED seharusnya berkedip dengan pola yang lebih stabil dan sesuai dengan waktu spesifikasi. Ini menunjukkan bahwa penggunaan mutual exclusion efektif dalam mencegah kontensi.
### 6. Kesimpulan
- Percobaan ini menunjukkan bahwa ketika beberapa tugas berbagi sumber daya tanpa pengaturan yang tepat, hal itu dapat menyebabkan kontensi dan menurunkan kinerja sistem.
- Mutual exclusion adalah solusi yang dapat mencegah kontensi dengan membatasi akses ke sumber daya bersama sehingga hanya satu tugas yang dapat mengaksesnya pada satu waktu.
- Penting untuk mempertimbangkan penggunaan mekanisme mutual exclusion dalam desain sistem multitasking untuk memastikan performa sistem yang stabil dan menghindari masalah kontensi.

### 7. Demo

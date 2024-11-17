#FreeRTOS-Demonstrate	access	contention	problems when	using	shared	resources	in	a multitasking	system
Proyek ini memperlihatkan bagaimana FreeRTOS digunakan untuk mengelola beberapa tugas (tasks) yang mengakses shared resource dalam sistem multitasking. Dalam implementasi ini, LED berfungsi sebagai indikator aktivitas dari masing-masing tugas dan konflik akses terhadap shared resource.

Diagram Task :

![Screenshot 2024-11-17 193544](https://github.com/user-attachments/assets/10191aaf-f847-4c35-af86-312c27aadbef)


Hardware yang diperlukan :
1. STM32f401CCU6
2. LED

Software yang diperlukan :
1. STM32CubeIDE
2. FreeRTOS

Cara Kerja :
1. Inisialisasi dan Penjadwalan Tugas :
   - Program memulai kernel FreeRTOS untuk mengatur eksekusi beberapa threads.
   - Tugas-tugas memiliki prioritas berbeda untuk mencerminkan kebutuhan sistem.
     
2. Mutual Exclusion (Pengelolaan Shared Resource) :
   - Tugas GreenTask dan RedTask bergantian mengakses variabel StartFlag.
   - Akses ke variabel dilindungi untuk mencegah dua tugas mengakses pada waktu bersamaan.
   - Jika akses tidak berhasil (saat shared resource sedang digunakan), LED kuning menyala sebagai indikator konflik.
     
3. Indikator Konflik Akses :
   - Jika critical section dihapus, konflik akses ke shared resource akan muncul, dan LED kuning akan menyala lebih sering.
     
4. Siklus Perilaku LED :
- Kasus Normal:

LED hijau dan merah akan menyala bergantian, menunjukkan bahwa akses shared resource berlangsung tanpa konflik.

-  Kasus Konflik:

Jika critical section tidak diterapkan dengan benar, LED kuning menyala, menunjukkan adanya konflik.
     
Ringkasan Perilaku LED :
- LED Hijau (Green): Menyala saat GreenTask mengakses shared resource.
- LED Merah (Red): Menyala saat RedTask mengakses shared resource.
- LED Kuning (Yellow): Menyala ketika terjadi konflik akses ke shared resource.

Pinout Hardware :

![Pinout Hardware FreeRTOS](https://github.com/user-attachments/assets/8b814f64-fa02-4ee5-a5e5-d6a85f395bb2)

Hasil Hardware :

![5-GIF](https://github.com/user-attachments/assets/648bc249-7fa2-4e7a-8028-b3777174279c)


Hasil dari proyek ini sebagai berikut :
1. **Normal**:
   - LED hijau dan merah menyala bergantian tanpa konflik.
   - LED kuning tetap mati.
   - Menunjukkan keberhasilan pengelolaan shared resource.
     
2. **Problem** :
   - LED kuning sering menyala, menunjukkan bahwa dua tugas mencoba mengakses shared resource secara bersamaan.
   - Terjadi karena tidak diterapkannya mekanisme critical section.
   
Project ini dikerjakan di Politeknik Elektronika Negeri Surabaya dengan dosen pengampu bapak Fernando Ardilla

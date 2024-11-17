#Demonstrate	access	contention	problems when	using	shared	resources	in	a multitasking	system
Proyek ini menunjukkan penggunaan FreeRTOS Semaphore untuk sinkronisasi antara beberapa task dalam sistem multitasking. Program ini berfokus pada bagaimana penggunaan semaphore dapat mengatur urutan eksekusi task, khususnya dalam mengendalikan perilaku LED pada STM32F401CCU6.

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
   - Program dimulai dengan inisialisasi FreeRTOS dan pembuatan dua task utama (GreenTask dan RedTask) serta satu fungsi untuk simulasi critical section.
   - Semaphore digunakan untuk sinkronisasi antara task, memastikan hanya satu task yang mengakses shared resource.
     
2. Deskripsi Task :
   a. GreenTask
   - Task ini akan menyalakan LED Hijau
   - Mengakses critical section menggunakan semaphore
   - Delay selama 500ms setelah selesai mengakses
     
   b. RedTask
   - Task ini menyalakan LED Merah
   - Mengakses critical section menggunakan semaphore
   - Delay selama 100ms setelah selesai mengakses
  
  c. Blue LED (LED Yellow)
   - Menyala ketika ada task yang mencoba mengakses shared resource tanpa berhasil mendapatkan semaphore
     
3. Mekanisme Semaphore
   - Binary Semaphore digunakan untuk memastikan hanya satu task yang dapat mengakses critical section (dalam hal ini, kontrol LED).
   - Jika semaphore tidak tersedia, task masuk ke mode blocked state.
     
5. Penanganan Konflik :
   - Jika bagian *critical section* dihapus atau tidak diterapkan dengan benar, tugas 'GreenTask' dan 'RedTask' mungkin mencoba mengkases *shared resource* pada saat yang bersamaan, yang menyebabkan konflik.
   - 'BlueTask' akan sering menyala untuk menunjukkan adanya konflik ketika dua tugas mencoba mengakses *shared resource* pada waktu yang bersamaan.
     
6. Siklus Kerja LED :
   - **Kasus Normal** : Jika mutual exclusion bekerja dengan baik, 'GreenTask' dan 'RedTask' akan menyala bergantian, menunjukkan bahwa kedua task berhasil mengakses *shared resource*. 'OrangeTask' akan terus berkedip dengan cepat.
   - **Kasus Problem** : Jika mutual exclusion tidak diterapkan dengan bena, 'GreenTask' dan 'RedTask' mungkin menyala bersamaan atau dengan pola yang tidak teratur, dan 'BlueTask' akan menyala untuk menunjukkan adanyan konflik.

Ringkasan Perilaku LED :




Pinout Hardware :

![Pinout Hardware FreeRTOS](https://github.com/user-attachments/assets/8b814f64-fa02-4ee5-a5e5-d6a85f395bb2)

Hasil Hardware :

![5-GIF](https://github.com/user-attachments/assets/648bc249-7fa2-4e7a-8028-b3777174279c)


Hasil dari proyek ini sebagai berikut :
1. **Normal**: LED Hijau dan Kuning bergantian menyala tanpa terdapat masalah, LED Merah tetap mati.
2. **Problem** : Jika dengan sengaja menghapus mekanismer *critical section*, LED Biru akan sering menyala.
   
Project ini dikerjakan di Politeknik Elektronika Negeri Surabaya dengan dosen pengampu bapak Fernando Ardilla

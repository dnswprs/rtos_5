# Percobaan Demonstrasi Resource Contention RTOS

## Tentang Proyek
Program ini menjalankan tiga task yang berbeda dalam sistem operasi FreeRTOS. Task pertama adalah DefaultTask yang berfungsi sebagai task idle system. Dua task utama lainnya, GreenLedTask dan RedLedTask, beroperasi secara bersamaan untuk mengakses shared resource dan menunjukkan aktivitasnya melalui LED.
GreenLedTask dan RedLedTask memiliki pola kerja yang serupa namun dengan timing yang berbeda. GreenLedTask beroperasi dengan interval 100ms, sementara RedLedTask beroperasi dengan interval 500ms. Perbedaan timing ini sengaja dirancang untuk mensimulasikan skenario di mana dua proses yang berbeda mencoba mengakses resource yang sama dengan frekuensi yang berbeda.
## Fitur
- Implementasi multi-threading dengan FreeRTOS
- Manajemen resource sharing
- Kontrol LED dengan timing yang berbeda
- Deteksi resource contention dengan indikator LED

## Komponen Task
Program ini terdiri dari dua task utama:
### 1. GreenLedTask
- Fungsi:
  - Mengontrol LED Hijau
  - Mengakses shared data setiap 100ms
  - Menunjukkan aktivitas dengan mengedipkan LED

### 2. RedLedTask
- Fungsi:
  - Mengontrol LED Merah
  - Mengakses shared data setiap 500ms
  - Menunjukkan aktivitas dengan mengedipkan LED

## Cara Kerja Program

### Diagram Alur Kerja Program
![image](https://github.com/user-attachments/assets/5c7b975f-75cf-42a4-a995-ed90af659f85)

### Inisialisasi
1. Program menginisialisasi semua peripheral yang diperlukan
2. Mengkonfigurasi system clock
3. Menginisialisasi GPIO untuk LED
4. Mematikan semua LED pada awal program

### Shared Resource Management
Program menggunakan mekanisme flag sederhana untuk mengelola akses ke shared resource:
- `startFlag` digunakan sebagai indikator ketersediaan resource
- LED Biru digunakan sebagai indikator resource contention
- Setiap task harus memeriksa availability sebelum mengakses shared resource

### Mekanisme LED
- LED Hijau dan Merah berkedip bergantian menandakan eksekusi task
- LED Biru menyala ketika terjadi resource contention
- Timing yang berbeda pada setiap task (100ms vs 500ms) untuk mendemonstrasikan perbedaan timing eksekusi

## Konfigurasi Hardware
Program menggunakan konfigurasi GPIO berikut:
- GPIOE: LED Oranye dan Biru
- GPIOB: LED Hijau dan Merah

## Analisa 
Program ini mendemonstrasikan masalah klasik dalam sistem multi-tasking yaitu resource contention, di mana dua task (GreenLedTask dan RedLedTask) berkompetisi untuk mengakses shared resource yang sama. Implementasi program menggunakan mekanisme flag sederhana (startFlag) untuk mengontrol akses, yang meskipun berfungsi sebagai demonstrasi, tidak sepenuhnya aman untuk sistem real-time karena berpotensi mengalami race condition. 
Program menggunakan LED Biru sebagai indikator visual untuk mendeteksi resource contention, yang terjadi ketika satu task mencoba mengakses resource sementara task lain sedang menggunakannya. Perbedaan timing antara kedua task (100ms vs 500ms) dan penggunaan global variable tanpa proper mutex atau semaphore menciptakan kondisi yang ideal untuk terjadinya simultaneous access.

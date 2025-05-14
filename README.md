### a. Apa itu AMQP?

AMQP (Advanced Message Queuing Protocol) adalah protokol standar terbuka yang bekerja di layer aplikasi dan dirancang khusus untuk komunikasi berbasis pesan. Protokol ini memungkinkan berbagai aplikasi — bahkan yang dibangun dengan bahasa pemrograman dan platform berbeda — untuk bertukar pesan secara lebih mudah. AMQP menetapkan dua hal penting: bagaimana data dikirim melalui jaringan, dan bagaimana klien serta broker pesan harus berperilaku dalam proses pengiriman dan penerimaan pesan. Beberapa fitur unggulan dari AMQP mencakup pengiriman pesan yang lebih mudah, kemampuan routing yang fleksibel, dukungan terhadap antrian pesan, serta fitur keamanan. Karena keandalannya, AMQP banyak digunakan dalam sistem berskala besar seperti sistem enterprise atau layanan cloud. Beberapa implementasi populer dari protokol ini adalah RabbitMQ, Apache ActiveMQ, dan Azure Service Bus, yang semuanya memanfaatkan standarisasi AMQP untuk integrasi antar sistem yang lebih mudah dan stabil.

### b. Apa arti dari `guest:guest@localhost:5672`?

String koneksi `amqp://guest:guest@localhost:5672` adalah alamat yang digunakan aplikasi untuk terhubung ke server AMQP, seperti RabbitMQ. Format ini mengikuti pola `amqp://username:password@host:port`, dan dalam contoh tersebut, `guest` yang pertama adalah username default, sedangkan `guest` yang kedua adalah password-nya. Ini adalah kredensial standar yang biasanya disediakan secara default saat RabbitMQ pertama kali diinstal. Bagian `localhost` menunjukkan bahwa server RabbitMQ berjalan di mesin yang sama dengan aplikasi yang mengaksesnya. Sementara itu, angka `5672` adalah port default yang digunakan oleh protokol AMQP untuk mendengarkan koneksi masuk. Kombinasi dari username, password, alamat host, dan port ini sangat penting agar aplikasi dapat mengakses broker pesan dengan benar dan aman.

![Image](https://github.com/user-attachments/assets/cf1156a1-1746-4926-a864-ae6eea19e6c3)

Jumlah pesan dalam antrean (dalam kasus ini Unacked = 73) meningkat karena kamu menambahkan thread::sleep(Duration::from_millis(1000)) di dalam fungsi handle. Artinya, setiap kali subscriber menerima satu pesan, ia akan berhenti sejenak selama 1 detik sebelum memproses pesan berikutnya.

Karena publisher mengirim banyak pesan dengan cepat, sementara subscriber hanya bisa memproses satu pesan per detik, maka pesan-pesan lain akan menumpuk di antrean sebagai "unacked" — artinya pesan sudah diterima oleh subscriber, tapi belum selesai diproses (belum di-acknowledge).

Di mesinku sendiri, jumlahnya bisa berbeda tergantung kecepatan publish, durasi sleep, dan berapa kali publisher dijalankan. Jadi, saat kamu melihat antrean bisa mencapai 20 atau bahkan 73, itu wajar jika sleep menyebabkan bottleneck di sisi subscriber.








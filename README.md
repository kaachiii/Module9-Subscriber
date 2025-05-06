# Tutorial Module 9
### Nama : Ischika Afrilla
### NPM : 2306227955

7a. What is amqp? 

    amqp (Advanced Message Queuing Protocol) adalah protokol komunikasi yang digunakan agar aplikasi atau sistem bisa bertukar pesan secara teratur, meskipun mereka berjalan di waktu yang berbeda atau di tempat yang berbeda. Dalam sistem amqp, ada broker (seperti RabbitMQ) yang bisa diibaratkan sebagai kurir dalam pengiriman paket. Broker ini bertugas menyimpan, mengatur, dan meneruskan pesan dari pengirim ke penerima dengan cara yang aman dan terstruktur.

7b. What does it mean? guest:guest@localhost:5672, what is the first guest, and what is the second guest, and what is localhost:5672 is for?  

    Format guest:guest@localhost:5672 biasa digunakan untuk mengakses amqp (seperti RabbitMQ) yang bentuknya mengikuti pola username:password@host:port.

        - first guest = username (nama pengguna yang digunakan untuk login ke server)
        - second guest = password (kata sandi dari pengguna tersebut)
        - localhost = komputer lokal (artinya server RabbitMQ dijalankan di komputer yang sama karena tidak ada IP komputer lain)
        - 5672 = port yang digunakan oleh protokol amqp

    Jadi, guest:guest@localhost:5672 artinya, login ke server amqp (RabbitMQ) yang berjalan di localhost lewat port 5672, menggunakan username 'guest' dan password 'guest'.

### Commit Simulation slow subscriber
![Simulation slow subscriber](images/Screenshot%202025-05-06%20102912.png)

Pada mesin saya, total antrean (queue) berjumlah sekitar 10. Hal ini terjadi karena ada delay pada proses penerimaan, sehingga publisher mengirim pesan lebih cepat daripada subscriber dapat memprosesnya. Akibatnya, pesan menumpuk di antrean.

### Commit Reflection and Running at least three subscribers
![Reflection and Running at least three subscribers](images/Screenshot%202025-05-06%20104718.png)
![Reflection and Running at least three subscribers](images/Screenshot%20(1073).png)

Pada gambar pertama terlihat bahwa ketiga subscriber menerima pesan secara bergantian. Misalnya, subscriber pertama menerima pesan dengan user_id 1, subscriber kedua menerima user_id 2, dan subscriber ketiga menerima user_id 3. Hal ini menunjukkan bahwa message broker membagi pesan secara rata ke subscriber yang terhubung ke antrean (queue) yang sama.

Pada gambar kedua terlihat bahwa jumlah pesan dalam antrean berkurang, dari sekitar 10 menjadi 7,5. Hal ini terjadi karena semakin banyak subscriber yang aktif dan terhubung ke antrean yang sama, maka proses konsumsi pesan menjadi lebih cepat. Broker akan mendistribusikan pesan ke subscriber secara bergiliran, sehingga beban diproses lebih efisien. Setelah pesan diambil dari antrean oleh salah satu subscriber, pesan tersebut akan dihapus dari antrean dan tidak bisa diambil oleh subscriber lain.

Menariknya, kita bisa mengubah perilaku sistem hanya dengan mengubah konfigurasi broker atau menambah/mengurangi jumlah subscriber, tanpa perlu memodifikasi kode program. Hal ini memberi fleksibilitas dalam mengatur performa dan skalabilitas sistem.
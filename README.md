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
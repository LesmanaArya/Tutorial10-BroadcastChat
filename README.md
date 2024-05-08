# Tutorial 10 chat-async

## 2.1 Original code of broadcast chat

### Sending message from three clients
![client1](img/ss_client1.png) ![client2](img/ss_client2.png) ![client3](img/ss_client3.png)

### Server receiving messages
![server](img/ss_server.png)

Kita dapat menjalankan server dan client masing-masing menggunakan ```cargo run --bin server``` dan ```cargo run --bin client```. Setiap client akan terhubung ke server melalui Websocket. Setiap client menginput suatu message, maka message tersebut akan diteruskan ke server dan server akan mengirimkannya ke semua client yang terhubung saat itu. Itulah sebabnya setiap client dapat melihat pesan-pesan yang dikirimkan oleh client lainnya
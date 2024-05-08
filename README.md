# Tutorial 10 chat-async

## 2.1 Original code of broadcast chat

### Sending message from three clients
![client1](img/ss_client1.png) ![client2](img/ss_client2.png) ![client3](img/ss_client3.png)

### Server receiving messages
![server](img/ss_server.png)

Kita dapat menjalankan server dan client masing-masing menggunakan ```cargo run --bin server``` dan ```cargo run --bin client```. Setiap client akan terhubung ke server melalui Websocket. Setiap client menginput suatu message, maka message tersebut akan diteruskan ke server dan server akan mengirimkannya ke semua client yang terhubung saat itu. Itulah sebabnya setiap client dapat melihat pesan-pesan yang dikirimkan oleh client lainnya

##  Modifying the websocket port
Untuk mengubah port menjadi 8080, pertama-tama kita perlu mengubah bagian server.rs tepatnya pada kode:
```
let listener = TcpListener::bind("127.0.0.1:2000").await?;
println!("listening on port 2000");
```
menjadi:
```
let listener = TcpListener::bind("127.0.0.1:8080").await?;
println!("listening on port 8080");
```
Hal ini berarti kita mengubah listener dari server kita menjadi port nomot 8080. Setelah itu, kita perlu merubah url port number dari ClientBuilder supaya mereka akan memilih menghubungkan ke port 8080. Hal ini dapat dirubah pada bagian:
```
let (mut ws_stream, _) =
        ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:2000"))
            .connect()
            .await?;
```
menjadi:
```
let (mut ws_stream, _) =
        ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8080"))
            .connect()
            .await?;
```
Websocket protocol yang digunakan di program ini tetap menggunakan ```tokio_websockets``` yang umum digunakan dalam app berbasis tokio. 
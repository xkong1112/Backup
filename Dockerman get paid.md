### 什么是socket？
其中的传输层就是 TCP/IP 所在的地方，而你平时通过代码编写的应用程序大多属于应用层范畴，socket 在这里起到就是连接应用层与传输层的作用。

socket 的诞生是为了应用程序能够更方便的将数据经由传输层来传输，所以它本质上就是对 TCP/IP 的运用进行了一层封装，然后应用程序直接调用 socket API 即可进行通信。那么它是如何工作的呢？它分为 2 个部分，服务端需要建立 socket 来监听指定的地址，然后等待客户端来连接。而客户端则需要建立 socket 并与服务端的 socket 地址进行连接。
### 什么是SSH？
Secure Shell ( SSH ) is a protocol for securely connecting to other computers over the Internet . It is available in two versions, SSH-1 and SSH-2 . SSH is a replacement for Telnet but with the difference that all traffic between the computers is encrypted . SSH consists of a server part , which usually listens to port 22, and a client part . The client software is used to connect to the server.
SSH是加密过的，由一个服务器和一个客户端组成。服务器监听端口22。

可以在搭建一个Socket通过SSH来传输数据。

### 多线程优化
1. 总任务被直接分到多线程同时做，也就是多线程同时处理一个task。
2. 总任务拆了之后再分给不同的线程同时做，但是不同的线程做的任务是不同的。
3. 

### TCP/IP协议
1. Transmission Control Protocol传输
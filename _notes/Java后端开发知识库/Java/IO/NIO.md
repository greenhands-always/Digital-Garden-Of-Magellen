---
createDate: 2024-07-26
createTime: 2024-07-26 16:05
type: concept
tags:
  - K/CS/java/JDK
father:
  - "[[JDK标准库]]"
aliases:
  - 同步非阻塞I/O
title: NIO
---
Summary::同步阻塞模型，一个连接一个线程

NIO是Java 1.4引入的新IO模型，也称为同步非阻塞IO，它提供了一种基于[[事件驱动架构|事件驱动]]的方式来处理I/O操作。

相比于传统的BIO模型，NIO采用了Channel、Buffer和Selector等组件，线程可以对某个IO事件进行监听，并继续执行其他任务，不需要阻塞等待。当IO事件就绪时，线程会得到通知，然后可以进行相应的操作，实现了非阻塞式的高伸缩性网络通信。在NIO模型中，数据总是从Channel读入Buffer，或者从Buffer写入Channel，这种模式提高了IO效率，并且可以充分利用系统资源。
![Pasted image 20240729102258](https://obsidian-notes-of-huangyh.oss-cn-hangzhou.aliyuncs.com/Pasted%20image%2020240729102258.png)
NIO主要由三部分组成：**选择器**（Selector）、**缓冲**区（Buffer）和**通道**（Channel）。**Channel**是一个可以进行数据读写的对象，所有的数据都通过**Buffer**来处理，这种方式避免了直接将字节写入通道中，而是将数据写入包含一个或者多个字节的缓冲区。在多线程模式下，一个线程可以处理多个请求，这是通过将客户端的连接请求注册到多路复用器上，然后由多路复用器轮询到连接有I/O请求时进行处理。
- **通道（[[NIO Channel]]）**：Channel是**NIO**中用于数据读写的双向通道，可以从通道中读取数据，也可以将数据写入通道。与传统的IO不同，Channel是双向的，可以同时进行读写操作，而传统的IO只能通过**InputStream**或**OutputStream**进行单向读写。Java NIO中常见的Channel有：**FileChannel**（文件读写）、**DatagramChannel**（UDP协议）、**SocketChannel**（TCP协议）和**ServerSocketChannel**（监听TCP连接请求）等。
- **缓冲区（Buffer）：** Buffer是NIO中用于存储数据的缓冲区，可以理解为一个[容器](https://cloud.tencent.com/product/tke?from_column=20065&from=20065)，可以从中读取数据，也可以将数据写入其中。Buffer具有一组指针来跟踪当前位置、限制和容量等属性。Java NIO中提供了多种类型的Buffer，例如**ByteBuffer**、**CharBuffer**、**ShortBuffer**、**IntBuffer**等。每种类型的Buffer都有自己特定的读写方法，可以使用`get()`和`put()`等方法来读写缓冲区中的数据。
- **选择器（[[NIO Selector]]）：** Selector是NIO中用于监控多个Channel的选择器，可以实现单线程管理多个Channel。Selector可以检测多个Channel是否有事件发生，包括连接、接收、读取和写入等事件，并根据不同的事件类型进行相应处理。Selector可以有效地减少单线程管理多个Channel时的资源占用，提高程序的运行效率。
## 适用场景
NIO适用于连接数目多且连接比较短（轻操作）的架构，例如聊天服务器、弹幕系统、服务器间通讯等。它通过引入非阻塞通道的概念，提高了系统的伸缩性和并发性能。同时，NIO的使用也简化了程序编写，提高了开发效率。
## 特点
事件驱动模型、单线程处理多任务、非阻塞I/O，I/O读写不再阻塞，而是返回0、基于block的传输比基于流的传输更高效、更高级的IO函数zero-copy、IO多路复用大大提高了Java网络应用的可伸缩性和实用性。基于[[Reactor线程模型]]
## 优缺点
优点：
- **高并发性：** 使用选择器（Selector）和通道（Channel）的NIO模型可以在单个线程上处理多个连接，提供更高的并发性能。
- **节省资源：** 相对于BIO，NIO需要更少的线程来处理相同数量的连接，节省了系统资源。
- **灵活性：** NIO提供了多种类型的**Channel**和**Buffer**，可以根据需要选择适合的类型。NIO允许开发人员自定义协议、编解码器等组件，从而提高系统的灵活性和可扩展性。
- **高性能：** NIO采用了基于通道和缓冲区的方式来读写数据，这种方式比传统的流模式更高效。可以减少数据拷贝次数，提高数据处理效率。
- **内存管理**：NIO允许用户手动管理缓冲区的内存分配和回收，避免了传统**I/O**模型中的内存泄漏问题。
缺点：
- **编程复杂：** 相对于BIO，NIO的编程方式更加复杂，需要理解选择器和缓冲区等概念，也需要考虑多线程处理和同步问题。
- **可靠性较低：** NIO模型中，一个连接的读写操作是非阻塞的，无法保证IO操作的结果是可靠的，可能会出现部分读写或者错误的数据。

> - NIO的类库和API相当复杂，使用它来开发，需要非常熟练地掌握Selector、ByteBuffer、ServerSocketChannel、SocketChannel等。
> - 需要很多额外的编程技能来辅助使用NIO,例如，因为NIO涉及了Reactor线程模型，所以必须必须对多线程和网络编程非常熟悉才能写出高质量的NIO程序。
> - 想要有高可靠性，工作量和难度都非常的大，因为服务端需要面临客户端频繁的接入和断开、网络闪断、半包读写、失败缓存、网络阻塞的问题，这些将严重影响我们的可靠性，而使用原生NIO解决它们的难度相当大。
> - JDK NIO中著名的BUG--epoll空轮询，当select返回0时，会导致Selector空轮询而导致CUP100%，官方表示JDK1.6之后修复了这个问题，其实只是发生的概率降低了，没有根本上解决。
作者：FreddyChen  
链接：https://juejin.cn/post/6844903815846559757  
> 
  



NIO适合一些复杂的、高频的、长连接的通信场景，例如聊天室、网络游戏等。
## 操作流程
1. 打开通道并设置为非阻塞模式。
2. 将通道注册到选择器上，并指定感兴趣的事件类型（如连接打开、可读等）。
3. 线程通过调用选择器的`select()`方法等待事件发生。
4. 当有一个或多个事件发生时，线程可以从选择器中获取已经准备好的通道，并进行相应的IO操作。
5. IO操作完成后，关闭通道和选择器。
# 代码样例
## server端
```java
package Java.IO.NIODemo;  
import java.io.*;  
import java.net.*;  
import java.nio.ByteBuffer;  
import java.nio.channels.SelectionKey;  
import java.nio.channels.Selector;  
import java.nio.channels.ServerSocketChannel;  
import java.nio.channels.SocketChannel;  
import java.util.Iterator;  
import java.util.Set;  
public class NIOServer {  
    public static void main(String[] args) throws IOException {  
        // Selector是抽象类,根据具体的平台选择实现类,windows下使用WindowsSelectorImpl实现类,linux下使用EPollSelectorImpl实现类  
        Selector selector = Selector.open();  
        // 创建一个ServerSocketChannel并绑定到指定的端口  
        ServerSocketChannel serverSocketChannel = ServerSocketChannel.open();  
        serverSocketChannel.bind(new InetSocketAddress(9999));  
        // 设置为非阻塞模式  
        serverSocketChannel.configureBlocking(false);  
        // 将ServerSocketChannel注册到Selector上,并监听OP_ACCEPT事件,ServerSocketChannel只需要关注ACCEPT事件
        serverSocketChannel.register(selector, SelectionKey.OP_ACCEPT);  
        System.out.println("服务器已启动,等待客户端连接...");  
        while (true) {  
            // 在没有事件发生时,线程阻塞;反之,则线程恢复运行  
            selector.select();  
            // 处理事件,SelectionKey 内部包含了所有发生的事件  
            Set<SelectionKey> selectedKeys = selector.selectedKeys();  
            Iterator<SelectionKey> keyIterator = selectedKeys.iterator();  
            while (keyIterator.hasNext()) {  
                SelectionKey key = keyIterator.next();  
                // 根据事件类型分别处理  
                if (key.isAcceptable()) {  
                    // 处理连接请求事件  
                    SocketChannel client = serverSocketChannel.accept();  
                    client.configureBlocking(false);  
                    client.register(selector, SelectionKey.OP_READ|SelectionKey.OP_WRITE|SelectionKey.OP_CONNECT);
                    // 必须手动移除SelectionKey,否则会导致已被处理过的事件再次被处理,引发错误  
                    keyIterator.remove();  
                } else if (key.isReadable()) {  
                    SocketChannel client = (SocketChannel) key.channel();  
                    client.getRemoteAddress();  
                    //分配缓存区容量  
                    ByteBuffer buffer = ByteBuffer.allocate(1024);  
                    try {  
                        // 在客户端主动断开连接的时候, read()方法会返回-1,需要关闭客户端连接  
                        int read = client.read(buffer);  
                        if (read == -1) {  
                            // 取消此事件,并关闭连接  
                            key.cancel();  
                            client.close();  
                        } else {  
                            buffer.flip();  
                            buffer.clear();  
                        }  
                        String output = new String(buffer.array()).trim();  
                        Socket socket = client.socket();  
                        InetAddress inetAddress = socket.getInetAddress();  
                        int port = socket.getPort();  
                        String clientInfo = inetAddress+":"+port;  
                        String message = String.format("来自客户端 %s , 消息：%s", clientInfo , output);  
                        System.out.println(message);  
                        System.out.print("回复消息: ");  
                        NIOUtil.writeMessage(selector, client, buffer);  
                        // 必须手动移除SelectionKey,否则会导致已被处理过的事件再次被处理,引发错误  
                        keyIterator.remove();  
                    } catch (IOException e) {  
                        e.printStackTrace();  
                        // 取消此事件,并关闭连接  
                        key.cancel();  
                        client.close();  
                        // 必须手动移除SelectionKey,否则会导致已被处理过的事件再次被处理,引发错误  
                        keyIterator.remove();  
                    }  
                }  
            }  
        }  
    }  
}
```
## client
```java
package Java.IO.NIODemo;  
import java.io.*;  
import java.net.InetSocketAddress;  
import java.nio.ByteBuffer;  
import java.nio.channels.SelectionKey;  
import java.nio.channels.Selector;  
import java.nio.channels.SocketChannel;  
import java.util.Iterator;  
import java.util.Scanner;  
import java.util.Set;  
public class NIOClient {  
    public static void main(String[] args) throws IOException {  
        Selector selector = Selector.open();  
        SocketChannel socketChannel = SocketChannel.open();  
        socketChannel.configureBlocking(false);  
        socketChannel.connect(new InetSocketAddress("localhost", 9999));  
        socketChannel.register(selector, SelectionKey.OP_CONNECT);  
        while (true) {  
            selector.select();  
            Set<SelectionKey> selectedKeys = selector.selectedKeys();  
            Iterator<SelectionKey> keyIterator = selectedKeys.iterator();  
            while (keyIterator.hasNext()) {  
                SelectionKey key = keyIterator.next();  
                if (key.isConnectable()) {  
                    SocketChannel client = (SocketChannel) key.channel();  
                    if (client.isConnectionPending()) {  
                        client.finishConnect();  
                    }  
                    System.out.print("Enter message to server: ");  
                    Scanner scanner = new Scanner(System.in);  
                    String message = scanner.nextLine();  
                    ByteBuffer buffer = ByteBuffer.wrap(message.getBytes());  
                    client.write(buffer);  
                    client.register(selector, SelectionKey.OP_READ);  
                } else if (key.isReadable()) {  
                    SocketChannel client = (SocketChannel) key.channel();  
                    ByteBuffer buffer = ByteBuffer.allocate(1024);  
                    client.read(buffer);  
                    String output = new String(buffer.array()).trim();  
                    System.out.println("来自客户端的消息: " + output);  
                    System.out.print("输入消息: ");  
                    // 和服务端代码一样  
                    NIOUtil.writeMessage(selector, client, buffer);  
                }  
                keyIterator.remove();  
            }  
        }  
    }  
}
```
## Util
```java
package Java.IO.NIODemo;  
import java.io.IOException;  
import java.nio.ByteBuffer;  
import java.nio.channels.SelectionKey;  
import java.nio.channels.Selector;  
import java.nio.channels.SocketChannel;  
import java.util.Scanner;  
public class NIOUtil {  
    static void writeMessage(Selector selector, SocketChannel client, ByteBuffer buffer) throws IOException {  
        Scanner scanner = new Scanner(System.in);  
        String message = scanner.nextLine();  
        buffer.clear();  
        buffer.put(message.getBytes());  
        //从写模式切换到读模式  
        buffer.flip();  
        while (buffer.hasRemaining()) {  
            client.write(buffer);  
        }  
        //  重新监听OP_ACCEPT事件  
        client.register(selector, SelectionKey.OP_READ);  
    }  
}
```
# 参考文章
[从理论到实践：深度解读BIO、NIO、AIO的优缺点及使用场景-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2337352)
[【Netty】「NIO」（三）剖析 Selector-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2319786)

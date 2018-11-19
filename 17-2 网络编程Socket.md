# 17-2 **网络编程Socket**
**2. IP地址**
概念：所谓IP地址就是给每个连接在互联网上的主机分配的一个32位地址;IP是互联网上的每一台计算机都有得一个唯一表示自己的标记。  
IPv4：32位，分4段。每段4个8位（0-255）的十进制表示。
IPv6：128位，分8段。0000~FFFF的十六进制用**冒号**分开。
**4.网络协议TCP&UDP**  
**什么是TCP**  

- 概念：Transmission Control Protocol 传输控制协议 TCP 是一种面向连接（连接导向）的，可靠的，基于**字节流**的运输层(Transport layer)通讯协议；当客户和服务彼此交互数据前，必须先在双方之间建立一个TCP连接，之后才能传输数据。  
- 重点是此协议中有两个类`Socket`和`ServerSocket`其中有一些方法，**能够实现在两个不同的终端之间传输数据**(服务器-客户端)  
![](https://photos-4.dropbox.com/t/2/AADd06mokVk1KUHwod5ZufLBmurDch9XNi2yeSakb43GgQ/12/82155074/png/1600x1/4/1539100800/0/10/image.png/_/png%2520https%253A%252F%252Fd2mxuefqeaa7sj.cloudfront.net%252Fs_7DDD195A9AAC877FD95D4BCB902EEA9BBD80A33A5546A1F296FE47344F5069B7_1539083182064_Socket.png?preserve_transparency=1&size=1600x1&size_mode=4)


  
**客户端**

    package com.fs.pojo04;
    
    import java.io.IOException;
    import java.io.PrintStream;
    import java.net.InetAddress;
    import java.net.Socket;
    import java.net.UnknownHostException;
    
    public class SocketTest  {
        public SocketTest() throws UnknownHostException, IOException{
            this.run();
            System.out.println("Socket running");
        }
        public void run() throws UnknownHostException, IOException {
            Socket s = new Socket(InetAddress.getLocalHost(), 6666);
            PrintStream ps = new PrintStream(s.getOutputStream());
            ps.close();
            s.close();
        }
    
        public static void main(String[] args) throws UnknownHostException, IOException  {
            new SocketTest();
        }
    }

**服务器**  

    package com.fs.pojo04;
    
    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.net.ServerSocket;
    import java.net.Socket;
    public class ServerSocketTest  {
        public ServerSocketTest() throws IOException {
            this.run();
        }
        public void run() throws IOException {
            ServerSocket s = new ServerSocket(6666);
            Socket client = s.accept();
            BufferedReader br = new BufferedReader(new InputStreamReader(client.getInputStream()));
            s.close();
            br.close();
        }
        public static void main(String[] args) throws IOException  {
            new ServerSocketTest();
        }
    }

**5. UDP协议**
**什么是UDP协议**  

1. 概念： 用户数据报协议，是一个简单的面向数据报的运输层协议，UDP不提供可靠性，他只是把应用程序传给IP层的数据报发送出去，但是并不能保证他们能够达到目的地。由于UDP在传输报前不用再客户端和服务器之间建立一个连接，并且没有超时重发机制，故而传输速度快。  
2. TCP的所操作必须建立可靠的连接，这样会浪费很大的性能，为此UDP这种不可靠的连接出现。  
3. UDP开发中使用DatagramPacket包装一条要发送的消息，之后使用DatagramSocket完成发送操作，也能实现在两个终端之间传送数据。  
4. **传输**  
    package com.fs.pojo05;
    
    import java.net.DatagramPacket;
    import java.net.DatagramSocket;
    import java.net.InetAddress;
    
    public class DSender {
        public static void main(String[] args) throws Exception {
            DatagramSocket ds = new DatagramSocket();
            String str = "Welcome java";
            InetAddress ip = InetAddress.getByName("127.0.0.1");
            DatagramPacket dp = new DatagramPacket(str.getBytes(), str.length(), ip, 3000);
            ds.send(dp);
            ds.close();
        }
    }

**接收**

    package com.fs.pojo05;
    
    import java.net.DatagramPacket;
    import java.net.DatagramSocket;
    
    public class DReceiver {
        public static void main(String[] args) throws Exception {
            DatagramSocket ds = new DatagramSocket(3000);
            byte[] buf = new byte[1024];
            DatagramPacket dp = new DatagramPacket(buf, 1024);
            ds.receive(dp);
            String str = new String(dp.getData(), 0, dp.getLength());
            System.out.println(str);
            ds.close();
        }
    }

**TCP和UDP的区别**  

1. 基于连接（TCP）与无连接（UDP）；  
2. 对系统资源的要求（TCP较多，UDP少）；  
3. UDP程序结构较简单 ；    
4. 流模式（TCP）与数据报模式（UDP） ；
5. TCP保证数据正确性，UDP可能丢包，TCP保证数据顺序，UDP不保证；  


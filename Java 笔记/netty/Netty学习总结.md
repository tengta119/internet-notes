# Netty

![image-20250207132246111](C:\Users\11922\AppData\Roaming\Typora\typora-user-images\image-20250207132246111.png)





## EventLoopGroup

**EventLoopGroup**可以理解为线程池，**eventloop**可以理解成线程

多个**eventloop**组成**EventLoopGroup**，**eventloop**主要处理**channel**上的io事件

```java
        new ServerBootstrap()
                // boss, worker
                //boss 只负责 NioServerSocketChannel 上 accept事件， worker 只负责 socketChannel 上的读写
                //第一个是boss，第二个是worker
                .group(new NioEventLoopGroup(), new NioEventLoopGroup())
                .channel(NioServerSocketChannel.class)
                .childHandler(new ChannelInitializer<NioSocketChannel>() {
                    @Override
                    protected void initChannel(NioSocketChannel ch) throws Exception {
                        ch.pipeline().addLast( "handler - 1", new ChannelInboundHandlerAdapter() {
                            @Override
                            public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
                                ByteBuf buf = (ByteBuf) msg;
                                log.debug(buf.toString(Charset.defaultCharset()));
                                ctx.fireChannelRead(msg); //将数据传递给x
                            }
                        }).addLast(group, "handler - 2", new ChannelInboundHandlerAdapter() {
                            @Override
                            public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
                                ByteBuf buf = (ByteBuf) msg;
                                log.debug(buf.toString(Charset.defaultCharset()));
                            }
                        });
                    }
                })
                .bind("127.0.0.1", 8888);
```

```java
.group(new NioEventLoopGroup(), new NioEventLoopGroup())
```

第一个group主要处理accept事件，第二个group主要处理可读可写事件，每当一个channel连接时，会固定与一个eventloop连接

```java
.addLast(group, "handler - 2", new ChannelInboundHandlerAdapter() {
                            @Override
                            public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
                                ByteBuf buf = (ByteBuf) msg;
                                log.debug(buf.toString(Charset.defaultCharset()));
                            }
                        });
```

在"handler - 2"中，专门添加一个group来处理这个handler，是为了防止worker处理该handler时间过长导致阻塞其他channel的事件



## channelFuture

### 处理连接

```java
        ChannelFuture channelFuture = new Bootstrap()
                .group(new NioEventLoopGroup())
                .channel(NioSocketChannel.class)
                .handler(new ChannelInitializer<SocketChannel>() {
                    @Override
                    protected void initChannel(SocketChannel ch) throws Exception {
                        ch.pipeline().addLast(new StringEncoder());
                    }
                })
                //连接到服务器
                //异步非阻塞， main发起了调用，真正执行connect是nio线程
                .connect(new InetSocketAddress("127.0.0.1", 8888));
```

**connect()**是异步操作

```java
        阻塞当前线程直到nio线程建立连接完毕
        channelFuture.sync();
```

```java
        //2.2 使用addListener(回调对象) 异步处理结果
        channelFuture.addListener(new ChannelFutureListener() {
            @Override
            //在 nio 线程建立连接后，会调用operationComplete
            public void operationComplete(ChannelFuture future) throws Exception {
                Channel channel = future.channel();
                log.debug(channel.toString());
                channel.writeAndFlush("hello world");
            }
        });
```

### 处理关闭

```java
        NioEventLoopGroup group = new NioEventLoopGroup();
        ChannelFuture channelFuture = new Bootstrap()
                .group(group)
                .channel(NioSocketChannel.class)
                .handler(new ChannelInitializer<SocketChannel>() {
                    @Override
                    protected void initChannel(SocketChannel ch) throws Exception {
                        ch.pipeline().addLast(new LoggingHandler(LogLevel.DEBUG));
                        ch.pipeline().addLast(new StringEncoder());
                    }
                })
                .connect(new InetSocketAddress("127.0.0.1", 8888));

        Channel channel = channelFuture.sync().channel();
        new Thread(() -> {
            Scanner scanner = new Scanner(System.in);
            while (scanner.hasNextLine()) {
                String s = scanner.nextLine();
                if ("q".equals(s)) {
                    //close异步操作
                    channel.close();
                    break;
                } else {
                    channel.writeAndFlush(s);
                }
            }
        }, "input").start();
```

**channel.close()**是异步操作

```java
        同步处理关闭
        closeFuture.sync();
```

```java
        //异步处理关闭
        closeFuture.addListener(new ChannelFutureListener() {
            @Override
            public void operationComplete(ChannelFuture future) throws Exception {
                log.debug("处理关闭之后的操作");
                group.shutdownGracefully();
            }
        });
```



## NettyPromise

| 功能/名称    | jdk Future                     | netty Future                                                 | Promise      |
| ------------ | ------------------------------ | ------------------------------------------------------------ | ------------ |
| cancel       | 取消任务                       | -                                                            | -            |
| isCanceled   | 任务是否取消                   | -                                                            | -            |
| isDone       | 任务是否完成，不能区分成功失败 | -                                                            | -            |
| get          | 获取任务结果，阻塞等待         | -                                                            | -            |
| getNow       | -                              | 获取任务结果，非阻塞，还未产生结果时返回 null                | -            |
| await        | -                              | 等待任务结束，如果任务失败，不会抛异常，而是通过 isSuccess 判断 | -            |
| sync         | -                              | 等待任务结束，如果任务失败，抛出异常                         | -            |
| isSuccess    | -                              | 判断任务是否成功                                             | -            |
| cause        | -                              | 获取失败信息，非阻塞，如果没有失败，返回null                 | -            |
| addLinstener | -                              | 添加回调，异步接收结果                                       | -            |
| setSuccess   | -                              | -                                                            | 设置成功结果 |
| setFailure   | -                              | -                                                            | 设置失败结果 |

promise是主线程与普通线程之间的容器

### jdk Future

```java
        ExecutorService service = Executors.newFixedThreadPool(2);
        Future<Integer> future = service.submit(new Callable<Integer>() {
            @Override
            public Integer call() throws Exception {
                Thread.sleep(2000);
                log.debug("正在计算");
                return 20;
            }
        });

        log.debug("结果：{}", future.get());
```

get()等待线程返回结果，阻塞等待



### NettyFuture

```java
        NioEventLoopGroup group = new NioEventLoopGroup();
        EventLoop next = group.next();

        Future<Integer> future = next.submit(new Callable<Integer>() {
            @Override
            public Integer call() throws Exception {
                Thread.sleep(2000);
                log.debug("计算完成");
                return 10;
            }
        });
        
        future.addListener(new GenericFutureListener<Future<? super Integer>>() {
            @Override
            public void operationComplete(Future<? super Integer> future) throws Exception {
                log.debug("接收结果：{}", future.getNow());
            }
        });
```

异步处理，当Future完成操作后，会触发addListener()



### NettyPromise

```java
        EventLoop eventLoop = new NioEventLoopGroup().next();
        DefaultPromise<Integer> promise = new DefaultPromise<>(eventLoop);

        new Thread(()->{
            try {
                Thread.sleep(1000);
                log.debug("计算成功");
                promise.setSuccess(12); //b
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }).start();

        log.debug("计算结果：{}",promise.get());
```



## pipeline

```java
        new ServerBootstrap()
                .group(new NioEventLoopGroup())
                .channel(NioServerSocketChannel.class)
                .childHandler(new ChannelInitializer<NioSocketChannel>() {
                    @Override
                    protected void initChannel(NioSocketChannel ch) throws Exception {
                        ChannelPipeline pipeline = ch.pipeline();
                        // head -> h1 -> tail
                        pipeline.addLast("h1", new ChannelInboundHandlerAdapter() {
                            @Override
                            public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
                                log.debug("h1 - 1");
                                ByteBuf buf = (ByteBuf) msg;
                                String s = buf.toString(Charset.defaultCharset());
                                super.channelRead(ctx, s); //传递给下一个handler
                            }
                        });

                        pipeline.addLast("h2", new ChannelInboundHandlerAdapter() {
                            @Override
                            public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
                                log.debug("h2 - 2");
                                super.channelRead(ctx, msg);
                            }
                        });
                        //head -> h1 -> h2 -> h3 -> tail 双向链表
                        pipeline.addLast("h3", new ChannelInboundHandlerAdapter() {
                            @Override
                            public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
                                log.debug("h3 - 3");
                                //super.channelRead(ctx, msg); 4, 5, 6都是出站，不需要super.channelRead(ctx, msg)

                                //从后往前找出栈处理器，从h3往前找是否有出栈处理器
                                //ctx.writeAndFlush(ctx.alloc().buffer().writeBytes("server".getBytes(Charset.defaultCharset())));

                                //ch从tail开始找出站处理器
      				 ch.writeAndFlush(ctx.alloc().buffer().writeBytes("server".getBytes(Charset.defaultCharset())));
                            }
                        });


                        //出站处理器，只有向channel写入数据才会触发
                        //head -> h1 -> h2 -> h3 -> h4 -> h5 -> h6 -> tail 出站是从tail开始处理
                        pipeline.addLast("h4", new ChannelOutboundHandlerAdapter() {
                            @Override
                            public void write(ChannelHandlerContext ctx, Object msg, ChannelPromise promise) throws Exception {
                                log.debug("h4 - 4");
                                super.write(ctx, msg, promise);
                            }
                        });
                        pipeline.addLast("h5", new ChannelOutboundHandlerAdapter() {
                            @Override
                            public void write(ChannelHandlerContext ctx, Object msg, ChannelPromise promise) throws Exception {
                                log.debug("h5 - 5");
                                super.write(ctx, msg, promise);
                            }
                        });
                        pipeline.addLast("h6", new ChannelOutboundHandlerAdapter() {
                            @Override
                            public void write(ChannelHandlerContext ctx, Object msg, ChannelPromise promise) throws Exception {
                                log.debug("h6 - 6");
                                super.write(ctx, msg, promise);
                            }
                        });

                    }
                })
                .bind("127.0.0.1", 8899);
```



###  通道初始化与处理器链

- **`ChannelInitializer`**：用于初始化新的通道，在通道注册到事件循环组后，会自动调用`initChannel`方法来初始化通道的处理器链。
- **`ChannelPipeline`**：通道的处理器链，是一个双向链表，包含了一系列的入站和出站处理器。处理器按照添加的顺序依次处理网络事件。
- **`Handler`**：在内部有头处理器和尾处理器，如果bytebuf传递到头处理器或者尾处理器，bytebuf会释放，但是还是建议在自定义的handler中手动处理bytebuf释放问题



###  入站处理器（`ChannelInboundHandler`）

- **`ChannelInboundHandlerAdapter`**：入站处理器的适配器类，用于处理入站事件，如`channelRead`方法用于处理接收到的数据。
- **`channelRead`方法**：当有数据到达通道时，会调用该方法。在该方法中，可以对数据进行处理，并通过`super.channelRead(ctx, msg)`将数据传递给下一个入站处理器。



###  出站处理器（`ChannelOutboundHandler`）

- **`ChannelOutboundHandlerAdapter`**：出站处理器的适配器类，用于处理出站事件，如`write`方法用于处理向通道写入数据的操作。
- **`write`方法**：当需要向通道写入数据时，会调用该方法。在该方法中，可以对要写入的数据进行处理，并通过`super.write(ctx, msg, promise)`将数据传递给下一个出站处理器。



## ByteBuf







## 粘包半包

TCP 是流式协议，消息无边界

![image-20250213160224001](C:/Users/11922/AppData/Roaming/Typora/typora-user-images/image-20250213160224001.png)

> * 窗口实际就起到一个缓冲区的作用，同时也能起到流量控制的作用
>
>   * 图中深色的部分即要发送的数据，高亮的部分即窗口
>   * 窗口内的数据才允许被发送，当应答未到达前，窗口必须停止滑动
>   * 如果 1001~2000 这个段的数据 ack 回来了，窗口就可以向前滑动
>   * 接收方也会维护一个窗口，只有落在窗口内的数据才能允许接收

### 预设长度

```java
// 最大长度，长度偏移，长度占用字节，长度调整，剥离字节数
ch.pipeline().addLast(new LengthFieldBasedFrameDecoder(1024, 0, 1, 0, 1));
```

![image-20250213160900654](C:/Users/11922/AppData/Roaming/Typora/typora-user-images/image-20250213160900654.png)
下面是对 `LengthFieldBasedFrameDecoder` 构造函数参数的详细解释：

- `maxFrameLength` (1024)：这是可以接收的最大帧长度。如果帧的长度超过这个值，将会抛出 `TooLongFrameException` 异常。这个参数确保了不会处理过大的帧，从而避免内存溢出。
- `lengthFieldOffset` (0)：这是长度字段的偏移量，即长度字段在帧中的起始位置（从0开始计数）。参数值为0表示长度字段位于帧的开始。
- `lengthFieldLength` (1)：这是长度字段的长度，即长度字段本身的字节数。参数值为1表示长度字段是一个字节。
- `lengthAdjustment` (0)：这是长度调整值。在某些情况下，帧的实际数据可能不在长度字段之后立即开始，可能还需要跳过一些额外的字节。如果需要跳过这些字节，就可以通过这个参数进行调整。如果长度字段之后立即是帧的数据，则这个值通常为0。
- `initialBytesToStrip` (1)：这是解码后从帧中跳过的字节数。如果这个值为0，解码器将返回整个帧（包括长度字段）。如果值为1，解码器将从返回的帧中跳过长度字段。



## 协议设计与解析

### 自定义协议要素

* 魔数，用来在第一时间判定是否是无效数据包
* 版本号，可以支持协议的升级
* 序列化算法，消息正文到底采用哪种序列化反序列化方式，可以由此扩展，例如：json、protobuf、hessian、jdk
* 指令类型，是登录、注册、单聊、群聊... 跟业务相关
* 请求序号，为了双工通信，提供异步能力
* 正文长度
* 消息正文

### 编解码器

```java
    @Override
    //出站时将信息编写成byteBuf
    protected void encode(ChannelHandlerContext ctx, Message msg, ByteBuf out) throws Exception {
        // 1. 4 字节的魔数
        out.writeBytes(new byte[]{1, 2, 3, 4});
        // 2. 1 字节的版本,
        out.writeByte(1);
        // 3. 1 字节的序列化方式 jdk 0 , json 1
        out.writeByte(0);
        // 4. 1 字节的指令类型
        out.writeByte(msg.getMessageType());
        // 5. 4 个字节
        out.writeInt(msg.getSequenceId());
        // 无意义，对齐填充
        out.writeByte(0xff);
        // 6. 获取内容的字节数组
        ByteArrayOutputStream bos = new ByteArrayOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(bos);
        oos.writeObject(msg);
        byte[] bytes = bos.toByteArray();
        // 7. 长度
        out.writeInt(bytes.length);
        // 8. 写入内容
        out.writeBytes(bytes);
    }

    @Override
    //入站时将信息编写成对应类型
    protected void decode(ChannelHandlerContext ctx, ByteBuf in, List<Object> out) throws Exception {
        int magicNum = in.readInt();
        byte version = in.readByte();
        byte serializerType = in.readByte();
        byte messageType = in.readByte();
        int sequenceId = in.readInt();
        in.readByte();
        int length = in.readInt();
        byte[] bytes = new byte[length];
        in.readBytes(bytes, 0, length);
        ObjectInputStream ois = new ObjectInputStream(new ByteArrayInputStream(bytes));
        Message message = (Message) ois.readObject();
        log.debug("{}, {}, {}, {}, {}, {}", magicNum, version, serializerType, messageType, sequenceId, length);
        log.debug("{}", message);
        out.add(message);
    }
```


#### RESTful

一种软件架构风格，设计风格而不是标准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。

在 REST 样式的 Web 服务中，每个资源都有一个地址。资源本身都是方法调用的目标，方法列表对所有资源都是一样的。这些方法都是标准方法，包括 HTTP GET、POST、PUT、DELETE，还可能包括 HEADER 和 OPTIONS。

优势在于能够穿透防火墙，使用方便，语言无关，基本上可以使用各种开发语言实现的系统，都可以接受Restful 的请求。 但性能和带宽占用上有劣势。


#### RPC

RPC（Remote Procedure Call Protocol）就是远程调用。远程调用免不了消息通信，所以本质上都是一种通信。RPC应该有各种各样的协议，基于或扩展与socket，HTTP等协议。

以Apache Thrift为代表的二进制RPC，支持多种语言（但不是所有语言），四层通讯协议，性能高，节省带宽。相对Restful协议，使用Thrifpt RPC，在同等硬件条件下，带宽使用率仅为前者的20%，性能却提升一个数量级。但是这种协议最大的问题在于，无法穿透防火墙。


#### RPC VS RESTful

- 从使用方面看，Http接口只关注服务提供方，对于客户端怎么调用，调用方式怎样并不关心，通常情况下，我们使用Http方式进行调用时，只要将内容进行传输即可，这样客户端在使用时，需要更关注网络方面的传输，比较不适用与业务方面的开发；而RPC服务则需要客户端接口与服务端保持一致，服务端提供一个方法，客户端通过接口直接发起调用，业务开发人员仅需要关注业务方法的调用即可，不再关注网络传输的细节，在开发上更为高效。

- 从性能角度看，使用Http时，Http本身提供了丰富的状态功能与扩展功能，但也正由于Http提供的功能过多，导致在网络传输时，需要携带的信息更多，从性能角度上讲，较为低效。而RPC服务网络传输上仅传输与业务内容相关的数据，传输数据更小，性能更高。

- 从运维角度看，使用Http接口时，常常使用一个前端代理，来进行Http转发代理请求的操作，需要进行扩容时，则需要去修改代理服务器的配置，较为繁琐，也容易出错。而使用RPC方式的微服务，则只要增加一个服务节点即可，注册中心可自动感知到节点的变化，通知调用客户端进行负载的动态控制，更为智能，省去运维的操作。
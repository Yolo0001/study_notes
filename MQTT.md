# MQTT

![image-20220815161649249](C:\Users\26871\AppData\Roaming\Typora\typora-user-images\image-20220815161649249.png)

![image-20220815161705072](C:\Users\26871\AppData\Roaming\Typora\typora-user-images\image-20220815161705072.png)

![image-20220815161718571](C:\Users\26871\AppData\Roaming\Typora\typora-user-images\image-20220815161718571.png)

## Retain

订阅者只能接收在订阅之后发布的消息，但如果发布者事先发布了 带有 Retain 标志的消息，那么订阅者就能在订阅后马上收到消息。 当发布者发布了带有 Retain 标志的消息时，中介会把消息传递给 订阅了主题的订阅者，同时保存带有 Retain 标志的最新的消息。此时， 若别的订阅者订阅了主题，就能马上收到带有 Retain 标志的新消息

![image-20220815161818668](C:\Users\26871\AppData\Roaming\Typora\typora-user-images\image-20220815161818668.png)

## Will

Will 有“遗言”的意思。由于中介的 I/O 错误或网络故障等情况， 发布者可能会突然从中介断开，Will 就是专门针对于这种情况的一个机 构，它用于定义中介向订阅者发送的消息（图 2.15）。 发布者在连接中介时会用到 CONNECT（连接）消息，连接时对其 指定 Will 标志、要发送的消息以及 QoS。这样一来，如果连接意外断 开，Will 消息就会被传递给订阅者。另外，还有一个标志叫作 Will  Retain。通过指定这个标志，就能跟前面说的 Retain 达到同样的效果， 即在中介处保存消息。

## Clean session

![image-20220815162349582](C:\Users\26871\AppData\Roaming\Typora\typora-user-images\image-20220815162349582.png)
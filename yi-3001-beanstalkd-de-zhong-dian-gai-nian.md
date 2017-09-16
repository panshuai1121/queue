# Beanstalkd重点概念

---

## tubo（管道）

一个Beanstalkd可以支持多个tube（管道），每个tube（管道）有自己的producer（生产者）/worker（消费者），tube之间相互不影响。一个job（任务）的生命周期永远都会在同一个tube中；

## Job（任务）

Beanstalkd 用任务 \(job\) 代替消息 \(message\) 的概念，Job 是一个需要异步处理的任务，**job 需要放在 tubo 中**

与消息不同，job有一系列的状态

![](http://ww2.sinaimg.cn/mw600/68c3cad3jw1dpsqabts9dj.jpg)

* **READY - 需要立即处理的任务，当延时 \(DELAYED\) 任务到期后会自动成为当前任务；**
* **DELAYED - 延迟执行的任务, 当消费者处理任务后, 可以用将消息再次放回 DELAYED 队列延迟执行；**
* **RESERVED - 已经被消费者获取, 正在执行的任务。Beanstalkd 负责检查任务是否在 TTR\(time-to-run\) 内完成；**
* **BURIED - 保留的任务: 任务不会被执行，也不会消失，除非有人把它 “踢” 回队列；**
* **DELETED - 消息被彻底删除。Beanstalkd 不再维持这些消息。**

## producer （生产者）

任务job的生产者，通过put命令将一个job（任务） 放到一个tubo\(管道\)中。

## consumer（消费者）

任务（`job`）的消费者，通过`reserve、release、bury、delete`命令来获取或改变`job`的状态。




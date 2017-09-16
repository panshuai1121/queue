# Beanstalked的优先级（priority）

job可以有0~2^32个优先级，0代表最高优先级，小于1024的优先级beanstalkd认为是urgent。beanstalkd使用最大最小堆来实现优先级排序，任何时刻调用reserve命令，拿到的都是优先级最高的job，时间复杂度是O\(logN\)。

* 延时任务 \(delay\)  
  有两种方式可以延时执行任务\(job\): 生产者发布任务时指定延时\(put with delay\)；或者当任务处理完毕后, 消费者再次将任务放入队列延时执行\(release with delay\)。这种机制可以实现分布式的 java.util.Timer，这种分布式定时任务的优势是：如果某个消费者节点故障，任务超时重发 \(time-to-run\) 能够保证任务转移到另外的节点执行。

* 任务超时重发 \(time-to-run\)  
  Beanstalkd 把任务返回给消费者以后，消费者必须在预设的 TTR \(time-to-run\) 时间内发送 delete / release/ bury 改变任务状态；否则 Beanstalkd 会认为消息处理失败，然后把任务交给另外的消费者节点执行。如果消费者预计在 TTR \(time-to-run\) 时间内无法完成任务, 也可以发送 touch 命令, 它的作用是让 Beanstalkd 从系统时间重新计算 TTR \(time-to-run\).

* 任务预留 \(buried\)  
  如果任务因为某些原因无法执行, 消费者可以把任务置为 buried 状态让 Beanstalkd 保留这些任务。管理员可以通过 peek buried 命令查询被保留的任务，并且进行人工干预。简单的, kick能够一次性把 n 条被保留的任务踢回队列。




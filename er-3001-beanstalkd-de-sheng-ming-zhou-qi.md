# Beanstalkd的生命周期

---

![](https://cdn.itbilu.com/beanstalkd-job-status.png)

job 代替了 message的概念，任务有一系列的状态，生命周期如下：

一个`Beanstalkd`任务可能会包含以下状态：

* **`READY`- 需要立即处理的任务**。当`producer`直接`put`一个任务时，任务就处于`READY`状态，以等待`consumer`来处理。当延时 \(`DELAYED`\) 任务到期后会自动成为当前`READY`状态的任务
* `DELAYED`- 延迟执行的任务。当任务被延时`put`时，任务就处于`DELAYED`状态。等待时间过后，任务会被迁移到`READY`
  状态。当消费者处理任务后，可以用将消息再次放回`DELAYED`队列延迟执行
* `RESERVED` 已经被消费者获取，正在执行的任务。当`consumer`获取了当前`READY`的任务后，该任务的状态就会到`RESERVED`
  状态，这时其它的`consumer`就不能再操作该任务。`Beanstalkd`会检查任务是否在`TTR`\(time-to-run\)内完成
* `BURIED`- 保留的任务，这时任务不会被执行，也不会消失。当`consumer`完成该任务后，可以选择`delete`、`release`或者
  `bury`操作，`delete`后，任务会被删除，生命周期结束；`release`操作可以重新把任务状态迁移回`READY`或`DELAYED`状态，使其他`consumer`可以继续获取和执行该任务`bury`会拔任务休眠，等需要该任务时，再将休眠的任务`kick`回`READY`；也可能过`delete`删除`BURIED`状态的任务
* `DELETED`- 消息被删除，`Beanstalkd`不再维持这些消息。即任务生命周期结束。




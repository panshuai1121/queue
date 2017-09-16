# Beanstalkd重点概念

## tubo（管道）

一个Beanstalkd可以支持多个tube（管道），每个tube（管道）有自己的producer（生产者）/worker（消费者），tube之间相互不影响。一个job（任务）的生命周期永远都会在同一个tube中；

## Job（任务）




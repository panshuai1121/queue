# 适用场景

## 延时系统

比如延迟20分钟发送短信，在投放的时候就设定一定的延迟时间值，让任务在延迟时间到了之后进入ready队列，等待worker预订处理。

## 轮询系统

一个被投放的任务，在延迟时间过后需要再检查一遍状态，如果不符合，继续释放（release with delay）为延迟投放状态（DELAYED），直到时间过期之后，再次进入ready队列，被worker预订，进行一些逻辑判断，比如微信银行卡退款是否成功，如果成功，删除该任务，如果没成功，继续释放（release with delay）为延迟投放状态。

![](http://cpper.info/public/img/beanstalkd_job_status.png)


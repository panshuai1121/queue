# Beanstalkd重点概念

## tubo（管道）

一个Beanstalkd可以支持多个tube（管道），每个tube（管道）有自己的producer/worker，tube之间相互不影响。一个job的生命周期永远都会在同一个tube中






# Yii2中的使用

可以使用composer一条命令直接安装，但是为了更清晰，知道composer 安装在了哪里，用另外一种方式进行安装

### 一、在项目目录的compser.json 文件中添加如下配置

```
{
  "require": {
  ...
    "udokmeci/yii2-beanstalk" : "dev-master"
  }
}
```

执行

```
$> composer update
```

### 二、在组件的主配置文件和控制台配置文件中添加以内容

```
'components' => [
    // ...
    'beanstalk' => [
        'class' => 'udokmeci\yii2beanstalk\Beanstalk',
        'host' => 127.0.0.1, // default host
        'port' => 11300,
        'connectTimeout' => 1,
        'sleep' => false, // or int for usleep after every job
    ],
    // ...
],
```

### 三、在confg 下的console.php 中添加

```
...
'params' => $params,
// add you controller with name and class name next to params.
'controllerMap' => [
        'worker'=>[
            'class' => 'app\commands\WorkerController',
        ]

    ],
```

### 四、开启服务

```
beanstalkd -l 127.0.0.1 -p 11300
```

### 五、进行测试




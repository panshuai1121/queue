# phpBeanstalkdAdmin

---

这个是一个可视化工具，可以看见beanstalkd的当前的队列的状态

![](http://upload-images.jianshu.io/upload_images/26326-b79d0a8f193d342c.png?imageView2/2/w/1240/q/100)

## 安装方法

下载phpBeanstalkdAdmin ，要求PHP version &gt;= 5.3 可以通过git的方式：

```
git clone https://github.com/mnapoli/phpBeanstalkdAdmin.git
```

如果没有使用git 可以通过 [http://mnapoli.fr/phpBeanstalkdAdmin/](http://mnapoli.fr/phpBeanstalkdAdmin/) 下载对应的安装包

**另外 MAC OS 可以使用别名**

```
ln -s /path/to/phpBeanstalkdAdmin/public /var/www/phpbeanstalkdadmin
```

下载好之后进行nginx 或 apache 配置

```
server {
    listen       80;
    server_name  xx.xx.com;
    root         /var/www/phpBeanstalkdAdmin/public;
    location / {
         try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        fastcgi_buffer_size 128k;
        fastcgi_buffers 32 32k;
        try_files $uri = 404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass    unix:/var/run/php/php7.0-fpm.sock;
	#fastcgi_pass 127.0.0.1:9000;
        fastcgi_index   $index;
        fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include         fastcgi_params;
    }
}
```




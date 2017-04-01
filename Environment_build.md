## php环境搭建

安装php的两种方式:

- PHP作为一个CGI二进制包安装,每次调用PHP时都会重新读取php.ini，修改该php.ini将会立即生效
- PHP作为Apache模块安装，那么只会在第一次启动Apache守护进程时读取一次php.ini,如果修改php.ini，该种方式需要重启Apache才能生效


win下: wamp , xampp 等环境安装包

    在php.ini下注意配置
    extension_dir: C:\php\ext 指向php扩展目录
    打开必须的扩展,如: extension = php_xmlrpc.dll

mac下: mamp



linux下安装lamp环境安装:

常用配置:
- short_open_tag
- extension_dir 指定php扩展模块
- error_reporting

    可以在开发阶段 error_reporting = E_ALL 或者 error_reporting = E_ALL & ~E_NOTICE

- display_errors
- upload_max_filesize 允许的上传文件大小
- output_buffering 输出缓存
    作用: 提高性能
    在开发时，设置为0，方便调试
    优势: 
        ① 会降低下载和渲染HTML所需的时间
        ② 将php存储的所有缓存输出的缓冲区，提高网络性能
        ③ 在设置cookies时遇到的错误，Warning: Cannot modify header information - headers already sent by (output)",通过设置output_buffering解决
参考:[深入理解php的输出缓冲区(output buffer)](http://gywbd.github.io/posts/2015/1/php-output-buffer-in-deep.html)
[ob缓存机制（ob：output_buffer）](https://segmentfault.com/a/1190000000578885)

资源限制配置:
> 确保php脚本不会由于程序员或者用户的动作而独占服务器资源,过度耗费资源影响的三个方面: 脚本执行时间、脚本输入处理时间和内存

- max_execution_time = 30 php执行脚本上限时间    
- max_input_time = 60     php脚本解析请求数据所用时间限制
- memory_limit = 128M     为php分配的最大内存量
- post_max_size           表单允许上传的最大文件大小

# php 版本 DockerFile 文件

- 7.0  已完成  目前 130M 左右
- 7.2  已完成  目前 130M 左右
- 8.0  已完成  目前 140M 左右
- 8.1  已完成  目前 150M 左右

## 使用

- `$PHP_INI_DIR` 是docker 中 php ini 配置目录
- 切换对应版本目录中 实例构建镜像 `sudo docker build --no-cache -t php-版本号 .`
- 交互式运行 `sudo docker run --name php版本号 -it php-版本号 /bin/sh`
- 全局安装了 `composer`

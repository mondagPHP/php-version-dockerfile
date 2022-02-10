# php 版本 DockerFile 文件

- 7.0  已完成  目前 130M 左右
- 7.2  已完成  目前 130M 左右
- 8.0  已完成  目前 140M 左右
- 8.1  已完成  目前 150M 左右

## php版本基础镜像

- `$PHP_INI_DIR` 是docker 中 php ini 配置目录
- 切换对应版本目录中 实例构建镜像 `sudo docker build --no-cache -t php-版本号 .`
- 交互式运行 `sudo docker run --name php版本号 -it php-版本号 /bin/sh`
- 全局安装了 `composer`

## app镜像demo

- 这下面只是参考demo 具体按实际情况修改
- dockerfile

    ```dockerflie
    #FROM php版本基础镜像
    FROM 8095a2b8a034

    ADD . /var/www/heros-worker-demo
    WORKDIR /var/www/heros-worker-demo

    RUN composer install -vvv --no-dev

    #如果不想在基础镜像装composer ， 可以注释基础镜像中composer相关命令 (7.0 版本没装)
    # RUN php composer.phar config -g repo.packagist composer https://mirrors.aliyun.com/composer \
          && php composer.phar install -vvv --no-dev 

    CMD php bin/start start

    EXPOSE 8080
    ```

- 构建 `sudo docker build --no-cache -t worker-demo:v1 .`
- 启动 `sudo docker run --name=worker-demo-v1 --network=host -d worker-demo:v1`

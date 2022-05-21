# php 版本 DockerFile 文件

# 完成`redis`,`event`等相关扩展

- 7.2  已完成  目前 100M 左右
- 8.0  已完成  目前 110M 左右
- 8.1  已完成  目前 110M 左右

## php版本基础镜像

- `$PHP_INI_DIR` 是docker 中 php ini 配置目录
- 切换对应版本目录中 实例构建镜像 `sudo docker build --no-cache -t php-版本号 .`
- 交互式运行 `sudo docker run --name php版本号 -it php-版本号 /bin/sh`

## app镜像demo

- 这下面只是参考demo 具体按实际情况修改
  - dockerfile

      ```dockerflie
      #FROM php版本基础镜像
      FROM xxxxx

      ADD . /var/www/heros-worker-demo
      WORKDIR /var/www/heros-worker-demo

      RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer \
          && composer install -vvv --no-dev --prefer-dist \
          && composer dump-autoload -o

      CMD php bin/start start

      EXPOSE 8080
      ```

- 构建 `sudo docker build --no-cache -t worker-demo:v1 .`
- 启动 `sudo docker run --name=worker-demo-v1 --network=host -d worker-demo:v1`

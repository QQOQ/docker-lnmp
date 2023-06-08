FROM alpine

EXPOSE 9501
EXPOSE 9502

ENV TZ=Asia/Shanghai

RUN apk update --no-cache \
	&& apk add --no-cache tzdata \
	&& echo "${TZ}" > /etc/timezone \
	&& ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime

RUN wget https://wenda-1252906962.file.myqcloud.com/dist/swoole-cli-v5.0.3-linux-x64.tar.xz
RUN tar -xvf swoole-cli-v5.0.3-linux-x64.tar.xz
RUN mv ./swoole-cli /usr/bin/swoole-cli
RUN rm -rf swoole-cli-v5.0.3-linux-x64.tar.xz
RUN chmod +x /usr/bin/swoole-cli

# 替代 PHP
RUN ln -s /usr/bin/swoole-cli /usr/bin/php
#RUN wget https://getcomposer.org/download/2.5.7/composer.phar -O /usr/local/bin/composer
RUN wget https://install.phpcomposer.com/composer.phar -O /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

VOLUME /www
WORKDIR /www

#CMD ["tail", "-f", "/dev/null"]
FROM mysql:8
ENV MYSQL_ROOT_PASSWORD root

EXPOSE 3306

COPY custom.mysql.cnf /etc/mysql/conf.d/custom.mysql.cnf

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
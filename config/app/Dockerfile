FROM amd64/centos:6

# 2020年11月30日 CentOS6系 のすべてのサポートが終了
# yum のリポジトリなどがすべてアーカイブに移動しているため
# デフォルトのままだとリポジトリが見つからずにエラーとなる
# yumリポジトリがアーカイブされているので、参照先を書き換える。
RUN sed -i -e "s/^mirrorlist=http:\/\/mirrorlist.centos.org/#mirrorlist=http:\/\/mirrorlist.centos.org/g" /etc/yum.repos.d/CentOS-Base.repo
RUN sed -i -e "s/^#baseurl=http:\/\/mirror.centos.org/baseurl=http:\/\/vault.centos.org/g" /etc/yum.repos.d/CentOS-Base.repo

ENV PHP_VERSION 5.3.3

RUN yum install -y \
        php \
        php-mbstring \
        php-pgsql \
        php-mysql \
        php-gd \
        zip \
        unzip \
        git \
        httpd && \
    yum clean all

# 設定ファイルをdockerコンテナ内のPHP、Apacheに読み込ませる
# ADD：ローカルのファイルをDockerコンテナ内にコピーする
ADD config/app/php.ini /etc/php.ini
ADD config/app/httpd.conf /etc/httpd/conf/httpd.conf

CMD chmod 777 -R /var/www/html/site1/app/tmp
CMD chmod 777 -R /var/www/html/site2/app/tmp

EXPOSE 80

# Apache2の起動
CMD ["/usr/sbin/apachectl","-DFOREGROUND"]
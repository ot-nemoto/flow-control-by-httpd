FROM centos:7

WORKDIR /root

RUN yum update -y && \
    yum install -y httpd httpd-devel gcc bind-utils net-tools && \
    curl -L -o mod_bw-0.92.tgz "http://sourceforge.net/projects/bwmod/files/bwmod/mod_bw%200.92/mod_bw-0.92.tgz/download" && \
    tar xf mod_bw-0.92.tgz && \
    sed -i -e "s/remote_addr/client_addr/g" mod_bw.c && \
    apxs -i -a -c mod_bw.c

COPY html/ /var/www/html/
COPY conf/ /etc/httpd/conf.d/

ENTRYPOINT ["/usr/sbin/httpd", "-DFOREGROUND"]
